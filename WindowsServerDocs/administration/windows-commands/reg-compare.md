---
title: reg-Vergleich
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 177dc6a3-034e-4846-a394-330d03c14e0b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 49e9b993f512fdbc4728ee08ec42a8bc7ce0ab8f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722587"
---
# <a name="reg-compare"></a>reg-Vergleich



Vergleicht die angegebenen Registrierungs Unterschlüssel oder-Einträge.



## <a name="syntax"></a>Syntax

```
reg compare <KeyName1> <KeyName2> [{/v ValueName | /ve}] [{/oa | /od | /os | on}] [/s]
```

### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                                                                                                                                                                                                          BESCHREIBUNG                                                                                                                                                                                                                                                                                           |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   \<KeyName1>   |                                                               Gibt den vollständigen Pfad des ersten zu vergleichenden unter Schlüssels an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen ( \\ \\im Format\) Computername als Teil des *keyName*-Steuerelement ein. Wenn Computer \\ \\Name \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.                                                                |
|   \<KeyName2>   | Gibt den vollständigen Pfad des zweiten unter Schlüssels an, der verglichen werden soll. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen ( \\ \\im Format\) Computername als Teil des *keyName*-Steuerelement ein. Wenn Computer \\ \\Name \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Wenn Sie nur den Computernamen in *KeyName2* angeben, wird vom-Vorgang der Pfad zum Unterschlüssel verwendet, der in *KeyName1*angegeben ist. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU. |
| /v \<valueName> |                                                                                                                                                                                                                                                                     Gibt den Namen des Werts an, der unter dem Unterschlüssel verglichen werden soll.                                                                                                                                                                                                                                                                      |
|       /ve       |                                                                                                                                                                                                                                                         Gibt an, dass nur Einträge mit dem Wertnamen NULL verglichen werden sollen.                                                                                                                                                                                                                                                         |
|      [{/oa      |                                                                                                                                                                                                                                                                                              /od                                                                                                                                                                                                                                                                                               |
|       /oa       |                                                                                                                                                                                                                                             Gibt an, dass alle Unterschiede und Übereinstimmungen angezeigt werden. Standardmäßig sind nur die Unterschiede aufgeführt.                                                                                                                                                                                                                                             |
|       /od       |                                                                                                                                                                                                                                                          Gibt an, dass nur Unterschiede angezeigt werden. Dies ist das Standardverhalten.                                                                                                                                                                                                                                                          |
|       /OS       |                                                                                                                                                                                                                                                    Gibt an, dass nur Übereinstimmungen angezeigt werden. Standardmäßig sind nur die Unterschiede aufgeführt.                                                                                                                                                                                                                                                     |
|       /on       |                                                                                                                                                                                                                                                       Gibt an, dass nichts angezeigt wird. Standardmäßig sind nur die Unterschiede aufgeführt.                                                                                                                                                                                                                                                        |
|       /s        |                                                                                                                                                                                                                                                                         Vergleicht alle Unterschlüssel und Einträge rekursiv.                                                                                                                                                                                                                                                                          |
|       /?        |                                                                                                                                                                                                                                                                    Zeigt die Hilfe für den **reg Compare** an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                    |

## <a name="remarks"></a>Bemerkungen

In der folgenden Tabelle sind die Rückgabewerte für **reg Compare**aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Der Vergleich ist erfolgreich, und das Ergebnis ist identisch.|
|1|Der Vergleich ist fehlgeschlagen.|
|2|Der Vergleich war erfolgreich, und es wurden Unterschiede gefunden.|

In der folgenden Tabelle werden die Symbole aufgelistet, die in den Ergebnissen angezeigt werden.

|Symbol|BESCHREIBUNG|
|------|-----------|
|=|*KeyName1* -Daten sind gleich *KeyName2* -Daten.|
|<|*KeyName1* -Daten sind kleiner als *KeyName2* -Daten.|
|>|*KeyName1* -Daten sind größer als *KeyName2* -Daten.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Werte unter dem Schlüssel " **myapp** " mit allen Werten unter dem Schlüssel " **SaveMyApp**" zu vergleichen:

REG COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

Um den Wert für die Version unter dem Schlüssel **myco** und den Wert für die Version unter dem Schlüssel **MyCo1**zu vergleichen, geben Sie Folgendes ein:

REG COMPARE HKLM\Software\MyCo hklm\software\meineco1/v Version

Geben Sie Folgendes ein, um alle untergeordneten Schlüssel und Werte unter "HKLM\Software\MyCo" auf dem Computer mit dem Namen "Zodiac" mit allen unter Schlüsseln und Werten unter "HKLM\Software\MyCo" auf dem lokalen Computer zu vergleichen:

REG Compare \\ \\zodiac\hklm\software\myco \\ \\. /s

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)