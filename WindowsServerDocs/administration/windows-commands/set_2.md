---
title: set_2
description: Referenz Artikel für set_2, mit dem der Kontext, die Optionen, der ausführliche Modus und die Metadatendatei für die Erstellung von Schatten Kopien festgelegt werden.
ms.topic: reference
ms.assetid: acf24663-1a50-4321-b48d-1717655e9476
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 685f66692e324b29bb0a33aaaefaec44b52b218d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639479"
---
# <a name="set_2"></a>set_2

Legt den Kontext, die Optionen, den ausführlichen Modus und die Metadatendatei für die Erstellung von Schatten Kopien fest. Wenn Sie ohne Parameter verwendet wird, werden alle aktuellen Einstellungen von **festgelegt** .

## <a name="syntax"></a>Syntax

```
set
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
set verbose {on|off}
set metadata <MetaData.cab>
```

## <a name="set-sub-commands"></a>Unterbefehle festlegen

|Unterbefehl|Beschreibung|
|-----------|-----------|
|context|Legt den Kontext für die Erstellung von Schatten Kopien fest. Siehe [Festlegen des Kontexts](set-context.md) für Syntax und Parameter.|
|Option|Legt Optionen für die Erstellung von Schatten Kopien fest. Informationen finden Sie unter [Set-Option](set-option.md) für Syntax und Parameter.|
|Ausführlich|Schaltet den ausführlichen Ausgabemodus ein oder aus. Weitere Informationen zu Syntax und Parametern finden Sie unter [Set ausführliche](set-verbose.md) .|
|metadata|Legt den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung fest. Informationen zu Syntax und Parametern finden Sie unter [Set Metadata](set-metadata.md) .|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)