---
title: diskcopy
description: Referenz Artikel für den Befehl diskcopy, der den Inhalt der Diskette im Quelllaufwerk in eine formatierte oder unformatierte Diskette auf dem Ziellaufwerk kopiert.
ms.topic: reference
ms.assetid: 5fd21efa-52cc-4e70-a7fe-35125a435106
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 05/07/2018
ms.openlocfilehash: 5ed6c3eee6f096e6069e5752441229015db8ed86
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634952"
---
# <a name="diskcopy"></a>diskcopy

Kopiert den Inhalt des Disketten Datenträgers im Quelllaufwerk in eine formatierte oder unformatierte Diskette auf dem Ziellaufwerk. Bei Verwendung ohne Parameter verwendet **diskcopy** das aktuelle Laufwerk für den Quell Datenträger und den Ziel Datenträger.

## <a name="syntax"></a>Syntax

```
diskcopy [<drive1>: [<drive2>:]] [/v]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<drive1>` | Gibt das Laufwerk an, das den Quell Datenträger enthält. |
| /v | Überprüft, ob die Informationen ordnungsgemäß kopiert werden. Diese Option verlangsamt den Kopiervorgang. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- **Diskcopy** funktioniert nur mit Wechsel Datenträgern, z. b. Disketten Datenträgern, die denselben Typ aufweisen müssen. **Diskcopy** kann nicht mit einer Festplatte verwendet werden. Wenn Sie ein Festplattenlaufwerk für *drive1* oder *drive2*angeben, wird von **diskcopy** die folgende Fehlermeldung angezeigt:

    ```
    Invalid drive specification
    Specified drive does not exist or is nonremovable
    ```

    Der **diskcopy** -Befehl fordert Sie auf, die Quell-und Ziel Datenträger einzufügen, und wartet, bis Sie eine beliebige Taste drücken, bevor Sie fortfahren.

    Nachdem der Datenträger kopiert wurde, zeigt **diskcopy** die folgende Meldung an:

    ```
    Copy another diskette (Y/N)?
    ```

    Wenn Sie Y drücken, werden Sie von **diskcopy** aufgefordert, Quell-und Ziel Datenträger für den nächsten Kopiervorgang einzufügen. **Y** Um den **diskcopy** -Prozess anzuhalten, drücken Sie **N**.

    Wenn Sie auf eine unformatierte Diskette in *drive2*kopieren, formatiert **diskcopy** den Datenträger mit der gleichen Anzahl von Seiten und Sektoren pro Spur, die sich auf dem Datenträger in *drive1*befinden. **Diskcopy** zeigt die folgende Meldung an, während die Festplatte formatiert und die Dateien kopiert werden:

    ```
    Formatting while copying
    ```

- Wenn der Quell Datenträger eine Volumeseriennummer aufweist, erstellt **diskcopy** eine neue Volumeseriennummer für den Ziel Datenträger und zeigt die Nummer an, wenn der Kopiervorgang beendet ist

- Wenn Sie den *drive2* -Parameter weglassen, verwendet **diskcopy** das aktuelle Laufwerk als Ziellaufwerk. Wenn Sie beide Laufwerk Parameter weglassen, verwendet **diskcopy** das aktuelle Laufwerk für beide. Wenn das aktuelle Laufwerk mit *drive1*identisch ist, werden Sie von **diskcopy** aufgefordert, Datenträger nach Bedarf auszutauschen.

- Führen Sie **diskcopy** von einem anderen Laufwerk als dem Diskettenlaufwerk aus, z. b. von Laufwerk C. Wenn Disketten *drive1* und Diskette *drive2* identisch sind, werden Sie von **diskcopy** aufgefordert, Datenträger zu wechseln. Wenn die Datenträger mehr Informationen enthalten, als der verfügbare Arbeitsspeicher aufnehmen kann, kann **diskcopy** nicht alle Informationen gleichzeitig lesen. **Diskcopy** liest vom Quell Datenträger, schreibt auf den Ziel Datenträger und fordert Sie auf, den Quell Datenträger erneut einzufügen. Dieser Prozess wird fortgesetzt, bis Sie den gesamten Datenträger kopiert haben.

- Fragmentierung ist das vorhanden sein kleiner Bereiche von nicht verwendetem Speicherplatz zwischen vorhandenen Dateien auf einem Datenträger. Ein fragmentierter Quell Datenträger kann das Auffinden, lesen oder Schreiben von Dateien verlangsamen.

    Da **diskcopy** eine exakte Kopie des Quell Datenträgers auf dem Ziel Datenträger erstellt, wird jede Fragmentierung auf dem Quell Datenträger auf den Ziel Datenträger über Um zu vermeiden, dass die Fragmentierung von einem Datenträger auf einen anderen übertragen wird, kopieren Sie den Datenträger mit dem [Kopier Befehl](copy.md) oder dem [xcopy-Befehl](xcopy.md) Da **Kopier** -und **xcopy** -Dateien nacheinander kopiert werden, wird der neue Datenträger nicht fragmentiert.

    > [!NOTE]
    > Sie können mit **xcopy** keinen Start Datenträger kopieren.

- Exitcodes für **diskcopy** :

    | Exitcode | BESCHREIBUNG |
    | --------- | ----------- |
    | 0 | Der Kopiervorgang war erfolgreich. |
    | 1 | Nicht schwerwiegender Lese-/Schreibfehler |
    | 3 | Schwerwiegender schwerwiegender Fehler |
    | 4 | Initialisierungsfehler |

    Um die von **diskcomp**zurückgegebenen Exitcodes zu verarbeiten, können Sie die *ERRORLEVEL* -Umgebungsvariable in der **if** -Befehlszeile in einem Batch-Programm verwenden.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Datenträger in Laufwerk B auf den Datenträger in Laufwerk a zu kopieren:

```
diskcopy b: a:
```

Wenn Sie Diskettenlaufwerk A verwenden möchten, um eine Diskette in eine andere zu kopieren, wechseln Sie zunächst zum Laufwerk C, und geben Sie dann Folgendes ein:

```
diskcopy a: a:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [xcopy-Befehl](xcopy.md)

- [Befehl "Kopieren"](copy.md)
