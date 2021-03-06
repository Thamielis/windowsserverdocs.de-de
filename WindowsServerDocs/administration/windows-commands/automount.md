---
title: automount
description: Referenz Artikel für den automatischen Bereitstellung-Befehl, der die Funktion "automatischen Bereitstellung" aktiviert oder deaktiviert.
ms.topic: reference
ms.assetid: 4635fc91-a477-4f17-8dcc-aa08854bfe45
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0f4be54f7610929627e0cc0332a7f5d65eafc8b2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632996"
---
# <a name="automount"></a>automount

Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

> [!IMPORTANT]
> In Storage Area Network-Konfigurationen (San) verhindert die Deaktivierung der automatischen Bereitstellung, dass Windows Laufwerksbuchstaben automatisch für neue Basisvolumes bereitstellt oder zuweist, die für das System sichtbar sind.

## <a name="syntax"></a>Syntax

automatischen Bereitstellung [{Enable | enable | scru}] [noerr]

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| enable | Ermöglicht Windows das automatische Einbinden neuer grundlegender und dynamischer Volumes, die dem System hinzugefügt werden, und das Zuweisen von Laufwerk Buchstaben. |
| disable | Verhindert, dass Windows neue grundlegende und dynamische Volumes, die dem System hinzugefügt werden, automatisch bereitstellen.<p>**Hinweis**: durch das Deaktivieren der automatischen Problem Umgehung können Failovercluster den Speicher Teil des Konfigurationsüberprüfungs-Assistenten nicht beeinträchtigen. |
| volumebereinigung | Entfernt Volumes für das Volumebereitstellungspunkt und Registrierungs Einstellungen für Volumes, die sich nicht mehr im System befinden. Dadurch wird verhindert, dass Volumes, die zuvor im System waren, automatisch bereitgestellt werden, und ihre früheren Volumebereitstellungspunkte wurden beim Hinzufügen wieder zum System bereitgestellt. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Um festzustellen, ob die Funktion für die automatische Einbindung aktiviert ist, geben Sie die folgenden Befehle in den Diskpart-Befehl ein:

```
automount
```

Geben Sie Folgendes ein, um die Funktion für automatische Bereitstellung zu aktivieren:

```
automount enable
```

Geben Sie zum Deaktivieren der automatischen Bereitstellung-Funktion Folgendes ein:

```
automount disable
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DiskPart-Befehle](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc770877(v%3dws.11))
