---
title: macfile
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2ce586c-b316-41d3-90f8-4be0d074cc0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf914e4e7da4f00c547353da4fc8d04ad6828646
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820520"
---
# <a name="macfile"></a>macfile

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwaltet den Datei Server für Macintosh-Server, Volumes, Verzeichnisse und Dateien. Sie können administrative Aufgaben automatisieren, indem Sie eine Reihe von Befehlen in Batch Dateien einschließen und manuell oder zu vordefinierten Zeiten starten.
-   [So ändern Sie Verzeichnisse in auf Macintosh zugänglichen Volumes](#BKMK_Moddirs)
-   [So verknüpfen Sie die Daten und Ressourcen Verzweigungen einer Macintosh-Datei](#BKMK_Joinforks)
-   [So ändern Sie die Anmelde Nachricht und schränken Sitzungen ein](#BKMK_LogonLimit)
-   [So können Sie Macintosh-barrierefreie Volumes hinzufügen, ändern oder entfernen](#BKMK_addvol)

## <a name="to-modify-directories-in-macintosh-accessible-volumes"></a><a name=BKMK_Moddirs></a>So ändern Sie Verzeichnisse in auf Macintosh zugänglichen Volumes

### <a name="syntax"></a>Syntax
```
macfile directory[/server:\\<computerName>] /path:<directory> [/owner:<OwnerName>] [/group:<GroupName>] [/permissions:<Permissions>]
```

#### <a name="parameters"></a>Parameter
-   /Server: \\ \\ <computerName> gibt den Server an, auf dem ein Verzeichnis geändert werden soll. Wenn der Vorgang nicht weggelassen wird, wird der Vorgang auf dem lokalen Computer ausgeführt.
-   /Path: <directory> erforderlich. Gibt den Pfad zu dem Verzeichnis an, das Sie ändern möchten. Das Verzeichnis muss vorhanden sein. im **MacFile-Verzeichnis** werden keine Verzeichnisse erstellt.
-   /Owner: <OwnerName> ändert den Besitzer des Verzeichnisses. Wenn die Angabe ausgelassen wird, bleibt der Besitzer unverändert.
-   /Group: <GroupName> gibt die primäre Macintosh-Gruppe an, die dem Verzeichnis zugeordnet ist, oder ändert Sie. Wenn diese Angabe ausgelassen wird, bleibt die primäre Gruppe unverändert.
-   /Permissions: <Permissions> legt Berechtigungen für das Verzeichnis für den Besitzer, die primäre Gruppe und die Welt (alle) fest. Zum Festlegen von Berechtigungen wird eine elf stellige Zahl verwendet. Die Zahl 1 erteilt die Berechtigung und die Berechtigung "0 widerruft" (z. b. 11111011000). Wenn die Angabe weggelassen wird, bleiben die Berechtigungen unverändert.
    Die Position der Ziffer bestimmt, welche Berechtigung festgelegt wird, wie in der folgenden Tabelle beschrieben.

    |Position|Legt die Berechtigung für|
    |------|------------|
    |First (Erster)|Besitzer Dateien|
    |Sekunde|Besitzer Ordner|
    |Dritter|Besitzmakechanges|
    |Vierter|GroupSeeFiles|
    |5.|Groupseedner|
    |6.|GroupMakeChanges|
    |Siebten|Worldseefiles|
    |Platz|Worldseedner|
    |När|WorldMakeChanges|
    |Zehnten|Das Verzeichnis kann nicht umbenannt, verschoben oder gelöscht werden.|
    |Stündigen|Die Änderungen gelten für das aktuelle Verzeichnis und alle Unterverzeichnisse.|

-   /?
    Zeigt die Hilfe an der Eingabeaufforderung an.

### <a name="remarks"></a>Hinweise
- Wenn die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z. b. * * * *<em>Computer Name</em>* * * *).
- Verwenden Sie **macfiledirectory** , um ein vorhandenes Verzeichnis auf einem auf Macintosh zugänglichen Volume für Macintosh-Benutzer verfügbar zu machen. Mit dem Befehl " **macfiledirectory** " werden keine Verzeichnisse erstellt. Erstellen Sie mit dem Datei-Manager, der Eingabeaufforderung oder dem **Macintosh New Folder** -Befehl ein Verzeichnis auf einem auf Macintosh zugänglichen Volume, bevor Sie den Befehl " **Macfile Directory** " verwenden.
  ### <a name="examples"></a>Beispiele
  Um die Berechtigungen des Unterverzeichnisses für den Vertrieb in der über Macintosh zugänglichen Volumen Statistik auf dem E-Laufwerk des lokalen Servers zu ändern. Im Beispiel werden die Dateien Siehe Dateien, Ordner und Änderungs Berechtigungen für den Besitzer zugewiesen, und es werden Dateien angezeigt und Ordner Berechtigungen für alle anderen Benutzer angezeigt. gleichzeitig wird verhindert, dass das Verzeichnis umbenannt, verschoben oder gelöscht wird.
  ```
  macfile directory /path:e:\statistics\may sales /permissions:11111011000
  ```

## <a name="to-join-a-macintosh-files-data-and-resource-forks"></a><a name=BKMK_Joinforks></a>So verknüpfen Sie die Daten und Ressourcen Verzweigungen einer Macintosh-Datei

### <a name="syntax"></a>Syntax
```
macfile forkize[/server:\\<computerName>] [/creator:<CreatorName>] [/type:<typeName>]  [/datafork:<Filepath>] [/resourcefork:<Filepath>] /targetfile:<Filepath>
```

#### <a name="parameters"></a>Parameter

|         Parameter          |                                                                                                           BESCHREIBUNG                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Server\\\\<computerName> |                                                            Gibt den Server an, auf dem Dateien verknüpft werden sollen. Wenn der Vorgang nicht weggelassen wird, wird der Vorgang auf dem lokalen Computer ausgeführt.                                                            |
|   Hersteller<CreatorName>   |                                      Gibt den Ersteller der Datei an. Der Macintosh-Finder verwendet die Befehlszeilenoption **/Creator** , um die Anwendung zu ermitteln, die die Datei erstellt hat.                                       |
|      /Type<typeName>      |                                 Gibt den Dateityp an. Der Macintosh-Finder verwendet die Befehlszeilenoption **/Type** , um den Dateityp innerhalb der Anwendung zu ermitteln, von der die Datei erstellt wurde.                                 |
|    /datafork:<Filepath>    |                                                                   Gibt den Speicherort der Daten Verzweigung an, die verknüpft werden soll. Sie können einen Remote Pfad angeben.                                                                   |
|  /resourcefork:<Filepath>  |                                                                 Gibt den Speicherort der Ressourcenverzweigung an, der verknüpft werden soll. Sie können einen Remote Pfad angeben.                                                                 |
|   targetfile<Filepath>   | Erforderlich. Gibt den Speicherort der Datei an, die durch den Beitritt zu einer Daten Verzweigung und einer Ressourcen Verzweigung erstellt wird, oder gibt den Speicherort der Datei an, deren Typ oder Ersteller Sie ändern. Die Datei muss sich auf dem angegebenen Server befinden. |
|             /?             |                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                               |

### <a name="remarks"></a>Hinweise
- Wenn die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z. b. * * * *<em>Computer Name</em>* * * *).

### <a name="examples"></a>Beispiele
Zum Erstellen der Datei treeapp auf dem Macintosh-zugänglichen Volume d:\Release mithilfe der Ressourcen Verzweigung c:\cross\mac\appcode, und um diese neue Datei für Macintosh-Clients als Anwendung anzuzeigen (Macintosh-Anwendungen verwenden den Typ APPL), wobei der Ersteller (Signatur) auf Magnolia festgelegt ist, geben Sie Folgendes ein:
```
macfile forkize /resourcefork:c:\cross\mac\appcode /type:APPL /creator:MAGNOLIA /targetfile:D:\Release\treeapp
```
Um den Datei Ersteller in Microsoft Word 5,1 zu ändern, geben Sie für die Datei "Word. txt" im Verzeichnis "d:\Word documents\group Files" auf dem Server " \\ \servera" Folgendes ein:
```
macfile forkize /server:\\servera /creator:MSWD /type:TEXT /targetfile:d:\Word documents\Group files\Word.txt
```

## <a name="to-change-the-logon-message-and-limit-sessions"></a><a name=BKMK_LogonLimit></a>So ändern Sie die Anmelde Nachricht und schränken Sitzungen ein
### <a name="syntax"></a>Syntax
```
macfile server [/server:\\<computerName>] [/maxsessions:{Number | unlimited}] [/loginmessage:<Message>]
```

#### <a name="parameters"></a>Parameter

|               Parameter                |                                                                                                                                                                           BESCHREIBUNG                                                                                                                                                                            |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /Server\\\\<computerName>       |                                                                                                                        Gibt den Server an, auf dem die Parameter geändert werden sollen. Wenn der Vorgang nicht weggelassen wird, wird der Vorgang auf dem lokalen Computer ausgeführt.                                                                                                                         |
| /MaxSessions: {Number &#124; Unlimited} |                                                                                         Gibt die maximale Anzahl von Benutzern an, die gleichzeitig Datei-und Druckserver für Macintosh verwenden können. Wenn der Wert nicht angegeben wird, bleibt die **MaxSessions** -Einstellung für den Server unverändert.                                                                                         |
|        /loginmessage:<Message>         | ändert die Nachricht, die Macintosh-Benutzer bei der Anmeldung beim Datei Server für Macintosh-Server sehen. Die maximale Anzahl von Zeichen für die Anmelde Nachricht beträgt 199. Wenn der Wert nicht ausgelassen wird, bleibt die **loginmessage** -Nachricht für den Server unverändert. Wenn Sie eine vorhandene Anmelde Nachricht entfernen möchten, schließen Sie den **/loginmessage** -Parameter ein, lassen Sie die *Nachrichten* Variable jedoch leer. |
|                   /?                   |                                                                                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                               |

### <a name="remarks"></a>Hinweise
- Wenn die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z. b. * * * *<em>Computer Name</em>* * * *).

### <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um die Anzahl von Datei-und Druckservern für Macintosh-Sitzungen, die auf dem lokalen Server zulässig sind, von der aktuellen Einstellung auf fünf Sitzungen zu ändern und das Anmelde Nachrichtenprotokoll von Server für Macintosh zu ändern, wenn Sie fertig sind. Geben Sie Folgendes ein:
```
macfile server /maxsessions:5 /loginmessage:Log off from Server for Macintosh when you are finished.
```

## <a name="to-add-change-or-remove-macintosh-accessible-volumes"></a><a name=BKMK_addvol></a>So können Sie Macintosh-barrierefreie Volumes hinzufügen, ändern oder entfernen
### <a name="syntax"></a>Syntax
```
macfile volume {/add|/set} [/server:\\<computerName>] /name:<volumeName>/path:<directory>[/readonly:{true | false}] [/guestsallowed:{true | false}] [/password:<Password>] [/maxusers:{<Number>>|unlimited}]
macfile volume /remove[/server:\\<computerName>] /name:<volumeName>
```

#### <a name="parameters"></a>Parameter

|              Parameter               |                                                                                                                                                                       BESCHREIBUNG                                                                                                                                                                        |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          {/Add &#124;/Set}          |                                                                                                                      Erforderlich, wenn Sie ein auf Macintosh zugängliches Volume hinzufügen oder ändern. Fügt das angegebene Volume hinzu oder ändert es.                                                                                                                       |
|      /Server\\\\<computerName>      |                                                                                                             Gibt den Server an, auf dem ein Volume hinzugefügt, geändert oder entfernt werden soll. Wenn der Vorgang nicht weggelassen wird, wird der Vorgang auf dem lokalen Computer ausgeführt.                                                                                                              |
|          /Name<volumeName>          |                                                                                                                                          Erforderlich. Gibt den Volumenamen an, der hinzugefügt, geändert oder entfernt werden soll.                                                                                                                                           |
|          /Path<directory>           |                                                                                                                Erforderlich und gültig nur, wenn Sie ein Volume hinzufügen. Gibt den Pfad zum Stammverzeichnis des hinzu zufügenden Volumes an.                                                                                                                 |
|    /ReadOnly: {true &#124; false}     | Gibt an, ob Benutzer Dateien im Volume ändern können. Geben Sie true ein, um anzugeben, dass Benutzer die Dateien im Volume nicht ändern können. Geben Sie false ein, um anzugeben, dass Benutzer Dateien im Volume ändern können. Wenn beim Hinzufügen eines Volumes weggelassen wird, sind Änderungen an Dateien zulässig. Wenn beim Ändern eines Volumes ausgelassen wird, bleibt die Schreib **geschützte Einstellung für** das Volume unverändert. |
|  /guestsallowed: {true &#124; false}  |      Gibt an, ob Benutzer, die sich als Gäste anmelden, das Volume verwenden können. Geben Sie true ein, um anzugeben, dass Gäste das Volume verwenden können. Geben Sie false ein, um anzugeben, dass Gäste das Volume nicht verwenden können. Wenn Sie beim Hinzufügen eines Volumes ausgelassen werden, können Gäste das Volume verwenden. Wenn beim Ändern eines Volumes ausgelassen wird, bleibt die Einstellung **GUESTSALLOWED** für das Volume unverändert.       |
|         /Password<Password>         |                                                                               Gibt ein Kennwort an, das für den Zugriff auf das Volume erforderlich ist. Wenn beim Hinzufügen eines Volumes kein Kennwort angegeben wird, wird kein Kennwort erstellt. Wenn beim Ändern eines Volumes kein Kennwort angegeben wird, bleibt das Kennwort unverändert.                                                                               |
| /maxUsers: { <Number>>&#124;unbegrenzt} |                                                 Gibt die maximale Anzahl von Benutzern an, die die Dateien auf dem Volume gleichzeitig verwenden können. Wenn der Wert beim Hinzufügen eines Volumes weggelassen wird, kann das Volume von einer unbegrenzten Anzahl von Benutzern verwendet werden. Wenn beim Ändern eines Volumes ausgelassen wird, bleibt der Wert **maxUsers** unverändert.                                                 |
|               /remove                |                                                                                                                                Erforderlich, wenn Sie ein Macintosh-accesible-Volume entfernen. entfernt das angegebene Volume.                                                                                                                                |
|                  /?                  |                                                                                                                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                           |

### <a name="remarks"></a>Hinweise
- Wenn die Informationen, die Sie angeben, Leerzeichen oder Sonderzeichen enthalten, verwenden Sie Anführungszeichen um den Text (z. b. * * * *<em>Computer Name</em>* * * *).

### <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um ein Volume mit der Bezeichnung "US-Marketing Statistik" auf dem lokalen Server zu erstellen, indem Sie das Verzeichnis "Stats" im Laufwerk E verwenden und angeben, dass der Zugriff auf das Volume nicht von Gästen
```
macfile volume /add /name:US Marketing Statistics /guestsallowed:false /path:e:\Stats
```
Geben Sie Folgendes ein, um das oben erstellte Volume so zu ändern, dass es schreibgeschützt ist und ein Kennwort erforderlich ist. Geben Sie zum Festlegen der maximalen Anzahl von Benutzern auf fünf Folgendes ein:
```
macfile volume /set /name:US Marketing Statistics /readonly:true /password:saturn /maxusers:5
```
Geben Sie Folgendes ein, um ein Volume Namens Landscape Design auf dem Server \\ \magnolia zu verwenden, indem Sie das Verzeichnis Trees im Laufwerk E verwenden und angeben, dass auf das Volume von Gästen zugegriffen werden kann:
```
macfile volume /add /server:\\Magnolia /name:Landscape Design /path:e:\trees
```
Geben Sie Folgendes ein, um das Volume namens Sales Reports auf dem lokalen Server zu entfernen:
```
macfile volume /remove /name:Sales Reports
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
