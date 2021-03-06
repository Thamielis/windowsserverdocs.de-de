---
title: pubprn
description: Referenz Artikel für den Pubprn-Befehl, mit dem ein Drucker im Active Directory Domain Services veröffentlicht wird.
ms.topic: reference
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 36366e91f390ee8afb4884e31951cd5efde9251a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640610"
---
# <a name="pubprn"></a>pubprn

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Veröffentlicht einen Drucker auf dem Active Directory Domain Services. Dieser Befehl ist ein Visual Basic Skript, das sich im `%WINdir%\System32\printing_Admin_Scripts\<language>` Verzeichnis befindet. Wenn Sie diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben Sie **cscript** gefolgt vom vollständigen Pfad der Pubprn-Datei ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn`.

## <a name="syntax"></a>Syntax

```
cscript pubprn {<servername> | <UNCprinterpath>} LDAP://CN=<container>,DC=<container>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<servername>` | Gibt den Namen des Windows-Servers an, der den zu veröffentlichenden Drucker hostet. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet. |
| `<UNCprinterpath>` | Der UNC-Pfad (Universal Naming Convention) zu dem freigegebenen Drucker, den Sie veröffentlichen möchten. |
| `LDAP://CN=<Container>,DC=<Container>` | Gibt den Pfad zum Container in Active Directory Domain Services an, in dem Sie den Drucker veröffentlichen möchten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Computer Name").

### <a name="examples"></a>Beispiele

Wenn Sie alle Drucker auf dem \\ Server1-Computer im Container MyContainer in der mydomain.Company.com-Domäne veröffentlichen möchten, geben Sie Folgendes ein:

```
cscript pubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

Zum Veröffentlichen des Laserprinter1-Druckers auf dem \\ Server "\server1" im Container "MyContainer" in der Domäne "mydomain.Company.com" geben Sie Folgendes ein:

```
cscript pubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
