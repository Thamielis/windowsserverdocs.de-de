---
title: Get-allimagegroups
description: Referenz Artikel zu Get-allimagegroups, der Informationen zu allen Image Gruppen auf einem Server und alle Images in diesen Abbild Gruppen abruft.
ms.topic: reference
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b69375cff867d317c3ac6c83ec1c75358455ac03
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626420"
---
# <a name="get-allimagegroups"></a>Get-allimagegroups

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu allen Abbild Gruppen auf einem Server und alle Images in diesen Abbild Gruppen ab.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Detailed|Gibt die Bild Metadaten aus jedem Bild zurück. Wenn dieser Parameter nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen für jedes Image zurückzugeben.|
## <a name="examples"></a>Beispiele
Zum Anzeigen von Informationen zu den Bildgruppen geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-add-imagegroup-command.md) 
 "Add-ImageGroup" [Verwenden des Befehls](using-the-get-imagegroup-command.md) 
 Get-ImageGroup [Verwenden des Remove-ImageGroup-Befehls](using-the-remove-imagegroup-command.md) 
 [Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
