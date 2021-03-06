---
title: fsutil transaction
description: Referenz Artikel für den Befehl "sasutil Transaction", der NTFS-Transaktionen verwaltet.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
ms.topic: reference
ms.date: 10/16/2017
ms.openlocfilehash: 4eeefc4e98e621cf44baa881c69ccbe36d20a689
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032938"
---
# <a name="fsutil-transaction"></a>fsutil transaction

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Verwaltet NTFS-Transaktionen.

## <a name="syntax"></a>Syntax

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <filename>
fsutil transaction [list]
fsutil transaction [query] [{files | all}] <GUID>
fsutil transaction [rollback] <GUID>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Commit | Markiert das Ende einer erfolgreichen impliziten oder expliziten angegebenen Transaktion. |
| `<GUID>` | Gibt den GUID-Wert an, der eine Transaktion darstellt. |
| FileInfo  | Zeigt Transaktionsinformationen für die angegebene Datei an. |
| `<filename>` | Gibt den vollständigen Pfad und den Dateinamen an. |
| list | Zeigt eine Liste der derzeit laufenden Transaktionen an. |
| Abfrage | Zeigt Informationen für die angegebene Transaktion an.<ul><li>Wenn `fsutil transaction query files` angegeben wird, werden die Dateiinformationen nur für die angegebene Transaktion angezeigt.</li><li>Wenn `fsutil transaction query all` angegeben wird, werden alle Informationen für die Transaktion angezeigt.</li></ul> |
| rollback | Führt ein Rollback für eine angegebene Transaktion zum Anfang aus. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Transaktionsinformationen für Datei *c:\test.txt*anzuzeigen:

```
fsutil transaction fileinfo c:\test.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [Transaktions-NTFS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v=ws.10))
