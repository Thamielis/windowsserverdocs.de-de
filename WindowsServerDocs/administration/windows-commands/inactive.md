---
title: inactive
description: Referenz Artikel für den inaktiven Befehl, der die Systempartition oder Start Partition mit dem Fokus als inaktiv auf grundlegenden Master Boot Record (MBR) kennzeichnet.
ms.topic: reference
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 265e1ca2ef7c352aead87ab19bdabed3a0abe476
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634499"
---
# <a name="inactive"></a>inactive

Markiert die Systempartition oder Start Partition, deren Fokus auf grundlegenden Master Boot Record-Datenträgern (MBR) liegt.

Ein aktives System oder eine Start Partition muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl [Partitions Befehl auswählen](select-partition.md) die aktive Partition aus, und verschieben Sie den Fokus auf die Partition.

> [!CAUTION]
> Ihr Computer wird möglicherweise nicht ohne eine aktive Partition gestartet. Markieren Sie ein System oder eine Start Partition nur dann als inaktiv, wenn Sie ein erfahrener Benutzer sind, der über ein umfassendes Verständnis der Windows-Betriebssystem Familie verfügt.<p>Wenn Sie den Computer nicht starten können, nachdem Sie das System oder die Start Partition als inaktiv gekennzeichnet haben, legen Sie die Windows Setup CD in das CD-ROM-Laufwerk ein, starten Sie den Computer neu, und reparieren Sie dann die Partition mithilfe der Befehle **fixmbr** und **fixboot** in der Wiederherstellungskonsole.
>
> Nachdem Sie die Systempartition oder Start Partition als inaktiv markiert haben, startet der Computer mit der nächsten im BIOS angegebenen Option, z. b. dem CD-ROM-Laufwerk oder einer Pre-Boot Execution Environment (PXE).

## <a name="syntax"></a>Syntax

```
inactive
```

### <a name="examples"></a>Beispiele

```
inactive
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Partitions Befehl auswählen](select-partition.md)

- [Erweiterte Problembehandlung für Windows-Startprobleme](/windows/client-management/advanced-troubleshooting-boot-problems)
