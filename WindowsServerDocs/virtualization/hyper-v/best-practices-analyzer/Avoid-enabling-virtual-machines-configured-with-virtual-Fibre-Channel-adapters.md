---
title: Vermeiden Sie das Aktivieren von virtuellen Computern, die mit virtuellen Fibre Channel Adaptern konfiguriert sind, damit Live Migrationen zulässig sind, wenn es weniger Pfade zu Fibre Channel logischen Einheiten (LUNs) auf dem Ziel als der Quelle gibt.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 7989d2e1908f6be32f4661900fc507b5843b55c9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857773"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>Vermeiden Sie das Aktivieren von virtuellen Computern, die mit virtuellen Fibre Channel Adaptern konfiguriert sind, damit Live Migrationen zulässig sind, wenn es weniger Pfade zu Fibre Channel logischen Einheiten (LUNs) auf dem Ziel als der Quelle gibt.

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.
  
## <a name="issue"></a>**Problem:**  
*Bei mindestens einer virtuellen Maschine ist die allowreducedfkredunancy-Eigenschaft im WMI-Anbieter für die Virtualisierung festgelegt.*  
  
## <a name="impact"></a>**Auswirkt**  
*Die Live Migration der folgenden virtuellen Computer kann zu Datenverlusten oder Unterbrechungen des Speichers führen:*  
  
\<Liste der virtuellen Computer >  
  
## <a name="resolution"></a>**Lösung**  
*Löschen Sie ggf. die Eigenschaft allowreducedfkredundancy WMI auf den betroffenen virtuellen Computern. Wenn diese Eigenschaft deaktiviert ist, können Sie eine Live Migration auf virtuellen Computern, die mit virtuellen Fibre Channel Adaptern konfiguriert sind, nur dann ausführen, wenn die Anzahl der Pfade Fibre Channel auf dem Ziel gleich oder größer als die Anzahl der Pfade in der Quelle ist. Diese Überprüfungen helfen dabei, Datenverluste oder e/a-Vorgänge im Speicher zu vermeiden.* 