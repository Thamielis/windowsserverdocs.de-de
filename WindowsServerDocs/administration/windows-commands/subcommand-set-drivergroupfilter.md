---
title: Unterbefehls Satz-drivergroupfilter
description: Referenz Artikel für den Unterbefehl set-drivergroupfilter, mit dem ein vorhandener Treiber Gruppen Filter aus einer Treiber Gruppe hinzugefügt oder daraus entfernt wird.
ms.topic: reference
ms.assetid: 829ab1f0-4514-421e-9cc0-767b238da69c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a27795fb6a4f6851a8b114f3ce1f91560df9ce76
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640886"
---
# <a name="subcommand-set-drivergroupfilter"></a>Unterbefehl: Set-drivergroupfilter

Hiermit wird ein vorhandener Treiber Gruppen Filter aus einer Treiber Gruppe hinzugefügt oder daraus entfernt.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type> [/Policy:{Include | Exclude}] [/AddValue:<Value> [/AddValue:<Value> ...]] [/RemoveValue:<Value> [/RemoveValue:<Value> ...]]
```

### <a name="parameters"></a>Parameter

|         Parameter          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               BESCHREIBUNG                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup:\<Group Name> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 Gibt den Namen der Treiber Gruppe an.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|  [/Server:\<Server name>]  |                                                                                                                                                                                                                                                                                                                                                                                                                Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Filter Type\<FilterType>  |                                                                                                                                                                                                                                                                       Gibt den Typ des Treiber Gruppen Filters an, der hinzugefügt oder entfernt werden soll. Sie können mehrere Filter in einem einzelnen Befehl angeben. Für jede **/FilterType**können Sie mehrere Werte mithilfe von **/RemoveValue** und **/AddValue**hinzufügen oder entfernen. \<FilterType> kann eines der folgenden sein:</br>**Biosvendor**</br>**Biosversion**</br>**ChassisType**</br>**Manufacturer**</br>**UUID**</br>**OsVersion**</br>**Odition**</br>**OSLanguage**                                                                                                                                                                                                                                                                        |
|     [/Policy: {include      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                Ausschließen}]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|    [/AddValue: \<Value> ]    | Gibt den neuen Client Wert an, der dem Filter hinzugefügt werden soll. Sie können mehrere Werte für einen einzelnen Filtertyp angeben. In der folgenden Liste finden Sie gültige Attributwerte für **chassistype**. Weitere Informationen zum Abrufen der Werte für alle anderen Filtertypen finden Sie unter [Treiber Gruppen Filter](https://go.microsoft.com/fwlink/?LinkID=155158) ( <https://go.microsoft.com/fwlink/?LinkID=155158> ).</br>**Andere**</br>**Unknownchassis**</br>**Desktop**</br>**Lowprofiledesktop**</br>**Pizzabox**</br>**Minitower**</br>**Kühl**</br>**Tabel**</br>**Laptop**</br>**Notebook**</br>**Gehaltenen**</br>**Dockingstation**</br>**AllInOne**</br>**Unter Notebook**</br>**Spacesaving**</br>**Lunchbox**</br>**Mainsystemchassis**</br>**Expansions Chassis**</br>**Subchassis**</br>**Busexpansionchassis**</br>**Peripherie Chassis**</br>**Storagechassis**</br>**Rackmountchassis**</br>**Versiegencasecomputer**</br>**Multisystemchassis**</br>**CompactPCI**</br>**AdvancedTCA** |
|  [/RemoveValue: \<Value> ]   |                                                                                                                                                                                                                                                                                                                                                                                                                                     Gibt den vorhandenen Client Wert an, der aus dem Filter entfernt werden soll, wie in **/AddValue**angegeben.                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## <a name="examples"></a>Beispiele

Um einen Filter zu entfernen, geben Sie einen der folgenden Informationen ein:
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /AddValue:Name1 /RemoveValue:Name2
```
```
WDSUTIL /Set-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /Policy:Include /RemoveValue:Name1 /FilterType:ChassisType /Policy:Exclude /AddValue:Tower /AddValue:MiniTower
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)