---
title: Gebietsübergreifende, hochverfügbare AD FS-Bereitstellung in Azure mit Azure Traffic Manager | Microsoft-Dokumentation
description: Bereitstellen von AD FS in Azure für hohe Verfügbarkeit.
services: active-directory
author: anandyadavmsft
manager: mtillman
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: billmath
ms.openlocfilehash: 9ce16db4a50fbb31c8454b085a6d0471ebbdf32c
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078657"
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Gebietsübergreifende, hochverfügbare AD FS-Bereitstellung in Azure mit Azure Traffic Manager
Unter [AD FS-Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md) erfahren Sie Schritt für Schritt, wie Sie in Azure eine einfache AD FS-Infrastruktur für Ihre Organisation bereitstellen. Dieser Artikel enthält die nächsten Schritte, mit denen Sie in Azure mithilfe von [Azure Traffic Manager](/azure/traffic-manager/) eine gebietsübergreifende AD FS-Bereitstellung erstellen können. Azure Traffic Manager unterstützt Sie beim Erstellen einer geografisch verteilten, hochverfügbaren und hochleistungsfähigen AD FS-Infrastruktur für Ihre Organisation. Hierbei kommt eine Reihe von Routingmethoden zum Einsatz, die zur Erfüllung der verschiedenen Anforderungen der Infrastruktur zur Verfügung stehen.

Eine hochverfügbare, gebietsübergreifende AD FS-Infrastruktur bietet folgende Vorteile:

* **Beseitigung einer einzelnen Fehlerquelle (Single Point of Failure):** Mit den Failoverfunktionen von Azure Traffic Manager steht auch dann eine hochverfügbare AD FS-Infrastruktur zur Verfügung, wenn eines der Rechenzentren in einem Teil der Welt ausfällt.
* **Verbesserte Leistung:** Mit der in diesem Artikel empfohlenen Bereitstellung können Sie eine hochleistungsfähige AD FS-Infrastruktur bereitstellen, mit der sich Benutzer schneller authentifizieren können.

## <a name="design-principles"></a>Entwurfsprinzipien
![Allgemeines Design](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

Die grundlegenden Entwurfsprinzipien entsprechen den Entwurfsprinzipien aus dem Artikel „AD FS-Bereitstellung in Azure“. Das obige Diagramm zeigt eine einfache Erweiterung der grundlegenden Bereitstellung auf eine weitere geografische Region. Im Anschluss folgen einige Aspekte, die berücksichtigt werden müssen, wenn Sie Ihre Bereitstellung auf eine neue geografische Region erweitern:

* **Virtuelles Netzwerk:** Es empfiehlt sich, in der geografischen Region, in der Sie die zusätzliche AD FS-Infrastruktur bereitstellen möchten, ein neues virtuelles Netzwerk zu erstellen. Im obigen Diagramm sind „Geo1 VNET“ und „Geo2 VNET“ die beiden virtuellen Netzwerke in den einzelnen geografischen Regionen.
* **Domänencontroller und AD FS-Server im neuen geografischen VNET:** Zur Verbesserung der Leistung empfiehlt sich, Domänencontroller in der neuen geografischen Region bereitzustellen, damit die AD FS-Server in der neuen Region bei der Authentifizierung nicht einen Domänencontroller in einem anderen (weit entfernten) Netzwerk kontaktieren müssen.
* **Speicherkonten:** Speicherkonten sind einer Region zugeordnet. Da Sie Computer in einer neuen geografischen Region bereitstellen möchten, müssen Sie neue Speicherkonten für diese Region erstellen.
* **Netzwerksicherheitsgruppen:** Netzwerksicherheitsgruppen werden genau wie Speicherkonten in einer Region erstellt und können nicht anderen geografischen Regionen verwendet werden. Aus diesem Grund müssen in der neuen geografischen Region neue Netzwerksicherheitsgruppen erstellt werden, die den Netzwerksicherheitsgruppen aus der ersten geografischen Region für das INT- und das DMZ-Subnetz ähneln.
* **DNS-Bezeichnungen für öffentliche IP-Adressen:** Azure Traffic Manager kann AUSSCHLIESSLICH über DNS-Bezeichnungen auf Endpunkte verweisen. Daher müssen Sie DNS-Bezeichnungen für die öffentlichen IP-Adressen der externen Lasten Ausgleichs Module erstellen.
* **Azure Traffic Manager:** Microsoft Azure Traffic Manager ermöglicht die Verteilung von Benutzerdatenverkehr auf Ihre Dienstendpunkte in unterschiedlichen Datencentern auf der ganzen Welt. Azure Traffic Manager arbeitet auf DNS-Ebene. Er verwendet DNS-Antworten, um Endbenutzer-Datenverkehr an global verteilte Endpunkte zu leiten. Clients stellen dann eine direkte Verbindung mit diesen Endpunkten her. Mit unterschiedlichen Routing Optionen für Leistung, gewichtet und Priorität können Sie problemlos die Routing Option auswählen, die für die Anforderungen Ihrer Organisation am besten geeignet ist.
* **VNet-zu-VNet-Konnektivität zwischen zwei Regionen:** Zwischen den eigentlichen virtuellen Netzwerken muss keine Verbindung bestehen. Da jedes virtuelle Netzwerk Zugriff auf Domänencontroller hat und selbst über AD FS und WAP-Server verfügt, kann es ganz ohne Verbindung zwischen den virtuellen Netzwerken in verschiedenen Regionen verwendet werden.

## <a name="steps-to-integrate-azure-traffic-manager"></a>Schritte zum Integrieren von Azure Traffic Manager
### <a name="deploy-ad-fs-in-the-new-geographical-region"></a>Bereitstellen von AD FS in der neuen geografischen Region
Orientieren Sie sich an den Schritten und Richtlinien in [AD FS-Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md) , um die gleiche Topologie in der neuen geografischen Region bereitzustellen.

### <a name="dns-labels-for-public-ip-addresses-of-the-internet-facing-public-load-balancers"></a>DNS-Bezeichnungen für öffentliche IP-Adressen der (öffentlichen) Lastenausgleichsmodule mit Internetzugriff
Wie bereits erwähnt, kann der Azure-Traffic Manager nur auf DNS-Bezeichnungen als Endpunkte verweisen. Daher ist es wichtig, dass DNS-Bezeichnungen für die öffentlichen IP-Adressen der externen Lasten Ausgleichs Module erstellt werden. Der folgende Screenshot zeigt, wie Sie Ihre DNS-Bezeichnung für die öffentliche IP-Adresse konfigurieren können:

![DNS-Bezeichnung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Bereitstellen von Azure Traffic Manager
Führen Sie die folgenden Schritte aus, um ein Traffic Manager-Profil zu erstellen. Weitere Informationen finden Sie unter [Verwalten von Azure Traffic Manager-Profilen](/azure/traffic-manager/traffic-manager-manage-profiles).

1. **Erstellen eines Traffic Manager-Profils**: Versehen Sie Ihr Traffic Manager-Profil mit einem eindeutigen Namen. Dieser Profilname ist Teil des DNS-Namens und fungiert als Präfix für die Traffic Manager-Domänennamenbezeichnung. Der Name bzw. das Präfix wird „.trafficmanager.net“ hinzugefügt, um eine DNS-Bezeichnung für Ihre Traffic Manager-Instanz zu erstellen. Im folgenden Screenshot wird das Traffic Manager-DNS-Präfix auf „mysts“ festgelegt, was die DNS-Bezeichnung „mysts.trafficmanager.net“ ergibt:

    ![Traffic Manager-Profilerstellung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Datenverkehrrouting-Methode:** In Traffic Manager stehen drei Routingoptionen zur Verfügung:

   * Priority
   * Leistung
   * Gewichtet

     **Leistung** erhalten Sie eine besonders reaktionsschnelle AD FS-Infrastruktur. Sie können aber natürlich auch eine der anderen Routingmethoden verwenden, wenn diese für Ihre Anforderungen besser geeignet ist. Die Wahl der Routingoption hat keine Auswirkungen auf die AD FS-Funktion. Weitere Informationen finden Sie unter [Traffic Manager-Methoden für das Datenverkehrsrouting](/azure/traffic-manager/traffic-manager-routing-methods) . Im obigen Beispielscreenshot ist die Methode **Performance** (Leistung) ausgewählt.
3. **Konfigurieren von Endpunkten:** Klicken Sie auf der Traffic Manager-Seite auf „Endpunkte“, und wählen Sie „Hinzufügen“ aus. Dadurch wird eine Seite zum Hinzufügen eines Endpunkts angezeigt, die in etwa wie auf dem folgenden Screenshot aussieht:

   ![Konfigurieren von Endpunkten](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)

   Orientieren Sie sich bei den verschiedenen Eingaben an der folgenden Richtlinie:

   **Typ:** Wählen Sie „Azure-Endpunkt“ aus, da wir auf eine öffentliche Azure-IP-Adresse verweisen möchten.

   **Name:** Erstellen Sie einen Namen, den Sie dem Endpunkt zuordnen möchten. Dies ist nicht der DNS-Name und hat keinen Einfluss auf DNS-Einträge.

   **Zielressourcentyp:** Wählen Sie für diese Eigenschaft den Wert „Öffentliche IP-Adresse“ aus.

   **Zielressource:** Hier können Sie aus den verschiedenen DNS-Bezeichnungen wählen, die im Rahmen Ihres Abonnements zur Verfügung stehen. Wählen Sie die DNS-Bezeichnung entsprechend dem Endpunkt aus, den Sie konfigurieren.

   Fügen Sie für jede geografische Region, an die Azure Traffic Manager Datenverkehr weiterleiten soll, einen Endpunkt hinzu.
   Weitere Informationen und ausführliche Schritte zum Hinzufügen/Konfigurieren von Endpunkten in Traffic Manager finden Sie unter [Hinzufügen, Deaktivieren, Aktivieren oder Löschen von Endpunkten](/azure/traffic-manager/traffic-manager-manage-endpoints)
4. **Konfigurieren eines Tests:** Klicken Sie auf der Traffic Manager-Seite auf „Konfiguration“. Auf der Konfigurationsseite müssen Sie die Überwachungseinstellungen so festlegen, dass der Test am HTTP-Port 80 und am relativen Pfad „/adfs/probe“ durchgeführt wird:

    ![Konfigurieren des Tests](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png)

   > [!NOTE]
   > **Vergewissern Sie sich, dass die Endpunkte nach Abschluss die Konfiguration den Status „ONLINE“ aufweisen.** Wenn sich alle Endpunkte im Status "heruntergestuft" befinden, versucht Azure Traffic Manager, den Datenverkehr weiterzuleiten, wobei angenommen wird, dass die Diagnose falsch ist und alle Endpunkte erreichbar sind.
   >
   >
5. **Ändern von DNS-Einträgen für Azure Traffic Manager:** Bei Ihrem Verbunddienst muss es sich um einen CNAME-Eintrag für den DNS-Namen von Azure Traffic Manager handeln. Erstellen Sie einen CNAME-Eintrag in den öffentlichen DNS-Einträgen, sodass jemand, der den Verbunddienst erreichen möchte, tatsächlich Azure Traffic Manager erreicht.

    Wenn Sie also beispielsweise den Verbunddienst „fs.fabidentity.com“ an Traffic Manager verweisen möchten, müssen Sie Ihren DNS-Ressourceneintrag wie folgt ändern:

    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-the-routing-and-ad-fs-sign-in"></a>Testen des Routings und der AD FS-Anmeldung
### <a name="routing-test"></a>Routingtest
Für einen einfachen Routingtest können Sie den DNS-Namen des Verbunddiensts jeweils über einen Computer in den einzelnen geografischen Region anpingen. Der tatsächlich angepingte Endpunkt wird (abhängig von der verwendeten Routingmethode) in der Pingausgabe angezeigt. Bei Verwendung der Routingmethode „Leistung“ wird also beispielsweise der nächstgelegene Endpunkt erreicht. Im Anschluss sehen Sie einen Screenshot mit zwei Pings von zwei Clientcomputern aus unterschiedlichen Regionen („EastAsia“ und „WestUS“):

![Routingtest](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>Test der AD FS-Anmeldung
Die einfachste Möglichkeit zum Testen von AD FS ist die Verwendung der Seite „IdpInitiatedSignon.aspx“. Hierfür ist es erforderlich, in den AD FS-Eigenschaften „IdpInitiatedSignOn“ zu aktivieren. Führen Sie die unten angegebenen Schritte aus, um Ihr AD FS-Setup zu überprüfen.

1. Führen Sie das unten angegebene Cmdlet auf dem AD FS-Server aus, und verwenden Sie PowerShell, um es auf „Aktiviert“ festzulegen.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Rufen Sie auf einem beliebigen externen Computer „https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx“ auf.
3. Die folgende AD FS-Seite wird angezeigt:

    ![AD FS-Test – Authentifizierungsaufforderung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)

    Bei einer erfolgreichen Anmeldung wird die folgende Erfolgsmeldung angezeigt:

    ![AD FS-Test – Authentifizierung erfolgreich](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Verwandte Links
* [AD FS-Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md)
* [Was ist Traffic Manager?](/azure/traffic-manager/)
* [Informationen zu Traffic Manager-Routingmethoden für Datenverkehr](/azure/traffic-manager/traffic-manager-routing-methods)

## <a name="next-steps"></a>Nächste Schritte
* [Verwalten von Azure Traffic Manager-Profilen](/azure/traffic-manager/traffic-manager-manage-profiles)
* [Hinzufügen, deaktivieren, aktivieren oder Löschen von Endpunkten](/azure/traffic-manager/traffic-manager-manage-endpoints)
