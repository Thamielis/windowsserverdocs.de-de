---
title: Leistungsoptimierung Remotedesktop Gateways
description: Empfehlungen zur Leistungsoptimierung für Remotedesktop Gateways
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: hammadbu; vladmis
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 3794b47e7226a905944495dd7c31f3196a33d0d5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851733"
---
# <a name="performance-tuning-remote-desktop-gateways"></a>Leistungsoptimierung Remotedesktop Gateways

> [!NOTE]
> In Windows 8 und höher und Windows Server 2012 R2 und höher unterstützt Remotedesktop Gateway (RD-Gateway) TCP, UDP und ältere RPC-Transporte. Die meisten der folgenden Daten betreffen den veralteten RPC-Transport. Wenn der ältere RPC-Transport nicht verwendet wird, ist dieser Abschnitt nicht anwendbar.

In diesem Thema werden die leistungsbezogenen Parameter beschrieben, mit denen die Leistung einer Kunden Bereitstellung und die Tunings, die auf den Netzwerk Verwendungs Mustern des Kunden basieren, verbessert werden können.

Im Kern führt RD-Gateway viele Paketweiterleitungs Vorgänge zwischen Remotedesktopverbindung Instanzen und den RD-Sitzungshost Server Instanzen im Netzwerk des Kunden durch.

> [!NOTE]
> Die folgenden Parameter gelten nur für den RPC-Transport.

Internetinformationsdienste (IIS) und RD-Gateway exportieren Sie die folgenden Registrierungs Parameter, um die Systemleistung in der RD-Gateway zu verbessern.

**Thread-Tunings**

-   **MaxIoThreads**

    ``` syntax
    HKLM\Software\Microsoft\Terminal Server Gateway\Maxiothreads (REG_DWORD)
    ```

    Dieser APP-spezifische Thread Pool gibt die Anzahl der Threads an, die RD-Gateway erstellt, um eingehende Anforderungen zu verarbeiten. Wenn diese Registrierungs Einstellung vorhanden ist, wird Sie wirksam. Die Anzahl der Threads ist mit der Anzahl logischer Prozesse verknüpft. Wenn die Anzahl der logischen Prozessoren kleiner als 5 ist, beträgt der Standardwert 5 Threads.

-   **MaxPoolThreads**

    ``` syntax
    HKLM\System\CurrentControlSet\Services\InetInfo\Parameters\MaxPoolThreads (REG_DWORD)
    ```

    Dieser Parameter gibt die Anzahl der IIS-Poolthreads an, die pro logischem Prozessor erstellt werden. Die IIS-Poolthreads beobachten das Netzwerk auf Anforderungen und verarbeiten alle eingehenden Anforderungen. Die Anzahl der **MaxPoolThreads** schließt keine Threads ein, die RD-Gateway verbraucht. Der Standardwert ist 4.

**Tunings für Remote Prozedur Aufrufe für RD-Gateway**

Die folgenden Parameter können helfen, die Remote Prozedur Aufrufe (RPC) zu optimieren, die von Remotedesktopverbindung und RD-Gateway Computern empfangen werden. Durch das Ändern der Fenster können Sie Drosseln, wie viele Daten durch die einzelnen Verbindungen übertragen werden, und die Leistung für RPC-über-HTTP v2-Szenarien steigern

-   **Serverreceivewindow**

    ``` syntax
    HKLM\Software\Microsoft\Rpc\ServerReceiveWindow (REG_DWORD)
    ```

    Der Standardwert ist 64 KB. Dieser Wert gibt das Fenster an, das der Server für Daten verwendet, die vom RPC-Proxy empfangen werden. Der Minimalwert ist auf 8 KB festgelegt, und der Höchstwert wird auf 1 GB festgelegt. Wenn kein Wert vorhanden ist, wird der Standardwert verwendet. Wenn an diesem Wertänderungen vorgenommen werden, muss IIS neu gestartet werden, damit die Änderung wirksam wird.

-   **Serverreceivewindow**

    ``` syntax
    HKLM\Software\Microsoft\Rpc\ServerReceiveWindow (REG_DWORD)
    ```

    Der Standardwert ist 64 KB. Dieser Wert gibt das Fenster an, das der Client für Daten verwendet, die vom RPC-Proxy empfangen werden. Der Minimalwert ist 8 KB, und der Höchstwert beträgt 1 GB. Wenn kein Wert vorhanden ist, wird der Standardwert verwendet.

## <a name="monitoring-and-data-collection"></a>Überwachung und Datensammlung

Die folgende Liste der Leistungsindikatoren wird als Basissatz von Indikatoren betrachtet, wenn Sie die Ressourcenverwendung auf dem RD-Gateway überwachen:

-   \\Terminal Dienst Gateway\\\*

-   \\RPC/HTTP-Proxy\\\*

-   \\des RPC/HTTP-Proxys pro Server\\\*

-   \\Webdienst\\\*

-   \\W3SVC\_w3wp\\\*

-   \\IPv4-\\\*

-   \\Arbeitsspeicher\\\*

-   \\Netzwerkschnittstelle (\*)\\\*

-   \\Prozess (\*)\\\*

-   \\Prozessor Informationen (\*)\\\*

-   \\Synchronisierung (\*)\\\*

-   \\System\\\*

-   \\TCPv4\\\*

Die folgenden Leistungsindikatoren sind nur für den Legacy-RPC-Transport anwendbar:

-   \\RPC/HTTP-Proxy\\\* RPC

-   \\RPC/HTTP-Proxy pro Server\\\* RPC

-   \\Webdienst\\\* RPC

-   \\W3SVC\_w3wp\\\* RPC

> [!NOTE]
> Fügen Sie ggf. die \\IPv6-\\\* und \\TCPv6\\\* Objekte hinzu. ReplaceThisText

