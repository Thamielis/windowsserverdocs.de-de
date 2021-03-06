---
title: ksetup addhosttorealmmap
description: Referenz Artikel für den Befehl "Ksetup addhosttorealmmap", mit dem eine SPN-Zuordnung (Service Principal Name) zwischen dem angegebenen Host und dem Bereich hinzugefügt wird.
ms.topic: reference
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 16ffe4431167ef63c73d4889febed49c40344e8b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639759"
---
# <a name="ksetup-addhosttorealmmap"></a>ksetup addhosttorealmmap

Fügt eine Zuordnung des Dienst Prinzipal namens (SPN) zwischen dem angegebenen Host und dem Bereich hinzu. Mit diesem Befehl können Sie auch einen Host oder mehrere Hosts, die das gleiche DNS-Suffix gemeinsam nutzen, dem Bereich zuordnen.

Die Zuordnung wird in der Registrierung unter **HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**gespeichert.

## <a name="syntax"></a>Syntax

```
ksetup /addhosttorealmmap <hostname> <realmname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- |------------ |
| `<hostname>` | Der Hostname ist der Computername, und er kann als voll qualifizierter Domänen Name des Computers angegeben werden. |
| `<realmname>` | Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Host Computer *IPops897* *dem Bereich "* Configuration Manager" zuzuordnen:

```
ksetup /addhosttorealmmap IPops897 CONTOSO
```

Überprüfen Sie die Registrierung, um sicherzustellen, dass die Zuordnung wie beabsichtigt erfolgt ist.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Befehl "Delta Host-Map"](ksetup-delhosttorealmmap.md)
