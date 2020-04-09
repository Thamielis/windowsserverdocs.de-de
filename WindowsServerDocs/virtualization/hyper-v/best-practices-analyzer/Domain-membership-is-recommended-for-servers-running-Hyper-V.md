---
title: Die Domänen Mitgliedschaft wird für Server mit Hyper-V empfohlen.
description: Online Version des Texts für diese Best Practices Analyzer Regel.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f4578e5-0848-46b4-a50b-7dbd480b80bf
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: de38374a127a15c2a1d4bf262b72781429fa477c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861993"
---
# <a name="domain-membership-is-recommended-for-servers-running-hyper-v"></a>Die Domänen Mitgliedschaft wird für Server mit Hyper-V empfohlen.

>Gilt für: Windows Server 2016


  
*Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
  
*Dieser Server ist Mitglied einer Arbeitsgruppe.*  
  
## <a name="impact"></a>Auswirkungen  
  
*Es gibt keine zentrale Verwaltung für diesen Server.*  
  
Das Hinzufügen dieses Computers zur Domäne ermöglicht die zentralisierte Verwaltung mithilfe von Richtlinien für Identität, Sicherheit und Überwachung.  
  
## <a name="resolution"></a>Auflösung  
  
*Wenn eine Domänen Umgebung verfügbar ist, verknüpfen Sie diesen Server mit dieser Domäne.*  
  
> [!IMPORTANT]  
> Es wird empfohlen, die Arbeits Auslastungen, die auf den virtuellen Computern auf diesem Computer ausgeführt werden, zu überprüfen, um zu ermitteln, ob sich der Beitritt dieses Computers zu einer Domäne durch die Sicherheit Wenn es sich bei einem virtuellen Computer um virtualisierte Domänen Controller handelt, finden Sie unter [Überlegungen zur Planung für virtualisierte Domänen Controller](https://go.microsoft.com/fwlink/?LinkId=190192) (https://go.microsoft.com/fwlink/?LinkId=190192).  
  
Zum Hinzufügen eines Computers zu einer Domäne sind Berechtigungen für den Computer und die Domäne erforderlich:   
- Auf dem Computer benötigen Sie ein Benutzerkonto, das Mitglied der Gruppe "Administratoren" ist. Melden Sie sich mit diesem Kontotyp an, oder geben Sie den Benutzernamen und das Kennwort für das Konto an, wenn Sie dazu aufgefordert werden.   
- In der Domäne benötigen Sie ein Benutzerkonto, das zum Hinzufügen des Computers zur Domäne autorisiert ist. Sie werden zur Eingabe des Benutzernamens und des Kennworts aufgefordert.  
  
Anweisungen hierzu finden [Sie unter Hinzufügen des Computers zur Domäne](https://go.microsoft.com/fwlink/?LinkId=190193) (https://go.microsoft.com/fwlink/?LinkId=190193).  
  


