---
title: Fehlertoleranz und Speichereffizienz in Direkte Speicherplätze
ms.prod: windows-server
ms.author: cosmosdarwin
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/11/2017
ms.assetid: 5e1d7ecc-e22e-467f-8142-bad6d82fc5d0
description: Eine Erörterung von resilienzoptionen in direkte Speicherplätze einschließlich Spiegelung und Parität.
ms.localizationpriority: medium
ms.openlocfilehash: 540398e78b35d7cd61464e012d0f3ccfa85d7152
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475487"
---
# <a name="fault-tolerance-and-storage-efficiency-in-storage-spaces-direct"></a>Fehlertoleranz und Speichereffizienz in Direkte Speicherplätze

>Gilt für: Windows Server 2016

In diesem Thema werden die in [Direkte Speicherplätze](storage-spaces-direct-overview.md) verfügbaren Resilienzoptionen vorgestellt und die Skalierungsanforderungen, Speichereffizienz sowie allgemeine Vorteile und Nachteile der einzelnen Optionen beschrieben. Außerdem finden Sie einige Anweisungen zur Verwendung, um Ihnen den Einstieg erleichtern, sowie Verweise auf einige hilfreiche Dokumente, Blogs und weitere Inhalte, mit denen Sie sich informieren können.

Falls Sie bereits mit Speicherplätzen vertraut sind, können Sie mit dem Abschnitt [Zusammenfassung](#summary) fortfahren.

## <a name="overview"></a>Übersicht

Im Grunde geht es bei Speicherplätzen um die Bereitstellung von Fehlertoleranz, die häufig als "Resilienz" bezeichnet wird, für Ihre Daten. Die Implementierung erfolgt ähnlich wie bei RAID, allerdings verteilt über mehrere Server und in Software implementiert.

Wie bei RAID gibt es auch für Speicherplätze verschiedene Implementierungsmethoden, bei denen jeweils unterschiedliche Kompromisse zwischen Fehlertoleranz, Speichereffizienz und rechnerischer Komplexität gelten. Diese werden im Wesentlichen in zwei Kategorien unterteilt: "Spiegelung" und "Parität", letztere wird manchmal als "Erasure Coding" bezeichnet.

## <a name="mirroring"></a>Spiegelung

Die Spiegelung ermöglicht Fehlertoleranz, indem mehrere Kopien aller Daten aufbewahrt werden. Diese Methode ist am ehesten mit RAID-1 vergleichbar. Das Striping und platzieren dieser Daten ist nicht trivial (Weitere Informationen finden Sie in [diesem Blog](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/) ). es ist jedoch absolut zu sagen, dass alle Daten, die mit der Spiegelung gespeichert werden, in ihrer Gesamtheit mehrmals geschrieben werden. Jede Kopie wird auf andere physische Hardware (unterschiedliche Laufwerke von nicht identischen Servern) geschrieben, für die angenommen wird, dass sie nicht gemeinsam ausfallen.

In Windows Server 2016 bieten Speicherplätze zwei Arten von Spiegelung – "bidirektional" und "drei-Wege".

### <a name="two-way-mirror"></a>Zwei-Wege-Spiegelung

Die Zwei-Wege-Spiegelung schreibt zwei Kopien aller Elemente. Die Speichereffizienz ist 50 % – zum Schreiben von 1 TB an Daten benötigen Sie mindestens 2 TB physische Speicherkapazität. Ebenso benötigen Sie mindestens zwei [Fehler Domänen der Hardware](../../failover-clustering/fault-domains.md) – mit direkte Speicherplätze, d. h. zwei Server.

![Zwei-Wege-Spiegelung](media/Storage-Spaces-Fault-Tolerance/two-way-mirror-180px.png)

   >[!WARNING]
   > Wenn Sie über mehr als zwei Server verfügen, empfiehlt es sich, stattdessen den drei-Wege-Spiegelungen zu verwenden.

### <a name="three-way-mirror"></a>Drei-Wege-Spiegelung

Die Drei-Wege-Spiegelung schreibt drei Kopien aller Elemente. Die Speichereffizienz ist 33.3 % – zum Schreiben von 1 TB an Daten benötigen Sie mindestens 3 TB physische Speicherkapazität. Ebenso benötigen Sie mindestens drei Hardware-Fehlerdomänen – bei Direkte Speicherplätze bedeutet das drei Server.

Die drei-Wege-Spiegelung kann [jeweils mindestens zwei Hardwareprobleme (Laufwerk oder Server)](#examples)sicher tolerieren. Wenn Sie beispielsweise einen Server neu starten und plötzlich ein anderes Laufwerk bzw. ein Server ausfällt, bleiben alle Daten geschützt und sind ohne Unterbrechung zugänglich.

![Drei-Wege-Spiegelung](media/Storage-Spaces-Fault-Tolerance/three-way-mirror-180px.png)

## <a name="parity"></a>Parität

Die Paritäts Codierung, oft als "Erasure Coding" bezeichnet, bietet Fehlertoleranz mithilfe bitweiser Arithmetik, die [erheblich kompliziert](https://www.microsoft.com/research/wp-content/uploads/2016/02/LRC12-cheng20webpage.pdf)werden kann. Die Funktionsweise ist weniger offensichtlich als bei der Spiegelung, und es gibt viele hilfreiche Onlineressourcen (z. B. das Dokument [Dummies Guide to Erasure Coding](http://smahesh.com/blog/2012/07/01/dummies-guide-to-erasure-coding/) eines Drittanbieter), die Ihnen einen Eindruck davon vermitteln. Hervorzuheben ist lediglich, dass diese Methode eine bessere Speichereffizienz bietet, ohne die Fehlertoleranz zu beeinträchtigen.

In Windows Server 2016 bieten Speicherplätze zwei Arten von Parität – die Parität "Single" und "Dual", letztere verwendet ein erweitertes Verfahren mit dem Namen "local Reconstruction Codes" in größerem Maßstab.

> [!IMPORTANT]
> Wir empfehlen die Verwendung von Spiegelung für die meisten Leistungs sensitiven Workloads. Weitere Informationen zum Ausgleichen der Leistung und Kapazität in Abhängigkeit von der Arbeitsauslastung finden Sie unter [Planen von Volumes](plan-volumes.md#choosing-the-resiliency-type).

### <a name="single-parity"></a>Einzelparität
Die Einzelparität behält nur ein bitweises Paritätssymbol bei, das nur Fehlertoleranz für jeweils einen Ausfall bereitstellt. Diese Methode ist am ehesten mit RAID-5 vergleichbar. Zur Verwendung der Einzelparität benötigen Sie mindestens drei Hardware-Fehlerdomänen – bei Direkte Speicherplätze bedeutet das drei Server. Da die Drei-Wege-Spiegelung mehr Fehlertoleranz im selben Maßstab bereitstellt, wird von der Verwendung einer Einzelparität abgeraten. Aber es ist, wenn Sie darauf beharren, es zu verwenden, und es wird vollständig unterstützt.

   >[!WARNING]
   > Wir raten davon ab, die einfache Parität zu verwenden, da Sie nur einen Hardwarefehler gleichzeitig sicher tolerieren kann: Wenn Sie einen Server neu starten, während plötzlich ein anderes Laufwerk oder Server ausfällt, treten Ausfallzeiten auf. Wenn Sie nur über drei Server verfügen, wird die Drei-Wege-Spiegelung empfohlen. Wenn Sie mindestens vier Server haben, lesen Sie im nächsten Abschnitt weiter.

### <a name="dual-parity"></a>Duale Parität

Die duale Parität implementiert Fehler Behebungs Codes von Reed-Solomon, um zwei bitweise Paritäts Symbole beizubehalten, die dieselbe Fehlertoleranz wie die drei-Wege-Spiegelung (d. h. bis zu zwei Fehler gleichzeitig) bereitstellen, aber mit besserer Speichereffizienz. Diese Methode ist am ehesten mit RAID-6 vergleichbar. Zur Verwendung der dualen Parität benötigen Sie mindestens vier Hardware-Fehlerdomänen – bei Direkte Speicherplätze bedeutet das vier Server. In diesem Umfange beträgt die Speichereffizienz 50 % – zum Speichern von 2 TB an Daten benötigen Sie mindestens 4 TB physische Speicherkapazität.

![dual-parity](media/Storage-Spaces-Fault-Tolerance/dual-parity-180px.png)

Die Speichereffizienz der dualen Parität steigt mit der Anzahl vorhandener Hardware-Fehlerdomänen von 50 % auf bis zu 80 %. Bei sieben Domänen (d. h. sieben Servern bei Direkte Speicherplätze) steigt die Effizienz auf 66,7 % – zum Speichern von 4 TB an Daten benötigen Sie nur 6 TB physische Speicherkapazität.

![dual-parity-wide](media/Storage-Spaces-Fault-Tolerance/dual-parity-wide-180px.png)

Im Abschnitt [Zusammenfassung](#summary) finden Sie Informationen zur Effizienz der dualen Parität und von Codes für die lokale Wiederherstellung in jeder Größenordnung.

### <a name="local-reconstruction-codes"></a>Codes für die lokale Wiederherstellung

Mithilfe von Speicherplätzen in Windows Server 2016 wird ein erweitertes Verfahren eingeführt, das von Microsoft Research entwickelt wurde, das als "local Reconstruction Codes" oder LRC bezeichnet wird. Bei umfangreichen Vorgängen verwendet die duale Parität LRC, um ihre Codierung/Decodierung in einige kleinere Gruppen aufzuteilen, sodass der Aufwand für Schreibvorgänge oder Wiederherstellungen nach Ausfällen reduziert wird.

Bei Festplattenlaufwerken (HDDs) umfasst eine Gruppe vier Symbole, und bei Festkörperlaufwerken (SSDs) umfasst eine Gruppe sechs Symbole. Beispiel: Hier sehen Sie das Layout bei Festplattenlaufwerken und 12 Hardware-Fehlerdomänen (also 12 Server). Es sind zwei Gruppen mit je vier Datensymbolen vorhanden. Es wird eine Speichereffizienz von 72,7 % erzielt.

![local-reconstruction-codes](media/Storage-Spaces-Fault-Tolerance/local-reconstruction-codes-180px.png)

Wir empfehlen Ihnen diese ausführliche, aber hervorragend lesbare Exemplarische Vorgehens [Weise, wie die Code der lokalen Wiederherstellung verschiedene Fehler Szenarien behandelt und warum Sie ansprechend](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)sind, von unserem eigenen [Claus Joergensen](https://twitter.com/clausjor).

## <a name="mirror-accelerated-parity"></a>Durch Spiegelung beschleunigte Parität

Ab Windows Server 2016 kann ein direkte Speicherplätze Volume Teil Spiegelung und Teil Parität sein. Schreibt das Land zuerst in den gespiegelten Teil und wird später allmählich in den Paritäts Teil verschoben. Dadurch wird [die Verwendung von Spiegelung beschleunigt, um das Programmieren zu beschleunigen](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/).

Für die Kombination aus Drei-Wege-Spiegelung und dualer Parität benötigen Sie mindestens vier Fehlerdomänen, d. h. vier Server.

Die Speichereffizienz von Spiegel beschleunigter Parität liegt zwischen dem, was Sie bei der Verwendung der gesamten Spiegelung oder der gesamten Parität erzielen, und hängt von den Proportionen ab, die Sie auswählen. Die Demo in Minute 37 dieser Präsentation zeigt z. B. [verschiedene Kombinationen, die eine Effizienz von 46 %, 54 % und 65 % Effizienz](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s) mit 12 Servern erzielen.

> [!IMPORTANT]
> Wir empfehlen die Verwendung von Spiegelung für die meisten Leistungs sensitiven Workloads. Weitere Informationen zum Ausgleichen der Leistung und Kapazität in Abhängigkeit von der Arbeitsauslastung finden Sie unter [Planen von Volumes](plan-volumes.md#choosing-the-resiliency-type).

## <a name="summary"></a><a name="summary"></a>Zusammenfassung

Dieser Abschnitt enthält die in „Direkte Speicherplätze“ verfügbaren Resilienztypen, die Mindestanforderungen für die Skalierung bei Verwendung der einzelnen Typen, die Anzahl von tolerierbaren Fehlern pro Typ und die entsprechende Speichereffizienz.

### <a name="resiliency-types"></a>Resilienztypen

|    Resilienz          |    Fehlertoleranz       |    Speichereffizienz      |
|------------------------|----------------------------|----------------------------|
|    Zwei-Wege-Spiegelung      |    1                       |    50.0%                   |
|    Drei-Wege-Spiegelung    |    2                       |    33,3 %                   |
|    Duale Parität         |    2                       |    50,0 % - 80,0 %           |
|    Mixed               |    2                       |    33,3 % - 80,0 %           |

### <a name="minimum-scale-requirements"></a>Mindestanforderungen für Skalierung

|    Resilienz          |    Mindestens erforderliche Fehler Domänen   |
|------------------------|-------------------------------------|
|    Zwei-Wege-Spiegelung      |    2                                |
|    Drei-Wege-Spiegelung    |    3                                |
|    Duale Parität         |    4                                |
|    Mixed               |    4                                |

   >[!TIP]
   > Sofern Sie nicht die [Gehäuse- oder Rackfehlertoleranz](../../failover-clustering/fault-domains.md) verwenden, bezieht sich die Anzahl von Fehlerdomänen auf die Anzahl von Servern. Die Anzahl von Laufwerken auf jedem Server hat keine Auswirkung darauf, welche Resilienztypen Sie verwenden können, solange Sie die Mindestanforderungen für „Direkte Speicherplätze“ erfüllen.

### <a name="dual-parity-efficiency-for-hybrid-deployments"></a>Effizienz der dualen Parität für Hybridbereitstellungen

In dieser Tabelle sind die Speichereffizienz der dualen Parität und die Codes für die lokale Wiederherstellung in jeder Größenordnung für Hybridbereitstellungen mit Festplattenlaufwerken (HDDs) und Festkörperlaufwerken (SSDs) angegeben.

|    Fehlerdomänen      |    Layout           |    Effizienz   |
|-----------------------|---------------------|-----------------|
|    2                  |    –                |    –            |
|    3                  |    –                |    –            |
|    4                  |    RS 2+2           |    50.0%        |
|    5                  |    RS 2+2           |    50.0%        |
|    6                  |    RS 2+2           |    50.0%        |
|    7                  |    RS 4+2           |    66,7 %        |
|    8                  |    RS 4+2           |    66,7 %        |
|    9                  |    RS 4+2           |    66,7 %        |
|    10                 |    RS 4+2           |    66,7 %        |
|    11                 |    RS 4+2           |    66,7 %        |
|    12                 |    LRC (8, 2, 1)    |    72,7 %        |
|    13                 |    LRC (8, 2, 1)    |    72,7 %        |
|    14                 |    LRC (8, 2, 1)    |    72,7 %        |
|    15                 |    LRC (8, 2, 1)    |    72,7 %        |
|    16                 |    LRC (8, 2, 1)    |    72,7 %        |

### <a name="dual-parity-efficiency-for-all-flash-deployments"></a>Effizienz der dualen Parität für reine Flash-Bereitstellungen

In dieser Tabelle sind die Speichereffizienz der dualen Parität und die Codes für die lokale Wiederherstellung in jeder Größenordnung für reine Flash-Bereitstellungen mit Festkörperlaufwerken (SSDs) angegeben. Für das Paritätslayout können höhere Gruppengrößen verwendet werden, und für eine reine Flash-Konfiguration kann eine bessere Speichereffizienz erzielt werden.

|    Fehlerdomänen      |    Layout           |    Effizienz   |
|-----------------------|---------------------|-----------------|
|    2                  |    –                |    –            |
|    3                  |    –                |    –            |
|    4                  |    RS 2+2           |    50.0%        |
|    5                  |    RS 2+2           |    50.0%        |
|    6                  |    RS 2+2           |    50.0%        |
|    7                  |    RS 4+2           |    66,7 %        |
|    8                  |    RS 4+2           |    66,7 %        |
|    9                  |    RS 6+2           |    75.0%        |
|    10                 |    RS 6+2           |    75.0%        |
|    11                 |    RS 6+2           |    75.0%        |
|    12                 |    RS 6+2           |    75.0%        |
|    13                 |    RS 6+2           |    75.0%        |
|    14                 |    RS 6+2           |    75.0%        |
|    15                 |    RS 6+2           |    75.0%        |
|    16                 |    LRC (12, 2, 1)   |    80,0 %        |

## <a name="examples"></a><a name="examples"></a>Beispiele

Sofern Sie nicht nur zwei Server verwenden, empfehlen wir Ihnen die Nutzung der Drei-Wege-Spiegelung bzw. der dualen Parität, weil dies eine bessere Fehlertoleranz ermöglicht. Es wird sichergestellt, dass alle Daten auch dann sicher und ständig verfügbar sind, wenn zwei Fehlerdomänen – bei „Direkte Speicherplätze“ also zwei Server – von gleichzeitigen Ausfällen betroffen sind.

### <a name="examples-where-everything-stays-online"></a>Beispiele für Fälle, in denen alle Komponenten online bleiben

Diese sechs Beispiele verdeutlichen, was bei der Drei-Wege-Spiegelung bzw. der dualen Parität toleriert werden **kann**.

- **1.**    Ausfall eines Laufwerks (einschließlich Cachelaufwerke)
- **2.**    Ausfall eines Servers

![fault-tolerance-examples-1-and-2](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-12.png)

- **3.**    Ausfall eines Servers und eines Laufwerks
- **4.**    Ausfall von zwei Laufwerken auf unterschiedlichen Servern

![fault-tolerance-examples-3-and-4](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-34.png)

- **5.**    Ausfall von mehr als zwei Laufwerken, sofern maximal zwei Server betroffen sind
- **6.**    Ausfall von zwei Servern

![fault-tolerance-examples-5-and-6](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-56.png)

In all diesen Fällen bleiben alle Volumes online. (Stellen Sie sicher, dass für Ihren Cluster das Quorum beibehalten wird.)

### <a name="examples-where-everything-goes-offline"></a>Beispiele, in denen alles offline geschaltet wird

Während ihrer gesamten Lebensdauer können Speicherplätze eine beliebige Anzahl von Ausfällen tolerieren, da die Resilienz nach jedem Ausfall vollständig wiederhergestellt wird, sofern genügend Zeit ist. Es können aber jeweils nur maximal zwei Fehlerdomänen von einem Fehler betroffen sein, ohne dass es zu Problemen kommt. Daher sind hier Beispiele dafür angegeben, was bei der Drei-Wege-Spiegelung bzw. der dualen Parität toleriert werden **kann**.

- **7.** Gleichzeitiger Ausfall von Laufwerken auf drei oder mehr Servern
- **8.** drei oder mehr Server, die gleichzeitig verloren gehen

![fault-tolerance-examples-7-and-8](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-78.png)

## <a name="usage"></a>Zweck

Weitere Informationen finden Sie [unter Erstellen von Volumes in direkte Speicherplätze](create-volumes.md).

## <a name="additional-references"></a>Zusätzliche Referenzen

Alle folgenden Links sind inline im Text dieses Themas vorhanden.

- [Direkte Speicherplätze in Windows Server 2016](storage-spaces-direct-overview.md)
- [Fehler Domänen Bewusstsein in Windows Server 2016](../../failover-clustering/fault-domains.md)
- [Erasure Coding in Azure von Microsoft Research](https://www.microsoft.com/research/publication/erasure-coding-in-windows-azure-storage/)
- [Codes für die lokale Wiederherstellung und Beschleunigung von Paritätsvolumes](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)
- [Volumes in der Speicherverwaltungs-API](https://blogs.technet.microsoft.com/filecab/2016/08/29/deep-dive-volumes-in-spaces-direct/)
- [Demo zur Speichereffizienz auf der Microsoft Ignite 2016](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s)
- [Kapazitätsrechner (VORSCHAU) für Direkte Speicherplätze](https://aka.ms/s2dcalc)
