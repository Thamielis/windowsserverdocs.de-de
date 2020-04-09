---
title: Übersicht über DFS-Namespaces
ms.prod: windows-server
ms.author: jgerend
manager: daveba
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 06/07/2019
description: In diesem Thema wird beschrieben, wie Sie mithilfe des Rollendiensts für DFS-Namespaces in Windows Server freigegebene Ordner, die sich auf verschiedenen Servern befinden, in logisch strukturierten Namespaces gruppieren.
ms.openlocfilehash: 07f6ac857164257810b297f9e2b83db4e4bd42be
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858983"
---
# <a name="dfs-namespaces-overview"></a>Übersicht über DFS-Namespaces

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server (halbjährlicher Kanal)

Mithilfe des Rollendiensts für DFS-Namespaces in Windows Server können Sie freigegebene Ordner, die sich auf verschiedenen Servern befinden, in logisch strukturierten Namespaces gruppieren. Dadurch ist eine virtuelle Ansicht der freigegebenen Ordner für Benutzer möglich, wobei ein einzelner Pfad zu Dateien führt, die sich auf mehreren Servern befinden, wie in der folgenden Abbildung dargestellt:

![DFS-Namespaces-Technologieelemente](media/dfs-overview.png)

Hier ist eine Beschreibung der Elemente, die einen DFS-Namespace bilden:

- **Namespace-Server** -Ein Namespaceserver, der einen Namespace hostet. Der Namespaceserver kann ein Mitgliedsserver oder ein Domänencontroller sein.
- **Namespacestamm** -Der Namespacestamm ist der Ausgangspunkt des Namespaces. In der obigen Abbildung ist der Name des Stamms öffentlich, und der Namespace Pfad ist \\\\\\Public von. Bei dieser Art von Namespace handelt es sich um einen domänenbasierten Namespace, weil er mit einem Domänen Namen (z. b. "Configuration Manager") beginnt und seine Metadaten in Active Directory Domain Services (AD DS) gespeichert sind. Obwohl in der vorherigen Abbildung ein einzelner Namespaceserver angezeigt wird, kann ein domänenbasierter Namespace auf mehreren Namespaceservern zum Erhöhen der Verfügbarkeit des Namespaces gehostet.
- **Ordner** - Ordner ohne Ordnerziele fügen dem Namespace Struktur und Hierarchie hinzu und Ordner mit Ordnerzielen stellen Benutzern den tatsächlichen Inhalt zur Verfügung. Wenn Benutzer einen Ordner durchsuchen, der Ordnerziele im Namespace hat, erhält der Clientcomputer einen Verweis, der den Clientcomputer transparent auf einen der Ordnerziele verweist.
- **Ordnerziele** - Ein Ordnerziel ist der UNC-Pfad eines freigegebenen Ordners oder ein anderer Namespace, der einem Ordner in einem Namespace zugeordnet ist. Das Ordnerziel ist der Ort, an dem Daten und Inhalte gespeichert ist. In der obigen Abbildung verfügt der Ordner mit dem Namen „Tools” über zwei Ordnerziele, eins in London und eins in New York, und der Ordner mit dem Namen „Schulungshandbuch” verfügt über ein einziges Ordnerziel in New York. Ein Benutzer, der die \\\\\\Public\\Software\\Tools durchsucht, wird in Abhängigkeit von der Website, in der sich der Benutzer befindet, transparent an den freigegebenen Ordner \\\\\\Tools \\\\Tools oder\\NYC-SVR-01 umgeleitet.

In diesem Thema wird erläutert, wie Sie DFS installieren, welche Neuerungen es gibt und wo Sie Evaluierungs-und Bereitstellungs Informationen finden.

Sie können Namespaces mithilfe der DFS-Verwaltung verwalten, mit [DFS-Namespace (DFSN)-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/dfsn/?view=win10-ps), dem Befehl **DfsUtil** oder Skripts, die WMI-aufrufen.

## <a name="server-requirements-and-limits"></a>Server-Systemanforderungen und -beschränkungen

Für die Ausführung der DFS-Verwaltung oder die Verwendung von DFS-Namespaces müssen keine zusätzlichen Hardware- oder Softwareanforderungen erfüllt werden.

Ein Namespaceserver ist ein Domänencontroller oder ein Mitgliedsserver, der einen Namespace hostet. Die Anzahl der Namespaces, die auf einem Server gehostet werden können, wird durch das Betriebssystem auf dem Namespaceserver bestimmt.

Server, auf denen die folgenden Betriebssysteme ausgeführt werden, können zusätzlich zu einem einzelnen eigenständigen Namespace mehrere domänenbasierte Namespaces hosten. 

- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 Datacenter und Enterprise Edition
- Windows Server (Halbjährlicher Kanal)

Server, auf denen die folgenden Betriebssysteme ausgeführt werden, können einen einzelnen eigenständigen Namespace hosten:

- Windows Server 2008 R2 Standard

Die folgende Tabelle enthält zusätzliche zu berücksichtigende Faktoren, wenn Sie Server zum Hosten eines Namespaces auswählen.

| Server, auf dem sich eigenständige Namespaces befinden | Server, auf dem sich domänenbasierte Namespaces befinden |
| ---                                   |        ---                                |
| Muss ein NTFS-Volume zum Hosten des Namespaces enthalten.|Muss ein NTFS-Volume zum Hosten des Namespaces enthalten. |
| Hierbei kann es sich um einen Mitgliedsserver oder Domänencontroller handeln.|Muss ein Mitgliedsserver oder Domänencontroller in der Domäne sein, in der der Namespace konfiguriert ist. (Diese Anforderung gilt für jeden Namespaceserver, der einen domänenbasierten Namespace hostet.) |
| Kann von einem Failovercluster zum Erhöhen der Verfügbarkeit der Namespace gehostet werden.|Der Namespace kann nicht eine geclusterte Ressource in einem Failovercluster sein. Allerdings können Sie den Namespace auf einem Server suchen, der auch als Knoten in einem Failovercluster fungiert, wenn Sie den Namespace konfigurieren, der nur lokale Ressourcen auf diesem Server verwendet. |

## <a name="installing-dfs-namespaces"></a>Installieren von DFS-Namespaces

DFS-Namespaces und die DFS-Replikation sind Teil der Rolle %%amp;quot;Datei- und Speicherdienste%%amp;quot;. Die Verwaltungstools für DFS (DFS-Verwaltung, das DFS-Namespaces-Modul für Windows PowerShell sowie Befehlszeilentools) werden separat im Rahmen der Remoteserver-Verwaltungstools installiert.

Installieren Sie DFS-Namespaces mithilfe des [Windows Admin Centers](../../manage/windows-admin-center/understand/windows-admin-center.md), Server-Manager oder PowerShell, wie in den folgenden Abschnitten beschrieben.

### <a name="to-install-dfs-by-using-server-manager"></a>So installieren Sie DFS mithilfe des Server-Managers

1. Klicken Sie im Server-Manager auf **Verwalten** und anschließend auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features erscheint.

2. Wählen Sie auf der Seite **Serverauswahl** den Server oder die virtuelle Festplatte (Virtual Hard Disk, VHD) eines virtuellen Computers im Offlinemodus aus, auf dem Sie DFS installieren möchten.

3. Wählen Sie die zu installierenden Rollendienste und Features aus.

    - Um den DFS-Namespaces-Dienst auf der Seite **Serverrollen** zu installieren, wählen Sie **DFS-Namespaces** aus.

    - Erweitern Sie auf der Seite **Features** die Option **Remoteserver-Verwaltungstools**, erweitern Sie **Rollenverwaltungstools**, erweitern Sie **Tools für Dateidienste**, und wählen Sie anschließend **DFS-Verwaltungstools** aus.

         Im Rahmen der DFS-Verwaltungstools werden auf dem Server das DFS-Verwaltungs-Snap-In, das DFS-Namespaces-Modul für Windows PowerShell sowie Befehlszeilentools, aber keine DFS-Dienste installiert.

### <a name="to-install-dfs-by-using-windows-powershell"></a>So installieren Sie DFS mithilfe von Windows PowerShell

Öffne eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten, und gib den folgenden Befehl ein, wobei <name\> für den zu installierenden Rollendienst bzw. für das zu installierende Feature steht. Eine Liste mit relevanten Rollendienst- oder Featurenamen findest du in der folgenden Tabelle:

```PowerShell
Install-WindowsFeature <name>
```

| Rollendienst oder Feature | Name |
| ----------------------- | ---- |
| DFS-Namespaces          | `FS-DFS-Namespace` |
| DFS-Verwaltungstools    | `RSAT-DFS-Mgmt-Con` |

Geben Sie beispielsweise Folgendes ein, um die DFS-Tools zu installieren, die Teil der Remoteserver-Verwaltungstools sind:

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

Geben Sie Folgendes ein, um DFS-Namespaces und die DFS-Tools zu installieren, die Teil der Remoteserver-Verwaltungstools sind:

```PowerShell
Install-WindowsFeature "FS-DFS-Namespace", "RSAT-DFS-Mgmt-Con"
```

## <a name="interoperability-with-azure-virtual-machines"></a>Interoperabilität mit virtuellen Azure-Computern

Die Verwendung von DFS-Namespaces auf Microsoft Azure wurde getestet, es gibt jedoch einige Einschränkungen und Anforderungen, die Sie befolgen müssen.

- Sie können keine Cluster mit eigenständigen Namespaces auf virtuellen Azure-Computern gruppieren.

- Sie können Domänen basierte Namespaces auf virtuellen Azure-Computern hosten, einschließlich Umgebungen mit Azure Active Directory.

Weitere Informationen zu den ersten Schritten mit virtuellen Azure-Computern finden Sie in der [Dokumentation für virtuelle Azure-Computer](https://docs.microsoft.com/azure/virtual-machines/).

## <a name="see-also"></a>Siehe auch

Weitere verwandte Informationen finden Sie in den folgenden Ressourcen:

| Art des Inhalts        | Verweise |
| ------------------  | ----------------|
| **Produktbewertung** | [Neues in DFS-Namespaces und DFS-Replikation in Windows Server](https://technet.microsoft.com/library/dn281957(v=ws.11).aspx) |
| **Bereitstellung**    | [Überlegungen zur Skalierbarkeit von DFS-Namespaces](https://blogs.technet.com/b/filecab/archive/2012/08/26/dfs-namespace-scalability-considerations.aspx) |
| **Betrieb**    | [DFS-Namespaces: Häufig gestellte Fragen](https://technet.microsoft.com/library/ee404780.aspx) |
| **Communityressourcen** | [TechNet-Forum für Dateidienste und Speicher](https://social.technet.microsoft.com/forums/winserverfiles/threads/) |
| **Protokolle**        | [Datei Dienst Protokolle in Windows Server](https://msdn.microsoft.com/library/cc239318.aspx) (veraltet) |
| **Verwandte Technologien** | [Failoverclustering](../../failover-clustering/failover-clustering-overview.md)|
| **Support** | [Unterstützung für Windows IT pro](https://www.microsoft.com/itpro/windows/support)|
