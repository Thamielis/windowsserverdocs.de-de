---
title: manage-bde-Status
description: Referenz Artikel zum Befehl "manage-bde Status", der Informationen zu allen Laufwerken auf dem Computer bereitstellt, unabhängig davon, ob Sie durch BitLocker geschützt sind.
ms.topic: reference
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ad22cf542aaf3f61d9fe861d20ad25087adfe0a1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639282"
---
# <a name="manage-bde-status"></a>manage-bde-Status

Enthält Informationen zu allen Laufwerken auf dem Computer. unabhängig davon, ob Sie durch BitLocker geschützt sind, einschließlich:

- Size

- BitLocker-Version

- Konvertierungs Status

- Verschlüsselter Prozentsatz

- Verschlüsselungsmethode

- Schutzstatus

- Sperr Status

- Identifikations Feld

- Schlüssel Schutzvorrichtungen

## <a name="syntax"></a>Syntax

```
manage-bde -status [<drive>] [-protectionaserrorlevel] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -schutzaserrorlevel | Bewirkt, dass das Befehlszeilen Tool manage-bde den Rückgabecode **0** (null) sendet, wenn das Volume geschützt ist, und **1** , wenn das Volume nicht geschützt ist. wird am häufigsten für Batch Skripts verwendet, um zu bestimmen, ob ein Laufwerk durch BitLocker geschützt ist. Sie können auch **-p** als abgekürzte Version dieses Befehls verwenden. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Status von Laufwerk C anzuzeigen:

```
manage-bde –status C:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
