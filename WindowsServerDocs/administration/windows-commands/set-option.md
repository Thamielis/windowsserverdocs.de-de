---
title: SET-Option
description: Referenz Artikel für die Set-Option, mit der die Optionen für die Erstellung von Schatten Kopien festgelegt werden.
ms.topic: reference
ms.assetid: 4d8d4921-9fdd-4a3c-bb0f-9df5458c4b84
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 143530ce3f781b7635cd596a376c5bea71994bf4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637691"
---
# <a name="set-option"></a>SET-Option

Legt die Optionen für die Erstellung von Schatten Kopien fest. Bei Verwendung ohne Parameter zeigt die **Option Set die Option** Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

### <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                  BESCHREIBUNG                                                                                                  |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [differenziell   |                                                                                                     Plex                                                                                                     |
|  austauschen  |                       Gibt an, dass die Schatten Kopie noch nicht importiert werden soll. Die Datei "Metadata. cab" kann später verwendet werden, um die Schatten Kopie auf denselben oder einen anderen Computer zu importieren.                       |
| [rollbackrecovery] |                     Signalisiert Writer, während des **PostSnapshot** -Ereignisses *Auto Wiederherstellen* zu verwenden. Dies ist hilfreich, wenn die Schatten Kopie für das Rollback verwendet wird (z. b. mit Data Mining).                      |
|   [txfrecover]    |                                                               Fordert VSS auf, die schattenkopiekonsistenz während der Erstellung Transaktions konsistent zu machen.                                                                |
|  [noautorecover]  | Hindert Writer und das Dateisystem daran, Wiederherstellungs Änderungen an der Schatten Kopie in einem Transaktions konsistenten Zustand auszuführen. **Noautorecover** kann nicht mit **txfrecover** oder **rollbackrecover**verwendet werden. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)