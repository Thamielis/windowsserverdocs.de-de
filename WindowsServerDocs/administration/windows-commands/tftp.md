---
title: tftp
description: Übertragen von Dateien auf und von einem Remote Computer.
ms.topic: reference
ms.assetid: 772f19a8-dafe-45cd-878a-f5691f6568ef
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0d2d7c0c62cb0285347e1309f8dadf48a8ef27dc
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640802"
---
# <a name="tftp"></a>tftp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überträgt Dateien an und von einem Remote Computer, in der Regel auf einem Computer mit UNIX, auf dem der Trivial File Transfer Protocol-Dienst oder-Daemon ausgeführt wird. TFTP wird in der Regel von eingebetteten Geräten oder Systemen verwendet, die während des Startvorgangs von einem TFTP-Server aus Firmware, Konfigurationsinformationen oder ein System Abbild abrufen.

## <a name="syntax"></a>Syntax
```
tftp [-i] [<Host>] [{get | put}] <Source> [<Destination>]
```

#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|-i|Gibt den binären Bild Übertragungsmodus (auch als Octett-Modus bezeichnet) an. Im binären Bild Modus wird die Datei in 1-Byte-Einheiten übertragen. Verwenden Sie diesen Modus beim Übertragen von Binärdateien. Wenn **-i** weggelassen wird, wird die Datei im ASCII-Modus übertragen. Dies ist der Standard Übertragungsmodus. In diesem Modus werden die Zeilenende (EOL)-Zeichen in ein entsprechendes Format für den angegebenen Computer konvertiert. Verwenden Sie diesen Modus beim Übertragen von Textdateien. Wenn eine Dateiübertragung erfolgreich ist, wird die Datenübertragungsrate angezeigt.|
|\<Host\>|Gibt den lokalen oder Remote Computer an.|
|put|Überträgt die Datei *Quelle* auf dem lokalen Computer an das *Dateiziel* auf dem Remote Computer. Da das TFTP-Protokoll keine Benutzerauthentifizierung unterstützt, muss der Benutzer auf dem Remote Computer angemeldet sein, und die Dateien müssen auf dem Remote Computer beschreibbar sein.|
|get|Überträgt das *Dateiziel* auf dem Remote Computer an die Datei *Quelle* auf dem lokalen Computer.|
|\<Source\>|Gibt die zu übertragenden Datei an.|
|\<Destination\>|Gibt an, wohin die Datei übertragen werden soll.|

## <a name="remarks"></a>Hinweise
-   Der TFTP-Client kann mithilfe des Assistenten zum Hinzufügen von Features installiert werden.
-   Das TFTP-Protokoll unterstützt keinen Authentifizierungs-oder Verschlüsselungsmechanismus und kann daher ein Sicherheitsrisiko darstellen, wenn es vorhanden ist. Die Installation des TFTP-Clients wird für Systeme, die mit dem Internet verbunden sind, nicht empfohlen.
-   Der TFTP-Client ist optionale Software und wird unter Windows Vista und höheren Versionen des Windows-Betriebssystems als veraltet markiert. Ein TFTP-Server Dienst wird von Microsoft aus Sicherheitsgründen nicht mehr bereitgestellt.

## <a name="examples"></a>Beispiele
Kopieren Sie die Datei **Boot. img** vom Remote Computer **host1**.
```
tftp  -i Host1 get boot.img
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
