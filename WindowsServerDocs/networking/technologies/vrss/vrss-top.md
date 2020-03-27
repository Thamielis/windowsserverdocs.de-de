---
title: Virtual Receive Side Scaling (vRSS)
description: Erfahren Sie mehr über die virtuelle Empfangs seitige Skalierung (vrss) in Windows Server und wie Sie einen virtuellen Netzwerkadapter konfigurieren, um einen Lastenausgleich für eingehenden Netzwerk Datenverkehr über mehrere logische Prozessorkerne auf einem virtuellen Computer durchzusetzen Sie können auch physische Kerne für eine virtuelle Netzwerkschnittstellenkarte (VNIC) des Hosts konfigurieren.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 9be477b3-f81d-4e84-a6b0-ac4c1ea97715
ms.date: 09/05/2018
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8841e0e5b33df6b44d63598ebf1f29caf89e1f3f
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315255"
---
# <a name="virtual-receive-side-scaling-vrss"></a>Virtuelle Empfangs seitige Skalierung \(vrss-\)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie mehr über die virtuelle Empfangs seitige Skalierung (vrss) und wie Sie einen virtuellen Netzwerkadapter konfigurieren, um einen Lastenausgleich für eingehenden Netzwerk Datenverkehr über mehrere logische Prozessorkerne auf einem virtuellen Computer durchzusetzen. Sie können vrss auch verwenden, um mehrere physische Kerne für eine virtuelle Netzwerkschnittstellenkarte des Hosts \(vNIC-\)zu konfigurieren.

Diese Konfiguration ermöglicht die Verteilung der Last von einem virtuellen Netzwerkadapter auf mehrere virtuelle Prozessoren in einem virtuellen Computer \(VM-\), sodass der virtuelle Computer mehr Netzwerk Datenverkehr schneller verarbeiten kann als mit einem einzelnen logischen Prozessor.

>[!TIP]
>Sie können vrss auf virtuellen Computern auf Hyper\-V-Hosts verwenden, die über mehrere Prozessoren verfügen, einen einzelnen Prozessor mit mehreren Kernen oder mehr als einen Prozessor mit mehreren Kernen, die für die Verwendung durch den virtuellen Computer installiert und konfiguriert sind.

vrss ist kompatibel mit allen anderen Hyper\-V-Netzwerktechnologien. vrss ist abhängig von Warteschlange für virtuelle Computer \(VMQ-\) auf dem Hyper\-V-Host und RSS auf dem virtuellen Computer oder auf der Host-vNIC.

Standardmäßig aktiviert Windows Server vrss, Sie können es jedoch mithilfe von Windows PowerShell auf einem virtuellen Computer deaktivieren. Weitere Informationen finden Sie unter [Verwalten von vrss](vrss-manage.md) -und [Windows PowerShell-Befehlen für RSS und vrss](vrss-wps.md).



## <a name="operating-system-compatibility"></a>Betriebssystemkompatibilität

Sie können RSS auf jedem Multiprozessor-oder mehr Kern-Computer oder vrss auf einem beliebigen Multiprozessor-oder Multi-Core-virtuellen Computer verwenden, auf dem Windows Server 2016 ausgeführt wird.

Multiprozessor-oder mehr Kern-VMS, auf denen die folgenden Microsoft-Betriebssysteme ausgeführt werden, unterstützen ebenfalls vrss.

- Windows Server 2016
- Windows 10 pro oder Enterprise
- Windows Server 2012 R2
- Windows 8.1 pro oder Enterprise
- Windows Server 2012 mit installierter Windows Server 2012 R2-Integrations Komponenten.
- Windows 8 mit installierter Windows Server 2012 R2-Integrations Komponenten.

Informationen zur vrss-Unterstützung für VMS, auf denen FreeBSD oder Linux als Gast Betriebssystem auf Hyper-v ausgeführt wird, finden Sie [unter Unterstützte virtuelle Linux-und FreeBSD-Computer für Hyper-v unter Windows](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows).
  
## <a name="hardware-requirements"></a>Hardwareanforderungen

Im folgenden sind die Hardwareanforderungen für vrss aufgeführt.
 
- Physische Netzwerkadapter müssen Warteschlange für virtuelle Computer \(VMQ-\)unterstützen. Wenn VMQ deaktiviert ist oder nicht unterstützt wird, ist vrss für den Hyper\-V-Host und alle auf dem Host konfigurierten virtuellen Computer deaktiviert.
- Netzwerkadapter müssen eine Verbindungsgeschwindigkeit von 10 Gbit/s oder mehr aufweisen.
- Hyper\-V-Hosts müssen mit mehreren Prozessoren oder mindestens einem Multi\-Core-Prozessor für die Verwendung von vrss konfiguriert werden.
- Virtuelle Computer \(VMS\) müssen für die Verwendung von mindestens zwei logischen Prozessoren konfiguriert werden.


## <a name="use-case-scenarios"></a>Anwendungsfall Szenarios

Die folgenden beiden Szenarien für Anwendungsfälle beschreiben die allgemeine Verwendung von vrss für den Prozessor Lastenausgleich und den Software Lastenausgleich.

### <a name="processor-load-balancing"></a>Prozessorlastenausgleich
  
Anthony, ein Netzwerkadministrator, richtet einen neuen Hyper-V-Host mit zwei Netzwerkadaptern ein, die die Virtualisierung mit einzelnen Stamm-Eingabe-und Ausgabe \(SR\-IOV-\)unterstützen. Er stellt Windows Server 2016 zum Hosten eines VM-Dateiservers bereit.

Nach der Installation der Hardware und Software konfiguriert Anthony einen virtuellen Computer für die Verwendung von acht virtuellen Prozessoren und von 4096 MB Arbeitsspeicher. Leider hat Anthony nicht die Möglichkeit, SR\-IOV zu aktivieren, da seine virtuellen Computer die Richtlinien Erzwingung durch den virtuellen Switch verlassen, den er mit dem virtuellen Switch Manager von Hyper\-V erstellt hat. Aus diesem Grund beschließt Anthony die Verwendung von vrss anstelle von SR\-IOV.

Zuerst weist Anthony mithilfe von Windows PowerShell vier virtuelle Prozessoren zu, die für die Verwendung mit vrss verfügbar sein sollen. Die Verwendung des Dateiservers nach einer Woche scheint sehr beliebt zu sein, sodass Anthony die Leistung der VM prüft.  Er ermittelt die vollständige Auslastung der vier virtuellen Prozessoren.

Aus diesem Grund beschließt Anthony das Hinzufügen von Prozessoren zum virtuellen Computer für die Verwendung durch vrss.  Er weist zwei weitere virtuelle Prozessoren der VM zu, die automatisch für vrss verfügbar sind, um die große Netzwerk Last zu bewältigen. Seine Bemühungen führen zu einer besseren Leistung für den VM-Dateiserver, wobei die sechs Prozessoren die Last des Netzwerk Datenverkehrs effizient verarbeiten.


### <a name="software-load-balancing"></a>Softwarelastenausgleich

Sandra, ein Netzwerkadministrator, richtet eine einzelne Hochleistungs-VM auf einem ihrer Systeme ein, die als Software Lastenausgleich fungieren soll. Sie hat diesem einzelnen virtuellen Computer alle verfügbaren logischen Prozessoren zugewiesen.

Nach der Installation von Windows Server verwendet Sie vrss, um die parallele Verarbeitung des Netzwerk Datenverkehrs für mehrere logische Prozessoren auf dem virtuellen Computer zu erhalten. Da Windows Server vrss aktiviert, muss Sandra keine Konfigurationsänderungen vornehmen.


## <a name="related-topics"></a>Verwandte Themen

- [Planen der Verwendung von vrss](vrss-plan.md)
- [Aktivieren von vrss auf einem Virtual Network Adapter](vrss-enable.md)
- [Verwalten von vRSS](vrss-manage.md)
- [häufig gestellte Fragen zu vrss](vrss-faq.md)
- [Windows PowerShell-Befehle für RSS und vrss](vrss-wps.md)

---
