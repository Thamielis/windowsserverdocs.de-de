---
title: telnet send
description: Referenz Artikel für Telnet Send, bei dem Telnet-Befehle an den Telnet-Server gesendet werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44a0415a3516fcb15cd292c9e4c9c0a4a18e5ad9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937371"
---
# <a name="telnet-send"></a>Telnet: senden

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Telnet-Befehle an den Telnet-Server.

## <a name="syntax"></a>Syntax
```
sen[d] {ao | ayt | brk | esc | ip | synch | <string>} [?]
```
#### <a name="parameters"></a>Parameter

| Parameter |                     Beschreibung                      |
|-----------|------------------------------------------------------|
|    OS     |       Sendet die Ausgabe des Telnet-Befehls abgebrochen.        |
|    AYT    |       Sendet den Telnet-Befehl.       |
|    BRK    |            Sendet den Telnet-Befehl BRK.            |
|    ESC-TASTE    |      Sendet das aktuelle Telnet-Escapezeichen.      |
|    ip     |     Sendet den Telnet-Befehls Unterbrechungs Prozess.     |
|   synch   |           Sendet den Telnet-Befehl "Synch".           |
| <string>  | Sendet jede Zeichenfolge, die Sie an den Telnet-Server eingeben. |
|     ?     |     Zeigt die diesem Befehl zugeordnete Hilfe an.      |

## <a name="examples"></a>Beispiele
Senden Sie an den Telnet-Server.
```
sen ayt
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
