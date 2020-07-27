---
title: Installieren von Nano Server
description: Neuinstallation, Upgrade, Migration und Evaluierung von Nano Server
ms.prod: windows-server
manager: dougkim
ms.technology: server-nano
ms.date: 09/06/2017
ms.topic: get-started-article
ms.assetid: 2c2fa45b-6f3b-4663-b421-2da6ecc463bf
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 4002126ee6d9919c0a7fbfb3c068587c9acbecef
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953682"
---
# <a name="install-nano-server"></a>Installieren von Nano Server

>Gilt für: Windows Server 2016

> [!IMPORTANT]
> Ab Windows Server, Version 1709, steht Nano Server nur als [Basis-Betriebssystemimage für Container](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image) zur Verfügung. Sieh dir [Änderungen an Nano Server](nano-in-semi-annual-channel.md) an und erfahre, was dies bedeutet. 

Windows Server 2016 bietet eine neue Installationsoption: Nano Server. Nano Server ist ein remote verwaltetes Serverbetriebssystem, das für private Clouds und Rechenzentren optimiert ist. Das Betriebssystem ähnelt Windows Server im Modus Server Core, ist aber deutlich kleiner, hat keine Möglichkeit zur lokalen Anmeldung, und unterstützt ausschließlich 64-Bit-Anwendungen, Tools und Agents. Es beansprucht weit weniger Speicherplatz, wird erheblich schneller eingerichtet und erfordert wesentlich weniger Updates und Neustarts als Windows Server. Wenn Neustarts notwendig sind, erfolgen diese deutlich schneller. Die Installationsoption Nano Server ist für die Editionen Standard und Datacenter von Windows Server 2016 verfügbar.  

Nano Server eignet sich sehr gut für eine Anzahl von Szenarios:  
  
-   Als „Computehost“ für virtuelle Hyper-V-Computer, entweder in Clustern oder nicht  
  
-   Als Speicherhost für einen Dateiserver mit horizontaler Skalierung  
  
-   Als DNS-Server  
  
-   Als Webserver mit Ausführung von Internetinformationsdiensten (Internet Information Services, IIS)  
  
-   Als Host für Anwendungen, die mithilfe von Cloudanwendungsmustern entwickelt werden und in einem Container oder Gastbetriebssystem eines virtuellen Computers ausgeführt werden  
  
## <a name="important-differences-in-nano-server"></a>Wichtige Unterschiede in Nano Server

Da Nano Server als schlankes Betriebssystem für die Ausführung von nativen Cloudanwendungen basierend auf Containern und Microservices oder als flexibler und kosteneffizienter Datencenterhost mit deutlich reduziertem Ressourcenbedarf optimiert ist, gibt es wichtige Unterschiede zwischen Nano Server- und Server Core- bzw. „Server mit Desktopdarstellung“-Installationen:

- Nano Server ist monitorlos, d. h. Nano Server verfügt über keine grafische Benutzeroberfläche, und es gibt keine Möglichkeit zur lokalen Anmeldung.
- Nur 64-Bit-Anwendungen, -Tools und -Agents werden unterstützt.
- Sie können Nano Server nicht als Active Directory-Domänencontroller verwenden.
- Gruppenrichtlinien werden nicht unterstützt. Sie können jedoch [DSC](/previous-versions//dn387184(v=vs.85)) (Desired State Configuration) verwenden, um Einstellungen bedarfsgerecht anzuwenden.
- Nano Server kann nicht für die Verwendung eines Proxyservers für den Internetzugriff konfiguriert werden.
- NIC-Teamvorgänge (insbesondere Lastenausgleich und Failover oder LBFO) werden nicht unterstützt. Stattdessen wird Switch Embedded Teaming (SET) unterstützt.
- Microsoft Endpoint Configuration Manager und System Center Data Protection Manager werden nicht unterstützt.
- Best Practices Analyzer (BPA)-Cmdlets und BPA-Integration mit dem Server-Manager werden nicht unterstützt.
- Nano-Server unterstützen keine virtuellen Hostbusadapter (HBA).
- Nano Server muss nicht mit einem Product Key aktiviert werden. Wenn Nano Server als Hyper-V-Host fungiert, wird keine [automatische Aktivierung virtueller Computer](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303421(v=ws.11)) (AVMA) unterstützt. Virtuelle Computer, die auf einem Nano Server-Host ausgeführt werden, können mithilfe des [Schlüsselverwaltungsdienstes](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612867(v=ws.11)) (Key Management Service, KMS) mit einem generischen Volumenlizenzschlüssel oder mit der [Aktivierung über Active Directory](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502534(v=ws.11)) aktiviert werden.
- Die mit Nano Server bereitgestellte Version von Windows PowerShell weist wichtige Unterschiede auf. Details finden Sie unter [Unterschiede in PowerShell unter Nano Server](PowerShell-on-Nano-Server.md).
- Nano Server wird nur im aktuellen CBB-Modell (Current Branch for Business) unterstützt. Es gibt zurzeit keine LTSB-Version (Long-Term Servicing Branch) für Nano Server. Weitere Informationen finden Sie in den folgenden Unterabschnitten.

### <a name="current-branch-for-business"></a>Current Branch for Business
Nano Server wird mit einem aktiveren Modell namens Current Branch for Business (CBB) gewartet, um Kunden, die cloudgestützt ein hohes Aktionstempo vorlegen, unter Verwendung schneller Entwicklungszyklen zu unterstützen. In diesem Modell sind Featureupdateversionen von Nano Server zwei- bis dreimal pro Jahr zu erwarten. Für dieses Modell muss [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx) für Nano Server in der Produktionsumgebung bereitgestellt und betrieben werden. Um Support zu erhalten, müssen Administratoren stets mindestens die vorvorletzte CBB-Version verwenden. Vorhandene Bereitstellungen werden jedoch nicht automatisch mit diesen Versionen aktualisiert. Administratoren führen die manuelle Installation einer neuen CBB-Version bei Gelegenheit aus. Weitere Informationen finden Sie unter [Windows Server 2016 new Current Branch for Business servicing option](https://cloudblogs.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/) (Neue Wartungsoption Current Branch for Business in Windows Server 2016).

Die Server Core- und „Server mit Desktopdarstellung“-Installationsoptionen werden weiterhin über das [LTSB-Modell (Long-Term Servicing Branch)](https://support.microsoft.com/lifecycle#gp%2Fgp_msl_policy) gewartet, das 5 Jahre Mainstream-Support und 5 Jahre erweiterten Support umfasst.

## <a name="installation-scenarios"></a>Installationsszenarios

### <a name="evaluation"></a>Bewertung
Sie erhalten eine für 180 Tage lizenzierte Evaluierungskopie von Windows Server unter [Windows Server-Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016). Um Nano Server zu testen, wählen Sie zum Einstieg die **Nano Server | 64-Bit-EXE-Option**, und kehren dann entweder zu [Nano Server-Schnellstart](Nano-Server-Quick-Start.md) oder [Bereitstellen von Nano Server](Deploy-Nano-Server.md) zurück.

### <a name="clean-installation"></a>Neuinstallation
Da Sie Nano Server durch Konfigurieren einer virtuellen Festplatte (VHD) installieren, ist eine Neuinstallation die schnellste und einfachste Methode zur Bereitstellung.

- Wenn Sie schnell mit einer einfachen Bereitstellung von Nano Server mithilfe von DHCP zum Abrufen einer IP-Adresse beginnen möchten, finden Sie weitere Informationen unter [Nano Server-Schnellstart](Nano-Server-Quick-Start.md). 
- Wenn Sie bereits mit den Grundlagen von Nano Server vertraut sind, bieten detailliertere Themen Anweisungen zum Anpassen von Images, zum Arbeiten mit Domänen, zur Installation von Paketen für Serverrollen und andere Features (online und offline) und vieles mehr, beginnend bei [Bereitstellen von Nano Server](Deploy-Nano-Server.md).

> [!IMPORTANT]  
> Sobald das Setup abgeschlossen ist und alle Serverrollen und Features, die Sie benötigen, installiert sind, suchen und installieren Sie verfügbare Updates für Windows Server 2016. Updates für Nano Server finden Sie im Abschnitt „Verwalten von Updates in Nano Server“ unter [Verwalten von Nano Server](Manage-Nano-Server.md).

### <a name="upgrade"></a>Upgrade/Aktualisieren
Nano Server ist neu in Windows Server 2016. Daher gibt es keinen Upgradepfad von älteren Betriebssystemversionen zu Nano Server.

### <a name="migration"></a>Migration
Nano Server ist neu in Windows Server 2016. Daher gibt es keinen Migrationspfad von älteren Betriebssystemversionen zu Nano Server.
  
-------------------------------------
Wenn Sie eine andere Installationsoption benötigen, können Sie [zur Hauptseite von Windows Server 2016 zurückkehren.](windows-server-2016.md) 

  


 
