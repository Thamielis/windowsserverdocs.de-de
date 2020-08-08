---
title: Verwalten von Failoverclustern mit dem Windows Admin Center
description: Verwalten von Failoverclustern mit Windows Admin Center (Project Honolulu)
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: e181e52c2e461d6f1ef00f72684b8228cf9889d1
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995977"
---
# <a name="manage-failover-clusters-with-windows-admin-center"></a>Verwalten von Failoverclustern mit dem Windows Admin Center

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

> [!Tip]
> Neu bei Windows Admin Center?
> [Weitere Informationen zum Windows Admin Center finden Sie hier](../overview.md).

## <a name="managing-failover-clusters"></a>Verwalten von Failoverclustern
[Failoverclustering](../../../failover-clustering/failover-clustering-overview.md) ist eine Windows Server-Funktion, mit der Sie mehrere Server zu einem fehlertoleranten Cluster gruppieren können, um die Verfügbarkeit und Skalierbarkeit von Anwendungen und Diensten wie Dateiserver mit horizontaler Skalierung, Hyper-V und Microsoft SQL Server zu erhöhen.

Während Sie Failoverclusterknoten als einzelne Server verwalten können, indem Sie Sie als [Server Verbindungen](manage-servers.md) im Windows Admin Center hinzufügen, können Sie Sie auch als Failovercluster hinzufügen, um Cluster Ressourcen, Speicher, Netzwerk, Knoten, Rollen, virtuelle Maschinen und virtuelle Switches anzuzeigen und zu verwalten.

![Übersichtsbildschirm des Failoverclusters](../media/manage-failover-clusters/fcm-overview.png)

## <a name="adding-a-failover-cluster-to-windows-admin-center"></a>Hinzufügen eines Failoverclusters zum Windows Admin Center
So fügen Sie dem Windows Admin Center einen Cluster hinzu:

1. Klicken Sie unter alle Verbindungen auf **+ Hinzufügen** .
2. Wählen Sie das Hinzufügen einer **failoververbindung**aus.
3. Geben Sie den Namen des Clusters und, falls Sie dazu aufgefordert werden, die zu verwendenden Anmelde Informationen ein.
4. Sie haben die Möglichkeit, die Cluster Knoten als einzelne Serververbindungen im Windows Admin Center hinzuzufügen.
5. Klicken Sie zum fertig **Stellen auf Senden** .

Der Cluster wird auf der Übersichtsseite zur Verbindungsliste hinzugefügt. Klicken Sie darauf, um eine Verbindung mit dem Cluster herzustellen.

> [!NOTE]
> Sie können auch hyperkonvergierte gruppierten verwalten, indem Sie den Cluster als [hyperkonvergierte Cluster Verbindung](manage-hyper-converged.md) im Windows Admin Center hinzufügen.

## <a name="tools"></a>Tools

Die folgenden Tools sind für failoverclusterverbindungen verfügbar:

| Tool | BESCHREIBUNG |
| ---- | ----------- |
| Übersicht | Anzeigen von failoverclusterdetails und Verwalten von Cluster Ressourcen |
| Datenträger | Anzeigen frei gegebener Cluster Datenträger und Volumes |
| Netzwerke | Anzeigen von Netzwerken im Cluster |
| Nodes | Anzeigen und Verwalten von Cluster Knoten |
| Rollen | Verwalten von Cluster Rollen oder Erstellen einer leeren Rolle |
| Aktualisierungen | Verwalten von Cluster fähigen Updates (erfordert " [kredssp](../understand/faq.md#does-windows-admin-center-use-credssp)") |
| [Virtuelle Computer](manage-virtual-machines.md) | Anzeigen und Verwalten virtueller Maschinen |
| Virtuelle Switches | Virtuelle Switches anzeigen und verwalten |

## <a name="more-coming"></a>Weitere Informationen

Die Failoverclusterverwaltung wird in Windows Admin Center aktiv ausgeführt, und in naher Zukunft werden neue Funktionen hinzugefügt. Sie können den Status anzeigen und die Features in UserVoice abstimmen:

|Funktionsanfrage|
|-------|
| [Weitere Informationen zum Cluster Datenträger anzeigen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [Zusätzliche Cluster Aktionen unterstützen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [Unterstützen konvergierter Cluster mit Hyper-V und Dateiserver mit horizontaler Skalierung auf verschiedenen Clustern](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [CSV-Block Cache anzeigen](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [Alle anzeigen oder neues Feature vorschlagen](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |