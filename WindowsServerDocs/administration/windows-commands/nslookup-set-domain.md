---
title: nslookup set domain
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fa433383e23fd19779960348e0af88e0a405ff83
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838463"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Standard-DNS-Domänen Namen (Domain Name System) in den angegebenen Namen.
## <a name="syntax"></a>Syntax
```
set domain=<DomainName>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                           Beschreibung                                           |
|-----------------|-------------------------------------------------------------------------------------------------|
|  <DomainName>   | Gibt einen neuen Namen für den Standard-DNS-Domänen Namen an. Der Standard Domänen Name ist der Hostname. |
| {Help &#124; ?} |                      Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                      |

## <a name="remarks"></a>Hinweise
- Der Standard-DNS-Domänen Name wird an eine Such Anforderung angehängt, abhängig vom Status der Optionen " **defname** " und " **Search** ". Die DNS-Domänen Suchliste enthält die übergeordneten Elemente der DNS-Standard Domäne, wenn Ihr Name aus mindestens zwei Komponenten besteht. Wenn die DNS-Standard Domäne z. b. MFG.widgets.com lautet, heißt die Suchliste sowohl MFG.widgets.com als auch Widgets.com. Verwenden Sie den Befehl **set srchlist** , um eine andere Liste anzugeben, und den Befehl **alle festlegen** , um die Liste anzuzeigen.
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup set srchlist](nslookup-set-srchlist.md)
  [nslookup alle festlegen](nslookup-set-all.md)
