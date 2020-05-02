---
title: Telnet-Satz
description: Referenz Thema für den Telnet-Satz, mit dem Optionen festgelegt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 67316b5f-9c6f-43e3-86d5-dcff9ae2ac3e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a785a9448860752c79dc1c2369b8dd870409990
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721480"
---
# <a name="telnet-set"></a>Telnet: Set

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt Optionen fest.   

## <a name="syntax"></a>Syntax  
```  
set [bsasdel] [crlf] [delasbs] [escape <Char>] [localecho] [logfile <FileName>] [logging] [mode {console | stream}] [ntlm] [term {ansi | vt100 | vt52 | vtnt}] [?]  
```  
#### <a name="parameters"></a>Parameter  

|                    Parameter                     |                                                                                                                                              BESCHREIBUNG                                                                                                                                              |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     bsasdel                      |                                                                                                                                 Sendet **Rückraum** als **Lösch**Vorgang.                                                                                                                                  |
|                       CRLF                       |                                                                                                        Sendet CR & LF (0x0D, 0x 0A), wenn die **Eingabe** Taste gedrückt wird. Wird als neuer Zeilen Modus bezeichnet.                                                                                                        |
|                     Delta-                      |                                                                                                                                 Sendet **Delete** als **RÜCKTASTE**.                                                                                                                                  |
|                Weg<Character>                | Legt das Escapezeichen fest, mit dem die Telnet-Client Eingabeaufforderung eingegeben wird. Das Escapezeichen kann ein einzelnes Zeichen oder eine Kombination aus der **STRG** -Taste und einem Zeichen sein. Halten Sie zum Festlegen einer Tastenkombination die **STRG** -Taste gedrückt, während Sie das Zeichen eingeben, das Sie zuweisen möchten. |
|                    LOCALECHO                     |                                                                                                                                         Schaltet das lokale Echo ein.                                                                                                                                          |
|                Protokolldatei<FileName>                |                                                                                               Protokolliert die aktuelle Telnet-Sitzung in der lokalen Datei. Die Protokollierung beginnt automatisch, wenn Sie diese Option festlegen.                                                                                               |
|                     logging                      |                                                                                                                  Schaltet die Protokollierung ein. Wenn keine Protokolldatei festgelegt ist, wird eine Fehlermeldung angezeigt.                                                                                                                   |
|           Modus {Konsole &#124; Bildschirm}           |                                                                                                                                       Legt den Betriebsmodus fest.                                                                                                                                        |
|                       ntlm                       |                                                                                                                                     Schaltet die NTLM-Authentifizierung ein.                                                                                                                                     |
| Begriff {ANSI &#124; VT100 &#124; VT52 &#124; VTNT} |                                                                                                                                        Legt den Terminaltyp fest.                                                                                                                                        |
|                        ?                         |                                                                                                                                    Zeigt die Hilfe für diesen Befehl an.                                                                                                                                    |

## <a name="remarks"></a>Bemerkungen  
1. Sie können den **Festlegung** -Befehl verwenden, um eine Option zu deaktivieren, die zuvor festgelegt wurde.  
2. In nicht englischsprachigen Versionen von Telnet ist das **Codeset** <option> verfügbar. **Codeset** <option> legt den aktuellen Code fest, der auf eine Option festgelegt ist. dabei kann es sich um einen der folgenden handeln: **Shift JIS**, **Japanese EUC**, **JIS Kanji**, **JIS Kanji (78)**, **Dec**Kanji, **NEC Kanji**. Sie sollten den gleichen Code festlegen, der auf dem Remote Computer festgelegt ist.  
   ## <a name="examples"></a>Beispiele  
   Festlegen der Protokolldatei und Starten der Protokollierung in der lokalen Datei "tnlog. txt"  
   ```  
   set logfile tnlog.txt  
   ```  
   ## <a name="additional-references"></a>Zusätzliche Referenzen  
3. - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
