---
title: Erkennen von Engpässen in einer virtualisierten Umgebung
description: Erkennen und beheben potenzieller Leistungsengpässe bei Hyper-v
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 211f35c151e94bc8b8a11a614edad18053cb18b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851777"
---
# <a name="detecting-bottlenecks-in-a-virtualized-environment"></a>Erkennen von Engpässen in einer virtualisierten Umgebung

In diesem Abschnitt finden Sie einige Hinweise dazu, was Sie mit dem System Monitor überwachen müssen, und wie Sie ermitteln können, wo das Problem möglicherweise auftritt, wenn der Host oder einige der virtuellen Maschinen nicht wie erwartet ausgeführt werden.

## <a name="processor-bottlenecks"></a>Prozessor Engpässe

Im folgenden finden Sie einige häufige Szenarien, die Prozessor Engpässe verursachen können:

-   Mindestens ein logischer Prozessor wird geladen.

-   Mindestens ein virtueller Prozessor wird geladen.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Auslastung des logischen Prozessors-\\logischer Hyper-V-Hypervisor-Prozessor (\*)\\% Gesamtlaufzeit

-   Auslastung des virtuellen Prozessors-\\virtuellen Hyper-V-Hypervisor-Prozessor (\*)\\% Gesamtlaufzeit

-   Auslastung des virtuellen Stamm Prozessors-\\virtuellen Hyper-V-Hypervisor-Stamm Prozessor (\*)\\% Gesamtlaufzeit

Wenn der **logische Prozessor des Hyper-V-Hypervisors (\_gesamt)\\% Total Runtime** Counter über 90% ist, wird der Host überladen. Sie sollten eine höhere Verarbeitungsleistung hinzufügen oder einige virtuelle Maschinen auf einen anderen Host verschieben.

Wenn der **virtuelle Hyper-V-Hypervisor-Prozessor (VM-Name: VP x)\\% Total Runtime** -Wert für alle virtuellen Prozessoren mehr als 90% beträgt, sollten Sie die folgenden Schritte ausführen:

-   Überprüfen, ob der Host nicht überladen ist

-   Ermitteln, ob die Arbeitsauslastung mehr virtuelle Prozessoren nutzen kann

-   Zuweisen von mehr virtuellen Prozessoren zum virtuellen Computer

Wenn der **virtuelle Hyper-V-Hypervisor-Prozessor (VM-Name: VP x)\\% Total-Lauf** Zeit Zählers bei einigen, jedoch nicht allen virtuellen Prozessoren mehr als 90% beträgt, sollten Sie folgende Schritte ausführen:

-   Wenn Ihre Arbeitsauslastung Netzwerk intensiv ist, sollten Sie die Verwendung von vrss in Erwägung gezogen.

-   Wenn auf den virtuellen Computern nicht Windows Server 2012 R2 ausgeführt wird, sollten Sie weitere Netzwerkadapter hinzufügen.

-   Wenn Ihre Arbeitsauslastung Speicher intensiv ist, sollten Sie virtuelle NUMA aktivieren und weitere virtuelle Datenträger hinzufügen.

Wenn der **virtuelle Hyper-V-Hypervisor-Stamm Prozessor (Stamm-VP x)\\% Total Runtime** -Zählers für einige über 90% beträgt, aber nicht alle virtuellen Prozessoren und Prozessor **(x)\\% Interruptzeit und Prozessor (x)\\% DPC-Zeit** Leistungsindikatoren summiert ungefähr den Wert für den Stamm- **virtuellen Prozessor (Stamm-VP x)\\% Total Runtime** -Leistungsindikatoren. Stellen Sie sicher, dass VMQ auf den Netzwerkadaptern aktiviert ist.

## <a name="memory-bottlenecks"></a>Arbeitsspeicher Engpässe

Im folgenden finden Sie einige häufige Szenarien, die Arbeitsspeicher Engpässe verursachen können:

-   Der Host reagiert nicht.

-   Virtuelle Maschinen können nicht gestartet werden.

-   Nicht genügend Arbeitsspeicher für virtuelle Computer.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Arbeitsspeicher\\verfügbare MB

-   Hyper-V dynamischer Arbeitsspeicher Balancer (\*)\\verfügbaren Arbeitsspeicher

Sie können die folgenden Leistungsindikatoren auf dem virtuellen Computer verwenden:

-   Arbeitsspeicher\\verfügbare MB

Wenn die **Speicher\\verfügbare** MB und **Hyper-V dynamischer Arbeitsspeicher Balancer (\*)\\verfügbaren Arbeitsspeicher** auf dem Host gering sind, sollten Sie nicht erforderliche Dienste anhalten und eine oder mehrere virtuelle Maschinen zu einem anderen Host migrieren.

Wenn der virtuelle Computer den Arbeits **Speicher\\verfügbare** MB-Anzahl (MB) niedrig ist, sollten Sie dem virtuellen Computer mehr Arbeitsspeicher zuweisen. Wenn Sie dynamischer Arbeitsspeicher verwenden, sollten Sie die Einstellung für den maximalen Arbeitsspeicher erhöhen.

## <a name="network-bottlenecks"></a>Netzwerk Engpässe

Im folgenden finden Sie einige häufige Szenarien, die zu Netzwerk Engpässen führen können:

-   Der Host ist Netzwerk gebunden.

-   Der virtuelle Computer ist Netzwerk gebunden.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Netzwerkschnittstelle (*Netzwerkadapter Name*)\\Bytes/Sek.

Sie können die folgenden Leistungsindikatoren auf dem virtuellen Computer verwenden:

-   Hyper-V-Virtual Network Adapter (*Name des virtuellen Computers&lt;GUID&gt;* )\\Bytes/Sek.

Wenn der Leistungswert für **physische NIC-Bytes/Sek** . größer als oder gleich 90% der Kapazität ist, sollten Sie zusätzliche Netzwerkadapter hinzufügen, virtuelle Maschinen zu einem anderen Host migrieren und Netzwerk-QoS konfigurieren.

Wenn der Wert für den Wert des **Hyper-V-Virtual Network Adapters für Bytes/Sek** . größer oder gleich 250 Mbit/s ist, sollten Sie zusätzliche Netzwerkadapter in der virtuellen Maschine hinzufügen, vrss aktivieren und SR-IOV verwenden.

Wenn Ihre Workloads Ihre Netzwerk Latenz nicht erreichen können, aktivieren Sie SR-IOV, um dem virtuellen Computer physische Netzwerkadapter Ressourcen bereitzustellen.

## <a name="storage-bottlenecks"></a>Speicher Engpässe

Im folgenden finden Sie einige häufige Szenarien, die Speicher Engpässe verursachen können:

-   Der Host und die Vorgänge der virtuellen Maschine sind langsam oder Timeout.

-   Der virtuelle Computer ist träge.

Sie können die folgenden Leistungsindikatoren auf dem Host verwenden:

-   Physischer Datenträger (Datenträger*Buchstabe*)\\Mittlere Sek./Lesevorgänge

-   Physischer Datenträger (Datenträger*Buchstabe*)\\Mittlere Sek./Schreibvorgänge

-   Physischer Datenträger (Datenträger*Buchstabe*)\\Durchschnittl. Warteschlangen Länge des Datenträgers

-   Physischer Datenträger (Datenträger*Buchstabe*)\\durchschnittliche Warteschlangen Länge des Datenträgers

Wenn die Latenzzeit konstant größer als 50 ms ist, sollten Sie folgende Schritte ausführen:

-   Verteilen virtueller Maschinen auf zusätzlichen Speicher

-   Kauf eines schnelleren Speichers in Erwägung gezogen

-   Beachten Sie Tiered Storage Leerzeichen, die in Windows Server 2012 R2 eingeführt wurden.

-   Verwenden Sie ggf. QoS für Speicher, das in Windows Server 2012 R2 eingeführt wurde.

-   Verwenden von vhdx

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Speicher](storage-io-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
