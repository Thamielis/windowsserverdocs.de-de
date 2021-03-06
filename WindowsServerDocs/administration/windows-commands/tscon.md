---
title: tscon
description: Referenz Artikel zu tscon, der eine Verbindung mit einer anderen Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host) herstellt.
ms.topic: reference
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2ba6df3a8878c42ac8ce8ac88671bb645bfedf86
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624601"
---
# <a name="tscon"></a>tscon

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit einer anderen Sitzung auf einem Remotedesktop-Sitzungshost Server her.



> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](/previous-versions/orphan-topics/ws.11/hh831527(v=ws.11)) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]
```
### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------|--------|
|\<SessionID>|Gibt die ID der Sitzung an, mit der Sie eine Verbindung herstellen möchten. Wenn Sie den optionalen Parameter **/dest:** < *Sessionname*> verwenden, ist dies die ID der Sitzung, mit der Sie eine Verbindung herstellen möchten.|
|\<SessionName>|Gibt den Namen der Sitzung an, mit der Sie eine Verbindung herstellen möchten.|
|/dest\<SessionName>|Gibt den Namen der aktuellen Sitzung an. Diese Sitzung wird getrennt, wenn Sie eine Verbindung mit der neuen Sitzung herstellen.|
|/Password\<pw>|Gibt das Kennwort des Benutzers an, der die Sitzung besitzt, mit der Sie eine Verbindung herstellen möchten. Dieses Kennwort ist erforderlich, wenn der Benutzer, der die Verbindung herstellt, die Sitzung nicht besitzt.|
|/Password: *|fordert das Kennwort des Benutzers an, der die Sitzung besitzt, mit der Sie eine Verbindung herstellen möchten.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Zum Herstellen einer Verbindung mit einer anderen Sitzung müssen Sie über die Berechtigung "Vollzugriff" verfügen oder eine spezielle Zugriffsberechtigung herstellen.
-   Mit dem Parameter " **/dest:** < *Sessionname*>" können Sie die Sitzung eines anderen Benutzers mit einer anderen Sitzung verbinden.
-   Wenn Sie im <*Password*>-Parameter kein Kennwort angeben und die Ziel Sitzung zu einem anderen Benutzer als dem aktuellen gehört, schlägt **tscon** fehl.
-   Sie können keine Verbindung mit der Konsolen Sitzung herstellen.

## <a name="examples"></a>Beispiele
- Geben Sie Folgendes ein, um eine Verbindung mit Sitzung 12 auf dem aktuellen RD-Sitzungs Host Server herzustellen und die aktuelle Sitzung zu trennen:
  ```
  tscon 12
  ```
- Geben Sie Folgendes ein, um eine Verbindung mit der Sitzung 23 auf dem aktuellen Remote Desktop-Sitzungs Host Server herzustellen, indem Sie das Kennwort mypass verwenden und die aktuelle Sitzung trennen:
  ```
  tscon 23 /password:mypass
  ```
- Wenn Sie die Sitzung mit dem Namen TERM03 mit der Sitzung namens TERM05 verbinden und dann Session TERM05 trennen möchten, geben Sie Folgendes ein, wenn eine Verbindung besteht:
  ```
  tscon TERM03 /v /dest:TERM05
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
   [Befehlsreferenz für Remotedesktopdienste (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
