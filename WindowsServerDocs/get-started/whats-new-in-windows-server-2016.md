---
title: Neuerungen in Windows Server 2016
description: Welche neuen Features sind für Compute, Identitäten, Verwaltung, Automatisierung, Netzwerk, Sicherheit und Speicher verfügbar?
ms.date: 05/21/2019
ms.topic: article
ms.assetid: 2827f332-44d4-4785-8b13-98429087dcc7
author: jasongerend
ms.author: jgerend
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 5dfed9e70e4f0406c59c31201c8d2d1a9b3caafe
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766863"
---
# <a name="whats-new-in-windows-server-2016"></a>Neuerungen in Windows Server 2016

>Gilt für: Windows Server 2016

![Symbol einer Zeitung](media/whats-new.png) Informationen über die neuesten Features in Windows finden Sie unter [Neues in Windows Server](whats-new-in-windows-server.md). In diesem Abschnitt wird beschrieben, was in Windows Server&reg; 2016 neu ist und was sich geändert hat. Die hier aufgeführten Neuerungen und Änderungen haben bei der Arbeit in dieser Version vermutlich die größte Auswirkung.

## <a name="compute"></a>[Compute](../virtualization/virtualization.yml)

Der Virtualisierungsbereich umfasst Virtualisierungsprodukte und -features, mit denen IT-Profis Windows Server entwerfen, bereitstellen und warten können.

### <a name="general"></a>Allgemein
Physische und virtuelle Computer profitieren durch Verbesserungen beim Win32-Zeitdienst und Hyper-V-Uhrzeitsynchronisierungsdienst von einer höheren Zeitgenauigkeit. Windows Server kann jetzt zum Hosten von Diensten genutzt werden, die zukünftige Bestimmungen einhalten, bei denen eine Genauigkeit von 1 ms für UTC erforderlich ist.

### <a name="hyper-v"></a>Hyper-V
-   [Neues in Hyper-V auf Windows Server 2016](../virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows.md): In diesem Thema werden die neuen und überarbeiteten Funktionen der Hyper-V-Rolle in Windows Server 2016, Hyper-V für Clients mit Windows 10 und Microsoft Hyper-V Server 2016 beschrieben.

-   [Windows-Container](/virtualization/windowscontainers/):  Die Windows Server 2016-Containerunterstützung ermöglicht eine höhere Leistung, eine vereinfachte Netzwerkverwaltung sowie Unterstützung für Windows-Container unter Windows 10. Zusätzliche Informationen zu Containern finden Sie im Blog [Containers: Docker, Windows and Trends](https://azure.microsoft.com/blog/2015/08/17/containers-docker-windows-and-trends/) (Container: Docker, Windows und Trends).

### <a name="nano-server"></a>Nano Server
Neuerungen in [Nano Server](getting-started-with-nano-server.md). Nano Server verfügt nun über ein aktualisiertes Modul zum Erstellen von Nano Server-Images. Außerdem ist die Funktionalität für physische Hosts und Gast-VMs stärker getrennt, und Kunden profitieren von der Unterstützung für unterschiedliche Windows Server-Editionen.

Darüber hinaus wurde auch die Wiederherstellungskonsole verbessert. Zu diesen Verbesserungen zählt u.a. die Trennung von eingehenden und ausgehenden Firewallregeln sowie die Möglichkeit, die Konfiguration von WinRM zu reparieren.

### <a name="shielded-virtual-machines"></a>Abgeschirmte virtuelle Computer
Windows Server 2016 bietet eine neue Hyper-V-basierte abgeschirmte VM, um jeden virtuellen Computer der Generation 2 vor einem gefährdeten Fabric zu schützen. Zu den in Windows Server 2016 eingeführten Funktionen zählen die folgenden:

- Der neue Modus „Verschlüsselung unterstützt“, der einen umfangreicheren Schutz bietet als bei herkömmlichen virtuellen Computern, jedoch weniger Schutzmaßnahmen als im Modus „Geschützt“. Gleichzeitig werden vTPM, Datenträgerverschlüsselung, Datenverkehrverschlüsselung bei der Livemigration und andere Features weiterhin unterstützt. Dazu zählen auch die benutzerfreundlichen direkten Fabric-Verwaltungsfunktionen wie VM-Konsolenverbindungen und PowerShell Direct.

- Vollständige Unterstützung für die Umwandlung vorhandener nicht abgeschirmter Generation 2-VMs in abgeschirmte virtuelle Computer (einschließlich automatisierter Datenträgerverschlüsselung).

- Hyper-V Virtual Machine Manager kann jetzt die Fabrics anzeigen, auf denen ein abgeschirmter virtueller Computer ausgeführt werden darf. Dabei kann der Fabric-Administrator die Schlüsselschutzvorrichtung eines abgeschirmten virtuellen Computers anzeigen und ermitteln, für welche Fabrics der virtuelle Computer autorisiert ist.

- Für einen ausgeführten Host-Überwachungsdienst kann nun der Nachweismodus geändert werden. Sie können jetzt während der Ausführung zwischen dem weniger sicheren, jedoch einfacheren Active Directory-basierten Nachweis und dem TPM-basierten Nachweis wechseln.

- Auf Windows PowerShell basierende End-to-End-Diagnosetools, mit denen falsch konfigurierte Einstellungen oder Fehler in geschützten Hyper-V-Hosts und im Host-Überwachungsdienst ermittelt werden können.

- Eine Wiederherstellungsumgebung, mit der eine sicher Problembehandlung und Reparatur von abgeschirmten virtuellen Computern innerhalb des Fabrics möglich ist, in der diese normalerweise ausgeführt werden. Gleichzeitig bietet diese Umgebung dieselbe Schutzebene wie die abgeschirmten virtuellen Computer selbst.

- Unterstützung für den Host-Überwachungsdienst für vorhandenes sicheres Active Directory: Sie können den Host-Überwachungsdienst so steuern, dass dieser eine vorhandene Active Directory-Gesamtstruktur als Active Directory verwendet, anstatt eine eigene Active Directory-Instanz zu erstellen.

Weitere Einzelheiten und Anweisungen zur Arbeit mit abgeschirmten virtuellen Computern finden Sie unter [Shielded VMs and Guarded Fabric Validation Guide for Windows Server 2016 (TPM)](../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md) (Validierungsleitfaden für abgeschirmte virtuelle Computer und geschützte Fabrics für Windows Server 2016 [TPM]).

## <a name="identity-and-access"></a>[Identität und Zugriff](../identity/Identity-and-Access.yml)
Mit den neuen Features für Identitäten wird die Möglichkeit verbessert, Active Directory-Umgebungen zu schützen. Außerdem können Unternehmen eine Migration zu reinen Cloudbereitstellungen oder Hybridbereitstellungen durchführen, bei denen einige Anwendungen und Dienste in der Cloud und andere Anwendungen und Dienste lokal gehostet werden.

### <a name="active-directory-certificate-services"></a>Active Directory-Zertifikatdienste
Active Directory-Zertifikatdienste (AD CS) in Windows Server 2016 jetzt mit verbesserter Unterstützung für den TPM-Schlüsselnachweis: Sie können jetzt Smart Card KSP für den Schlüsselnachweis nutzen, und Geräte, die kein Domänenmitglied sind, können jetzt die NDES-Registrierung nutzen, um Zertifikate abzurufen, die als Nachweis für Schlüssel in einem TPM verwendet werden können.

### <a name="active-directory-domain-services"></a>Active Directory-Domänendienste (AD DS)
Active Directory-Domänendienste beinhalten Verbesserungen, die Unternehmen beim Schutz Ihrer Active Directory-Umgebungen helfen und die Identitätsverwaltung für Unternehmens- und private Geräte verbessern. Weitere Informationen finden Sie unter [Neues in Active Directory Domain Services (AD DS) unter Windows Server 2016](../identity/whats-new-active-directory-domain-services.md).

### <a name="active-directory-federation-services"></a>Active Directory-Verbunddienste
Neuerungen in Active Directory-Verbunddienste. Active Directory-Verbunddienste (AD FS) unter Windows Server 2016 enthält neue Funktionen, die Ihnen die Konfiguration von AD FS für die Authentifizierung von Benutzern ermöglichen, die in Lightweight Directory Access Protocol-Verzeichnissen (LDAP) gespeichert sind. Weitere Informationen finden Sie unter [What's New in AD FS for Windows Server 2016](../identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server.md) (Neuerungen in AD FS für Windows Server 2016).

### <a name="web-application-proxy"></a>Webanwendungsproxy
Im Fokus der aktuellen Version des Webanwendungsproxys stehen neue Features, die die Veröffentlichung und Vorauthentifizierung weiterer Anwendungen ermöglichen und das Benutzererlebnis verbessern. Sehen Sie sich die vollständige Liste der neuen Features an, die die Präauthentifizierung für funktionsreiche Client-Apps wie Exchange ActiveSync sowie Platzhalterdomänen für die einfachere Veröffentlichung von SharePoint-Apps umfassen. Weitere Informationen finden Sie unter [Webanwendungsproxy unter Windows Server 2016](../remote/remote-access/web-application-proxy/web-application-proxy-windows-server.md).

##  <a name="administration"></a>[Verwaltung](../administration/manage-windows-server.yml)
Im Bereich Verwaltung und Automatisierung liegt der Schwerpunkt auf Tool- und Referenzinformationen für IT-Profis, die Windows Server 2016 (einschließlich Windows PowerShell) ausführen und verwalten möchten.

Windows PowerShell 5.1 enthält wichtige neue Features – einschließlich Unterstützung für die Entwicklung mit Klassen und neue Sicherheitsfunktionen –, die den Funktionsumfang erweitern, die Benutzerfreundlichkeit verbessern und die Steuerung und Verwaltung von Windows-basierten Umgebungen erleichtern und erweitern. Weitere Informationen finden Sie unter [Neue Szenarien und Features in WMF 5.1](/powershell/wmf/5.1/scenarios-features).

Die neuen Features für Windows Server 2016 umfassen Folgendes: PowerShell.exe kann lokal unter Nano Server ausgeführt werden (nicht mehr nur remote), neue Cmdlets für lokale Benutzer und Gruppen ersetzen die GUI, neue PowerShell-Debuggingunterstützung sowie neue Unterstützung in Nano Server für Sicherheitsprotokollierung und -aufzeichnung sowie JEA.

Dies sind einige weitere neue Verwaltungsfeatures:

### <a name="powershell-desired-state-configuration-dsc-in-windows-management-framework-wmf-5"></a>PowerShell Desired State Configuration (DSC) im Windows Management Framework (WMF) 5
Windows Management Framework 5 enthält Updates für Windows PowerShell Desired State Configuration (DSC), die Windows-Remoteverwaltung (Windows Remote Management, WinRM) und die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI).

Weitere Informationen zum Testen der DSC-Features von Windows Management Framework 5 finden Sie in der Blogbeitragsreihe, die unter [Validate features of PowerShell DSC](https://devblogs.microsoft.com/powershell/validate-features-of-powershell-dsc/) (Überprüfen der PowerShell DSC-Features) besprochen wird. Die Downloaddateien finden Sie unter [Windows Management Framework 5.1](/powershell/scripting/wmf/setup/install-configure).

### <a name="packagemanagement-unified-package-management-for-software-discovery-installation-and-inventory"></a>Einheitliche Paketverwaltung mit PackageManagement für die Softwareerkennung, Installation und Inventur
Windows Server 2016 und Windows 10 enthalten ein neues PackageManagement-Feature (ehemals OneGet), das IT-Experten oder DevOps ermöglicht, die Erkennung, Installation und Inventarisierung von Software (Software Discovery, Installation, Inventory – SDII) lokal oder remote zu automatisieren, unabhängig von der Installationstechnologie und davon, wo sich die Software befindet.

Weitere Informationen finden Sie unter [https://github.com/OneGet/oneget/wiki](https://github.com/OneGet/oneget/wiki).

### <a name="powershell-enhancements-to-assist-digital-forensics-and-help-reduce-security-breaches"></a>PowerShell-Erweiterungen zur Unterstützung der digitalen Forensik und Verringerung von Sicherheitslücken
Um das Team zu unterstützen, das für die Untersuchung kompromittierter Systeme zuständig ist – manchmal als „Blue Team“ bezeichnet –, haben wir zusätzliche PowerShell-Protokollierungen und andere digitale, forensische Features hinzugefügt. Wir haben außerdem die Features zur Reduzierung von Sicherheitsrisiken in Skripts, z.B. PowerShell (eingeschränkt) und sichere CodeGeneration-APIs, hinzugefügt.

Weitere Informationen finden Sie im Artikel zum [PowerShell ♥ Blue Team](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/).

## <a name="networking"></a>[Netzwerk](../networking/index.yml)
Dieser Bereich befasst sich mit Netzwerkprodukten und -features, die IT-Spezialisten beim Entwerfen, Bereitstellen und Warten von Windows Server 2016 verwenden können.

### <a name="software-defined-networking"></a>Softwaredefinierte Netzwerke
Sie können Datenverkehr jetzt sowohl spiegeln als auch an neue oder vorhandene virtuelle Geräte leiten. In Kombination mit einer verteilten Firewall und Netzwerksicherheitsgruppen können Sie Workloads so – vergleichbar mit Azure – dynamisch segmentieren und schützen. Außerdem können Sie den gesamten softwaredefinierten Netzwerkstapel mithilfe von System Center Virtual Machine Manager bereitstellen und verwalten. Und Sie können Docker zum Verwalten von Windows Server-Containernetzwerken verwenden und SDN-Richtlinien nicht nur virtuellen Computern, sondern auch Containern zuordnen. Weitere Informationen finden Sie unter [Planen einer softwaredefinierten Netzwerkinfrastruktur](../networking/sdn/plan/plan-a-software-defined-network-infrastructure.md).

### <a name="tcp-performance-improvements"></a>TCP-Leistungsverbesserungen
Das standardmäßige anfängliche Überlastungsfenster (Initial Congestion Window, ICW) wurde von 4 auf 10 erhöht und TCP Fast Open (TFO) wurde implementiert. TFO reduziert den Zeitaufwand für das Herstellen einer TCP-Verbindung, und das erhöhte ICW ermöglicht die Übertragung von größeren Objekten in den anfänglichen Burst. Diese Kombination kann die erforderliche Zeit für die Übertragung eines Internetobjekts zwischen dem Client und der Cloud erheblich reduzieren.

Zur Verbesserung des TCP-Verhaltens bei der Wiederherstellung nach einem Paketverlust wurden TCP: Tail Loss Probe (TLP) und Recent ACKnowledgement (RACK) implementiert. TLP hilft bei der Konvertierung von RTOs (Retransmit TimeOuts) in schnelle Wiederherstellungen, und RACK reduziert die Zeit, die die schnelle Wiederherstellung benötigt, um ein verlorenes Paket erneut zu übertragen. 

## <a name="security-and-assurance"></a>[Sicherheit und Zuverlässigkeit](../security/Security-and-Assurance.yml)
Dieser Bereich umfasst Sicherheitslösungen und -features für Ihr Rechenzentrum und Ihre Cloudumgebung. Informationen zur allgemeinen Sicherheit in Windows Server 2016 finden Sie unter [Sicherheit und Zusicherungen](../security/Security-and-Assurance.yml).

### <a name="just-enough-administration"></a>Just Enough Administration
Just Enough Administration in Windows Server 2016 ist eine Sicherheitstechnologie, die eine delegierte Verwaltung für sämtliche Bereiche bietet, die sich mit Windows PowerShell verwalten lassen. Die Funktionen umfassen die Unterstützung für die Ausführung unter einer Netzwerkidentität, für das Herstellen einer Verbindung über PowerShell Direct, das sichere Kopieren von Dateien von/zu JEA-Endpunkten sowie das Konfigurieren der PowerShell-Konsole für den standardmäßigen Start in einem JEA-Kontext. Weitere Einzelheiten finden Sie auf den Webseiten zu [JEA auf GitHub](https://aka.ms/JEA).

### <a name="credential-guard"></a>Credential Guard
Credential Guard nutzt auf Virtualisierung basierende Sicherheitsverfahren, um geheime Daten zu isolieren, damit nur durch privilegierte Systemsoftware auf diese Daten zugegriffen werden kann. Siehe [Schützen abgeleiteter Domänenanmeldeinformationen mit Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard).

###  <a name="remote-credential-guard"></a>Remote Credential Guard
Credential Guard umfasst die Unterstützung für RDP-Sitzungen, damit die Anmeldeinformationen des Benutzers auf der Clientseite bleiben und nicht auf der Serverseite offengelegt werden. Außerdem wird Einmaliges Anmelden für Remotedesktop bereitgestellt. Weitere Informationen finden Sie unter [Schützen abgeleiteter Domänenanmeldeinformationen mit Windows Defender Credential Guard](/windows/access-protection/credential-guard/credential-guard).

### <a name="device-guard-code-integrity"></a>Device Guard (Codeintegrität)
Device Guard bietet Codeintegrität im Kernelmodus (Kernel Mode Code Integrity, KMCI) und Codeintegrität im Benutzermodus (User Mode Code Integrity, UMCI), indem Richtlinien erstellt werden, die angeben, welcher Code auf dem Server ausgeführt werden kann. Siehe [Einführung in Windows Defender Device Guard: virtualisierungsbasierte Sicherheit und Richtlinien zur Codeintegrität](/windows/device-security/device-guard/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies).


### <a name="windows-defender"></a>Windows Defender
[Übersicht über Windows Defender für Windows Server 2016](../security/windows-defender/windows-defender-overview-windows-server.md). Windows Server Antimalware wird in Windows Server 2016 standardmäßig installiert und aktiviert, die Benutzeroberfläche von Windows Server Antimalware wird jedoch nicht installiert. Windows Server Antimalware aktualisiert jedoch die Antischadsoftware-Definitionen und schützt Ihren Computer so auch ohne die Benutzeroberfläche. Wenn Sie die Benutzeroberfläche von Windows Server Antimalware benötigen, können Sie sie nach der Installation des Betriebssystems mit dem Assistenten zum Hinzufügen von Rollen und Features installieren.

### <a name="control-flow-guard"></a>Ablaufsteuerungsschutz
Beim Ablaufsteuerungsschutz (Control Flow Guard, CFG) handelt es sich um eine Plattformsicherheitsfunktion, die erstellt wurde, um auf Speicherbeschädigungs-Sicherheitsrisiken zu reagieren. Weitere Informationen finden Sie unter [Control Flow Guard (Ablaufsteuerungsschutz)](/windows/win32/secbp/control-flow-guard).


## <a name="storage"></a>[Speicher](../storage/storage.yml)

Der Speicher in Windows Server 2016 umfasst neue Funktionen und Verbesserungen für den softwaredefinierten Speicher sowie für herkömmliche Dateiserver. Nachstehend werden einige der neuen Funktionen dargestellt, weitere Verbesserungen und Informationen finden Sie unter [What's New in Storage in Windows Server 2016 (Neues im Speicher in Windows Server 2016)](../storage/whats-new-in-storage.md).

### <a name="storage-spaces-direct"></a>Speicherplätze DAS

Mit direkten Speicherplätzen kann hoch verfügbarer und skalierbarer Speicher unter Verwendung von Servern mit lokalem Speicher erstellt werden. Mit diesem Feature wird die Bereitstellung und die Verwaltung von softwaredefinierten Speichersystemen vereinfacht und auch der Weg zur Nutzung neuer Datenträgerklassen wie z. B. SATA-SSD und NVMe geebnet, was vorher bei gruppierten Speicherplätzen mit freigegebenen Datenträgern nicht möglich war.

Weitere Informationen finden Sie unter [Storage Spaces Direct (Direkte Speicherplätze)](../storage/storage-spaces/storage-spaces-direct-overview.md).

### <a name="storage-replica"></a>Speicherreplikat

Speicherreplikat ermöglicht eine speicheragnostische, synchrone Replikation auf Blockebene zwischen Servern oder Clustern für die Notfallwiederherstellung sowie das Strecken eines Failoverclusters zwischen Standorten. Die synchrone Replikation ermöglicht die Spiegelung von Daten an physischen Standorten mit ausfallsicheren Volumes, um auf Dateisystemebene sicherzustellen, dass kein Datenverlust auftritt. Die asynchrone Replikation ermöglicht die Standorterweiterung über regionale Bereiche hinaus mit der Möglichkeit von Datenverlusten.

Weitere Informationen finden Sie unter [Storage Replica overview (Speicherreplikat: Übersicht)](../storage/storage-replica/storage-replica-overview.md).

### <a name="storage-quality-of-service-qos"></a>Quality of Service (QoS) für Speicher

Sie können Quality of Service (QoS) für Speicher jetzt nutzen, um die End-to-End-Speicherleistung zu überwachen und Verwaltungsrichtlinien unter Verwendung von Hyper-V- und CSV-Clustern in Windows Server 2016 zu erstellen.

Weitere Informationen finden Sie unter [Storage Quality of Service (QoS für Speicher)](../storage/storage-qos/storage-qos-overview.md).

## <a name="failover-clustering"></a>[Failoverclustering](../failover-clustering/whats-new-in-failover-clustering.md)

Windows Server 2016 umfasst eine Reihe neuer Funktionen und Verbesserungen für mehrere Server, die mithilfe der Failoverclustering-Funktion in einem einzelnen fehlertoleranten Cluster zusammengefasst sind. Einige der Erweiterungen sind nachfolgend aufgeführt; eine vollständige Auflistung finden Sie unter [What's New in Failover Clustering in Windows Server 2016 (Neues beim Failoverclustering in Windows Server 2016)](../failover-clustering/whats-new-in-failover-clustering.md).

### <a name="cluster-operating-system-rolling-upgrade"></a>Paralleles Upgrade für Clusterbetriebssystem

Das parallele Upgrade für Clusterbetriebssysteme ermöglicht einem Administrator, das Upgrade des Betriebssystems des Clusterknotens von Windows Server 2012 R2 auf Windows Server 2016 ohne eine Unterbrechung von Hyper-V-Workloads oder Workloads des Dateiservers mit horizontaler Skalierung durchzuführen. Mit diesem Feature können die Downtimesanktionen laut Vereinbarungen zum Servicelevel (Service Level Agreements, SLA) vermieden werden.

Weitere Informationen finden Sie unter [Cluster Operating System Rolling Upgrade (Paralleles Upgrade für Clusterbetriebssysteme)](../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md).

### <a name="cloud-witness"></a>Cloudzeuge

Der Cloudzeuge ist ein neuer Failovercluster-Quorumzeugen-Typ in Windows Server 2016, der Microsoft Azure als Vermittlungspunkt nutzt. Der Cloudzeuge erhält wie jeder andere Quorumzeuge ein Votum und kann an der Quorumberechnung teilnehmen. Sie können den Cloudzeugen als Quorumzeugen konfigurieren, indem Sie den Assistenten zum Konfigurieren eines Clusterquorums verwenden.

Weitere Informationen finden Sie unter [Deploy a cloud witness for a Failover Cluster (Bereitstellen eines Cloudzeugen für einen Failovercluster)](../failover-clustering/deploy-cloud-witness.md).

### <a name="health-service"></a>Zustandsdienst

Mit dem Integritätsdienst werden die täglichen Überwachungsabläufe, Vorgänge und Wartungsaktivitäten von Clusterressourcen auf einem Cluster von Direkte Speicherplätze verbessert.

Weiter Informationen finden Sie unter [Health Service in Windows Server 2016 (Integritätsdienst in Windows Server 2016)](../failover-clustering/health-service-overview.md).

## <a name="application-development"></a>Anwendungsentwicklung

### <a name="internet-information-services-iis-100"></a>Internetinformationsdienste (IIS) 10.0
Zu den neuen Features des IIS 10.0-Webservers unter Windows Server 2016 gehören:

- Die Unterstützung des HTTP/2-Protokolls im Netzwerkstapel und Integration in IIS 10.0 ermöglicht IIS 10.0-Websites die automatische Verarbeitung von HTTP/2-Anforderungen für unterstützte Konfigurationen. Dies ermöglicht zahlreiche Verbesserungen gegenüber HTTP/1.1, z.B. die effizientere Wiederverwendung von Verbindungen und geringere Latenz, wodurch die Ladezeiten für Webseiten verbessert werden.
- Möglichkeit zum Ausführen und Verwalten von IIS 10.0 unter Nano Server. Informationen dazu finden Sie unter [IIS unter Nano Server](iis-on-nano-server.md).
- Die Unterstützung für Platzhalter-Hostheader ermöglicht Administratoren die Einrichtung eines Webservers für eine Domäne und die anschließende Verarbeitung von Anforderungen für jede Unterdomäne durch den Webserver.
- Ein neues PowerShell-Modul (IISAdministration) zum Verwalten von IIS.

Weitere Informationen finden Sie unter [IIS](https://iis.net/learn).

### <a name="distributed-transaction-coordinator-msdtc"></a>Distributed Transaction Coordinator (MSDTC)
In Microsoft Windows 10 und Windows Server 2016 werden drei neue Features hinzugefügt:

- Eine neue Benutzeroberfläche für den erneuten Beitritt zum Ressourcen-Manager (Resource Manager Rejoin) kann von einem Ressourcenmanager zum Ermitteln des Ergebnisses einer unsicheren Transaktion nach dem Neustart einer Datenbank aufgrund eines Fehlers verwendet werden. Details finden Sie unter [IResourceManagerRejoinable::Rejoin](/previous-versions/windows/desktop/mt203799(v=vs.85)).

- Der Grenzwert des DSN-Namens wurde von 256 Bytes auf 3072 Bytes heraufgesetzt. Details finden Sie unter [IDtcToXaHelperFactory::Create](/previous-versions/windows/desktop/ms686861(v=vs.85)), [IDtcToXaHelperSinglePipe::XARMCreate](/previous-versions/windows/desktop/ms679248(v=vs.85)) oder [IDtcToXaMapper::RequestNewResourceManager](/previous-versions/windows/desktop/ms680310(v=vs.85)).

- Die verbesserte Ablaufverfolgung ermöglicht Ihnen das Festlegen eines Registrierungsschlüssels, um den Pfad einer Imagedatei in den Namen der Ablaufverfolgungs-Protokolldatei aufzunehmen, sodass Sie sehen können, welche Ablaufverfolgungs-Protokolldatei überprüft werden muss. Ausführliche Informationen zum Konfigurieren der Ablaufverfolgung für MSDTC finden Sie unter [Aktivieren der Diagnoseablaufverfolgung für MS DTC auf einem Windows-basierten Computer](https://support.microsoft.com/kb/926099).



## <a name="see-also"></a>Weitere Informationen
-   [Versionshinweise: Wichtige Probleme in Windows Server 2016](Windows-Server-2016-GA-Release-Notes.md)