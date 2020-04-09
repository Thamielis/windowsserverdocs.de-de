---
title: 'Ksetup: Delta Pass WD'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b849265e6036f338413b75fe1da2067e4cdb4cd8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841653"
---
# <a name="ksetupdelkpasswd"></a>Ksetup: Delta Pass WD

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

entfernt einen Kerberos-Kenn Wort Server (kpasswd) für einen Bereich. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).
## <a name="syntax"></a>Syntax
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
#### <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                   Beschreibung                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <RealmName>  |                                Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com, und wird als Standardbereich bzw. Bereich angezeigt, wenn **Ksetup** ausgeführt wird.                                |
| <KpasswdName> | Der KDC-Name, der als Kerberos-Kenn Wort Server verwendet werden soll, wird als voll qualifizierter Domänen Name ohne Beachtung der Groß-/Kleinschreibung angegeben, z. b. mitkdc.contoso.com Wenn der KDC-Name weggelassen wird, kann DNS verwendet werden, um nach KDCs zu suchen. |

## <a name="remarks"></a>Hinweise
Führen Sie den Befehl **Ksetup** aus, um den KDC-Namen zu überprüfen. Wenn **kpasswd =** nicht in der Ausgabe angezeigt wird, wurde die Zuordnung nicht konfiguriert. Wenn festgelegt, werden mehrere Zuordnungen aufgelistet.
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
Überprüfen Sie den Bereich Corp. CONTOSO.com verwendet den nicht-Windows-KDC-Server mitkdc.contoso.com als Kenn Wort Server:
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
Um zu überprüfen, ob der Befehl wie beabsichtigt funktioniert, führen Sie **Ksetup** auf dem Windows-Computer aus, um den Bereich Corp. CONTOSO.com ist keinem Kerberos-Kenn Wort Server (KDC-Name) zugeordnet.
## <a name="additional-references"></a>Weitere Verweise
-   [ksetup](ksetup.md)
-   [Ksetup: Delta Pass WD](ksetup-delkpasswd.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
