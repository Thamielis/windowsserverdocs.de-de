---
title: diskperf
description: Windows-Befehls Thema für diskperf, das verwendet werden kann, um Leistungsindikatoren für physische oder logische Datenträger auf Computern mit Windows 2000 Remote zu aktivieren bzw. zu deaktivieren.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b07471c051d57d0279e4fd8b38afdc4acdc4069
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845463"
---
# <a name="diskperf"></a>diskperf

In Windows 2000 sind Leistungsindikatoren für physische und logische Datenträger standardmäßig nicht aktiviert.

**Diskperf** ist in Windows XP, Windows Server 2003, Windows Server 2008, Windows Vista, Windows Server 2008 R2 und Windows 7 enthalten, sodass es für die Remote Aktivierung oder Deaktivierung von Leistungsindikatoren für physische oder logische Datenträger auf Computern mit Windows 2000 verwendet werden kann.

## <a name="syntax"></a>Syntax

```
diskperf [-Y[D|V] | -N[D|V]] [\\computername]
```

## <a name="options"></a>Optionen

|Option|Beschreibung|
|------|-----------|
|-?|Zeigt kontextabhängige Hilfe an.|
|-Y|Starten Sie alle Datenträger-Leistungsindikatoren, wenn der Computer neu gestartet wird.|
|-Yd|Aktivieren Sie Datenträger-Leistungsindikatoren für physische Laufwerke, wenn der Computer neu gestartet wird.|
|-YV|Aktivieren Sie Datenträger-Leistungsindikatoren für logische Laufwerke oder Speichervolumes, wenn der Computer neu gestartet wird.|
|-N|Deaktivieren Sie alle Datenträger Leistungsindikatoren, wenn der Computer neu gestartet wird.|
|-ND|Deaktivieren Sie die Datenträger Leistungsindikatoren für physische Laufwerke, wenn der Computer neu gestartet wird.|
|-NV|Deaktivieren Sie die Datenträger Leistungsindikatoren für logische Laufwerke oder Speichervolumes, wenn der Computer neu gestartet wird.|
|\\\\ *\<Computername >*|Geben Sie den Namen des Computers an, auf dem Sie die Datenträger-Leistungsindikatoren aktivieren bzw. deaktivieren möchten.|