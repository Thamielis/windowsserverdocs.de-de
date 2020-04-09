---
ms.assetid: c91c7196-ee0d-4856-8cfb-4c38494ccf1f
title: 'Übersicht: Arbeitsordner'
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 06/07/2019
description: Eine Übersicht über die Arbeitsordner - eine Serverrolle in Windows Server, durch die Benutzer auf einheitliche Art und Weise über PCs und Geräte auf ihre Arbeitsdateien zugreifen können.
ms.openlocfilehash: 67c62d81c7d9b6d33a198f5282fa39a88e07f2e8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820783"
---
# <a name="work-folders-overview"></a>Übersicht: Arbeitsordner

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1, Windows 7

In diesem Thema werden Arbeitsordner behandelt, ein Rollendienst für Dateiserver mit Windows Servern, durch die Benutzer auf einheitliche Art und Weise über PCs und Geräte auf ihre Arbeitsdateien zugreifen können.  
  
Wenn Sie Arbeitsordner auf Windows 10, Windows 7 oder einem Android-oder IOS-Gerät herunterladen oder verwenden möchten, finden Sie hier weitere Informationen:

- [Arbeitsordner für Windows 10](https://support.microsoft.com/help/12370/windows-10-work-folders)
- [Arbeitsordner für Windows 7 (64-Bit-Download)](https://www.microsoft.com/download/details.aspx?id=42558)
- [Arbeitsordner für Windows 7 (32-Bit-Download)](https://www.microsoft.com/download/details.aspx?id=42559)
- [Arbeitsordner für IOS](https://itunes.apple.com/app/work-folders/id950878067)
- [Arbeitsordner für Android](https://play.google.com/store/apps/details?id=com.microsoft.workfolders)

## <a name="role-description"></a>Rollenbeschreibung

 Benutzer können nicht nur mit Firmen-PCs sondern auch mit ihren eigenen Computern und Geräten auf Arbeitsdaten zugreifen und mit ihnen arbeiten. Dies wird als BYOD (bring-your-own-device) bezeichnet. Benutzer erhalten einen komfortablen Ort, um Arbeitsdateien zu speichern und von beliebigem Ort aus darauf zuzugreifen. Organisationen behalten die Kontrolle über Unternehmensdaten durch Speichern der Dateien auf zentral verwalteten Dateiservern und optionale Festlegung von Benutzerrichtlinien für Geräte (z.B. Verschlüsselung und Sperrbildschirmkennwörter).  
  
 Die Arbeitsordner können mit der vorhandenen Bereitstellung von Ordnerumleitung, Offlinedateien und Stammordner bereitgestellt werden. Arbeitsordner speichern Benutzerdateien in einem Ordner auf dem Server mit dem Namen *sync share*. Sie können einen Ordner angeben, der bereits Benutzerdaten enthält. Dadurch können Sie Arbeitsordner übernehmen, ohne Server und Daten zu migrieren oder sofort eine vorhandene Lösung abzulösen.  
  
## <a name="practical-applications"></a>Praktische Anwendungsfälle

 Administratoren können Arbeitsordner verwenden, um Benutzern Zugriff auf ihre Dateien zu ermöglichen und gleichzeitig die zentrale Speicherung und Kontrolle über die Daten des Unternehmens beizubehalten. Spezifische Anwendungen für Arbeitsordner umfassen:  
  
-   Eine zentrale Anlaufstelle für den Zugriff auf die Arbeitsdateien über private und geschäftliche PCs und Geräte des Benutzers bieten  
  
-   Zugriff auf Dateien offline und Synchronisierung mit dem zentralen Dateiserver, wenn der PC oder das Gerät mit dem Internet oder Intranet verbunden ist  
  
-   Mit vorhandenen Bereitstellungen von Ordnerumleitung, Offlinedateien und Stammordner bereitstellen  
  
-   Vorhandene Dateiserververwaltung-Technologien wie z. B. Dateiklassifizierung und Ordnerkontingente zum Verwalten von Benutzerdaten verwenden  
  
-   Sicherheitsrichtlinien für PCs und Geräte der Benutzer festlegen, um Arbeitsordner zu verschlüsseln und einen Sperrbildschirm mit Kennwort zu verwenden  
  
-   Failoverclustering mit Arbeitsordner für eine Hochverfügbarkeitslösung verwenden  
  
## <a name="important-functionality"></a>Wichtige Funktionalität

 Arbeitsordner enthalten folgende Funktionen.  
  
| Funktionalität | Verfügbarkeit | Beschreibung |  
| ------------------- | ------------------ | ----------------- |  
| Rollendienst für Arbeitsordner im Server-Manager | Windows Server 2019, Windows Server 2016 oder Windows Server 2012 R2 | Datei- und Speicherdienste bietet eine Möglichkeit zur Bereitstellung der Synchronisierungsfreigabe (Ordner, die Arbeitsdateien des Benutzers speichern), zur Überwachung von Arbeitsordnern und zur Verwaltung der Synchronisierungsfreigabe und der Zugriffsrechte von Benutzern |
| -Cmdlets für Arbeitsordner | Windows Server 2019, Windows Server 2016 oder Windows Server 2012 R2 | Ein Windows PowerShell-Modul, das umfassende -Cmdlets zum Verwalten von Arbeitsordnerservern enthält |  
| Integration der Arbeitsordner mit Windows | Windows 10<p> Windows 8.1<p> Windows RT 8.1<p> Windows 7 (Download erforderlich) | Arbeitsordner bietet folgende Funktionen in Windows-Computern:<p> -   Ein Systemsteuerungselement, das Arbeitsordner einrichtet und überwacht<br />-   Datei-Explorer-Integration, die den einfachen Zugriff auf Dateien in den Arbeitsordnern ermöglicht<br />-   Ein Synchronisierungsmodul, das Dateien von und zu einem zentralen Dateiserver überträgt und gleichzeitig die Akkulaufzeit und Systemleistung maximiert |
| Arbeitsordner-App für Geräte | Android<p> Apple iPhone und iPad® | Eine App, die häufig verwendeten Geräten Zugriff auf Dateien in den Arbeitsordnern ermöglicht |  
  
## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität
  
In der folgenden Tabelle werden einige der wichtigen Änderungen für Arbeitsordner beschrieben.  
  
| Feature/Funktionalität | Neu oder aktualisiert? | Beschreibung |
| ---------------------------- | --------------------- | ----------------- |
| Azure AD-Anwendungs-Proxyunterstützung | Wurde Windows 10, Version 1703, Android, iOS hinzugefügt | Remote-Benutzer können mithilfe von Azure AD-Anwendungsproxy sicher auf ihre Dateien auf dem Arbeitsordnerserver zugreifen. |
| Replikation schneller ändern | In Windows 10 und Windows Server 2016 aktualisiert | Werden unter Windows Server 2012 R2 Dateiänderungen auf die Arbeitsordner-Server synchronisiert, werden die Clients nicht über die Änderung benachrichtigt, und es dauert bis zu 10 Minuten, bis die Aktualisierungen verfügbar sind. Bei Verwendung von Windows Server 2016 benachrichtigt der Arbeitsordner Server sofort Windows 10-Clients, und die Dateiänderungen werden sofort synchronisiert. Diese Funktion ist neu in Windows Server 2016 und erfordert einen Windows 10-Client. Wenn Sie einen älteren Client verwenden oder wenn auf dem Arbeitsordnerserver Windows Server 2012 R2 ausgeführt wird, sucht der Client weiterhin alle zehn Minuten nach Änderungen. |  
| WIP-Integration (Windows Information Protection) | Wurde Windows 10 Version 1607 hinzugefügt | Wenn ein Administrator WIP bereit stellt, können die Arbeitsordner Datenschutz erzwingen, indem sie Daten auf dem PC verschlüsseln. Die Verschlüsselung verwendet einen der Enterprise-ID zugeordneten Schlüssel, der remote mithilfe eines unterstützten Mobilgerät Management-Pakets wie Microsoft Intune zurückgesetzt werden kann. |  
| Microsoft Office-Integration | Wurde Windows 10 Version 1511 hinzugefügt | Sie können in Windows 8.1 innerhalb der Office-Apps durch Anklicken oder Tippen auf „Dieser PC” zu den Arbeitsordnern auf den Speicherorten der Arbeitsordner auf Ihrem PC navigieren. In Windows 10 gelangen Sie noch einfacher zu den Arbeitsordnern, indem Sie diese der Liste der Speicherorte hinzufügen, die Office beim Speichern oder Öffnen von Dateien anzeigt. Weitere Informationen finden Sie unter [Arbeitsordner unter Windows 10](https://windows.microsoft.com/windows-10/work-folders-in-windows-10) und [Problembehandlung bei der Verwendung von Arbeitsordnern in Microsoft Office](https://social.technet.microsoft.com/wiki/contents/articles/32881.troubleshooting-using-work-folders-as-a-place-in-microsoft-office.aspx). |  
  
## <a name="software-requirements"></a>Softwareanforderungen

Für Arbeitsordner gelten die folgenden Softwareanforderungen für Dateiserver und die Netzwerkinfrastruktur:  
  
-   Ein Server, auf dem Windows Server 2019, Windows Server 2016 oder Windows Server 2012 R2 zum Hosting von Synchronisierungs Freigaben mit Benutzer Dateien ausgeführt wird  
  
-   Ein mit dem NTFS-Dateisystem formatiertes Volume zum Speichern von Benutzerdateien  
  
-   Sie müssen Kennwortrichtlinien für Gruppenrichtlinien verwenden, um Kennwortrichtlinien auf Computern mit Windows 7 zu erzwingen. Sie müssen die Computer mit Windows 7 auch aus Kennwortrichtlinien für Arbeitsordner ausschließen (wenn Sie diese verwenden).

-   Ein Serverzertifikat für jeden Dateiserver, der Arbeitsordner hostet. Diese Zertifikate sollten von einer Zertifizierungsstelle (ZS) stammen, die von den Benutzern als vertrauenswürdig eingestuft wird – im Idealfall von einer öffentlichen ZS.

-   Optionale Eine Active Directory Domain Services-Gesamtstruktur mit den-Schema Erweiterungen in Windows Server 2012 R2 zur Unterstützung der automatischen referenzierende von PCs und Geräten an den korrekten Dateiserver, wenn mehrere Dateiserver verwendet werden.  
  
Für die von Benutzern durchgeführte Synchronisierung über das Internet gelten die folgenden zusätzlichen Anforderungen:  
  
-   Die Möglichkeit, den Internetzugriff auf einen Server durch Erstellen von Veröffentlichungsregeln im Reverseproxy oder Netzwerkgateway der Organisation zu ermöglichen.  
  
-   (Optional) Ein öffentlich registrierter Domänenname und die Möglichkeit, zusätzliche öffentliche DNS-Einträge für die Domäne zu erstellen.  
  
-   (Optional) Active Directory-Verbunddienste (AD FS) (AD FS)-Infrastruktur bei Verwendung der AD FS-Authentifizierung.  
  
Für Arbeitsordner gelten die folgenden Softwareanforderungen für Clientcomputer:  
  
-   Auf dem PCs und Geräten muss eines der folgenden Betriebssysteme ausgeführt werden:  
  
    -   Windows 10  
  
    -   Windows 8.1  
  
    -   Windows RT 8.1  
  
    -   Windows 7  
  
    -   Android 4.4 KitKat und Nachfolgeversionen  
  
    -   iOS 10.2 und höher  
  
-   Computer mit Windows 7 müssen eine der folgenden Versionen von Windows ausführen:  
  
    -   Windows 7 Professional  
  
    -   Windows 7 Ultimate  
  
    -   Windows 7 Enterprise  
  
-   Computer mit Windows 7 müssen der Domäne Ihrer Organisation hinzugefügt werden (sie können keiner Arbeitsgruppe hinzugefügt werden).  
  
-   Ausreichend freier Speicherplatz auf einem lokalen, mit NTFS formatierten Laufwerk zum Speichern aller Dateien des Benutzers in Arbeitsordnern sowie zusätzliche 6 GB freier Speicherplatz, wenn sich Arbeitsordner auf dem Systemlaufwerk befinden (Standard). Arbeitsordner verwendet den folgenden Speicherort als Standardeinstellung: **%USERPROFILE%\Work Folders**  
  
     Benutzer können den Speicherort jedoch während der Installation ändern (mit dem NTFS-Dateisystem formatierte microSD-Karten und USB-Laufwerke werden als Speicherorte unterstützt, die Synchronisierung wird allerdings beendet, wenn die Laufwerke entfernt werden).  
  
     Die maximale Größe für einzelne Dateien beträgt standardmäßig 10 GB. Es gibt keine Speicherbegrenzung pro Benutzer, Administratoren können jedoch mit der Kontingentfunktion des Ressourcen-Managers für Dateiserver Kontingente implementieren.  
  
-   Arbeitsordner unterstützen das Zurücksetzen des Status von virtuellen Clientcomputern nicht. Führen Sie Sicherungs- und Wiederherstellungsvorgänge stattdessen innerhalb des virtuellen Clientcomputers mithilfe der Systemabbildsicherung oder einer anderen Sicherungsanwendung durch.  
  
## <a name="work-folders-compared-to-other-sync-technologies"></a>Arbeitsordner im Vergleich zu anderen Synchronisierungstechniken  

In der folgende Tabelle wird beschrieben, wie die verschiedenen Microsoft Synchronisierungstechnologien positioniert sind, und wann sie verwendet werden.  
  
| | Arbeitsordner | Offlinedateien | OneDrive for Business | OneDrive |
| - | ------------------ | ------------------- | -------------------------- | -------------- |
| **Zusammenfassung der Technologie** | Dateien synchronisieren, die auf einem Dateiserver mit PCs und Geräten gespeichert sind | Dateien synchronisieren, die auf einem Dateiserver mit PCs gespeichert sind, die auf Unternehmensnetzwerke zugreifen können (können durch Arbeitsordner ersetzt werden) | Dateien synchronisieren, die auf Office 365 oder SharePoint auf PCs und Geräte innerhalb oder außerhalb eines Unternehmensnetzwerks gespeichert sind und eine Funktion für die Zusammenarbeit bei Dokumenten bieten | Persönliche Dateien synchronisieren, die auf OneDrive mit PCs, Mac-Computern und Geräten gespeichert sind |
| **Bereitstellen des Benutzer Zugriffs auf Arbeitsdateien** | Ja | Ja | Ja | Nein |
| **Clouddienst** | Keine | Keine | Office 365 | Microsoft OneDrive |
| **Interne Netzwerkserver** | Dateiserver unter Windows Server 2012 R2 oder Windows Server 2016 | Dateiserver | SharePoint-Server (optional) | Keine |
| **Unterstützte Clients** | PCs, iOS, Android | In Unternehmensnetzwerken oder über DirectAccess, VPN oder andere RAS-Technologien verbundene PCs | PCs, iOS, Android, Windows Phone | PCs, Mac-Computer, Windows Phone, iOS, Android |
  
> [!NOTE]
>  Zusätzlich zu den in der vorherigen Tabelle aufgeführten Synchronisierungstechnologien bietet Microsoft andere Replikationstechnologien an, einschließlich DFS-Replikation, die für die Server-zu-Server-Replikation vorgesehen ist und BranchCache, die als WAN-Beschleunigungstechnologie für Zweigstellen vorgesehen ist. Weitere Informationen finden Sie unter [Übersicht über DFS-Namespaces und DFS-Replikation](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) und [Übersicht über BranchCache](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx) 
  
## <a name="server-manager-information"></a>Informationen zum Server-Manager  

Arbeitsordner sind Teil der Datei- und Speicherdienste-Rolle. Sie können Arbeitsordner mit dem Assistent zum Hinzufügen von Rollen und Features oder dem Cmdlet `Install-WindowsFeature` installieren. Beide Methoden erreichen Folgendes:  
  
-   Fügt die Seite **Arbeitsordner** im Server Manager unter **Datei- und Speicherdienste** hinzu  
  
-   Installiert den Windows-Synchronisierungsfreigabedienst, der von Windows Server zum Hosten von Synchronisierungsfreigaben verwendet wird  
  
-   Installiert das Windows PowerShell-Synchronisierungsfreigabemodul zum Verwalten von Arbeitsordnern auf dem Server  
  
## <a name="interoperability-with-windows-azure-virtual-machines"></a>Interoperabilität mit virtuellen Windows Azure-Computern

 Sie können diesen Windows Server-Rollendienst auf einem virtuellen Computer in Windows Azure ausführen. Dieses Szenario wurde für Windows Server 2012 R2 und Windows Server 2016 getestet.  
  
Weitere Informationen zu den ersten Schritten mit virtuellen Windows Azure-Computern finden Sie auf der [Windows Azure-Website](http://www.windowsazure.com/documentation/services/virtual-machines).  
  
## <a name="see-also"></a>Siehe auch

 Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:  
  
| Art des Inhalts | Verweise |
| ------------------ | ---------------- |
| **Produktbewertung** | -   [Arbeitsordner für Android – veröffentlicht](https://blogs.technet.microsoft.com/filecab/2016/03/16/work-folders-for-android-released) (Blogbeitrag)<br />-   [Arbeitsordner für IOS – iPad-App-Version](https://blogs.technet.com/b/filecab/archive/2015/01/16/work-folders-for-ios-ipad-app-release.aspx) (Blogbeitrag)<br />-   [Einführung in Arbeitsordner unter Windows Server 2012 R2](https://blogs.technet.com/b/filecab/archive/2013/07/09/introducing-work-folders-on-windows-server-2012-r2.aspx) (Blogbeitrag)<br />-   [Einführung in Arbeitsordner](https://channel9.msdn.com/posts/Introduction-to-Work-Folders) (Channel 9-Video)<br />[Arbeitsordner-Test Umgebungs Bereitstellung](https://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx) -   (Blogbeitrag)<br />[Arbeitsordner für Windows 7](https://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) -   (Blogbeitrag) |
| **Bereitstellung** | -   [Entwerfen einer Arbeitsordner Implementierung](plan-work-folders.md)<br />-   Bereitstellen von [Arbeits Ordnern](deploy-work-folders.md)<br />-   bereitstellen [von Arbeits Ordnern mit AD FS und webanwendungsproxy (WAP)](deploy-work-folders-adfs-overview.md)<br />-   bereitstellen [von Arbeits Ordnern mit Azure AD Anwendungs Proxy](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/)<br />[Migrations Handbuch für den - Offlinedateien (CSC) zu Arbeits Ordnern](https://blogs.technet.microsoft.com/filecab/2016/08/12/offline-files-csc-to-work-folders-migration-guide/)<br />[Überlegungen zur -   Leistung für Arbeitsordner Bereitstellungen](https://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx)<br />[Arbeitsordner für Windows 7 -   (64 Bit herunterladen)](https://www.microsoft.com/download/details.aspx?id=42558)<br />[Arbeitsordner für Windows 7 -   (32 Bit herunterladen)](https://www.microsoft.com/download/details.aspx?id=42559) |
| **Betrieb** | -   [Arbeitsordner iPad-App: FAQ](https://windows.microsoft.com/windows/work-folders-ipad-faq) (für Benutzer)<br />-   [Arbeitsordner Zertifikat Verwaltung](https://blogs.technet.com/b/filecab/archive/2013/08/09/work-folders-certificate-management.aspx) (Blogbeitrag)<br />-   über [Wachen von Windows Server 2012 R2-Arbeitsordner Bereitstellungen](https://blogs.technet.com/b/filecab/archive/2013/10/15/monitoring-windows-server-2012-r2-work-folders-deployments.aspx) (Blogbeitrag)<br />-   [syncshare-Cmdlets (Arbeitsordner) in Windows PowerShell](https://docs.microsoft.com/powershell/module/syncshare/?view=win10-ps)<br />-   [Storage-und Dateidienste PowerShell-Cmdlets kurz Referenzkarte für Windows Server 2012 R2 Preview Edition](https://blogs.technet.com/b/filecab/archive/2013/07/30/storage-and-file-services-powershell-cmdlets-quick-reference-card-for-windows-server-2012-r2-preview-edition.aspx) |
| **Problembehandlung** | -   [Windows Server 2012 R2 – Auflösen von Port Konflikten mit IIS-Websites und Arbeits Ordnern](https://blogs.technet.com/b/filecab/archive/2013/10/15/windows-server-2012-r2-resolving-port-conflict-with-iis-websites-and-work-folders.aspx) (Blogbeitrag)<br />-   von [häufigen Fehlern in Arbeits Ordnern](https://social.technet.microsoft.com/wiki/contents/articles/30578.common-errors-in-work-folders.aspx) |
| **Communityressourcen** | -   [Dateidienste und Speicher Forum](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverfiles)<br />-   [the Storage Team on Microsoft-File Cabinet Blog](https://blogs.technet.com/b/filecab/)<br />-   [Fragen Sie den Verzeichnisdienste-Teamblog](https://blogs.technet.com/b/askds/) |  
| **Verwandte Technologien** | -   [Speicher in Windows Server 2016](../storage.md)<br>[Datei-und Speicherdienste](https://technet.microsoft.com/library/hh831487(v=ws.11).aspx) -   <br />-   [Datei Server Ressourcen-Manager](https://technet.microsoft.com/library/hh831701(v=ws.11).aspx)<br />-   [Ordner Umleitung, Offlinedateien und Roamingbenutzerprofile](https://technet.microsoft.com/library/hh848267(v=ws.11).aspx)<br />[BranchCache](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx) -   <br />-   [DFS-Namespaces und DFS-Replikation](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) |
