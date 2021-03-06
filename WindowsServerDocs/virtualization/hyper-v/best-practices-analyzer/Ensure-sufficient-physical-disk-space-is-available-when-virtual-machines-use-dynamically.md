---
title: Stellen Sie sicher, dass genügend physischer Speicherplatz verfügbar ist, wenn virtuelle Computer dynamisch erweiterbare virtuelle Festplatten verwenden.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 9e3e3e64-4b3a-4b9d-acf1-e4df61a04f1e
ms.date: 8/16/2016
ms.openlocfilehash: 1e67b51aa3c41c9642a8972d25e0501b26e91cd5
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746865"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-dynamically-expanding-virtual-hard-disks"></a>Stellen Sie sicher, dass genügend physischer Speicherplatz verfügbar ist, wenn virtuelle Computer dynamisch erweiterbare virtuelle Festplatten verwenden.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer-Scans und Verwalten der Scanergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem
*Mindestens eine virtuelle Maschine verwendet dynamisch erweiterbare virtuelle Festplatten.*

## <a name="impact"></a>Auswirkung
*Für dynamisch erweiterbare virtuelle Festplatten ist der verfügbare Speicherplatz auf dem hostingvolume erforderlich, damit der Speicherplatz bei Schreibvorgängen auf den virtuellen Festplatten zugeordnet werden kann Wenn der verfügbare Speicherplatz erschöpft ist, kann der virtuelle Computer, der auf dem physischen Speicher basiert, beeinträchtigt werden. Dies wirkt sich auf die folgenden virtuellen Computer aus:*

\<list of virtual machines>

## <a name="resolution"></a>Lösung
*Überwachen Sie den verfügbaren Speicherplatz, um sicherzustellen, dass ausreichend Speicherplatz zur Erweiterung Sie sollten den virtuellen Computer Herunterfahren und im Hyper-V-Manager den Assistenten zum Bearbeiten von Datenträgern verwenden, um jede dynamisch erweiterbare virtuelle Festplatte für diese virtuelle Maschine in eine virtuelle Festplatte mit fester Größe zu konvertieren.*



