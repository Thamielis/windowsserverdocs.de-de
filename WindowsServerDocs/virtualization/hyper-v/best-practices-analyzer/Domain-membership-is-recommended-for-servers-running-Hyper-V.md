---
title: Die Domänen Mitgliedschaft wird für Server mit Hyper-V empfohlen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 2f4578e5-0848-46b4-a50b-7dbd480b80bf
ms.date: 8/16/2016
ms.openlocfilehash: 6a813af7d5064f91870652e6b0073c5c73c62604
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90745665"
---
# <a name="domain-membership-is-recommended-for-servers-running-hyper-v"></a>Die Domänen Mitgliedschaft wird für Server mit Hyper-V empfohlen.

>Gilt für: Windows Server 2016



*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).

|Eigenschaft|Details|
|-|-|
|**Betriebssystem**|Windows Server 2016|
|**Produkt/Feature**|Hyper-V|
|**Severity**|Warnung|
|**Kategorie**|Konfiguration|

In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.

## <a name="issue"></a>Problem

*Dieser Server ist Mitglied einer Arbeitsgruppe.*

## <a name="impact"></a>Auswirkung

*Es gibt keine zentrale Verwaltung für diesen Server.*

Das Hinzufügen dieses Computers zur Domäne ermöglicht die zentralisierte Verwaltung mithilfe von Richtlinien für Identität, Sicherheit und Überwachung.

## <a name="resolution"></a>Lösung

*Wenn eine Domänen Umgebung verfügbar ist, verknüpfen Sie diesen Server mit dieser Domäne.*

> [!IMPORTANT]
> Es wird empfohlen, die Arbeits Auslastungen, die auf den virtuellen Computern auf diesem Computer ausgeführt werden, zu überprüfen, um zu ermitteln, ob sich der Beitritt dieses Computers zu einer Domäne durch die Sicherheit Wenn es sich bei einem virtuellen Computer um virtualisierte Domänen Controller handelt, finden Sie unter [Überlegungen zur Planung für virtualisierte Domänen Controller](https://go.microsoft.com/fwlink/?LinkId=190192) ( https://go.microsoft.com/fwlink/?LinkId=190192) .

Zum Hinzufügen eines Computers zu einer Domäne sind Berechtigungen für den Computer und die Domäne erforderlich:
- Auf dem Computer benötigen Sie ein Benutzerkonto, das Mitglied der Gruppe "Administratoren" ist. Melden Sie sich mit diesem Kontotyp an, oder geben Sie den Benutzernamen und das Kennwort für das Konto an, wenn Sie dazu aufgefordert werden.
- In der Domäne benötigen Sie ein Benutzerkonto, das zum Hinzufügen des Computers zur Domäne autorisiert ist. Sie werden zur Eingabe des Benutzernamens und des Kennworts aufgefordert.

Anweisungen finden Sie unter [Hinzufügen des Computers zur Domäne](https://go.microsoft.com/fwlink/?LinkId=190193) ( https://go.microsoft.com/fwlink/?LinkId=190193) .



