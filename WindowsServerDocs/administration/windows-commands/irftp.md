---
title: irftp
description: Referenz Artikel für den Befehl "iriftp", mit dem Dateien über einen Infrarot Link gesendet werden.
ms.topic: reference
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c9546dad7bcba60ab73a9bef50c8d4347ef6dc97
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634413"
---
# <a name="irftp"></a>irftp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Dateien über einen Infrarot Link.

> [!IMPORTANT]
> Stellen Sie sicher, dass auf den Geräten, die für die Kommunikation über eine Infrarot Verbindung vorgesehen sind, eine Infrarot Funktion aktiviert und ordnungsgemäß funktioniert Stellen Sie außerdem sicher, dass zwischen den Geräten eine Infrarot Verbindung hergestellt wird.

## <a name="syntax"></a>Syntax

```
irftp [<drive>:\] [[<path>] <filename>] [/h][/s]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<drive>:\` | Gibt das Laufwerk an, das die Dateien enthält, die über einen Infrarot Link gesendet werden sollen. |
| `[path]<filename>` | Gibt den Speicherort und den Namen der Datei oder des Satzes von Dateien an, die über einen Infrarot Link gesendet werden sollen. Wenn Sie einen Satz von Dateien angeben, müssen Sie den vollständigen Pfad für jede Datei angeben. |
| /h | Gibt den verborgenen Modus an. Wenn der verborgene Modus verwendet wird, werden die Dateien gesendet, ohne dass das Dialogfeld drahtlos Verbindung angezeigt wird. |
| /s | Öffnet das Dialogfeld **drahtlos Verbindung** , sodass Sie die Datei oder den Satz von Dateien, die Sie senden möchten, ohne die Befehlszeile zum Angeben von Laufwerk, Pfad und Dateinamen auswählen können. Das Dialogfeld **drahtlos Verbindung** wird auch geöffnet, wenn Sie diesen Befehl ohne Parameter verwenden. |

### <a name="examples"></a>Beispiele

Um *c:\example.txt* über die Infrarot Verknüpfung zu senden, geben Sie Folgendes ein:

```
irftp c:\example.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
