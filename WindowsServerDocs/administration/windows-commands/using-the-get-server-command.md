---
title: Get-Server
description: Referenz Artikel zu Get-Server, der Informationen vom angegebenen Windows-Bereitstellungsdiensteserver abruft.
ms.topic: reference
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fe55e707dda58e65d2b86fe553910d010f8b2586
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628506"
---
# <a name="get-server"></a>Get-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen vom angegebenen Windows-Bereitstellungsdiensteserver ab.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {config &#124; Images &#124; alle}|Gibt den Typ der zurück zugebende Informationen an.<p>-   **Config** gibt Konfigurationsinformationen zurück.<br />-   **Images** gibt Informationen zu Bildgruppen, Start Abbildern und Installations Abbildern zurück.<br />-   **Alle** gibt Konfigurationsinformationen und Bild Informationen zurück.|
|/Detailed|Sie können diese Option mit **/Show: Images** oder **/Show: all** verwenden, um anzugeben, dass alle Bild Metadaten aus jedem Bild zurückgegeben werden sollen. Wenn die **/detailed** -Option nicht verwendet wird, besteht das Standardverhalten darin, den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zum Server anzuzeigen:
```
wdsutil /Get-Server /Show:Config
```
Geben Sie Folgendes ein, um ausführliche Informationen zum Server anzuzeigen:
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-server-command.md) 
 "deaktivierte Server" [Verwenden des Befehls](using-the-enable-server-command.md) 
 "Enable-Server" [Verwenden des Befehls](using-the-initialize-server-command.md) 
 "Initialize-Server" [Unterbefehl: Set-Server](subcommand-set-server.md) 
 [Unterbefehl: Start-Server](subcommand-start-server.md) 
 [Unterbefehl: "Ende-Server](subcommand-stop-server.md) 
 " [Die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
