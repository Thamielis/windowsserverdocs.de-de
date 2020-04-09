---
title: mstsc
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 59801227-1e7e-4dbd-96e6-f54102a3ce92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5accd56ea622b85966bf0cb95750d8bb2d97e42
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839073"
---
# <a name="mstsc"></a>mstsc

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

von werden Verbindungen mit Remotedesktop-Sitzungshost-Servern (RD-Sitzungs Host) oder anderen Remote Computern hergestellt, eine vorhandene Remotedesktopverbindung (RDP-Konfigurationsdatei) bearbeitet und ältere Verbindungs Dateien, die mit dem Clientverbindungs-Manager erstellt wurden, in neue RDP-Verbindungs Dateien migriert.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
mstsc.exe [<Connection File>] [/v:<Server>[:<Port>]] [/admin] [/f] [/w:<Width> /h:<Height>] [/public] [/span]
mstsc.exe /edit <Connection File>
mstsc.exe /migrate
```

### <a name="parameters"></a>Parameter

|        Parameter        |                                                         Beschreibung                                                         |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------|
|    <Connection File>    |                                   Gibt den Namen einer RDP-Datei für die Verbindung an.                                    |
|  /v: < Server\>[: < Port\>] |                Gibt den Remote Computer und optional die Portnummer an, mit der Sie eine Verbindung herstellen möchten.                 |
|         /admin          |                                   Stellt eine Verbindung mit einer-Sitzung zur Verwaltung des-Servers her.                                   |
|           /f            |                                    startet Remotedesktopverbindung im Vollbildmodus.                                    |
|       /w:<Width>        |                                      Gibt die Breite des Remotedesktop Fensters an.                                      |
|       /h:<Height>       |                                     Gibt die Höhe des Remotedesktop Fensters an.                                      |
|         /Public         |                  Führt Remotedesktop im öffentlichen Modus aus. Im öffentlichen Modus werden Kenn Wörter und Bitmaps nicht zwischengespeichert.                  |
|          /Span          | Entspricht der Remotedesktop Breite und-Höhe mit dem lokalen virtuellen Desktop, bei Bedarf über mehrere Monitore hinweg. |
| /Edit <Connection File> |                                         Öffnet die angegebene RDP-Datei zum Bearbeiten.                                          |
|        /migrate         |       Migriert Legacy-Verbindungs Dateien, die mit dem Clientverbindungs-Manager erstellt wurden, in neue RDP-Verbindungs Dateien.       |
|           /?            |                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                             |

## <a name="remarks"></a>Hinweise
-   "Default. RDP" wird für jeden Benutzer als versteckte Datei im Ordner "Dokumente" des Benutzers gespeichert. Vom Benutzer erstellte RDP-Dateien werden standardmäßig im Ordner "Dokumente" des Benutzers gespeichert, können aber an einem beliebigen Speicherort gespeichert werden.
-   Für Monitore muss die gleiche Auflösung verwendet werden, und Sie müssen horizontal ausgerichtet werden (d. h. nebeneinander). Es ist derzeit nicht unterstützt, mehrere Monitore vertikal auf dem Client System zu überspannen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
-   Zum Herstellen einer Verbindung mit einer Sitzung im Vollbildmodus geben Sie Folgendes ein:
    ```
    mstsc /f
    ```
-   Um eine Datei namens filename. RDP zum Bearbeiten zu öffnen, geben Sie Folgendes ein:
    ```
    mstsc /edit filename.rdp
    ```

## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
