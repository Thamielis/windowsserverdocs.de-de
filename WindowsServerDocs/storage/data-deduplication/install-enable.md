---
ms.assetid: 07d6b251-c492-4d9f-bcc4-031023695b24
title: Installieren und Aktivieren der Datendeduplizierung
ms.technology: storage-deduplication
ms.prod: windows-server
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 05/09/2017
description: Installieren der Datendeduplizierung unter Windows Server, bestimmen, ob eine Arbeitsauslastung ein guter Kandidat für die Deduplizierung ist, und Aktivieren der Deduplizierung auf Volumes.
ms.openlocfilehash: 82c55c12e7b5d5f60be7569ee2d7885daa6b6339
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953622"
---
# <a name="install-and-enable-data-deduplication"></a>Installieren und Aktivieren der Datenduplizierung
> Gilt für Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird erläutert, wie Sie [Datendeduplizierung](overview.md) installieren, Workloads für die Deduplizierung bestimmen und die Datendeduplizierung auf bestimmten Volumes aktivieren.

> [!Note]  
> Wenn Sie beabsichtigen, die Datendeduplizierung in einem Failovercluster auszuführen, muss für jeden Knoten im Cluster die datendeduplizierungsserver-Rolle installiert sein.

## <a name="install-data-deduplication"></a><a id="install-dedup"></a>Installieren der Datendeduplizierung
> [!Important]  
> [KB4025334](https://support.microsoft.com/kb/4025334) enthält einen Rollup der Fehlerbehebungen für die Datendeduplizierung, einschließlich wichtiger Korrekturen der Zuverlässigkeit. Wir empfehlen dringend, Sie zu installieren, wenn Sie die Datendeduplizierung mit Windows Server 2016 verwenden.

### <a name="install-data-deduplication-by-using-server-manager"></a><a id="install-dedup-via-server-manager"></a>So installieren Sie die Datendeduplizierung mithilfe des Server-Managers
1. Wählen Sie im Assistenten zum Hinzufügen von Rollen und Features **Serverrollen** aus, und wählen sie dann **Datendeduplizierung** aus.  
![Installieren Sie die Datendeduplizierung über Server-Manager: Wählen Sie Datendeduplizierung aus Server Rollen aus.](media/install-dedup-via-server-manager-1.png)
2. Klicken Sie auf **Weiter** , bis die Schaltfläche **Installieren** aktiviert wird, und klicken Sie dann auf **Installieren**.  
![Installieren Sie die Datendeduplizierung über Server-Manager: Klicken Sie auf installieren.](media/install-dedup-via-server-manager-2.png)

### <a name="install-data-deduplication-by-using-powershell"></a><a id="install-dedup-via-powershell"></a>Installieren der Datendeduplizierung mithilfe von PowerShell
Um die Datendeduplizierung zu installieren, führen Sie den folgenden PowerShell-Befehl als Administrator aus:  
`Install-WindowsFeature -Name FS-Data-Deduplication`

So installieren Sie die Datendeduplizierung in einer Nano Server-Installation

1. Erstellen Sie eine Nano Server-Installation mit dem installierten Speicher, wie unter [Install Nano Server (Installieren von Nano Server)](../../get-started/getting-started-with-nano-server.md) beschrieben.
2. Installieren Sie auf einem Server mit Windows Server 2016 in einem anderen Modus als Nano Server oder von einem Windows-PC mit installierten [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=45520) (Remote Server Administration Tools, RSAT) die Datendeduplizierung mit einem expliziten Verweis auf die Nano Server-Instanz (ersetzen Sie „MyNanoServer“ durch den tatsächlichen Namen der Nano Server-Instanz):  
    ```PowerShell
    Install-WindowsFeature -ComputerName <MyNanoServer> -Name FS-Data-Deduplication
    ```  
    <br />
    <strong>--Oder--</strong>
    <br />
    Stellen Sie mithilfe von PowerShell-Remoting eine Remoteverbindung mit der Nano Server-Instanz her, und installieren Sie die Datendeduplizierung, indem Sie DISM verwenden:  
    
    ```PowerShell
    Enter-PSSession -ComputerName MyNanoServer 
    dism /online /enable-feature /featurename:dedup-core /all
    ```

## <a name="enable-data-deduplication"></a><a id="enable-dedup"></a>Datendeduplizierung aktivieren
### <a name="determine-which-workloads-are-candidates-for-data-deduplication"></a><a id="enable-dedup-candidate-workloads"></a>Bestimmen, welche Workloads für die Deduplizierung in Frage kommen
Datendeduplizierung kann ein effektives Instrument zum Minimieren der Kosten für die Datennutzung einer Serveranwendung sein, indem der Speicherplatz reduziert wird, der von redundanten Daten belegt wird. Vor der Aktivierung der Deduplizierung ist es wichtig, dass Sie die Merkmale Ihrer Workload verstehen, um sicherzustellen, dass Ihr Speicher Ihnen die maximale Leistung bietet. Zwei Arten von Workloads müssen berücksichtigt werden:

* *Empfohlene Workloads*, die nachweislich sowohl Datasets enthalten, die umfassend von der Datendeduplizierung profitieren, als auch Ressourcennutzungsmuster aufweisen, die mit dem Nachbearbeitungsmodell der Datendeduplizierung kompatibel sind. Es wird empfohlen, dass Sie für die folgenden Workloads stets die [Datendeduplizierung aktivieren](install-enable.md#enable-dedup-lights-on):
    * Allgemeine Dateiserver mit Freigaben(General purpose file servers, GPFS) wie Teamfreigaben, Basisordner von Benutzern, Arbeitsordnern und Freigaben für die Softwareentwicklung
    * VDI-Server (virtuelle Desktopinfrastruktur)
    * Virtualisierte Sicherungs Anwendungen, wie z. b. [Microsoft Data Protection Manager (DPM)](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)).
* Workloads, die ggf. von der Deduplizierung profitieren, aber nicht immer gute Kandidaten für die Deduplizierung sind Die folgenden Workloads sind z.B. gut für die Deduplizierung geeignet, jedoch sollen Sie zunächst die Vorteile der Deduplizierung evaluieren:
    * Allgemeine Hyper-V-Hosts
    * SQL-Server
    * Branchenspezifische Server

### <a name="evaluate-workloads-for-data-deduplication"></a><a id="enable-dedup-evaluating-sometimes-workloads"></a>Auswerten von Workloads für die Datendeduplizierung
> [!Important]  
> Bei Ausführen einer empfohlenen Workload können Sie diesen Abschnitt überspringen und für Ihre Workload [Aktivieren der Datendeduplizierung](install-enable.md#enable-dedup-lights-on) aufrufen.

Um zu bestimmen, ob sich eine Workload gut für die Deduplizierung eignet, beantworten Sie die folgenden Fragen. Wenn Sie sich bei einer Workload nicht sicher sind, erwägen Sie eine Pilotbereitstellung der Datendeduplizierung für ein Testdataset Ihrer Workload, um das Ergebnis zu prüfen.

1. **Weist das Dataset meiner Workload genügend Duplizierung auf, um vom Aktivieren der Deduplizierung zu profitieren?**  
    Überprüfen Sie vor dem Aktivieren der Datendeduplizierung für eine Workload, wie viele Duplikate das Dataset Ihrer Workload aufweist. Nutzen Sie dazu das Tool für die Auswertung der Einsparungen durch Datendeduplizierung (DDPEval). Nach Installation der Datendeduplizierung finden Sie dieses Tool unter `C:\Windows\System32\DDPEval.exe`. DDPEval kann das Optimierungspotenzial für direkt angeschlossene Volumes (so z.B. lokale Laufwerke oder freigegebene Clustervolumes) sowie zugeordnete und nicht zugeordnete Netzwerkfreigaben einschätzen.  
    &nbsp;   
    Bei Ausführen von „DDPEval.exe“ wird eine Ausgabe ähnlich der folgenden zurückgegeben:  
    &nbsp;  
    `Data Deduplication Savings Evaluation Tool`  
    `Copyright 2011-2012 Microsoft Corporation.  All Rights Reserved.`    
    &nbsp;   
    `Evaluated folder: E:\Test`     
    `Processed files: 34`  
    `Processed files size: 12.03MB`  
    `Optimized files size: 4.02MB`  
    `Space savings: 8.01MB`  
    `Space savings percent: 66`  
    `Optimized files size (no compression): 11.47MB`  
    `Space savings (no compression): 571.53KB`  
    `Space savings percent (no compression): 4`  
    `Files with duplication: 2`  
    `Files excluded by policy: 20`  
    `Files excluded by error: 0`  

2. **Wie sehen die e/a-Muster meiner Arbeitsauslastung für das DataSet aus? Welche Leistung habe ich für meine Arbeitsauslastung?**  
     Die Datendeduplizierung optimiert die Daten im Rahmen eines regelmäßigen Auftrags, anstatt sie zu optimieren, wenn eine Datei auf einen Datenträger geschrieben wird. Deshalb ist es zunächst wichtig, dass die erwarteten Lesemuster einer Workload auf dem deduplizierten Volume untersucht werden. Da bei der Datendeduplizierung Dateiinhalte in den Blockspeicher verschoben werden und versucht wird, den Blockspeicher so umfassend wie möglich dateibezogen zu organisieren, liefern Lesevorgänge die beste Leistung, wenn sie entsprechend sequenziellen Bereichen einer Datei angewendet werden.  

    Datenbankähnliche Workloads weisen zumeist eher Lesemuster nach dem Zufallsprinzip als sequenzielle Lesemuster auf, da Datenbanken in der Regel nicht gewährleisten, dass das Datenbanklayout für alle möglicherweise ausgeführten Abfragen optimal ist. Da sich die Abschnitte des Blockspeichers auf dem gesamten Volume befinden können, kann es beim Zugriff auf Datenbereiche im Blockspeicher für Datenbankabfragen zu zusätzlicher Latenz kommen. Hochleistungsworkloads sind besonders empfindlich für diese zusätzliche Latenz, andere datenbankähnliche Workloads jedoch möglicherweise nicht.

    > [!Note]  
    > Diese Aspekte gelten in erster Linie für Speicherworkloads auf Volumes, die aus herkömmlichen rotierenden Speichermedien (also Festplattenlaufwerken bzw. HDDs) bestehen. Die gesamte Flashspeicherinfrastruktur (Solid State Disk-Laufwerke bzw. SSDs) ist von zufälligen E/A-Mustern weniger betroffen, da bei Flash-Speichermedien die Zugriffszeit auf alle Speicherorte im Datenträger gleich lang ist. Daher sorgt eine Deduplizierung nicht für denselben Umfang von Latenz bei Lesevorgängen in den Datasets einer Workload, die vollständig auf Flashmedien gespeichert sind, wie bei herkömmlichen rotierenden Speichermedien.

3. **Wie hoch ist der Ressourcenbedarf meiner Workload auf dem Server?**  
    Da bei der Datendeduplizierung ein Nachbearbeitungsmodell zum Einsatz kommt, sind für die Datendeduplizierung regelmäßig genügend Systemressourcen erforderlich, um die [Optimierung und andere Aufträge](understand.md#job-info) auszuführen. Dies bedeutet, dass Workloads mit Leerlaufzeit, z.B. abends oder am Wochenende, sich besonders für die Deduplizierung eignen, was bei rund um die Uhr ausgeführten Workloads ggf. nicht der Fall ist. Workloads ohne Leerlaufzeiten können sich dennoch gut für eine Deduplizierung eignen, wenn sie keinen hohen Ressourcenbedarf auf dem Server haben.

### <a name="enable-data-deduplication"></a><a id="enable-dedup-lights-on"></a>Datendeduplizierung aktivieren
Sie müssen vor dem Aktivieren der Datendeduplizierung den [Verwendungstyp](understand.md#usage-type) wählen, der Ihrer Workload am ehesten entspricht. Für die Datendeduplizierung gibt es drei Verwendungstypen.

* [Standard](understand.md#usage-type-default) – speziell für allgemeine Dateiserver optimiert
* [Hyper-V](understand.md#usage-type-hyperv) – speziell für VDI-Server optimiert
* [Sicherung](understand.md#usage-type-backup) – speziell für virtualisierte Sicherungsprogramme wie [Microsoft Data Protection Manager (DPM)](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) optimiert

#### <a name="enable-data-deduplication-by-using-server-manager"></a><a id="enable-dedup-via-server-manager"></a>Aktivieren der Datendeduplizierung mithilfe von Server-Manager
1. Wählen Sie in Server-Manager **Datei-und Speicherdienste** aus.  
![Klicken auf „Datei- und Speicherdienste“](media/enable-dedup-via-server-manager-1.PNG)
2. Wählen Sie **Volumes** im Menü **Datei- und Speicherdienste** aus.  
![Klicken auf „Volumes“](media/enable-dedup-via-server-manager-2.png)
3. Klicken Sie mit der rechten Maustaste auf das gewünschte Volume, und wählen Sie **Datendeduplizierung konfigurieren** aus.  
![Klicken auf „Datendeduplizierung konfigurieren“.](media/enable-dedup-via-server-manager-3.png)
4. Wählen Sie im Dropdownfeld den gewünschten **Verwendungstyp** aus, und klicken Sie auf **OK**.  
![Auswählen des gewünschten Verwendungstyps im Dropdownfeld](media/enable-dedup-via-server-manager-4.png)
5. Wenn Sie eine empfohlene Workload ausführen, sind Sie fertig. Sehen Sie sich für andere Workloads die [weiteren Aspekte](#enable-dedup-sometimes-considerations) an.

> [!Note]  
> Weitere Informationen zum Ausschließen von Dateinamenerweiterungen oder Ordnern und Auswählen des Zeitplans für die Deduplizierung, einschließlich Gründen, finden Sie unter [Konfigurieren der Datendeduplizierung](advanced-settings.md).

#### <a name="enable-data-deduplication-by-using-powershell"></a><a id="enable-dedup-via-powershell"></a>Aktivieren der Datendeduplizierung mit PowerShell
1. Führen Sie im Kontext eines Administrators den folgenden PowerShell-Befehl aus:  
    ```PowerShell
    Enable-DedupVolume -Volume <Volume-Path> -UsageType <Selected-Usage-Type>
    ```

2. Wenn Sie eine empfohlene Workload ausführen, sind Sie fertig. Sehen Sie sich für andere Workloads die [weiteren Aspekte](#enable-dedup-sometimes-considerations) an.

> [!Note]  
> Die PowerShell-Cmdlets für die Datendeduplizierung, einschließlich [`Enable-DedupVolume`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) , können Remote ausgeführt werden, indem der- `-CimSession` Parameter an eine CIM-Sitzung angehängt wird. Dies ist besonders nützlich für die Remoteausführung der PowerShell-Cmdlets für die Datendeduplizierung für eine Nano Server-Instanz. Zum Erstellen einer neuen CIM-Sitzungs Führung [`New-CimSession`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) .

#### <a name="other-considerations"></a><a id="enable-dedup-sometimes-considerations"></a>Weitere Überlegungen
> [!Important]  
> Wenn Sie eine empfohlene Workload ausführen, können Sie diesen Abschnitt überspringen.

* Die Verwendungstypen für die Datendeduplizierung arbeiten mit sinnvollen Standardwerten für empfohlene Workloads, bieten aber auch einen guten Ausgangspunkt für alle Workloads. Für andere Workloads als die empfohlenen lassen sich die [erweiterten Einstellungen für die Datendeduplizierung](advanced-settings.md) ändern, um die Deduplizierungsleistung zu verbessern.
* Wenn Ihre Workload einen hohen Ressourcenbedarf auf Ihrem Server hat, [müssen die Datendeduplizierungsaufträge während der erwarteten Leerlaufzeiten für die jeweilige Workload ausgeführt werden](advanced-settings.md#modifying-job-schedules-change-schedule). Dies ist besonders wichtig bei der Ausführung der Deduplizierung auf einem hyperkonvergenten Host, da die Ausführung der Datendeduplizierung während der Geschäftszeiten VMs beeinträchtigen kann.
* Wenn Ihre Workload keinen hohen Ressourcenbedarf hat oder es wichtiger ist, Optimierungsaufträge auszuführen anstatt Workloadanforderungen zu erfüllen, [können Sie den Arbeitsspeicher, die CPU-Leistung und Priorität der Datendeduplizierungsaufträge anpassen](advanced-settings.md#modifying-job-schedules).

## <a name="frequently-asked-questions-faq"></a><a id="faq"></a>Häufig gestellte Fragen (FAQ)
**Ich möchte die Datendeduplizierung für das Dataset für die X-Arbeitsauslastung ausführen. Wird dies unterstützt?**  
Abgesehen von Workloads, die [ bekanntermaßen nicht mit der Datendeduplizierung zusammenarbeiten](interop.md), unterstützen wir die Datenintegrität der Datendeduplizierung für alle Workloads. Empfohlene Workloads werden auch hinsichtlich Leistung von Microsoft unterstützt. Die Leistung anderer Workloads hängt erheblich davon ab, was diese auf dem Server ausführen. Sie müssen bestimmen, welche Leistungsbeeinträchtigungen die Datendeduplizierung auf Ihre Workload ausübt, und ob dies für diese Workload zulässig ist.

**Was sind die Anforderungen an die Volumegröße für deduplizierte Volumes?**  
Unter Windows Server 2012 und Windows Server 2012 R2 musste die Größe von Volumes sorgfältig geplant werden, um sicherzustellen, dass die Datendeduplizierung mit den Änderungsumfang auf dem Datenträger zurechtkam. Dies bedeutete in der Regel, dass die durchschnittliche maximale Größe eines deduplizierten Volumes bei einer Workload mit hohem Änderungsumfang 1-2 TB und die absolute maximale empfohlene Größe 10 TB betrug. Unter Windows Server 2016 gelten diese Einschränkungen nicht mehr. Weitere Informationen finden Sie unter [Neuigkeiten bei der Datendeduplizierung](whats-new.md#large-volume-support).

**Muss ich für empfohlene Workloads den Zeitplan oder andere datendeduplizierungseinstellungen ändern?**  
Nein, die angegebenen [Verwendungs Typen](understand.md#usage-type) wurden erstellt, um angemessene Standardwerte für empfohlene Workloads bereitzustellen.

**Welche Arbeitsspeicheranforderungen gelten für die Datendeduplizierung?**  
Für den Minimalfall sollten für die Datendeduplizierung 300 MB + 50 MB für jedes TB logischer Daten vorgesehen werden. Wenn Sie beispielsweise ein 10-TB-Volume optimieren, benötigen Sie für die Deduplizierung mindestens 800 MB Arbeitsspeicher (`300 MB + 50 MB * 10 = 300 MB + 500 MB = 800 MB`). Während die Datendeduplizierung ein Volume mit diesem niedrigen Umfang an Arbeitsspeicher optimieren kann, werden Datendeduplizierungsaufträge durch solch einschränkte Ressourcen verlangsamt.

Im optimalen Fall sollte die Datendeduplizierung über 1 GB Arbeitsspeicher pro 1 TB logischer Daten verfügen. Wenn Sie beispielsweise ein 10-TB-Volume optimieren, benötigen Sie im Optimalfall für die Deduplizierung mindestens 10 GB Arbeitsspeicher (`1 GB * 10`). Dieses Verhältnis stellt die maximale Leistung für Datendeduplizierungsaufträge sicher.

**Welche Speicherplatzanforderungen gelten für die Datendeduplizierung?**  
Unter Windows Server 2016 unterstützt die Datendeduplizierung Volumegrößen bis zu 64 TB. Weitere Informationen finden Sie unter [Neuigkeiten bei der Datendeduplizierung](whats-new.md#large-volume-support).
