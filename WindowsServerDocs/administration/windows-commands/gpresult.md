---
title: gpresult
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfaa3adf-2c83-486c-86d6-23f93c5c883c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ef183547b0991489a9bb95dc0a7ea938ca1847e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724958"
---
# <a name="gpresult"></a>gpresult

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Richtlinien Ergebnissatz-Informationen (RSoP) für einen Remote Benutzer und-Computer an.
Um die RSoP-Berichterstellung für Remote Zielcomputer über die Firewall verwenden zu können, müssen Sie über Firewallregeln verfügen, die eingehenden Netzwerk Datenverkehr für die Ports zulassen.

## <a name="syntax"></a>Syntax

```
gpresult [/s <system> [/u <USERNAME> [/p [<PASSWOrd>]]]] [/user [<TARGETDOMAIN>\]<TARGETUSER>] [/scope {user | computer}] {/r | /v | /z | [/x | /h] <FILENAME> [/f] | /?}
```

### <a name="parameters"></a>Parameter

> [!NOTE]
> Mit Ausnahme der Verwendung von **/?** müssen Sie eine Ausgabe Option ( **/r**, **/v**, **"/z**, **/x**oder **/h**) einschließen.

|                Parameter                 |                                                                                                     BESCHREIBUNG                                                                                                      |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              /s \<-System\>               |                                                  Gibt den Namen oder die IP-Adresse eines Remote Computers an. Verwenden Sie keine umgekehrten Schrägstriche. Der Standardwert ist der lokale Computer.                                                   |
|             /u \<Benutzername\>              |                                Verwendet die Anmelde Informationen des angegebenen Benutzers, um den Befehl auszuführen. Der Standardbenutzer ist der Benutzer, der auf dem Computer angemeldet ist, der den Befehl ausgibt.                                 |
|            /p [\<Kennwort\>]             |            Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben wird. Wenn **/p** ausgelassen wird, fordert **gpresult** das Kennwort an. **/p** kann nicht mit **/x** oder **/h**verwendet werden.            |
| /User [\<targetDomain\>\\]\<targetUser\> |                                                                            Gibt den Remote Benutzer an, dessen RSOP-Daten angezeigt werden sollen.                                                                             |
|      /Scope {Benutzer &#124; Computer}       |                                Zeigt die RSoP-Daten für den Benutzer oder den Computer an. Wenn **/Scope** ausgelassen wird, zeigt **gpresult** RSOP-Daten sowohl für den Benutzer als auch für den Computer an.                                 |
|        [/x &#124;/h]<FILENAME>         | Speichert den Bericht im XML-Format (**/x**) oder im HTML-Format (**/h**) am Speicherort und mit dem Dateinamen, der durch den *filename* -Parameter angegeben wird. Kann nicht mit **/u**, **/p**, **/r**, **/v**oder **"/z**verwendet werden. |
|                    /f                    |                                                           erzwingt **gpresult** , den Dateinamen zu überschreiben, der in der **/x** -Option oder der **/h** -Option angegeben ist.                                                           |
|                    /r                    |                                                                                             Zeigt RSoP-Zusammenfassungs Daten an.                                                                                              |
|                    /v                    |                                                    Zeigt ausführliche Richtlinien Informationen an. Dies schließt detaillierte Einstellungen ein, die mit einer Rangfolge von 1 angewendet wurden.                                                    |
|                    /z                    |                                     Zeigt alle verfügbaren Informationen zu Gruppenrichtlinie an. Dies schließt detaillierte Einstellungen ein, die mit einer Rangfolge von 1 und höher angewendet wurden.                                      |
|                    /?                    |                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                         |

## <a name="remarks"></a>Bemerkungen
- Gruppenrichtlinie ist das primäre Verwaltungs Tool zum Definieren und Steuern, wie Programme, Netzwerkressourcen und das Betriebssystem für Benutzer und Computer in einer Organisation ausgeführt werden. In einer Active Directory-Umgebung wird Gruppenrichtlinie auf Benutzer oder Computer basierend auf der Mitgliedschaft in Standorten, Domänen oder Organisationseinheiten angewendet.
- Da Sie überlappende Richtlinien Einstellungen auf alle Computer oder Benutzer anwenden können, generiert das Gruppenrichtlinie Feature eine Reihe von Richtlinien Einstellungen, wenn sich der Benutzer anmeldet. **gpresult** zeigt den sich ergebenden Satz von Richtlinien Einstellungen an, die für den angegebenen Benutzer bei der Anmeldung des Benutzers auf dem Computer erzwungen wurden.
- Da **/v** und **"/z** viele Informationen liefern, ist es hilfreich, die Ausgabe in eine Textdatei umzuleiten (z. b. **gpresult/z >Policy. txt**).
- Der **gpresult** -Befehl ist in Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows 8, Windows 7 und Windows Vista verfügbar.
  ## <a name="examples"></a>Beispiele
  Zum Abrufen von RSoP-Daten für den Remote Benutzer **targetusername** des **srvmain**-Computers und Anzeigen von RSoP-Daten über den Benutzer. Der Befehl wird mit den Anmelde Informationen des Benutzers **maindom\hiropln**ausgeführt und <strong>p@ssW23</strong> als Kennwort für diesen Benutzer eingegeben.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /scope user /r
  ```
  
Speichert alle verfügbaren Informationen über Gruppenrichtlinie für den Remote Benutzer **targetusername** des **srvmain** -Computers in eine Datei mit dem Namen " **Policy. txt**". Der Computer enthält keine Daten. Der Befehl wird mit den Anmelde Informationen des Benutzers **maindom\hiropln**ausgeführt und <strong>p@ssW23</strong> als Kennwort für diesen Benutzer eingegeben.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /z > policy.txt
  ```
  
Zum Anzeigen von RSoP-Daten für den Computer **srvmain** und den angemeldeten Benutzer. Daten werden sowohl für den Benutzer als auch für den Computer eingeschlossen. Der Befehl wird mit den Anmelde Informationen des Benutzers **maindom\hiropln**ausgeführt und <strong>p@ssW23</strong> als Kennwort für diesen Benutzer eingegeben.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /r
  ```
  
## <a name="additional-references"></a>Zusätzliche Referenzen
- [TechCenter zu Gruppenrichtlinien](https://go.microsoft.com/fwlink/?LinkID=145531)

- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
