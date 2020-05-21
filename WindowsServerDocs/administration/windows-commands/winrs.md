---
title: winrs
description: Referenz Thema für Winrs, mit dem Sie Programme remote verwalten und ausführen können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c370de31-5651-400a-872d-ef229aae2309
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1361cded9ebf26eeaea7abcaba1b1f3ca1428ac
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436795"
---
# <a name="winrs"></a>winrs

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe der Windows-Remote Verwaltung können Sie Programme remote verwalten und ausführen.
## <a name="syntax"></a>Syntax
```
winrs [/<parameter>[:<value>]] <command>
```
#### <a name="parameters"></a>Parameter

|           Parameter            |                                                                                                                                                                                    Beschreibung                                                                                                                                                                                     |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /Remote: \< Endpunkt>       |                                                                                          Gibt den Ziel Endpunkt mithilfe eines NetBIOS-Namens oder der Standardverbindung an:<p>-   <url>: [ \< Transport>://] \< Ziel> [: \< Port>]<p>Wenn nicht angegeben, wird **/r: localhost** verwendet.                                                                                          |
|          /unencrypted          | Gibt an, dass die Nachrichten an die Remoteshell nicht verschlüsselt werden. Dies ist nützlich für die Problembehandlung oder den Fall, dass der Netzwerk Datenverkehr bereits mit **IPSec**verschlüsselt ist oder wenn die physische Sicherheit erzwungen wird.<p>Standardmäßig werden die Nachrichten mithilfe von Kerberos-oder NTLM-Schlüsseln verschlüsselt.<p>Diese Befehlszeilenoption wird ignoriert, wenn HTTPS-Transport ausgewählt wird. |
|     /Username: \< username->      |                                                                                Gibt den Benutzernamen in der Befehlszeile an.<p>Wenn nichts angegeben wird, verwendet das Tool die Aushandlungs Authentifizierung oder die Eingabeaufforderung für den Namen.<p>Wenn **/username** angegeben wird, muss auch **/Password** angegeben werden.                                                                                 |
|     /Password: \< Kennwort>      |                                                                           Gibt das Kennwort in der Befehlszeile an.<p>Wenn **/Password** nicht angegeben ist, aber **/username** ist, fordert das Tool zur Eingabe des Kennworts auf.<p>Wenn **/Password** angegeben wird, muss auch **/username** angegeben werden.                                                                            |
|      /Timeout: \< Sekunden>       |                                                                                                                                                                             Diese Option ist veraltet.                                                                                                                                                                             |
|       /Directory: \< Pfad>       |                                                                                            Gibt das Start Verzeichnis für die Remoteshell an.<p>Wenn keine Angabe erfolgt, wird die Remoteshell im Basisverzeichnis des Benutzers gestartet, das durch die Umgebungsvariable " **% User Profile%**" definiert wird.                                                                                             |
| /Environment: \< String>=<value> |                                                                          Gibt eine einzelne Umgebungsvariable an, die beim Start der Shell festgelegt werden soll, sodass die Standardumgebung für die Shell geändert werden kann.<p>Mehrere Vorkommen dieses Schalters müssen verwendet werden, um mehrere Umgebungsvariablen anzugeben.                                                                          |
|            /noecho             |                                                                                                    Gibt an, dass ECHO deaktiviert werden soll. Dies kann erforderlich sein, um sicherzustellen, dass die Antworten von Benutzern auf Remote Aufforderungen nicht lokal angezeigt werden.<p>Standardmäßig ist Echo on.                                                                                                    |
|           /noprofile           |                                              Gibt an, dass das Profil des Benutzers nicht geladen werden soll.<p>Standardmäßig versucht der Server, das Benutzerprofil zu laden.<p>Wenn der Remote Benutzer kein lokaler Administrator auf dem Zielsystem ist, ist diese Option erforderlich (der Standardwert führt zu einem Fehler).                                               |
|         /allowdelegate         |                                                                                                                  Gibt an, dass die Anmelde Informationen des Benutzers für den Zugriff auf eine Remote Freigabe verwendet werden können, z. b. auf einem anderen Computer als dem Ziel Endpunkt.                                                                                                                   |
|          /Compression          |                                                                           Aktivieren Sie die Komprimierung.  Ältere Installationen auf Remote Computern unterstützen möglicherweise keine Komprimierung, sodass Sie standardmäßig deaktiviert ist.<p>Die Standardeinstellung ist off, da ältere Installationen auf Remote Computern die Komprimierung möglicherweise nicht unterstützen.                                                                           |
|            /usessl             |                                                                                                               Verwenden Sie eine SSL-Verbindung, wenn Sie einen Remote Endpunkt verwenden.  Diese Angabe anstelle des Transport- **https:** verwendet den standardmäßigen **WinRM** -Standardport.                                                                                                                |
|               /?               |                                                                                                                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                        |

## <a name="remarks"></a>Hinweise
-   Alle Befehlszeilenoptionen akzeptieren entweder eine Kurzform oder eine lange Form. Beispielsweise sind sowohl **/r** als auch **/Remote** gültig.
-   Um den **/Remote** -Befehl zu beenden, kann der Benutzer **STRG + C** oder STRG + **Pause**eingeben, das an die Remoteshell gesendet wird. Die zweite **STRG-C-Taste erzwingt** die Beendigung von " **Winrs. exe**".
-   Verwenden Sie das WinRM-Tool, um aktive Remoteshells oder Winrs-Konfigurationen zu verwalten.  Der URI-Alias zum Verwalten aktiver Shells ist **Shell/cmd**.  Der URI-Alias für die Winrs **-Konfiguration ist WinRM/config/Winrs**.

## <a name="examples"></a>Beispiele
```
winrs /r:https://contoso.com command
```
```
winrs /r:contoso.com /usessl command
```
```
winrs /r:myserver command
```
```
winrs /r:http://127.0.0.1 command
```
```
winrs /r:http://169.51.2.101:80 /unencrypted command
```
```
winrs /r:https://[::FFFF:129.144.52.38] command
```
```
winrs /r:http://[1080:0:0:0:8:800:200C:417A]:80 command
```
```
winrs /r:https://contoso.com /t:600 /u:administrator /p:$%fgh7 ipconfig
```
```
winrs /r:myserver /env:path=^%path^%;c:\tools /env:TEMP=d:\temp config.cmd
```
```
winrs /r:myserver netdom join myserver /domain:testdomain /userd:johns /passwordd:$%fgh789
```
```
winrs /r:myserver /ad /u:administrator /p:$%fgh7 dir \\anotherserver\share
```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

