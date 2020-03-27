---
title: 'Rechenzentrumsfirewall: Übersicht'
description: In diesem Thema erfahren Sie mehr über die Rechenzentrums Firewall, bei der es sich um eine Netzwerkschicht, 5-Tupel (Protokoll, Quell-und Ziel Portnummern, Quell-und Ziel-IP-Adressen), eine Zustands behaftete, mehr Instanzen fähige Firewall in Windows Server 2016 handelt.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67576533-206b-428a-956c-ed8c53218d9b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 141057d2ee3e648f589d255ea04fdef179cedf3c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317032"
---
# <a name="datacenter-firewall-overview"></a>Rechenzentrumsfirewall: Übersicht

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Datacenter Firewall ist ein neuer Dienst, der in Windows Server 2016 enthalten ist. Dabei handelt es sich um eine Netzwerkschicht, 5-Tupel (Protokoll, Quell-und Ziel Portnummern, Quell-und Ziel-IP-Adressen), Zustands behaftete, mehr Instanzen fähige Firewall. Wenn Sie vom Dienstanbieter als Dienst bereitgestellt und angeboten werden, können Mandanten Administratoren Firewallrichtlinien installieren und konfigurieren, um Ihre virtuellen Netzwerke vor unerwünschtem Datenverkehr aus Internet-und intranetnetzwerken zu schützen.  
  
![Rechenzentrums Firewall im Netzwerk Stapel](../../../media/Datacenter-Firewall-Overview/MultitenantFirewallOverview2.png)  
  
Der Dienstanbieter Administrator oder der Mandanten Administrator kann die Datacenter-Firewallrichtlinien über den Netzwerk Controller und die Northbound-APIs verwalten.  
  
Die Datacenter-Firewall bietet die folgenden Vorteile für clouddienstanbieter:  
  
-   Eine hochgradig skalierbare, verwaltbare und diagnosierbare softwarebasierte Firewalllösung, die Mandanten angeboten werden kann  
  
-   Freiheit zum Verschieben von virtuellen Mandanten Computern auf andere computehosts ohne Unterbrechung der Firewallrichtlinien für Mandanten  
  
    -   Wird als Firewall des Vswitch-Port Host-Agents bereitgestellt.  
  
    -   Virtuelle Mandanten Computer erhalten die Richtlinien, die ihrer Vswitch-Host-Agent-Firewall zugewiesen sind  
  
    -   Firewallregeln werden in jedem Vswitch-Port unabhängig vom eigentlichen Host, auf dem der virtuelle Computer ausgeführt wird, konfiguriert.  
  
-   Bietet Schutz für virtuelle Mandanten Computer unabhängig vom Gast Betriebssystem des Mandanten.  
  
Die Datacenter-Firewall bietet die folgenden Vorteile für Mandanten:  
  
-   Möglichkeit zum Definieren von Firewallregeln zum Schutz von Arbeits Auslastungen mit Internet Zugriff in virtuellen Netzwerken  
  
-   Möglichkeit zum Definieren von Firewallregeln zum Schutz des Datenverkehrs zwischen virtuellen Computern im gleichen virtuellen L2-Subnetz und zwischen virtuellen Computern in verschiedenen virtuellen L2-Subnetzen  
  
-   Möglichkeit zum Definieren von Firewallregeln, um den Netzwerk Datenverkehr zwischen lokalen Mandanten Netzwerken und Ihren virtuellen Netzwerken beim Dienstanbieter zu schützen und zu isolieren  
  


