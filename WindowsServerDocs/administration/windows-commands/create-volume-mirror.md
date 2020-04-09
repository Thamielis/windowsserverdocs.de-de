---
title: volumespiegelung erstellen
description: Windows-Befehls Artikel zum Erstellen einer volumespiegelung, mit dem eine volumespiegelung mithilfe der beiden angegebenen dynamischen Datenträger erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fa5ea72eb0edacb841f32126f31a257b0573dd6d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846973"
---
# <a name="create-volume-mirror"></a>volumespiegelung erstellen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine volumespiegelung mithilfe der beiden angegebenen dynamischen Datenträger.  
  
> [!NOTE]  
> Dieser Befehl ist nur in Windows 7 und Windows Server 2008 R2 verfügbar.

## <a name="syntax"></a>Syntax  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|         Parameter         |                                                                                                                                     Beschreibung                                                                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Größe\=<n>         |                 Gibt die Speicherplatz Menge in Megabyte \(MB\)an, die das Volume auf jedem Datenträger einnimmt. Wenn keine Größe angegeben ist, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem kleinsten Datenträger und den gleichen Speicherplatz auf jedem nachfolgenden Datenträger an.                 |
| Datenträger\=<n>,<n>\[,<n>,...\] |                       Gibt die dynamischen Datenträger an, auf denen das Spiegelungs Volume erstellt wird. Zum Erstellen eines Spiegelungs Volumes benötigen Sie zwei dynamische Datenträger. Eine Menge an Speicherplatz, die der Größe entspricht, die mit dem **size** -Parameter angegeben wird, wird auf jedem Datenträger zugeordnet.                        |
|        \=<n> ausrichten         | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Dieser Parameter wird in der Regel mit der logischen Gerätenummer des Hardware-RAID \(LUN\) Arrays verwendet, um die Leistung zu verbessern " *n* " ist die Anzahl der Kilobyte \(KB\) vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze. |
|           Noerr           |                                        Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehler beendet wird.                                         |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Geben Sie auf den Datenträgern 1 und 2 Folgendes ein, um ein gespiegeltes Volume mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

