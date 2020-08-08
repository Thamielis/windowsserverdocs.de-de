---
title: Schritt 2 Konfigurieren des grundlegenden DirectAccess-Servers
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit dem Assistenten für die ersten Schritte für Windows Server 2016
manager: brianlic
ms.topic: article
ms.assetid: 82bf5fed-93b3-4fa6-8e71-522146eccdb1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c70e68d6bdf96cd8493720936121b1ea90a9e971
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995909"
---
# <a name="step-2-configure-the-basic-directaccess-server"></a>Schritt 2 Konfigurieren des grundlegenden DirectAccess-Servers

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird die Konfiguration der Client- und Servereinstellungen erläutert, die für einen einfachen DirectAccess erforderlich sind. Vergewissern Sie sich vor Beginn der Bereitstellungs Schritte, dass Sie die in [Planen einer einfachen DirectAccess-Bereitstellung](Plan-a-Basic-DirectAccess-Deployment.md)beschriebenen Planungsschritte abgeschlossen haben.

|Aufgabe|BESCHREIBUNG|
|----|--------|
|Installieren der Remotezugriffsrolle|Installieren Sie die Remotezugriffsrolle.|
|Konfigurieren von DirectAccess mithilfe des Assistenten für erste Schritte|Der neue Assistent für erste Schritte sorgt für eine beträchtliche Vereinfachung der Konfiguration. Der Assistent hilft dabei, die Komplexität von DirectAccess zu überwinden, und ermöglicht so ein automatisches Setup in wenigen einfachen Schritten. Für den Administrator bietet der Assistent ein nahtloses Erlebnis, da der Kerberos-Proxy automatisch so konfiguriert wird, dass keine interne PKI-Bereitstellung erforderlich ist.|
|Aktualisieren von Clients mit der DirectAccess-Konfiguration|Zum Erhalt der DirectAccess-Einstellungen müssen Clients die Gruppenrichtlinien aktualisieren, während sie mit dem Intranet verbunden sind.|

> [!NOTE]
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="install-the-remote-access-role"></a><a name="BKMK_Role"></a>Installieren der Remotezugriffsrolle
Um den Remotezugriff bereitzustellen, müssen Sie die Remotezugriffsrolle auf einem Server in Ihrer Organisation installieren, der als RAS-Server fungiert.

#### <a name="to-install-the-remote-access-role"></a>So installieren Sie die Remotezugriffsrolle

1.  Klicken Sie auf dem Remote Zugriffs Server in der Server-Manager-Konsole im **Dashboard**auf **Rollen und Features hinzufügen**.

2.  Klicken Sie dreimal auf **Weiter**, um zur Anzeige für die Serverrollenauswahl zu gelangen.

3.  Wählen Sie im Dialogfeld **Serverrollen auswählen** die Option **Remotezugriff** aus, und klicken Sie dann auf **Weiter**.

4.  Klicken Sie im Dialogfeld **Features auswählen** auf **Weiter**.

5.  Klicken Sie auf **weiter**, und aktivieren Sie dann im Dialogfeld **Rollen Dienste auswählen** das Kontrollkästchen **DirectAccess und VPN (RAS)** .

6.  Klicken Sie auf **Features hinzufügen**, klicken Sie auf **weiter**und dann auf **Installieren**.

7.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.

![Äquivalente Windows PowerShell-Befehle in Windows](../../../media/Step-2-Configure-the-DirectAccess-Server/PowerShellLogoSmall.gif)***<em>PowerShell</em>***

Mit dem folgenden Windows PowerShell-Cmdlet oder den folgenden Cmdlets wird die Remote Zugriffs Rolle installiert:

1. Öffnen Sie PowerShell als Administrator.

2. Remote Zugriffs Feature installieren:

   ```
   Install-WindowsFeature RemoteAccess
   ```

3. Starten Sie den Computer neu:

   ```
   Restart-Computer
   ```

4. Installieren Sie PowerShell für den Remote Zugriff:

   ```
   Install-WindowsFeature RSAT-RemoteAccess-PowerShell
   ```




## <a name="configure-directaccess-with-the-getting-started-wizard"></a>Konfigurieren von DirectAccess mithilfe des Assistenten für erste Schritte

#### <a name="to-configure-directaccess-using-the-getting-started-wizard"></a>So konfigurieren Sie DirectAccess mithilfe des Assistenten für erste Schritte

1.  Klicken Sie im Server-Manager auf **Tools**, und klicken Sie anschließend auf **Remotezugriffsverwaltung**.

2.  Wählen Sie in der Remote Zugriffs-Verwaltungskonsole im linken Navigationsbereich den zu konfigurierendes Rollen Dienst aus, und klicken Sie dann auf **Assistent für die**ersten Schritte ausführen.

3.  Klicken Sie auf **Nur DirectAccess bereitstellen**.

4.  Wählen Sie die Topologie Ihrer Netzwerkkonfiguration aus, und geben Sie den öffentlichen Namen ein, mit dem Remotezugriffsclients eine Verbindung herstellen. Klicken Sie auf **Weiter**.

    > [!NOTE]
    > Standardmäßig stellt der Assistent für erste Schritte DirectAccess an alle Laptops und Notebookcomputer in der Domäne bereit, indem er einen WMI-Filter auf das Gruppenrichtlinienobjekt für die Clienteinstellungen anwendet.

5.  Klicken Sie auf **Fertig stellen**.

6.  Da in dieser Bereitstellung keine PKI verwendet wird, stellt der Assistent im Fall, dass keine Zertifikate gefunden werden, automatisch selbstsignierte Zertifikate für IP-HTTPS und den Netzwerkadressenserver bereit und aktiviert den Kerberos-Proxy. Außerdem aktiviert der Assistent NAT64 und DNS64 für die Protokollübersetzung in der auf IPv4 beschränkten Umgebung. Nachdem der Assistent die Konfiguration erfolgreich angewendet hat, klicken Sie auf **Schließen**.

7.  Wählen Sie in der Konsolenstruktur der Remotezugriffs-Verwaltungskonsole auf **Vorgangsstatus**. Warten Sie, bis der Status aller Monitore "Wird ausgeführt" lautet. Klicken Sie im Bereich %%amp;quot;Aufgaben%%amp;quot; unter %%amp;quot;Überwachung%%amp;quot; regelmäßig auf **Aktualisieren**, um die Anzeige zu aktualisieren.

## <a name="update-clients-with-the-directaccess-configuration"></a>Aktualisieren von Clients mit der DirectAccess-Konfiguration

#### <a name="to-update-directaccess-clients"></a>So aktualisieren Sie DirectAccess-Clients

1.  Starten Sie PowerShell als Administrator.

2.  Geben Sie im PowerShell-Fenster **gpupdate** ein, und drücken Sie dann die **EINGABETASTE**.

3.  Warten Sie, bis die Computerrichtlinien erfolgreich aktualisiert wurden.

4.  Geben Sie **Get-DnsClientNrptPolicy** ein, und drücken Sie die EINGABETASTE****.

    Die Einträge in der Richtlinientabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) für Direct Access werden angezeigt. Beachten Sie, dass die NLS-Serverausnahme angezeigt wird. Der Assistent für erste Schritte hat diesen DNS-Eintrag für den DirectAccess-Server automatisch erstellt und ein zugehöriges selbstsigniertes Zertifikat bereitgestellt, sodass der DirectAccess-Server als Netzwerkadressenserver fungieren kann.

5.  Geben Sie **Get-NCSIPolicyConfiguration** ein, und drücken Sie dann die EINGABETASTE****. Die vom Assistenten bereitgestellten Einstellungen für die Statusanzeige der Netzwerkkonnektivität werden angezeigt. Achten Sie auf den Wert von %%amp;quot;DomainLocationDeterminationURL%%amp;quot;. Sobald auf diese Netzwerkadressenserver-URL zugegriffen werden kann, ermittelt der Client, dass sie sich innerhalb des Unternehmensnetzwerks befindet, und die NRPT-Einstellungen werden nicht angewendet.

6.  Geben Sie **Get-DAConnectionStatus**, und drücken Sie dann die EINGABETASTE****. Da der Client die Netzwerkadressenserver-URL erreichen kann, wird der Status **Lokal verbunden** angezeigt.

## <a name="previous-step"></a><a name="BKMK_Links"></a>Vorheriger Schritt

-   [Schritt 1: Konfigurieren der DirectAccess-Infrastruktur](./da-basic-configure-s1-infrastructure.md)

## <a name="next-step"></a>Nächster Schritt

-   [Schritt 3 Überprüfen der grundlegenden DirectAccess-bereit Stellungen](da-basic-configure-s3-verify.md)