---
title: netcfg
description: Referenz Artikel für den Befehl "netcfg", der die Windows Preinstallation Environment (WinPE) installiert, eine vereinfachte Version von Windows, die zum Bereitstellen von Arbeitsstationen verwendet wird.
ms.topic: reference
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8680e2e4265f36058f8f0d7c57be144633060bba
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640338"
---
# <a name="netcfg"></a>netcfg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Installiert den Windows Preinstallation Environment (WinPE), eine für die Bereitstellung von Arbeitsstationen verwendete Lightweight-Version von Windows.

## <a name="syntax"></a>Syntax

```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /v | Wird im ausführlichen (ausführlichen) Modus ausgeführt. |
| /e | Verwendet Wartungs Umgebungsvariablen während der Installation und Deinstallation. |
| /winpe | Installiert TCP/IP, NetBIOS und den Microsoft-Client für Windows Preinstallation Environment (WinPE). |
| /l | Gibt den Speicherort der INF-Datei an. |
| /C | Stellt die Klasse der zu installierenden Komponente bereit. **Protokoll**, **Dienst**oder **Client**. |
| /i | Stellt die Komponenten-ID bereit. |
| /s | Gibt den Typ der anzuzeigenden Komponenten an, einschließlich **\ta** für Adapter oder **n** für NET-Komponenten. |
| /b | Zeigt die Bindungs Pfade an, wenn eine Zeichenfolge mit dem Namen des Pfads folgt. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Protokoll *Beispiel* mithilfe von "c:\oemdir\example.inf" zu installieren:

```
netcfg /l c:\oemdir\example.inf /c p /i example
```

Geben Sie Folgendes ein, um den *MS_Server* Dienst zu installieren:

```
netcfg /c s /i MS_Server
```

Geben Sie Folgendes ein, um TCP/IP, NetBIOS und den Microsoft-Client für die Vorinstallations Umgebung von Windows zu installieren:

```
netcfg /v /winpe
```

Um anzuzeigen, ob Component *MS_IPX* installiert ist, geben Sie Folgendes ein:

```
netcfg /q MS_IPX
```

Zum Deinstallieren von Komponenten *MS_IPX*geben Sie Folgendes ein:

```
netcfg /u MS_IPX
```

Geben Sie Folgendes ein, um alle installierten NET-Komponenten anzuzeigen:

```
netcfg /s n
```

Um Bindungs Pfade anzuzeigen, die *MS_TCPIP*enthalten, geben Sie Folgendes ein:

```
netcfg /b ms_tcpip
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
