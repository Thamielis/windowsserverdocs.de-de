---
title: ksetup setcomputerpassword
description: Referenz Artikel für den Ksetup-Befehl setcomputerpassword, mit dem das Kennwort für den lokalen Computer festgelegt wird.
ms.topic: reference
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9bd9d9fafae57c1c7804f7a214d9729cdb232b2d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627429"
---
# <a name="ksetup-setcomputerpassword"></a>ksetup setcomputerpassword

Legt das Kennwort für den lokalen Computer fest. Dieser Befehl wirkt sich nur auf das Computer Konto aus und erfordert einen Neustart, damit die Kenn Wort Änderung wirksam wird.

> [!IMPORTANT]
> Das Computer Konto Kennwort wird nicht in der Registrierung oder als Ausgabe des **Ksetup** -Befehls angezeigt.

## <a name="syntax"></a>Syntax

```
ksetup /setcomputerpassword <password>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<password>` | Gibt das angegebene Kennwort an, mit dem das Computer Konto auf dem lokalen Computer festgelegt wird. Das Kennwort kann nur mit einem Konto mit Administrator Berechtigungen festgelegt werden, und das Kennwort muss zwischen 1 und 156 alphanumerische Zeichen oder Sonderzeichen enthalten. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Computer Konto Kennwort auf dem lokalen Computer von *IPops897* auf *IPOP $897!* zu ändern:

```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)
