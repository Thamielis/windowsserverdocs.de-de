---
title: volumestripe erstellen
description: Windows-Befehls Artikel zum Erstellen von volumestripe, mit dem ein Stripesetvolume mit zwei oder mehr angegebenen dynamischen Datenträgern erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8123d2b5852f606398e3be7161ef0341698b7fb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846903"
---
# <a name="create-volume-stripe"></a>volumestripe erstellen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt ein Stripesetvolume mit zwei oder mehr angegebenen dynamischen Datenträgern.  
  
> [!IMPORTANT]  
> für Windows Vista ist dieser Diskpart-Befehl nur in den Business Editionen Windows Vista Ultimate, Windows Vista Enterprise und Windows Vista verfügbar.

## <a name="syntax"></a>Syntax  
  
```  
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|         Parameter         |                                                                                                                            Beschreibung                                                                                                                            |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Größe\=<n>         |             Der Speicherplatz in Megabyte \(MB\), den das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben ist, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem kleinsten Datenträger und den gleichen Speicherplatz auf jedem nachfolgenden Datenträger an.             |
| Datenträger\=<n>,<n>\[,<n>,...\] |                                  Die dynamischen Datenträger, auf denen das Stripesetvolume erstellt wird. Sie benötigen mindestens zwei dynamische Datenträger, um ein Stripesetvolume zu erstellen. Ein Speicherplatz gleich der **Größe\=<n>** auf jedem Datenträger zugeordnet ist.                                   |
|        \=<n> ausrichten         | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit der logischen Gerätenummer des Hardware-RAID-\(LUN\) Arrays verwendet, um die Leistung " *n* " ist die Anzahl der Kilobyte \(KB\) vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze. |
|           Noerr           |                               Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Geben Sie auf den Datenträgern 1 und 2 Folgendes ein, um ein Stripesetvolume mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create volume stripe size=1000 disk=1,2  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

