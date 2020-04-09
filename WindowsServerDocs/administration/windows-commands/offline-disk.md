---
title: Offline-Datenträger
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd7991f1f5967970690c7051612395fb47a764ec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837983"
---
# <a name="offline-disk"></a>Offline-Datenträger



Schaltet den Online Datenträger mit dem Fokus in den Offline Zustand.

> [!IMPORTANT]
> Dieser Diskpart-Befehl ist in keiner Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
offline disk [noerr]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Noerr|Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="remarks"></a>Hinweise

-   Dieser Befehl funktioniert auf Datenträgern im San Online-Modus. Der zugehörige San-Modus wird in Offline geändert.
-   Wenn ein dynamischer Datenträger in einer Datenträger Gruppe offline geschaltet wird, ändert sich der Status des Datenträgers in **fehlt** , und in der Gruppe wird ein Datenträger angezeigt, der offline ist. Der fehlende Datenträger wird in die ungültige Gruppe verschoben. Wenn die dynamische Festplatte der letzte Datenträger in der Gruppe ist, wird der Status des Datenträgers in **Offline**geändert, und die leere Gruppe wird entfernt.
-   Ein Datenträger muss ausgewählt werden, damit der **Offline** -Datenträger Befehl erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn Sie den Fokus offline schalten möchten, geben Sie Folgendes ein:
```
offline disk
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

