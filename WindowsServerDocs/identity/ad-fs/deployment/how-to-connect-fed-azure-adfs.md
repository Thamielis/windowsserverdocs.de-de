---
title: Active Directory-Verbunddienste in Azure | Microsoft Docs
description: In diesem Dokument wird beschrieben, wie Sie AD FS in Azure bereitstellen, um eine hohe Verfügbarkeit zu erzielen.
author: billmath
manager: mtillman
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.topic: get-started-article
ms.date: 10/28/2018
ms.subservice: hybrid
ms.author: billmath
ms.openlocfilehash: 5db03a2d275dc4a02295c588bd0789fa757b8503
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956218"
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Bereitstellen von Active Directory-Verbunddiensten in Azure
AD FS verfügt über Funktionen für den vereinfachten, geschützten Identitätsverbund und die einmalige Webanmeldung (SSO). Der Verbund mit Azure AD oder O365 ermöglicht Benutzern die Authentifizierung mit lokalen Anmeldeinformationen und den Zugriff auf Ressourcen in der Cloud. Daher ist es wichtig, dass eine hoch verfügbare AD FS-Infrastruktur vorhanden ist, um den Zugriff auf lokale Ressourcen und Ressourcen in der Cloud sicherzustellen. Durch die Bereitstellung von AD FS in Azure kann die erforderliche Hochverfügbarkeit mit wenig Aufwand erzielt werden.
Die Bereitstellung von AD FS in Azure hat mehrere Vorteile, von denen hier einige aufgeführt sind:

* **Hochverfügbarkeit**: Mit der Leistungsfähigkeit von Azure-Verfügbarkeitsgruppen sorgen Sie für eine Hochverfügbarkeitsinfrastruktur.
* **Einfache Skalierung** : Benötigen Sie eine höhere Leistung? Sie können die Migration zu leistungsfähigeren Computern in Azure leicht mit nur wenigen Klicks durchführen.
* **Standortübergreifende Redundanz** : Mit der geografischen Redundanz von Azure können Sie sicher sein, dass Ihre Infrastruktur weltweit eine hohe Verfügbarkeit aufweist.
* **Einfache Verwaltung** : Dank der stark vereinfachten Verwaltungsfunktionen im Azure-Portal ist die Verwaltung der Infrastruktur sehr einfach und problemlos. 

## <a name="design-principles"></a>Entwurfsprinzipien
![Bereitstellungsentwurf](./media/how-to-connect-fed-azure-adfs/deployment.png)

Im obigen Diagramm ist die empfohlene grundlegende Topologie dargestellt, mit der Sie die Bereitstellung Ihrer AD FS-Infrastruktur in Azure beginnen können. Die Prinzipien hinter den verschiedenen Komponenten der Topologie sind unten angegeben:

* **DC/AD FS-Server**: Wenn Sie weniger als 1.000 Benutzer haben, können Sie die AD FS-Rolle einfach auf Ihren Domänencontrollern installieren. Wenn Sie Leistungsbeeinträchtigungen für die Domänencontroller ausschließen möchten oder mehr als 1.000 Benutzer haben, können Sie AD FS auf separaten Servern bereitstellen.
* **WAP-Server** : Webanwendungsproxy-Server müssen so bereitgestellt werden, dass die Benutzer AD FS auch erreichen können, wenn sie sich nicht im Unternehmensnetzwerk befinden.
* **DMZ**: Die Webanwendungsproxy-Server werden in der DMZ angeordnet, und NUR der TCP/443-Zugriff ist zwischen der DMZ und dem internen Subnetz zulässig.
* **Load Balancers**: Zur Sicherstellung der Hochverfügbarkeit von AD FS- und Webanwendungsproxy-Servern empfehlen wir die Verwendung eines internen Load Balancers für AD FS-Server und von Azure Load Balancer für Webanwendungsproxy-Server.
* **Verfügbarkeitsgruppen**: Zur Sicherstellung der Redundanz für die AD FS-Bereitstellung wird empfohlen, zwei oder mehr virtuelle Computer für ähnliche Workloads in einer Verfügbarkeitsgruppe zu gruppieren. Durch diese Konfiguration wird sichergestellt, dass während eines geplanten oder ungeplanten Wartungsereignisses mindestens ein virtueller Computer verfügbar ist.
* **Speicherkonten**: Es wird empfohlen, zwei Speicherkonten zu verwenden. Die Verwendung von nur einem Speicherkonto kann zur Schaffung einer einzelnen Fehlerquelle führen und bewirken, dass die Bereitstellung in dem unwahrscheinlichen Fall, dass das Speicherkonto ausfällt, nicht mehr verfügbar ist. Bei zwei Speicherkonten kann jedem Fehlerpunkt ein Speicherkonto zugeordnet werden.
* **Netzwerktrennung**: Webanwendungsproxy-Server müssen in einem separaten DMZ-Netzwerk bereitgestellt werden. Sie können ein virtuelles Netzwerk in zwei Subnetze unterteilen und Webanwendungsproxy-Server dann in einem isolierten Subnetz bereitstellen. Sie können die Netzwerksicherheitsgruppen-Einstellungen für jedes Subnetz leicht konfigurieren und zwischen den beiden Subnetzen nur die erforderliche Kommunikation zulassen. Weitere Details sind unten jeweils für die einzelnen Bereitstellungsszenarien angegeben.

## <a name="steps-to-deploy-ad-fs-in-azure"></a>Schritte zum Bereitstellen von AD FS in Azure
Mit den Schritten dieser Anleitung wird die unten dargestellte AD FS-Infrastruktur in Azure bereitgestellt.

### <a name="1-deploying-the-network"></a>1. Bereitstellen des Netzwerks
Wie oben beschrieben, können Sie entweder zwei Subnetze in einem einzelnen virtuellen Netzwerk oder zwei gänzlich unterschiedliche virtuelle Netzwerke (VNet) erstellen. In diesem Artikel geht es um die Bereitstellung eines einzelnen virtuellen Netzwerks und die Unterteilung in zwei Subnetze. Dies ist derzeit ein einfacherer Ansatz, da bei zwei separaten VNets ein VNet-zu-VNet-Gateway für die Kommunikation erforderlich wäre.

**1.1 Erstellen eines virtuellen Netzwerks**

![Virtuelles Netzwerk erstellen](./media/how-to-connect-fed-azure-adfs/deploynetwork1.png)

Wählen Sie im Azure-Portal die Option „Virtuelles Netzwerk“. Sie können das virtuelle Netzwerk und ein Subnetz sofort mit nur einem Klick bereitstellen. Das INT-Subnetz wird ebenfalls definiert, und diesem Subnetz können VMs hinzugefügt werden.
Der nächste Schritt ist das Hinzufügen eines weiteren Subnetzes zum Netzwerk, nämlich des DMZ-Subnetzes. Gehen Sie wie folgt vor, um das DMZ-Subnetz zu erstellen:

* Wählen Sie das neu erstellte Netzwerk aus.
* Wählen Sie in den Eigenschaften die Option „Subnetz“.
* Klicken Sie im Bereich „Subnetz“ auf die Schaltfläche „Hinzufügen“.
* Geben Sie den Subnetznamen und die Adressrauminformationen an, um das Subnetz zu erstellen.

![Subnet](./media/how-to-connect-fed-azure-adfs/deploynetwork2.png)

![Subnetz-DMZ](./media/how-to-connect-fed-azure-adfs/deploynetwork3.png)

**1.2. Erstellen der Netzwerksicherheitsgruppen**

Eine Netzwerksicherheitsgruppe (NSG) enthält eine Zugriffssteuerungsliste (Access Control List, ACL) zum Zulassen oder Verweigern von Netzwerkdatenverkehr an Ihre VM-Instanzen in einem virtuellen Netzwerk. NSGs können Subnetzen oder einzelnen VM-Instanzen innerhalb dieses Subnetzes zugeordnet werden. Wenn eine Netzwerksicherheitsgruppe einem Subnetz zugeordnet ist, gelten die ACL-Regeln für alle VM-Instanzen in diesem Subnetz.
In dieser Anleitung erstellen wir zwei NSGs: jeweils eine für ein internes Netzwerk und eine DMZ. Sie erhalten die Namen NSG_INT und NSG_DMZ.

![NSG erstellen](./media/how-to-connect-fed-azure-adfs/creatensg1.png)

Nach der Erstellung der NSG sind 0 eingehende und 0 ausgehende Regeln vorhanden. Nachdem die Rollen auf den entsprechenden Servern installiert wurden und betriebsbereit sind, können die eingehenden und ausgehenden Regeln gemäß der gewünschten Sicherheitsebene eingerichtet werden.

![NSG initialisieren](./media/how-to-connect-fed-azure-adfs/nsgint1.png)

Ordnen Sie nach der NSG-Erstellung NSG_INT dem Subnetz INT und NSG_DMZ dem Subnetz DMZ zu. Unten ist ein Screenshot mit einem Beispiel angegeben:

![NSG konfigurieren](./media/how-to-connect-fed-azure-adfs/nsgconfigure1.png)

* Klicken Sie auf „Subnetze“, um den Bereich für Subnetze zu öffnen.
* Wählen Sie das Subnetz aus, das Sie der NSG zuordnen möchten. 

Nach der Konfiguration sollte der Bereich für Subnetze wie folgt aussehen:

![Subnetze nach NSG](./media/how-to-connect-fed-azure-adfs/nsgconfigure2.png)

**1.3. Erstellen einer Verbindung mit einem lokalen Ort**

Wir benötigen eine Verbindung mit einem lokalen Ort, um den Domänencontroller (DC) in Azure bereitzustellen. Azure verfügt über verschiedene Verbindungsoptionen, um für Ihre lokale Infrastruktur eine Verbindung mit der Azure-Infrastruktur herzustellen.

* Point-to-Site
* Standort-zu-Standort für virtuelle Netzwerke
* ExpressRoute

Es wird empfohlen, ExpressRoute zu verwenden. Mit expressroute können Sie private Verbindungen zwischen Azure-Rechenzentren und der Infrastruktur erstellen, die sich an Ihrem Standort oder in einer Co-Location-Umgebung befindet. ExpressRoute-Verbindungen verlaufen nicht über das öffentliche Internet. Sie bieten mehr Zuverlässigkeit, eine höhere Geschwindigkeit, niedrigere Latenzzeiten und mehr Sicherheit als herkömmliche Verbindungen über das Internet.
Die Verwendung von ExpressRoute wird zwar empfohlen, aber Sie können eine beliebige Verbindungsmethode wählen, die für Ihr Unternehmen am besten geeignet ist. Weitere Informationen zu ExpressRoute und den verschiedenen Verbindungsoptionen mit ExpressRoute finden Sie unter [ExpressRoute – Technische Übersicht](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Erstellen von Speicher Konten
Sie können zwei Speicherkonten erstellen, um für Hochverfügbarkeit zu sorgen und die Abhängigkeit von einem einzelnen Speicherkonto zu vermeiden. Teilen Sie die Computer in jeder Verfügbarkeitsgruppe in zwei Gruppen, und weisen Sie jeder Gruppe dann ein separates Speicherkonto zu.

![Speicherkonten erstellen](./media/how-to-connect-fed-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Erstellen von Verfügbarkeits Gruppen
Erstellen Sie für jede Rolle (DC/AD FS und WAP) Verfügbarkeitsgruppen, die jeweils mindestens zwei Computer enthalten. So erzielen Sie für jede Rolle ein höhere Verfügbarkeit. Beim Erstellen der Verfügbarkeitsgruppen ist es sehr wichtig, Entscheidungen zu den folgenden Komponenten zu treffen:

* **Fehlerdomänen**: Virtuelle Computer einer Fehlerdomäne nutzen die gleiche Stromquelle und den gleichen physischen Netzwerkswitch. Mindestens zwei Fehlerdomänen werden empfohlen. Der Standardwert ist 3. Sie können ihn für diese Bereitstellung beibehalten.
* **Updatedomänen**: Computer, die der gleichen Updatedomäne angehören, werden während eines Updates gemeinsam neu gestartet. Es wird empfohlen, mindestens zwei Updatedomänen zu verwenden. Der Standardwert ist 5. Sie können ihn für diese Bereitstellung beibehalten.

![Verfügbarkeitsgruppen](./media/how-to-connect-fed-azure-adfs/availabilityset1.png)

Erstellen Sie die folgenden Verfügbarkeitsgruppen:

| Verfügbarkeitsgruppe | Role | Fehlerdomänen | Updatedomänen |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Bereitstellen von virtuellen Maschinen
Der nächste Schritt ist die Bereitstellung von virtuellen Computern, auf denen die verschiedenen Rollen in Ihrer Infrastruktur gehostet werden. Es wird empfohlen, in jeder Verfügbarkeitsgruppe mindestens zwei Computer zu verwenden. Erstellen Sie vier virtuelle Computer für die grundlegende Bereitstellung.

| Machine | Role | Subnet | Verfügbarkeitsgruppe | Speicherkonto | IP-Adresse |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |statischen |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |statischen |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |statischen |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |statischen |

Sie haben vielleicht bemerkt, dass keine NSG angegeben wurde. Dies liegt daran, dass Sie NSGs bei Azure auf Subnetzebene verwenden können. Anschließend können Sie den Computerdatenverkehr steuern, indem Sie die individuelle NSG verwenden, die entweder dem Subnetz oder dem NIC-Objekt zugeordnet ist. Weitere Informationen finden Sie unter [Was ist eine Netzwerksicherheitsgruppe (NSG)?](https://aka.ms/Azure/NSG).
Eine statische IP-Adresse wird empfohlen, wenn Sie das DNS verwalten. Sie können auch Azure DNS verwenden und in den DNS-Einträgen für Ihre Domäne über die Azure FQDNs auf die neuen Computer verweisen.
Nach Abschluss der Bereitstellung sollte der Bereich für virtuelle Computer wie folgt aussehen:

![Bereitgestellte virtuelle Computer](./media/how-to-connect-fed-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a>5. Konfigurieren des Domänen Controllers/AD FS Servers
 Um jede eingehende Anforderung authentifizieren zu können, muss AD FS mit dem Domänencontroller Kontakt aufnehmen. Es wird empfohlen, ein Replikat des Domänencontrollers in Azure bereitzustellen, um für die Authentifizierung den aufwändigen Weg von Azure zum lokalen DC zu vermeiden. Um Hochverfügbarkeit zu erzielen, ist es ratsam, eine Verfügbarkeitsgruppe mit mindestens zwei Domänencontrollern zu erstellen.

| Domänencontroller | Role | Speicherkonto |
|:---:|:---:|:---:|
| contosodc1 |Replikat |contososac1 |
| contosodc2 |Replikat |contososac2 |

* Stufen Sie die beiden Server als Replikatdomänencontroller mit DNS hoch.
* Konfigurieren Sie die AD FS-Server, indem Sie die AD FS-Rolle mit dem Server-Manager installieren.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. bereitstellen interner Load Balancer (ILB)
**6.1. Erstellen des ILB**

Wählen Sie zum Bereitstellen eines ILB im Azure-Portal die Option „Lastenausgleichsmodule“, und klicken Sie auf „Hinzufügen“ (+).

> [!NOTE]
> Gehen Sie wie folgt vor, wenn **Lastenausgleichsmodule** nicht im Menü angezeigt wird. Klicken Sie unten links im Portal auf **Durchsuchen**, und scrollen Sie, bis **Lastenausgleichsmodule** erscheint.  Klicken Sie auf den gelben Stern, um die Option dem Menü hinzuzufügen. Wählen Sie anschließend das neue Load Balancer-Symbol, um den Bereich zu öffnen und mit der Konfiguration des Load Balancers zu beginnen.
> 
> 

![Load Balancer durchsuchen](./media/how-to-connect-fed-azure-adfs/browseloadbalancer.png)

* **Name**: Geben Sie dem Load Balancer einen beliebigen passenden Namen.
* **Schema**: da dieser Load Balancer vor den AD FS Servern platziert wird und nur für interne Netzwerkverbindungen gedacht ist, wählen Sie "intern" aus.
* **Virtuelles Netzwerk**: Wählen Sie das virtuelle Netzwerk aus, in dem Sie AD FS bereitstellen möchten.
* **Subnetz**: Wählen Sie hier das interne Subnetz aus.
* **IP-Adresszuweisung**: statisch

![Interner Lastenausgleich](./media/how-to-connect-fed-azure-adfs/ilbdeployment1.png)

Nach dem Klicken auf „Erstellen“ und der Bereitstellung des ILB sollte er in der Liste mit den Load Balancern angezeigt werden:

![Load Balancers nach ILB](./media/how-to-connect-fed-azure-adfs/ilbdeployment2.png)

Der nächste Schritt ist das Konfigurieren des Back-End-Pools und Back-End-Tests.

**6.2. Konfigurieren des ILB-Back-End-Pools**

Wählen Sie den neu erstellten ILB im Bereich „Lastenausgleichsmodule“ aus. Der Bereich mit den Einstellungen wird geöffnet. 

1. Wählen Sie im Bereich „Einstellungen“ die Option „Back-End-Pools“.
2. Klicken Sie im Bereich „Back-End-Pool“ auf „Virtuellen Computer hinzufügen“.
3. Es wird ein Bereich angezeigt, in dem Sie eine Verfügbarkeitsgruppe auswählen können.
4. Wählen Sie die AD FS-Verfügbarkeitsgruppe aus.

![ILB-Back-End-Pool konfigurieren](./media/how-to-connect-fed-azure-adfs/ilbdeployment3.png)

**6.3. Konfigurieren des Tests**

Wählen Sie im Bereich mit den ILB-Einstellungen die Option „Integritätstests“.

1. Klicken Sie auf „Hinzufügen“.
2. Details für Test angeben  
   a) **Name**: Testname  
   b) **Protokoll**: HTTP  
   c. **Port**: 80 (http)  
   d. **Pfad**:/ADFS/Probe   
   e. **Intervall**: 5 (Standardwert) – Dies ist das Intervall, in dem ILB die Computer im Back-End-Pool testet.  
   f. **Fehlerschwellenwert**: 2 (Standardwert). Dies ist der Schwellenwert für aufeinanderfolgende fehlgeschlagene Tests, nach denen der ILB einen Computer im Back-End-Pool als nicht reagierend deklariert und keinen Datenverkehr mehr sendet.


Hier wird der Endpunkt „/adfs/probe“ verwendet, der explizit für Integritätsprüfungen in einer AD FS-Umgebung erstellt wurde, in der keine vollständige HTTPS-Pfadüberprüfung möglich ist.  Dies ist wesentlich besser als eine allgemeine Überprüfung von Port 443, die den Status einer modernen AD FS-Bereitstellung nicht genau widerspiegelt.  Weitere Informationen dazu finden Sie unter https://blogs.technet.microsoft.com/applicationproxyblog/2014/10/17/hardware-load-balancer-health-checks-and-web-application-proxy-ad-fs-2012-r2/.

**6.4. Erstellen von Lastenausgleichsregeln**

Um den Datenverkehr effektiv ausgleichen zu können, sollte der ILB mit Lastenausgleichsregeln konfiguriert werden. Gehen Sie wie folgt vor, um eine Lastenausgleichsregel zu erstellen: 

1. Wählen Sie im Bereich „Einstellungen“ des ILB die Option „Lastenausgleichsregel“.
2. Klicken Sie im Bereich „Lastenausgleichsregel“ auf „Hinzufügen“.
3. Im Bereich "Lasten Ausgleichs Regel hinzufügen"  
   a) **Name**: Geben Sie einen Namen für die Regel an.  
   b) **Protokoll**: Wählen Sie TCP aus.  
   c. **Port**: 443  
   d. Back-End- **Port**: 443  
   e. Back-End- **Pool**: Wählen Sie den Pool aus, den Sie zuvor für den AD FS Cluster  
   f. **Test**: Wählen Sie den Test aus, den Sie zuvor für AD FS-Server erstellt haben.

![ILB-Ausgleichsregeln konfigurieren](./media/how-to-connect-fed-azure-adfs/ilbdeployment5.png)

**6.5. Aktualisieren des DNS mit ILB**

Erstellen Sie mit Ihrem internen DNS-Server einen A-Datensatz für den ILB. Der A-Datensatz sollte für den Verbund Dienst mit der IP-Adresse sein, die auf die IP-Adresse des ILB verweist. Wenn beispielsweise die ILB-IP-Adresse 10.3.0.8 und der installierte Verbund Dienst FS.contoso.com ist, erstellen Sie einen A-Datensatz für FS.contoso.com, der auf 10.3.0.8 zeigt.
Dadurch wird sichergestellt, dass alle Daten, die an FS.contoso.com gesendet werden, am ILB enden und entsprechend weitergeleitet werden. 

> [!WARNING]
> Wenn Sie die wid (interne Windows-Datenbank) für die AD FS-Datenbank verwenden, sollte dieser Wert stattdessen temporär so festgelegt werden, dass er auf Ihren primären AD FS Server verweist, oder der webanwendungsproxy schlägt nicht bei der Einschreibung fehl. Nachdem Sie alle Webanwendungs Proxy Server erfolgreich registriert haben, ändern Sie diesen DNS-Eintrag so, dass er auf den Load Balancer verweist.

> [!NOTE]
> Wenn die Bereitstellung auch IPv6 verwendet, achten Sie darauf, einen entsprechenden AAAA-Datensatz zu erstellen.
>

### <a name="7-configuring-the-web-application-proxy-server"></a>7. Konfigurieren des webanwendungsproxy-Servers
**7.1. Konfigurieren der Webanwendungsproxy-Server für die Verbindung mit AD FS-Servern**

Erstellen Sie für den ILB einen Eintrag unter „%systemroot%\system32\drivers\etc\hosts“, um sicherzustellen, dass Webanwendungsproxy-Server die AD FS-Server hinter dem ILB erreichen. Beachten Sie, dass der Distinguished Name (DN) der Verbunddienstname sein sollte, z.B. „fs.contoso.com“. Und der IP-Eintrag sollte die IP-Adresse des ILB lauten (wie im Beispiel 10.3.0.8).

> [!WARNING]
> Wenn Sie die wid (interne Windows-Datenbank) für die AD FS-Datenbank verwenden, sollte dieser Wert stattdessen temporär so festgelegt werden, dass er auf den primären AD FS Server verweist, oder der webanwendungsproxy schlägt nicht bei der Einschreibung fehl. Nachdem Sie alle Webanwendungs Proxy Server erfolgreich registriert haben, ändern Sie diesen DNS-Eintrag so, dass er auf den Load Balancer verweist.


**7.2. Installieren der Webanwendungsproxy-Rolle**

Nachdem Sie sichergestellt haben, dass Webanwendungsproxy-Server die AD FS-Server hinter dem ILB erreichen können, können Sie als Nächstes die Webanwendungsproxy-Server installieren. Webanwendungsproxy-Server brauchen nicht mit der Domäne verknüpft werden. Installieren Sie die Webanwendungsproxy-Rollen auf den beiden Webanwendungsproxy-Servern, indem Sie die Remotezugriffsrolle auswählen. Sie werden vom Server-Manager durch die Schritte der WAP-Installation geführt.
Weitere Informationen zur Bereitstellen von WAP finden Sie unter [Installieren und Konfigurieren des Webanwendungsproxy-Servers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383662(v=ws.11)).

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a>8. Bereitstellen der (öffentlichen) Load Balancer mit Internet Zugriff
**8,1. Erstellen einer Load Balancer mit Internet Zugriff (Public)**

Wählen Sie im Azure-Portal die Option „Lastenausgleichsmodule“, und klicken Sie dann auf „Hinzufügen“. Geben Sie im Bereich „Lastenausgleich erstellen“ die folgenden Informationen ein:

1. **Name**: Geben Sie den Namen für den Load Balancer ein.
2. **Schema**: Öffentlich. Mit dieser Option wird Azure mitgeteilt, dass für diesen Load Balancer eine öffentliche Adresse erforderlich ist.
3. **IP-Adresse**: Erstellen Sie eine neue IP-Adresse (dynamisch).

![Load Balancer mit Internetzugriff](./media/how-to-connect-fed-azure-adfs/elbdeployment1.png)

Nach der Bereitstellung wird der Load Balancer in der Liste „Lastenausgleichsmodule“ angezeigt.

![Load Balancer-Liste](./media/how-to-connect-fed-azure-adfs/elbdeployment2.png)

**8.2. Zuweisen einer DNS-Bezeichnung zur öffentlichen IP**

Klicken Sie im Bereich „Lastenausgleichsmodule“ auf den neu erstellten Load Balancer-Eintrag, um den Bereich für die Konfiguration zu öffnen. Führen Sie die unten angegebenen Schritte aus, um die DNS-Bezeichnung für die öffentliche IP zu konfigurieren:

1. Klicken Sie auf die öffentliche IP-Adresse. Der Bereich für die öffentliche IP und mit den dazugehörigen Einstellungen wird geöffnet.
2. Klicken Sie auf „Konfiguration“.
3. Geben Sie eine DNS-Bezeichnung an. Sie wird zur öffentlichen DNS-Bezeichnung, auf die Sie von jedem Ort aus zugreifen können, z.B. „contosofs.westus.cloudapp.azure.com“. Sie können einen Eintrag im externen DNS für den Verbunddienst (z.B. „fs.contoso.com“) hinzufügen, der in die DNS-Bezeichnung des externen Load Balancers (contosofs.westus.cloudapp.azure.com) aufgelöst wird.

![Load Balancer mit Internetzugriff konfigurieren](./media/how-to-connect-fed-azure-adfs/elbdeployment3.png) 

![Load Balancer mit Internetzugriff (DNS) konfigurieren](./media/how-to-connect-fed-azure-adfs/elbdeployment4.png)

**8.3. Konfigurieren des Back-End-Pools für den (öffentlichen) Load Balancer mit Internetzugriff** 

Führen Sie die gleichen Schritte wie beim Erstellen des internen Load Balancers aus, um den Back-End-Pool für den (öffentlichen) Load Balancer mit Internetzugriff als Verfügbarkeitsgruppe für die WAP-Server zu konfigurieren. Beispiel: „contosowapset“.

![Back-End-Pool für Load Balancer mit Internetzugriff konfigurieren](./media/how-to-connect-fed-azure-adfs/elbdeployment5.png)

**8.4. Konfigurieren des Tests**

Führen Sie die gleichen Schritte wie beim Konfigurieren des internen Load Balancers aus, um den Test für den Back-End-Pool von WAP-Servern zu konfigurieren.

![Test für Load Balancer mit Internetzugriff konfigurieren](./media/how-to-connect-fed-azure-adfs/elbdeployment6.png)

**8.5. Erstellen von Lastenausgleichsregeln**

Führen Sie die gleichen Schritte wie für den ILB aus, um die Lastenausgleichsregel für TCP 443 zu konfigurieren.

![Ausgleichsregeln für Load Balancer mit Internetzugriff konfigurieren](./media/how-to-connect-fed-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a>9. Sichern des Netzwerks
**9.1. Schützen des internen Subnetzes**

Generell benötigen Sie die folgenden Regeln, um Ihr internes Subnetz effizient zu schützen (in der unten angegebenen Reihenfolge).

| Regel | Beschreibung | Flow |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Mit dieser Regel wird die HTTPS-Kommunikation von der DMZ zugelassen. |Eingehend |
| DenyInternetOutbound |Es besteht kein Zugriff auf das Internet. |Ausgehend |

![INT-Zugriffsregeln (eingehend)](./media/how-to-connect-fed-azure-adfs/nsg_int.png)

**9.2. Schützen des DMZ-Subnetzes**

| Regel | Beschreibung | Flow |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |HTTPS aus dem Internet an die DMZ zulassen |Eingehend |
| DenyInternetOutbound |Alles außer HTTPS-Verbindungen ins Internet blockieren |Ausgehend |

![EXT-Zugriffsregeln (eingehend)](./media/how-to-connect-fed-azure-adfs/nsg_dmz.png)

> [!NOTE]
> Wenn die Client Zertifikat Authentifizierung (clienttls-Authentifizierung mit X. 509-Benutzer Zertifikaten) erforderlich ist, muss für AD FS der TCP-Port 49443 für den eingehenden Zugriff aktiviert werden.
> 
> 

### <a name="10-test-the-ad-fs-sign-in"></a>10. Testen der AD FS Anmeldung
Die einfachste Möglichkeit zum Testen von AD FS ist die Verwendung der Seite „IdpInitiatedSignon.aspx“. Hierfür ist es erforderlich, in den AD FS-Eigenschaften „IdpInitiatedSignOn“ zu aktivieren. Führen Sie die unten angegebenen Schritte aus, um Ihr AD FS-Setup zu überprüfen.

1. Führen Sie das unten angegebene Cmdlet auf dem AD FS-Server aus, und verwenden Sie PowerShell, um es auf „Aktiviert“ festzulegen.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. Rufen Sie auf einem beliebigen externen Computer „https:\//adfs-server.contoso.com/adfs/ls/IdpInitiatedSignon.aspx“ auf.  
3. Die folgende AD FS-Seite wird angezeigt:

![Anmeldeseite testen](./media/how-to-connect-fed-azure-adfs/test1.png)

Bei einer erfolgreichen Anmeldung wird die folgende Erfolgsmeldung angezeigt:

![Erfolgreiche Durchführung testen](./media/how-to-connect-fed-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Vorlage für die Bereitstellung von AD FS in Azure
Durch die Vorlage wird eine Konfiguration mit sechs Computern (je zwei für Domänencontroller, AD FS und WAP) bereitgestellt.

[AD FS in Azure – Bereitstellungsvorlage](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Sie können ein vorhandenes virtuelles Netzwerk verwenden oder beim Bereitstellen der Vorlage ein neues VNet erstellen. Im Anschluss finden Sie eine Liste mit den verschiedenen verfügbaren Parametern, mit denen Sie die Bereitstellung anpassen können, sowie eine Beschreibung der jeweiligen Verwendung im Rahmen des Bereitstellungsprozesses. 

| Parameter | BESCHREIBUNG |
|:--- |:--- |
| Standort |Die Region, in der die Ressourcen bereitgestellt werden sollen (beispielsweise „USA, Osten“). |
| StorageAccountType |Die Art des zu erstellenden Speicherkontos. |
| VirtualNetworkUsage |Gibt an, ob ein neues virtuelles Netzwerk erstellt oder ob ein bereits vorhandenes verwendet wird. |
| VirtualNetworkName |Der Name des zu erstellenden virtuellen Netzwerks. Diese Angabe ist sowohl bei Verwendung eines vorhandenen virtuellen Netzwerks als auch bei Verwendung eines neuen virtuellen Netzwerks obligatorisch. |
| VirtualNetworkResourceGroupName |Gibt den Namen der Ressourcengruppe an, in der sich das vorhandene virtuelle Netzwerk befindet. Bei Verwendung eines vorhandenen virtuellen Netzwerks muss dieser Parameter angegeben werden, damit die Bereitstellung die ID des vorhandenen virtuellen Netzwerks ermitteln kann. |
| VirtualNetworkAddressRange |Der Adressbereich des neuen VNet. Diese Angabe ist obligatorisch, wenn Sie ein neues virtuelles Netzwerk erstellen. |
| InternalSubnetName |Der Name des internen Subnetzes. Diese Angabe ist sowohl bei neuen als auch bei bereits vorhandenen virtuellen Netzwerken obligatorisch. |
| InternalSubnetAddressRange |Der Adressbereich des internen Subnetzes, das die Domänencontroller und die AD FS-Server enthält. Diese Angabe ist obligatorisch, wenn Sie ein neues virtuelles Netzwerk erstellen. |
| DMZSubnetAddressRange |Der Adressbereich des DMZ-Subnetzes, das die Windows-Anwendungsproxyserver enthält. Diese Angabe ist obligatorisch, wenn Sie ein neues virtuelles Netzwerk erstellen. |
| DMZSubnetName |Der Name des internen Subnetzes. Diese Angabe ist sowohl bei neuen als auch bei bereits vorhandenen virtuellen Netzwerken obligatorisch. |
| ADDC01NICIPAddress |Die interne IP-Adresse des ersten Domänencontrollers. Diese IP-Adresse wird dem Domänencontroller statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| ADDC02NICIPAddress |Die interne IP-Adresse des zweiten Domänencontrollers. Diese IP-Adresse wird dem Domänencontroller statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| ADFS01NICIPAddress |Die interne IP-Adresse des ersten AD FS-Servers. Diese IP-Adresse wird dem AD FS-Server statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| ADFS02NICIPAddress |Die interne IP-Adresse des zweiten AD FS-Servers. Diese IP-Adresse wird dem AD FS-Server statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| WAP01NICIPAddress |Die interne IP-Adresse des ersten WAP-Servers. Diese IP-Adresse wird dem WAP-Server statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des DMZ-Subnetzes sein. |
| WAP02NICIPAddress |Die interne IP-Adresse des zweiten WAP-Servers. Diese IP-Adresse wird dem WAP-Server statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des DMZ-Subnetzes sein. |
| ADFSLoadBalancerPrivateIPAddress |Die interne IP-Adresse des AD FS-Lastenausgleichs. Diese IP-Adresse wird dem Lastenausgleich statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| ADDCVMNamePrefix |VM-Namenspräfix für Domänencontroller |
| ADFSVMNamePrefix |VM-Namenspräfix für AD FS-Server |
| WAPVMNamePrefix |VM-Namenspräfix für WAP-Server |
| ADDCVMSize |VM-Größe der Domänencontroller |
| ADFSVMSize |VM-Größe der AD FS-Server |
| WAPVMSize |VM-Größe der WAP-Server |
| AdminUserName |Name des lokalen Administrators der virtuellen Computer |
| AdminPassword |Kennwort für das lokale Administratorkonto der virtuellen Computer |

## <a name="additional-resources"></a>Weitere Ressourcen
* [Verfügbarkeits Gruppen](https://aka.ms/Azure/Availability) 
* [Azure-Lastenausgleich](https://aka.ms/Azure/ILB)
* [Interner Load Balancer](https://aka.ms/Azure/ILB/Internal)
* [Load Balancer mit Internetzugriff](https://aka.ms/Azure/ILB/Internet)
* [Speicherkonten](https://aka.ms/Azure/Storage)
* [Virtuelle Azure-Netzwerke](https://aka.ms/Azure/VNet)
* [AD FS- und Webanwendungsproxy-Links](https://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Nächste Schritte
* [Integrieren lokaler Identitäten in Azure Active Directory](/azure/active-directory/hybrid/whatis-hybrid-identity)
* [Azure AD Connect und Verbund](/azure/active-directory/hybrid/how-to-connect-fed-whatis)
* [Regions übergreifende Hochverfügbarkeit AD FS Bereitstellung in Azure mit Azure Traffic Manager](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
