---
title: Paralleles Upgrade für Clusterbetriebssystem
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: get-started-article
ms.assetid: 6e102c1f-df26-4eaa-bc7a-d0d55d3b82d5
author: jasongerend
ms.author: jgerend
manager: lizross
ms.date: 03/27/2018
ms.openlocfilehash: 8b2ea665542d57b12899a5993a62973c446485a7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828353"
---
# <a name="cluster-operating-system-rolling-upgrade"></a>Paralleles Upgrade des Cluster Betriebssystems

> Gilt für: Windows Server 2019, Windows Server 2016

Das parallele Upgrade des Cluster Betriebssystems ermöglicht einem Administrator, ein Upgrade des Betriebssystems der Cluster Knoten auszuführen, ohne die Hyper-V-oder Dateiserver mit horizontaler Skalierung Arbeits Auslastungen zu beenden. Mit diesem Feature können die Downtimesanktionen laut Vereinbarungen zum Servicelevel (Service Level Agreements, SLA) vermieden werden.

Das parallele Upgrade des Cluster Betriebssystems bietet die folgenden Vorteile:

- Failovercluster mit virtuellen Hyper-V-Computern und sofs-Workloads (Scale-Out File Server) können von Windows Server 2012 R2 (auf allen Knoten im Cluster ausgeführt) auf Windows Server 2016 (auf allen Cluster Knoten des Clusters ausgeführt) ohne Ausfallzeiten aktualisiert werden. Andere clusterworkloads, wie z. b. SQL Server, sind während der Zeit (in der Regel weniger als fünf Minuten) nicht verfügbar, um ein Failover auf Windows Server 2016 auszuführen.  
- Es ist keine zusätzliche Hardware erforderlich. Sie können auch zusätzliche Cluster Knoten vorübergehend zu kleinen Clustern hinzufügen, um die Verfügbarkeit des Clusters während des parallelen Upgradevorgangs des Cluster Betriebssystems zu verbessern.  
- Der Cluster muss nicht beendet oder neu gestartet werden.  
- Ein neuer Cluster ist nicht erforderlich. Der vorhandene Cluster wird aktualisiert. Außerdem werden vorhandene in Active Directory gespeicherte Cluster Objekte verwendet.  
- Der Upgradevorgang kann nur rückgängig gemacht werden, wenn der Kunde den "Point-of-No-Return"-Wert abweist, wenn auf allen Clusterknoten Windows Server 2016 ausgeführt wird und das PowerShell-Cmdlet "Update-clusterfunctionallevel" ausgeführt wird.  
- Der Cluster unterstützt Patchen-und Wartungsvorgänge während der Ausführung im gemischten Betriebssystem Modus.  
- Es unterstützt die Automatisierung über PowerShell und WMI.  
- Die Eigenschaft **clusterfunctionallevel** der öffentlichen Cluster Eigenschaft gibt den Status des Clusters auf Windows Server 2016-Cluster Knoten an. Diese Eigenschaft kann mithilfe des PowerShell-Cmdlets von einem Windows Server 2016-Cluster Knoten, der zu einem Failovercluster gehört, abgefragt werden:  
    ```PowerShell
    Get-Cluster | Select ClusterFunctionalLevel  
    ```  

    Der Wert **8** gibt an, dass der Cluster auf der Windows Server 2012 R2-Funktionsebene ausgeführt wird. Der Wert **9** gibt an, dass der Cluster auf der Windows Server 2016-Funktionsebene ausgeführt wird.  

In diesem Leitfaden werden die verschiedenen Phasen des parallelen Upgradevorgangs für Cluster Betriebssysteme, Installationsschritte, Featureeinschränkungen und häufig gestellte Fragen (FAQs) beschrieben. Sie gelten auch für die folgenden Szenarien für das parallele Upgrade des Cluster Betriebssystems in Windows Server 2016:  
- Hyper-V-Cluster  
- Dateiserver mit horizontaler Skalierung Cluster  

Das folgende Szenario wird in Windows Server 2016 nicht unterstützt:  
-  Paralleles Upgrade des Cluster Betriebssystems von Gast Clustern unter Verwendung einer virtuellen Festplatte (vhdx-Datei) als frei gegebener Speicher  

Das parallele Upgrade des Cluster Betriebssystems wird von System Center Virtual Machine Manager (SCVMM) 2016 vollständig unterstützt. Wenn Sie SCVMM 2016 verwenden, finden Sie unter [Durchführen eines parallelen Upgrades eines Hyper-V-Host Clusters auf Windows Server 2016 in VMM eine](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade?view=sc-vmm-1807) Anleitung zum Aktualisieren der Cluster und zum Automatisieren der in diesem Dokument beschriebenen Schritte.  

## <a name="requirements"></a>Voraussetzungen  
Führen Sie die folgenden Anforderungen aus, bevor Sie mit dem parallelen Upgrade des Cluster Betriebssystems beginnen:

- Beginnen Sie mit einem Failovercluster, auf dem Windows Server (halbjährlicher Kanal), Windows Server 2016 oder Windows Server 2012 R2 ausgeführt wird.
- Das Upgrade eines direkte Speicherplätze Clusters auf Windows Server 1709 wird nicht unterstützt.
- Wenn es sich bei der Cluster Arbeitsauslastung um virtuelle Hyper-V-Computer oder Dateiserver mit horizontaler Skalierung handelt, kann ein Upgrade ohne Ausfallzeiten erwartet werden.
- Stellen Sie sicher, dass die Hyper-V-Knoten über CPUs verfügen, die die Adressierungs Tabelle (slat) der zweiten Ebene mithilfe einer der folgenden Methoden unterstützen:  
        -Überprüfen [Sie, dass Sie slat-kompatibel sind? WP8 SDK Tip 01](https://blogs.msdn.com/b/devfish/archive/2012/11/06/are-you-slat-compatible-wp8-sdk-tip-01.aspx) Artikel, in dem zwei Methoden zum überprüfen beschrieben werden, ob eine CPU SLATS unterstützt  
        -Laden Sie das [Coreinfo v 3,31](https://technet.microsoft.com/sysinternals/cc835722) -Tool herunter, um zu ermitteln, ob eine CPU slat unterstützt.

## <a name="cluster-transition-states-during-cluster-os-rolling-upgrade"></a>Cluster Übergangszustände beim parallelen Upgrade des Cluster Betriebssystems

In diesem Abschnitt werden die verschiedenen Übergangszustände des Windows Server 2012 R2-Clusters beschrieben, der mit dem parallelen Upgrade des Cluster Betriebssystems auf Windows Server 2016 aktualisiert wird.  

Damit die clusterworkloads während des parallelen Upgradevorgangs des Cluster Betriebssystems ausgeführt werden, funktioniert das Verschieben einer Cluster Arbeitsauslastung von einem Windows Server 2012 R2-Knoten auf einen Windows Server 2016-Knoten so, als ob auf beiden Knoten das Betriebssystem Windows Server 2012 R2 ausgeführt wird. Wenn dem Cluster Windows Server 2016-Knoten hinzugefügt werden, werden diese in einem Windows Server 2012 R2-Kompatibilitätsmodus ausgeführt. Im neuen konzeptionellen Cluster Modus mit dem Namen "gemischter Betriebssystem Modus" können Knoten unterschiedlicher Versionen im gleichen Cluster vorhanden sein (siehe Abbildung 1).  

![Abbildung mit den drei Phasen eines parallelen Upgrades für Cluster Betriebssysteme: alle Knoten Windows Server 2012 R2, gemischter Betriebssystem Modus und alle Knoten Windows Server 2016](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Overview.png)  
**Abbildung 1: Statusübergänge des Cluster Betriebssystems**  

Ein Windows Server 2012 R2-Cluster wechselt in den Modus mit gemischtem Betriebssystem, wenn dem Cluster ein Windows Server 2016-Knoten hinzugefügt wird. Der Prozess ist vollständig umkehrbar. Windows Server 2016-Knoten können aus dem Cluster entfernt werden, und Windows Server 2012 R2-Knoten können dem Cluster in diesem Modus hinzugefügt werden. Der "Point of No Return" tritt auf, wenn das PowerShell-Cmdlet "Update-clusterfunctionallevel" auf dem Cluster ausgeführt wird. Damit dieses Cmdlet erfolgreich ausgeführt werden kann, müssen alle Knoten Windows Server 2016 sein, und alle Knoten müssen online sein.  

## <a name="transition-states-of-a-four-node-cluster-while-performing-rolling-os-upgrade"></a>Übergangszustände eines Clusters mit vier Knoten beim Ausführen eines Upgrades für ein Betriebssystem

In diesem Abschnitt werden die vier verschiedenen Phasen eines Clusters mit frei gegebenem Speicher erläutert und beschrieben, dessen Knoten von Windows Server 2012 R2 auf Windows Server 2016 aktualisiert werden.  

"Phase 1" ist der anfängliche Status. wir beginnen mit einem Windows Server 2012 R2-Cluster.  

![Abbildung mit dem Anfangszustand: alle Knoten Windows Server 2012 R2](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage1.png)  
**Abbildung 2: Anfangs Status: Windows Server 2012 R2-Failovercluster (Phase 1)**  

In "Phase 2" wurden zwei Knoten angehalten, entladen, entfernt, neu formatiert und mit Windows Server 2016 installiert.  

![Abbildung, in der der Cluster im gemischten Betriebssystem Modus angezeigt wird: aus dem Beispiel 4-Knoten-Cluster werden auf zwei Knoten Windows Server 2016 und auf zwei Knoten Windows Server 2012 R2 ausgeführt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage2.png)  
**Abbildung 3: Zwischenzustand: gemischter Betriebssystem Modus: Windows Server 2012 R2 und Windows Server 2016-Failovercluster (Phase 2)**  

In "Phase 3" wurden alle Knoten im Cluster auf Windows Server 2016 aktualisiert, und der Cluster kann mit dem PowerShell-Cmdlet "Update-clusterfunctionallevel" aktualisiert werden.  

> [!NOTE]  
> Zu diesem Zeitpunkt kann der Prozess vollständig rückgängig gemacht werden, und Windows Server 2012 R2-Knoten können diesem Cluster hinzugefügt werden.  

![Abbildung, in der gezeigt wird, dass der Cluster vollständig auf Windows Server 2016 aktualisiert wurde, und ist für das Update-clusterfunctionallevel-Cmdlet bereit, um die Cluster Funktionsebene auf Windows Server 2016 zu bringen](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage3.png)  
**Abbildung 4: zwischen Status: alle Knoten, die auf Windows Server 2016 aktualisiert wurden, bereit für Update-clusterfunctionallevel (Phase 3)**  

Nachdem das Update-clusterfunctionallevelcmdlet ausgeführt wurde, wechselt der Cluster in "Phase 4", wo neue Windows Server 2016-Cluster Features verwendet werden können.  

![Abbildung, die anzeigt, dass das parallele Upgrade des Cluster Betriebssystems erfolgreich abgeschlossen wurde. alle Knoten wurden auf Windows Server 2016 aktualisiert, und der Cluster wird auf der Cluster Funktionsebene von Windows Server 2016 ausgeführt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_Stage4.png)  
**Abbildung 5: Endzustand: Windows Server 2016-Failovercluster (Stufe 4)**  

## <a name="cluster-os-rolling-upgrade-process"></a>Paralleles Upgrade des Cluster Betriebssystems

In diesem Abschnitt wird der Workflow für das parallele Upgrade des Cluster Betriebssystems beschrieben.  

![Abbildung mit dem Workflow zum Aktualisieren eines Clusters](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_RollingUpgrade_Workflow.png)  
**Abbildung 6: Workflow für parallele Upgrades des Cluster Betriebssystems**  

Das parallele Upgrade des Cluster Betriebssystems umfasst die folgenden Schritte:  

1. Bereiten Sie den Cluster auf das Betriebssystem Upgrade wie folgt vor:  
    1. Zum parallelen Upgrade des Cluster Betriebssystems muss jeweils ein Knoten aus dem Cluster entfernt werden. Überprüfen Sie, ob die Kapazität des Clusters ausreichend ist, um ha-SLAs beizubehalten, wenn einer der Cluster Knoten für ein Betriebssystem Upgrade aus dem Cluster entfernt wird. Dies bedeutet, dass Sie die Möglichkeit zum Failover von Arbeits Auslastungen auf einen anderen Knoten benötigen, wenn beim parallelen Upgrade des Cluster Betriebssystems ein Knoten aus dem Cluster entfernt wird? Verfügt der Cluster über die Kapazität zum Ausführen der erforderlichen Workloads, wenn ein Knoten für ein paralleles Upgrade des Cluster Betriebssystems aus dem Cluster entfernt wird?  
    2. Überprüfen Sie für Hyper-v-Arbeits Auslastungen, ob alle Windows Server 2016 Hyper-V-Hosts über CPU-Unterstützung für die Adress Tabelle (slat) der zweiten Ebene verfügen Die Hyper-V-Rolle in Windows Server 2016 kann nur von slat-fähigen Computern verwendet werden.  
    3. Überprüfen Sie, ob alle Arbeits Auslastungs Sicherungen abgeschlossen wurden, und sichern Sie den Cluster. Beendet Sicherungs Vorgänge beim Hinzufügen von Knoten zum Cluster.  
    4. Überprüfen Sie, ob alle Cluster Knoten online sind/Running/up mithilfe des Cmdlets [`Get-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) (siehe Abbildung 7).  

        ![ScreenCap, das die Ergebnisse der Ausführung des Cmdlets Get-clusternode anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterNode.png)  
        **Abbildung 7: Bestimmen des Knoten Status mithilfe des Get-clusternode-Cmdlets**  

    5. Wenn Sie Cluster fähige Updates (Cluster-Aware Updates, Cau) ausführen, überprüfen Sie, ob das **Cluster fähige aktualisieren** derzeit mithilfe der Benutzeroberfläche für Cluster fähiges aktualisieren oder mit dem Cmdlet " [`Get-CauRun`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) " ausgeführt wird (siehe Abbildung 8). Verwenden Sie das Cmdlet " [`Disable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) " (siehe Abbildung 9), um zu verhindern, dass Knoten während des parallelen Upgradevorgangs des Cluster Betriebssystems angehalten und durch Cau entladen werden.  

        ![ScreenCap, das die Ausgabe des Cmdlets Get-caurun anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetCAU.png)  
        **Abbildung 8: Verwenden des [`Get-CauRun`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Get-CauRun?view=win10-ps) Cmdlets, um zu bestimmen, ob Cluster fähige Updates auf dem Cluster ausgeführt werden**  

        ![ScreenCap, das die Ausgabe des Cmdlets "deaktivieren-cauclusterrole" anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_DisableCAU.png)  
        **Abbildung 9: Deaktivieren der Rolle "Cluster fähiges aktualisieren" mithilfe des [`Disable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole?view=win10-ps) -Cmdlets**  

2. Führen Sie für jeden Knoten im Cluster die folgenden Schritte aus:  
    1. Wählen Sie über die Benutzeroberfläche des Cluster-Managers einen Knoten aus, und verwenden Sie die **Pause Die Menüoption** zum Entfernen des Knotens (siehe Abbildung 10) oder Verwenden des [`Suspend-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) -Cmdlets (siehe Abbildung 11).  

        ![ScreenCap, das zeigt, wie Rollen mithilfe der Benutzeroberfläche des Cluster-Managers entladen werden](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_FCM_DrainRoles.png)  
        **Abbildung 10: Ableiten von Rollen von einem Knoten mithilfe von Failovercluster-Manager**  

        ![ScreenCap, das die Ausgabe des Suspend-clusternode-Cmdlets anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SuspendNode.png)  
        **Abbildung 11: Ableiten von Rollen von einem Knoten mithilfe des [`Suspend-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Suspend-ClusterNode?view=win10-ps) -Cmdlets**  

    2.  Entfernen Sie mithilfe der Benutzeroberfläche des Cluster-Managers den angehaltenen Knoten **aus dem Cluster** , oder verwenden Sie das Cmdlet " [`Remove-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) ".  

        ![ScreenCap, das die Ausgabe des Cmdlets Remove-clusternode anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_RemoveNode.png)  
        **Abbildung 12: Entfernen eines Knotens aus dem Cluster mithilfe [`Remove-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Remove-ClusterNode?view=win10-ps) Cmdlets**  

    3.  Formatieren Sie das Systemlaufwerk neu, und führen Sie eine "Neuinstallation des Betriebssystems" von Windows Server 2016 auf dem Knoten mithilfe der Option **Benutzer definiert: nur Windows installieren (erweitert)** (siehe Abbildung 13) in der Datei "Setup. exe" aus. Wählen Sie die Option **Upgrade: Windows installieren und Dateien beibehalten, Einstellungen und Anwendungen** nicht aus, da das parallele Upgrade des Cluster Betriebssystems keine direkte Aktualisierung fördert.  

        ![ScreenCap des Windows Server 2016-Installations-Assistenten, der die ausgewählte Option für die benutzerdefinierte Installation anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_InstallOption.png)  
        **Abbildung 13: verfügbare Installationsoptionen für Windows Server 2016**  

    4.  Fügen Sie den Knoten der entsprechenden Active Directory Domäne hinzu.  
    5.  Fügen Sie die entsprechenden Benutzer der Gruppe "Administratoren" hinzu.  
    6.  Installieren Sie mit dem PowerShell-Cmdlet "Server-Manager UI" oder "Install-Windows Feature" alle benötigten Server Rollen, z. b. Hyper-V.  

        ```PowerShell
        Install-WindowsFeature -Name Hyper-V  
        ```  

    7.  Installieren Sie das Failoverclustering-Feature mithilfe der Server-Manager-Benutzeroberfläche oder des PowerShell-Cmdlets install-Windows Feature.  

        ```PowerShell
        Install-WindowsFeature -Name Failover-Clustering  
        ```  

    8.  Installieren Sie alle zusätzlichen Funktionen, die von ihren clusterworkloads benötigt werden.  
    9. Überprüfen Sie die Netzwerk-und Speicher Verbindungseinstellungen mithilfe der Failovercluster-Manager Benutzeroberfläche.  
    10. Wenn die Windows-Firewall verwendet wird, überprüfen Sie, ob die Firewalleinstellungen für den Cluster korrekt sind. Beispielsweise kann für Cluster fähiges aktualisieren (Cluster-Aware Update, Cau) Cluster eine Firewallkonfiguration erforderlich sein.  
    11. Verwenden Sie für Hyper-v-Workloads die Hyper-v-Manager-Benutzeroberfläche, um das Dialogfeld "Virtual Switch Manager" zu öffnen (siehe Abbildung 14).  

        Überprüfen Sie, ob die Namen der verwendeten virtuellen Switches für alle Hyper-V-Host Knoten im Cluster identisch sind.  

        ![ScreenCap, das den Speicherort des Dialog Felds für den virtuellen Hyper-V-Switch-Manager anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_VMSwitch.png)  
        **Abbildung 14: Manager für virtuelle Switches**  

    12. Verwenden Sie auf einem Windows Server 2016-Knoten (verwenden Sie keinen Windows Server 2012 R2-Knoten) die Failovercluster-Manager (siehe Abbildung 15), um eine Verbindung mit dem Cluster herzustellen.  

        ![ScreenCap, das das Dialogfeld "Cluster auswählen" anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode.png)  
        **Abbildung 15: Hinzufügen eines Knotens zum Cluster mithilfe von Failovercluster-Manager**  

    13. Verwenden Sie entweder die Failovercluster-Manager-Benutzeroberfläche oder das [`Add-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) -Cmdlet (siehe Abbildung 16), um den Knoten zum Cluster hinzuzufügen.  

        ![ScreenCap, das die Ausgabe des Add-clusternode-Cmdlets anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_AddNode3.png)  
        **Abbildung 16: Hinzufügen eines Knotens zum Cluster mithilfe [`Add-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Add-ClusterNode?view=win10-ps) Cmdlets**  

        > [!NOTE]  
        > Wenn der erste Windows Server 2016-Knoten dem Cluster Beitritt, wechselt der Cluster in den Modus "gemischter Betriebssystem", und die Hauptressourcen des Clusters werden auf den Knoten "Windows Server 2016" verschoben. Bei einem Cluster mit gemischtem Betriebssystem handelt es sich um einen voll funktionsfähigen Cluster, in dem die neuen Knoten in einem Kompatibilitätsmodus mit den alten Knoten ausgeführt werden. Der Modus "gemischter Betriebssystem" ist ein transitiver Modus für den Cluster. Es ist nicht als permanent gedacht, und die Kunden möchten innerhalb von vier Wochen alle Knoten Ihres Clusters aktualisieren.  

    14. Nachdem der Windows Server 2016-Knoten dem Cluster erfolgreich hinzugefügt wurde, können Sie (optional) einen Teil der Cluster Arbeitsauslastung auf den neu hinzugefügten Knoten verschieben, um die Arbeitsauslastung wie folgt auf den Cluster umzuverteilen:

        ![ScreenCap, das die Ausgabe des Cmdlets Move-clustervirtualmachinerole anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_MoveVMRole.png)  
        **Abbildung 17: Verschieben einer Cluster Arbeitsauslastung (Cluster-VM-Rolle) mithilfe [`Move-ClusterVirtualMachineRole`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) Cmdlets**  

        1. Verwenden Sie **Livemigration** aus der Failovercluster-Manager für virtuelle Computer oder das [`Move-ClusterVirtualMachineRole`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterVirtualMachineRole?view=win10-ps) -Cmdlet (siehe Abbildung 17), um eine Live Migration der virtuellen Computer durchzuführen.  

            ```PowerShell
            Move-ClusterVirtualMachineRole -Name VM1 -Node robhind-host3  
            ```  

        2. Verwenden Sie **Move** from the Failovercluster-Manager oder das [`Move-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Move-ClusterGroup?view=win10-ps) -Cmdlet für andere clusterworkloads.  

3. Gehen Sie wie folgt vor, wenn jeder Knoten auf Windows Server 2016 aktualisiert und wieder dem Cluster hinzugefügt wurde oder wenn verbleibende Windows Server 2012 R2-Knoten entfernt wurden:  

    > [!IMPORTANT]  
    > -   Nachdem Sie die Cluster Funktionsebene aktualisiert haben, können Sie nicht mehr zur Windows Server 2012 R2-Funktionsebene zurückkehren und Windows Server 2012 R2-Knoten können dem Cluster nicht mehr hinzugefügt werden.
    > -   Bis zum Ausführen des Cmdlets " [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) " ist der Prozess vollständig umkehrbar, und Windows Server 2012 R2-Knoten können diesem Cluster hinzugefügt werden, und Windows Server 2016-Knoten können entfernt werden.  
    > -   Nachdem das Cmdlet " [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) " ausgeführt wurde, sind neue Features verfügbar.  

    1.  Überprüfen Sie mithilfe der Failovercluster-Manager-Benutzeroberfläche oder des [`Get-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) -Cmdlets, ob alle Cluster Rollen erwartungsgemäß auf dem Cluster ausgeführt werden. Im folgenden Beispiel wird der verfügbare Speicher nicht verwendet. stattdessen wird CSV verwendet. Daher zeigt der verfügbare Speicher einen **Offline** Status an (siehe Abbildung 18).  

        ![ScreenCap, das die Ausgabe des Cmdlets Get-clustergroup anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_GetClusterGroup.png)  
        **Abbildung 18: überprüfen, ob alle Clustergruppen (Cluster Rollen) mithilfe des [`Get-ClusterGroup`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterGroup?view=win10-ps) -Cmdlets ausgeführt werden**  

    2.  Überprüfen Sie, ob alle Cluster Knoten online sind und mit dem [`Get-ClusterNode`](https://docs.microsoft.com/powershell/module/failoverclusters/Get-ClusterNode?view=win10-ps) -Cmdlet ausgeführt werden.  
    3.  Führen Sie das [`Update-ClusterFunctionalLevel`](https://technet.microsoft.com/library/mt589702.aspx) Cmdlet aus. es sollten keine Fehler zurückgegeben werden (siehe Abbildung 19).  

        ![ScreenCap, das die Ausgabe des Cmdlets "Update-clusterfunctionallevel" anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_SelectFunctionalLevel.png)  
        **Abbildung 19: Aktualisieren der Funktionsebene eines Clusters mithilfe von PowerShell**  

    4.  Nachdem das Cmdlet " [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) " ausgeführt wurde, sind neue Features verfügbar.  

4. Windows Server 2016-fortsetzen normaler Cluster Aktualisierungen und-Sicherungen:  

    1. Wenn Sie zuvor Cau ausgeführt haben, starten Sie es mithilfe der Cau-Benutzeroberfläche neu, oder verwenden Sie das Cmdlet " [`Enable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) " (siehe Abbildung 20).  

        ![ScreenCap, das die Ausgabe von enable-cauclusterrole anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_EnableCAUClusterRole.png)  
        **Abbildung 20: Aktivieren der Rolle "Cluster fähige Updates" mithilfe des [`Enable-CauClusterRole`](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole?view=win10-ps) -Cmdlets**  

    2. Fortsetzen von Sicherungs Vorgängen.  

5. Aktivieren und verwenden Sie die Windows Server 2016-Features auf Hyper-V-Virtual Machines.  

    1. Nachdem der Cluster auf die Funktionsebene von Windows Server 2016 aktualisiert wurde, verfügen viele Workloads wie Hyper-V-VMS über neue Funktionen. Eine Liste der neuen Hyper-V-Funktionen. siehe [migrieren und Aktualisieren virtueller](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/migrating_vms) Computer  

    2. Verwenden Sie auf jedem Hyper-v-Host Knoten im Cluster das Cmdlet " [`Get-VMHostSupportedVersion`](https://docs.microsoft.com/powershell/module/hyper-v/Get-VMHostSupportedVersion?view=win10-ps) ", um die vom Host unterstützten Hyper-v-VM-Konfigurations Versionen anzuzeigen.  

        ![ScreenCap, das die Ausgabe des Cmdlets Get-vmhostsupportedversion anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Clustering_GetVMHostSupportVersion.png)  
        **Abbildung 21: Anzeigen der vom Host unterstützten Hyper-V-VM-Konfigurations Versionen**  

   3. Auf jedem Knoten des Hyper-v-Hosts im Cluster kann ein Upgrade für Hyper-v-VM-Konfigurations Versionen durchgeführt werden, indem ein kurzes Wartungsfenster für Benutzer geplant wird, um die virtuellen Computer zu sichern, zu deaktivieren und das Cmdlet " [`Update-VMVersion`](https://docs.microsoft.com/powershell/module/hyper-v/Update-VMVersion?view=win10-ps) " ausgeführt wird (siehe Abbildung 22). Dadurch wird die Version des virtuellen Computers aktualisiert, und neue Hyper-v-Features werden aktiviert, sodass keine weiteren Updates von Hyper-v-Integrations Komponenten (IC) erforderlich sind. Dieses Cmdlet kann über den Hyper-V-Knoten ausgeführt werden, der als Host für den virtuellen Computer dient, oder mithilfe des `-ComputerName`-Parameters können Sie die VM-Version Remote aktualisieren. In diesem Beispiel aktualisieren wir die Konfigurations Version von VM1 von 5,0 auf 7,0, um von vielen neuen Hyper-V-Features zu profitieren, die dieser VM-Konfigurations Version zugeordnet sind, z. b. Produktions Prüfpunkte (Anwendungs konsistente Sicherungen) und binäre VM-Konfigurationsdatei.  

       ![ScreenCap, das das Update-VMVersion-Cmdlet in Aktion anzeigt](media/Cluster-Operating-System-Rolling-Upgrade/Cluster_RollingUpgrade_StopVM.png)  
       **Abbildung 22: Aktualisieren einer VM-Version mithilfe des PowerShell-Cmdlets "Update-VMVersion"**  

6. Speicherpools können mithilfe des PowerShell-Cmdlets " [Update-storagepool](https://docs.microsoft.com/powershell/module/storage/Update-StoragePool?view=win10-ps) " aktualisiert werden. Dies ist ein Online Vorgang.  

Obwohl wir auf Szenarien für die Private Cloud abzielen, insbesondere Hyper-V-und Datei Server Cluster mit horizontaler Skalierung, die ohne Ausfallzeiten aktualisiert werden können, kann der parallele Upgradeprozess des Cluster Betriebssystems für jede beliebige Cluster Rolle verwendet werden.  

## <a name="restrictions--limitations"></a>Einschränkungen/Einschränkungen  
- Diese Funktion funktioniert nur für Windows Server 2012 R2-und Windows Server 2016-Versionen. Diese Funktion kann keine Upgrades früherer Versionen von Windows Server wie Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 auf Windows Server 2016 durchführen.  
- Jeder Knoten von Windows Server 2016 sollte neu formatiert bzw. neu installiert werden. Der Installationstyp "direkt" oder "Upgrade" wird nicht empfohlen.  
- Ein Windows Server 2016-Knoten muss zum Hinzufügen von Windows Server 2016-Knoten zum Cluster verwendet werden.  
- Wenn Sie einen Cluster im gemischten Betriebssystem Modus verwalten, führen Sie die Verwaltungsaufgaben immer über einen komplexer Darstellung-Knoten aus, auf dem Windows Server 2016 ausgeführt wird. Windows Server 2012 R2-downlevelknoten können keine Benutzeroberflächen-oder Verwaltungs Tools für Windows Server 2016 verwenden.  
- Wir empfehlen Kunden, den clusterupgradeprozess schnell durchzuführen, da einige Cluster Features nicht für den Modus mit gemischtem Betriebssystem optimiert sind.  
- Vermeiden Sie das Erstellen oder Ändern der Größe von Speicher auf Windows Server 2016-Knoten, während der Cluster im Modus mit gemischtem Betriebssystem ausgeführt wird, da die Inkompatibilitäten bei einem Failover von einem Windows Server 2016-Knoten auf Windows Server 2012 R2-Knoten mit einer untergeordneten  

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen  
**Wie lange kann der Failovercluster im gemischten Betriebssystem Modus ausgeführt werden?**  
    Wir empfehlen Kunden, das Upgrade innerhalb von vier Wochen abzuschließen. Es gibt viele Optimierungen in Windows Server 2016. Wir haben Hyper-V-und Datei Server Cluster mit horizontaler Skalierung ohne Ausfallzeiten in weniger als vier Stunden aktualisiert.  

**Wird diese Funktion auf Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 zurück portieren?**  
    Es ist nicht geplant, diese Funktion auf vorherige Versionen zurück zu portieren. Das parallele Upgrade des Cluster Betriebssystems ist unsere Vision für das Upgrade von Windows Server 2012 R2-Clustern auf Windows Server 2016 und höher.  

**Muss für den Windows Server 2012 R2-Cluster alle Software Updates installiert sein, bevor der parallele Upgradeprozess des Cluster Betriebssystems gestartet wird?**  
    Ja, bevor Sie mit dem parallelen Upgrade des Cluster Betriebssystems beginnen, überprüfen Sie, ob alle Cluster Knoten mit den neuesten Software Updates aktualisiert wurden.  

**Kann ich das [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) -Cmdlet ausführen, während Knoten deaktiviert oder angehalten werden?**  
    Nein. Alle Cluster Knoten müssen sich in der aktiven Mitgliedschaft befinden, damit das [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) -Cmdlet funktioniert.  

**Funktioniert das parallele Upgrade des Cluster Betriebssystems für jede Cluster Arbeitsauslastung? Funktioniert es für SQL Server?**  
    Ja, das parallele Upgrade des Cluster Betriebssystems funktioniert für jede Cluster Arbeitsauslastung. Allerdings ist es für Hyper-V-und Datei Server Cluster mit horizontaler Skalierung nur zu Ausfallzeiten. Bei den meisten anderen Arbeits Auslastungen treten bei einem Failover einige Ausfallzeiten (in der Regel einige Minuten) auf, und ein Failover muss mindestens einmal während des parallelen Upgradevorgangs des Cluster Betriebssystems ausgeführt werden.  

**Kann ich diesen Prozess mithilfe von PowerShell automatisieren?**  
    Ja, wir haben das parallele Upgrade für Cluster Betriebssysteme entworfen, um Sie mithilfe von PowerShell zu automatisieren.  

**Kann ich bei einem großen Cluster mit zusätzlicher Arbeitsauslastung und Failoverkapazität mehrere Knoten gleichzeitig aktualisieren?**  
    Ja. Wenn ein Knoten aus dem Cluster entfernt wird, um das Betriebssystem zu aktualisieren, verfügt der Cluster über einen geringeren Knoten für das Failover und verfügt daher über eine reduzierte Failoverkapazität. Bei großen Clustern mit ausreichender Arbeitsauslastung und Failoverkapazität können mehrere Knoten gleichzeitig aktualisiert werden. Sie können dem Cluster vorübergehend Cluster Knoten hinzufügen, um beim parallelen Upgradeprozess des Cluster Betriebssystems eine verbesserte Arbeitsauslastung und Failoverkapazität bereitzustellen.  

**Was geschieht, wenn ich nach dem erfolgreichen Ausführen [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps) ein Problem in meinem Cluster entdeckt?**  
    Wenn Sie die Cluster Datenbank vor dem Ausführen von [`Update-ClusterFunctionalLevel`](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel?view=win10-ps)mit einer Sicherung des System Status gesichert haben, können Sie eine autorisierende Wiederherstellung auf einem Windows Server 2012 R2-Cluster Knoten durchführen und die ursprüngliche Cluster Datenbank und-Konfiguration wiederherstellen.  

**Kann ich für jeden Knoten ein direktes Upgrade verwenden, anstatt die Clean-OS-Installation durch Neuformatierung des System Laufwerks zu verwenden?**  
    Wir empfehlen nicht die Verwendung eines direkten Upgrades von Windows Server, aber wir wissen, dass es in einigen Fällen funktioniert, in denen Standardtreiber verwendet werden. Lesen Sie sorgfältig alle Warnmeldungen, die während der direkten Aktualisierung eines Cluster Knotens angezeigt werden.  

**Wenn ich die Hyper-v-Replikation für eine Hyper-v-VM auf meinem Hyper-v-Cluster verwende, bleibt die Replikation während und nach dem parallelen Upgradeprozess des Cluster Betriebssystems erhalten?**  
    Ja, das Hyper-V-Replikat bleibt während und nach dem parallelen Upgrade des Cluster Betriebssystems intakt.  

**Kann ich System Center 2016 Virtual Machine Manager (SCVMM) verwenden, um den parallelen Upgradeprozess für Cluster Betriebssysteme zu automatisieren?**  
    Ja, Sie können das parallele Upgradeverfahren für Cluster Betriebssysteme mithilfe von VMM in System Center 2016 automatisieren.  

## <a name="see-also"></a>Siehe auch  
-   [Anmerkungen zu dieser Version: wichtige Probleme in Windows Server 2016](../get-started/Release-Notes--Important-Issues-in-Windows-Server-2016-Technical-Preview.md)  
-   [Neuerungen in Windows Server 2016](../get-started/What-s-New-in-windows-server-2016.md)  
-   [Neues beim Failoverclustering unter Windows Server](whats-new-in-failover-clustering.md)  
