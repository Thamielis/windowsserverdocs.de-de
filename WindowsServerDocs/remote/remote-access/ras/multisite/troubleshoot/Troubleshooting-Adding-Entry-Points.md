---
title: Beheben von Problemen beim Hinzufügen von Einstiegspunkten
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: dcc1037f-1a65-4497-99e6-0df9aef748a8
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9e8f67709e6059b879eab92fdd06609df90cb9a2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858303"
---
# <a name="troubleshooting-adding-entry-points"></a>Beheben von Problemen beim Hinzufügen von Einstiegspunkten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält Informationen zum Beheben von Problemen mit dem Befehl `Add-DAEntryPoint`. Um sicherzustellen, dass sich der angezeigte Fehler auf das Hinzufügen eines Einstiegspunkts bezieht, prüfen Sie, ob im Windows-Ereignisprotokoll die Ereignis-ID 10067 aufgeführt wird.  
  
## <a name="missing-remoteaccessserver-parameter"></a>Fehlender RemoteAccessServer-Parameter  
Der **Fehler wurde empfangen**. Sie müssen einen Wert für den Parameter "remoteaccessserver" angeben.  
  
**Ursache**  
  
Wenn Sie einer Bereitstellung für mehrere Standorte einen neuen Einstiegspunkt hinzufügen, müssen Sie den Parameter *RemoteAccessServer* angeben. Hierbei handelt es sich um den Namen des Servers, den Sie als neuen Einstiegspunkt hinzufügen möchten.  
  
**Lösung**  
  
Führen Sie den Befehl aus, und geben Sie für den Parameter *RemoteAccessServer* den Namen des Servers an, der als Einstiegspunkt hinzugefügt werden soll.  
  
## <a name="remote-access-is-not-configured"></a>Nicht konfigurierter Remotezugriff  
Der **Fehler wurde empfangen**. Der Remote Zugriff ist auf < server_name > nicht konfiguriert. Geben Sie den Namen eines Servers an, der zu einer Bereitstellung für mehrere Standorte gehört.  
  
**Ursache**  
  
Remotezugriff ist auf dem Computer, der durch den Parameter *ComputerName* definiert wird, oder auf dem Computer, auf dem Sie den Befehl ausführen, nicht konfiguriert.  
  
Wenn Sie einer Bereitstellung für mehrere Standorte einen neuen Einstiegspunkt hinzufügen, müssen Sie zwei Parameter angeben: *ComputerName* und *RemoteAccessServer*. *ComputerName* ist der Name eines Servers, der bereits zu der Bereitstellung für mehrere Standorte gehört. *RemoteAccessServer* ist der Name des Servers, den Sie als neuen Einstiegspunkt hinzufügen möchten. Bei der Ausführung auf einem Computer, der bereits zu der Bereitstellung für mehrere Standorte gehört, ist der Parameter %%amp;quot;ComputerName%%amp;quot; nicht erforderlich.  
  
**Lösung**  
  
Führen Sie den Befehl aus, und geben Sie für den Parameter *ComputerName* den Namen des Servers an, der bereits so konfiguriert ist, dass er zu der Bereitstellung für mehrere Standorte gehört. Alternativ können Sie den Befehl auf einem Computer ausführen, der zu der Bereitstellung für mehrere Standorte gehört.  
  
## <a name="multisite-not-enabled"></a>Nicht aktivierte Funktionen für mehrere Standorte  
Der **Fehler wurde empfangen**. Sie müssen eine Bereitstellung für mehrere Standorte aktivieren, bevor Sie diesen Vorgang ausführen. Verwenden Sie hierzu das Cmdlet `Enable-DAMultiSite`.  
  
**Ursache**  
  
Die Funktionen für mehrere Standorte sind auf dem Server, der durch den Parameter *ComputerName* angegeben wird, nicht aktiviert. Sie müssen die Funktionen für mehrere Standorte aktivieren, um einer Remotezugriffsbereitstellung einen neuen Einstiegspunkt hinzuzufügen.  
  
**Lösung**  
  
Verwenden Sie das Cmdlet `Enable-DaMultiSite` zum Aktivieren der Funktionen für mehrere Standorte. Weitere Informationen finden Sie unter Bereitstellen des [Remote Zugriffs für mehrere Standorte](https://technet.microsoft.com/library/hh831664.aspx).  
  
## <a name="ipv6-prefix-issues"></a>Probleme mit IPv6-Präfixen  
  
-   **Problem 1**  
  
    Der **Fehler wurde empfangen**. IPv6 wird im internen Netzwerk bereitgestellt, aber Sie haben kein IPv6-Client Präfix angegeben.  
  
    **Ursache**  
  
    IPv6 wird im Unternehmensnetzwerk bereitgestellt, und ein IP-HTTPS-Präfix ist erforderlich. Es wurde jedoch für den neuen Einstiegspunkt kein Präfix im Parameter *ClientIPv6Prefix* angegeben.  
  
    **Lösung**  
  
    1.  Weisen Sie dem neuen Einstiegspunkt ein eindeutiges IP-HTTPS-Präfix zu, und stellen Sie sicher, dass Pakete, die an eine IP-Adresse unter diesem Präfix adressiert sind, an den Server weitergeleitet werden, den Sie hinzufügen.  
  
    2.  Führen Sie das Cmdlet `Add-DAEntryPoint` aus, und geben Sie im Parameter *ClientIPv6Prefix* das IP-HTTPS-Präfix an.  
  
-   **Problem 2**  
  
    Der **Fehler wurde empfangen**. Das IPv6-Präfix des Clients wird bereits von einem anderen Einstiegspunkt verwendet. Geben Sie einen anderen Wert an.  
  
    **Ursache**  
  
    Das im Parameter *ClientIPv6Prefix* angegebene IP-HTTPS-Präfix wird bereits von einem anderen Einstiegspunkt verwendet.  
  
    **Lösung**  
  
    1.  Weisen Sie dem neuen Einstiegspunkt ein eindeutiges IP-HTTPS-Präfix zu, und stellen Sie sicher, dass Pakete, die an eine IP-Adresse unter diesem Präfix adressiert sind, an den Server weitergeleitet werden, den Sie hinzufügen.  
  
    2.  Führen Sie das Cmdlet `Add-DAEntryPoint` aus, und geben Sie im Parameter *ClientIPv6Prefix* das IP-HTTPS-Präfix an.  
  
## <a name="connectto-address"></a>ConnectTo-Adresse  
Der **Fehler wurde empfangen**. Die Adresse (< connect_to_address >), mit der DirectAccess-Clients auf dem remoteaccess-Server eine Verbindung herstellen, ist identisch mit der Adresse des Netzwerkadressen Servers. Geben Sie einen anderen Wert an.  
  
**Ursache**  
  
Die ConnectTo-Adresse ist identisch mit der Adresse des Netzwerkadressenservers.  
  
**Lösung**  
  
Die ConnectTo-Adresse muss über das Internet aufgelöst werden können, damit Clientcomputer eine Verbindung über IP-HTTPS herstellen können. Die Adresse des Netzwerkadressenservers muss über das Unternehmensnetzwerk aufgelöst werden können, nicht jedoch über das Internet. Stellen Sie sicher, dass die Adresse des Netzwerkadressenservers nicht identisch mit der ConnectTo-Adresse ist. Wählen Sie andere Adressen aus, und versuchen Sie es erneut.  
  
## <a name="directaccess-or-vpn-already-installed"></a>DirectAccess oder VPN bereits installiert  
Der **Fehler wurde empfangen**. Auf dem Server wurde eine VPN-Installation erkannt, < server_name >. Geben Sie einen alternativen Server an, auf dem kein Remotezugriff installiert ist, oder entfernen Sie die VPN-Konfiguration vom Server.  
  
Oder  
  
Der Remote Zugriff ist auf dem Server < server_name > bereits installiert. Geben Sie einen alternativen Server an, auf dem DirectAccess nicht ausgeführt wird, oder entfernen Sie die vorhandene DirectAccess-Konfiguration vom Server.  
  
**Ursache**  
  
DirectAccess oder VPN ist bereits auf dem neuen Einstiegspunkt konfiguriert. Sie können einer Bereitstellung für mehrere Standorte keinen konfigurierten Einstiegspunkt hinzufügen.  
  
**Lösung**  
  
Um einem Server eine Bereitstellung für mehrere Standorte hinzuzufügen, müssen Sie die Remotezugriffsrolle auf dem Server installieren. DirectAccess und VPN dürfen jedoch nicht konfiguriert sein.  
  
Führen Sie den Befehl aus, und stellen Sie sicher, dass für den von Ihnen im Parameter *RemoteAccessServer* angegebenen Server DirectAccess und VPN nicht konfiguriert sind.  
  
## <a name="ipsec-root-certificate"></a>IPsec-Stammzertifikat  
Der **Fehler wurde empfangen**. Das konfigurierte IPSec-Stamm Zertifikat kann nicht auf dem Server < server_name > gefunden werden.  
  
**Ursache**  
  
Auf dem Server, den Sie zur Bereitstellung hinzufügen möchten, konnte das Zertifikat der Stamm- oder Zwischenzertifizierungsstelle, von der Computerzertifikate ausgestellt werden, nicht gefunden werden.  
  
**Lösung**  
  
Klicken Sie in der Remotezugriffs-Verwaltungskonsole in Schritt 2 **RAS-Server** auf **Bearbeiten**. Das Zertifikat, das sich auf der Seite **Authentifizierung** unter **Computerzertifikate verwenden** befindet, muss gültig sein. Wenn das Zertifikat gültig ist, stellen Sie sicher, dass es sich auf dem Server, den Sie hinzufügen möchten, unter der vertrauenswürdigen Stammzertifizierungsstelle befindet, und versuchen Sie es erneut.  
  
> [!NOTE]  
> Das Zertifikat muss das gleiche Zertifikat mit dem gleichen Fingerabdruck sein.  
  
Ist das Zertifikat ungültig, wählen Sie ein gültiges Zertifikat aus, das auf allen RAS-Servern als vertrauenswürdige Stammzertifizierungsstelle konfiguriert ist.  
  
## <a name="mixing-ipv6-and-ipv4-entry-points"></a>Vermischen von IPv6- und IPv4-Einstiegspunkten  
Bei der ersten Installation von DirectAccess wird der interne Netzwerkadapter überprüft. Dies dient der Feststellung, ob im Netzwerk ausschließlich IPv4-Adressen vorhanden sind (reines IPv4-Netzwerk), IPv6- und IPv4-Adressen, oder ausschließlich IPv6-Adressen (reines IPv6-Netzwerk). Diese Informationen werden zur Bestimmung des Bereitstellungstyps verwendet (nur IPv4, IPv6 und IPv4 oder nur IPv6).  
  
-   **Problem 1**  
  
    Die **Warnung wurde empfangen**. Der hinzugefügte RAS-Server wird mit IPv4-und IPv6-Adressen konfiguriert. Bei dieser Bereitstellung handelt es sich um eine reine IPv4-Bereitstellung, und die IPv6-Adressen werden von Remotezugriff ignoriert.  
  
    **Ursache**  
  
    Als diese Bereitstellung zum ersten Mal installiert wurde, wurde das interne Netzwerk als reines IPv4-Netzwerk erkannt. In einer Bereitstellung für mehrere Standorte wird davon ausgegangen, dass sich unterschiedliche Einstiegspunkte in unterschiedlichen Subnetzen mit unterschiedlichen Eigenschaften befinden. Daher kann die Bereitstellung, obwohl sie als reine IPv4-Bereitstellung konfiguriert ist, einen Einstiegspunkt enthalten, der sich in einem IPv6/IPv4-Subnetz befindet. Obwohl der Einstiegspunkt der Bereitstellung hinzugefügt wird, ignoriert DirectAccess die IPv6-Adressen, die in der internen Schnittstelle des neuen Einstiegs Punkts konfiguriert sind.  
  
    **Lösung**  
  
    Wenn das gesamte interne Netzwerk mit IPv6- und IPv4-Adressen konfiguriert ist, ist es u. U. ratsam, zu einer IPv6/IPv4-Bereitstellung zu wechseln, um die Vorteile der IPv6-Technologie nutzen zu können. Weitere Informationen finden Sie unter "Übergang von einem reinen IPv4 zu einem IPv6 + IPv4-Unternehmensnetzwerk" in [Schritt 3: Planen der Bereitstellung für mehrere Standorte](assetId:///19d49dbf-1786-47bb-ab97-f0458c53d91d).  
  
-   **Problem 2**  
  
    Der **Fehler wurde empfangen**. Die internen Netzwerkadapter der Remote Zugriffs Server in dieser Bereitstellung für mehrere Standorte werden mit IPv4-Adressen konfiguriert. Der hinzugefügte Einstiegspunkt muss auch mit einer IPv4-Adresse im internen Netzwerkadapter konfiguriert werden.  
  
    **Ursache**  
  
    Als diese Bereitstellung zum ersten Mal installiert wurde, wurde das interne Netzwerk als reines IPv4-Netzwerk erkannt. Von Remotezugriff wurde erkannt, dass der Einstiegspunkt, den Sie hinzufügen möchten, in seinem internen Netzwerk ausschließlich mit IPv6-Adressen konfiguriert ist. Dies ist in einer reinen IPv4-Bereitstellung nicht zulässig.  
  
    **Lösung**  
  
    Wenn das gesamte Netzwerk bereits mit IPv6-Adressen konfiguriert ist, sollten Sie zu einer IPv6/IPv4-Bereitstellung oder einer reinen IPv6-Bereitstellung wechseln. Weitere Informationen finden Sie unter "Planen des Übergangs zu IPv6 bei Bereitstellung des Remote Zugriffs für mehrere Standorte".  
  
-   **Problem 3**  
  
    Der **Fehler wurde empfangen**. Dieser Einstiegspunkt befindet sich in einem IPv4-Netzwerk, aber vorherige Einstiegspunkte befinden sich in einem IPv6-Netzwerk. Verbinden Sie diesen Einstiegspunkt mit dem IPv6-Netzwerk, bevor Sie ihn zu derselben Bereitstellung für mehrere Standorte hinzufügen.  
  
    **Ursache**  
  
    Als diese Bereitstellung zum ersten Mal installiert wurde, wurde das interne Netzwerk als IPv6/IPv4-Netzwerk oder als reines IPv6-Netzwerk erkannt. Es wurde erkannt, dass im internen Netzwerk des neuen Einstiegspunkts, den Sie hinzufügen möchten, ausschließlich IPv4-Adressen konfiguriert sind. Dies ist in IPv6/IPv4-Bereitstellungen bzw. in reinen IPv6-Bereitstellungen nicht erlaubt.  
  
    **Lösung**  
  
    Konfigurieren Sie den neuen Einstiegspunkt mit IPv6-Adressen, und fügen Sie ihn dann der Bereitstellung für mehrere Standorte hinzu.  
  
-   **Problem 4**  
  
    Die **Warnung wurde empfangen**. Der interne Netzwerkadapter auf dem Remote Zugriffs Server ist nicht mit einer IPv4-Adresse konfiguriert. DNS64 und NAT64 werden auf diesem Server nicht konfiguriert. DirectAccess-Clients können nur auf interne IPv6-Server zugreifen.  
  
    **Ursache**  
  
    Als diese Bereitstellung zum ersten Mal installiert wurde, wurde das interne Netzwerk als IPv6/IPv4-Netzwerk erkannt. In diesem Bereitstellungsmodus werden DNS64 und NAT64 aktiviert, damit Clientcomputer auf Computer im internen Netzwerk zugreifen können, die ausschließlich mit IPv4-Adressen konfiguriert sind.  
  
    Beim Hinzufügen des neuen Einstiegspunkts wurde von Remotezugriff erkannt, dass die interne Schnittstelle auf dem neuen Computer ausschließlich über IPv6-Adressen verfügt. Zum Konfigurieren von DNS64 und NAT64 ist eine IPv4-Adresse erforderlich, um die Pakete vom RAS-Server an den reinen IPv4-Computer weiterzuleiten. Da auf dem neuen Computer keine solche IP-Adresse vorhanden ist, werden NAT64 und DNS64 auf dem RAS-Server nicht konfiguriert. Daher können Clientcomputer, die mithilfe von DirectAccess über diesen Einstiegspunkt auf das Unternehmensnetzwerk zugreifen, nicht auf reine IPv4-Server im internen Netzwerk zugreifen. Informationen zum Übergang zu einem IPv6 + IPv4-Netzwerk oder zu einem reinen IPv6-Netzwerk finden Sie unter "Planen des Übergangs zu IPv6 bei Bereitstellung des Remote Zugriffs für mehrere Standorte".  
  
    **Lösung**  
  
    Fügen Sie dem neuen RAS-Server eine IPv4-Adresse hinzu, um sicherzustellen, dass DNS64 und NAT64 funktionieren.  
  
## <a name="domain-issues-with-the-servergponame"></a>Domänenbezogene Probleme mit ServerGpoName  
  
-   **Problem 1**  
  
    Der **Fehler wurde empfangen**. Die im servergponame-Parameter angegebene Domäne < server_GPO > ist nicht vorhanden. Geben Sie stattdessen die Domänen < domain_name > an.  
  
    **Ursache**  
  
    Der Teil mit dem Domänennamen des vom Administrator gesendeten Namens des Server-Gruppenrichtlinienobjekts (Group Policy Object, GPO) konnte nicht gefunden werden.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass Sie den Domänennamen richtig eingegeben haben. Ist der Domänenname richtig, versuchen Sie es erneut mit dem vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN).  
  
-   **Problem 2**  
  
    Der **Fehler wurde empfangen**. Das Server-GPO muss sich in der RAS-Server Domäne befinden. Geben Sie die Domänen < domain_name > im servergponame-Parameter an.  
  
    **Ursache**  
  
    Die Domäne des Server-GPO ist nicht identisch mit der Domäne, zu der der RAS-Server gehört.  
  
    **Lösung**  
  
    Das Server-GPO sollte sich in der gleichen Domäne wie der RAS-Server befinden. Verwenden Sie den Domänennamen des Servers für das Server-GPO, und versuchen Sie es erneut.  
  
## <a name="split-brain-dns"></a>Split-Brain-DNS  
Die **Warnung wurde empfangen**. Der NRPT-Eintrag für das DNS-Suffix < DNS_suffix > enthält den öffentlichen Namen, der von Client Computern zum Herstellen einer Verbindung mit dem RAS-Server verwendet wird. Fügen Sie den Namen < connect_to_address > als Ausnahme in der NRPT hinzu.  
  
**Ursache**  
  
Sie verwenden Split-Brain-DNS. Damit Clients eine Verbindung über IP-HTTPS herstellen können, sollten Sie sicherstellen, dass die ausgewählte ConnectTo-Adresse in den NRPT-Regeln ausgenommen ist.  
  
**Lösung**  
  
Stellen Sie in einer Bereitstellung für mehrere Standorte sicher, dass alle Adressen der verschiedenen Einstiegspunkte, mit denen eine Verbindung hergestellt wird, von den NRPT-Regeln ausgenommen sind.  
  
So erstellen Sie eine Ausnahme für eine Adresse in den NRPT-Regeln:  
  
1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole in Schritt 3 **Infrastrukturserver** auf **Bearbeiten**.  
  
2.  Doppelklicken Sie im Assistenten zum Einrichten des Infrastrukturservers auf der Seite **DNS** auf die Tabelle, um ein neues Namenssuffix einzugeben.  
  
3.  Geben Sie im Dialogfeld **DNS-Serveradressen** unter %%amp;quot;DNS-Suffix%%amp;quot; die ConnectTo-Adresse des Einstiegspunkts ein, und klicken Sie auf **Übernehmen**.  
  
Wenn Sie Namenssuffixe hinzufügen, ohne eine Serveradresse anzugeben, wird das Suffix als NRPT-Ausnahme behandelt.  
  
## <a name="saving-server-gpo-settings"></a>Speichern der Server-GPO-Einstellungen  
Der **Fehler wurde empfangen**. Fehler beim Speichern der Remote Zugriffs Einstellungen auf dem GPO-< GPO_name >.  
  
Informationen zum Beheben dieses Fehlers finden Sie unter Speichern von Server-GPO-Einstellungen unter Problembehandlung beim [Aktivieren von Multisite](https://technet.microsoft.com/library/jj591658.aspx).  
  
## <a name="gpo-updates-cannot-be-applied"></a>GPO-Aktualisierungen können nicht angewendet werden  
Die **Warnung wurde empfangen**. GPO-Aktualisierungen können nicht auf < server_name > angewendet werden. Die Änderungen werden erst nach der nächsten Richtlinienaktualisierung wirksam.  
  
**Ursache**  
  
Beim Aktualisieren der Richtlinien auf dem angegebenen Computer ist ein Fehler aufgetreten. Daher werden vorgenommene Änderungen erst nach der nächsten Richtlinienaktualisierung wirksam.  
  
**Lösung**  
  
Führen Sie auf dem angegebenen Computer `gpupdate /force` aus, um eine Richtlinienaktualisierung zu erzwingen.  
  


