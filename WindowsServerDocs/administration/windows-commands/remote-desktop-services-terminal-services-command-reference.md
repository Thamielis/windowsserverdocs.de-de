---
title: 'Remotedesktopdienste (Terminaldienste): Befehlsreferenz'
description: Referenz Artikel für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2f371848-5c48-470c-908c-afbc95d3a805
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55466409517b63c52f88a7acec3a8f4aba7d258d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933471"
---
# <a name="remote-desktop-services-terminal-services-command-reference"></a>Remotedesktopdienste (Terminaldienste): Befehlsreferenz

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Im folgenden finden Sie eine Liste der Remotedesktopdienste Befehlszeilen Tools.
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
>
> |                 Befehl                 |                                                      Beschreibung                                                       |
> |-----------------------------------------|------------------------------------------------------------------------------------------------------------------------|
> |           [change](change.md)           | ändert Remotedesktop-Sitzungshost Servereinstellungen (RD-Sitzungs Host) für Anmeldungen, com-Port Zuordnungen und Installationsmodus. |
> |     [change logon](change-logon.md)     |    Aktiviert oder deaktiviert Anmeldungen von Client Sitzungen auf einem Remote Desktop-Sitzungs Host Server oder zeigt den aktuellen Anmeldestatus an.     |
> |      [change port](change-port.md)      |                   Listet die COM-Port Zuordnungen auf, die mit MS-DOS-Anwendungen kompatibel sind, oder ändert Sie.                    |
> |      [change user](change-user.md)      |                                ändert den Installationsmodus für den RD-Sitzungs Host Server.                                |
> |         [chglogon](chglogon.md)         |    Aktiviert oder deaktiviert Anmeldungen von Client Sitzungen auf einem Remote Desktop-Sitzungs Host Server oder zeigt den aktuellen Anmeldestatus an.     |
> |          [chgport](chgport.md)          |                   Listet die COM-Port Zuordnungen auf, die mit MS-DOS-Anwendungen kompatibel sind, oder ändert Sie.                    |
> |           [chgusr](chgusr.md)           |                                ändert den Installationsmodus für den RD-Sitzungs Host Server.                                |
> |         [flattemp](flattemp.md)         |                                      Aktiviert oder deaktiviert flattemporäre Ordner.                                       |
> |           [logoff](logoff.md)           |          Protokolliert einen Benutzer von einer Sitzung auf einem Remote Desktop-Sitzungs Host Server und löscht die Sitzung auf dem Server.          |
> |              [msg](msg.md)              |                                Sendet eine Nachricht an einen Benutzer auf einem Remote Desktop-Sitzungs Host Server.                                 |
> |            [mstsc](mstsc.md)            |                       erstellt Verbindungen mit Remote Desktop-Sitzungs Host Servern oder anderen Remote Computern.                        |
> |          [qappsrv](qappsrv.md)          |                             Zeigt eine Liste aller RD-Sitzungs Host Server im Netzwerk an.                             |
> |         [qprocess](qprocess.md)         |                  Zeigt Informationen zu Prozessen an, die auf einem Remote Desktop-Sitzungs Host Server ausgeführt werden.                   |
> |            [Frage](query.md)            |                      Zeigt Informationen zu Prozessen, Sitzungen und RD-Sitzungs Host Servern an.                      |
> |    [query process](query-process.md)    |                  Zeigt Informationen zu Prozessen an, die auf einem Remote Desktop-Sitzungs Host Server ausgeführt werden.                   |
> |    [query session](query-session.md)    |                           Zeigt Informationen zu Sitzungen auf einem Remote Desktop-Sitzungs Host Server an.                            |
> | [query termserver](query-termserver.md) |                             Zeigt eine Liste aller RD-Sitzungs Host Server im Netzwerk an.                             |
> |       [query user](query-user.md)       |                         Zeigt Informationen zu Benutzersitzungen auf einem Remote Desktop-Sitzungs Host Server an.                         |
> |            [quser](quser.md)            |                         Zeigt Informationen zu Benutzersitzungen auf einem Remote Desktop-Sitzungs Host Server an.                         |
> |          [qwinsta](qwinsta.md)          |                           Zeigt Informationen zu Sitzungen auf einem Remote Desktop-Sitzungs Host Server an.                            |
> |          [rdpsign](rdpsign.md)          |                          Ermöglicht das digitale Signieren einer Remotedesktopprotokoll Datei (. RDP).                          |
> |    [reset session](reset-session.md)    |                         Ermöglicht es Ihnen, eine Sitzung auf einem Remote Desktop-Sitzungs Host Server zurückzusetzen (zu löschen).                          |
> |          [rwinsta](rwinsta.md)          |                         Ermöglicht es Ihnen, eine Sitzung auf einem Remote Desktop-Sitzungs Host Server zurückzusetzen (zu löschen).                          |
> |           [shadow](shadow.md)           |            Ermöglicht die Remote Steuerung einer aktiven Sitzung eines anderen Benutzers auf einem Remote Desktop-Sitzungs Host Server.             |
> |            [tscon](tscon.md)            |                               Stellt eine Verbindung mit einer anderen Sitzung auf einem RD-Sitzungs Host Server her.                                |
> |         [tsdiscon](tsdiscon.md)         |                                 Trennt eine Sitzung von einem Remote Desktop-Sitzungs Host Server.                                  |
> |           [tskill](tskill.md)           |                           Beendet einen Prozess, der in einer Sitzung auf einem Remote Desktop-Sitzungs Host Server ausgeführt wird.                            |
> |           [tsprof](tsprof.md)           |              Kopiert die Remotedesktopdienste Benutzer Konfigurationsinformationen von einem Benutzer in einen anderen.               |
