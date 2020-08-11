---
title: Netzwerkrichtlinien
description: Bandbreitenempfehlungen für Remotedesktopbereitstellungen.
ms.author: helohr
ms.date: 12/12/2019
ms.topic: article
author: Heidilohr
manager: lizross
ms.openlocfilehash: 3817178ef303573490cc98af8a35844715286e8e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948893"
---
# <a name="network-guidelines"></a>Netzwerkrichtlinien

Bei Verwendung einer Windows-Remotesitzung hat die verfügbare Bandbreite des Netzwerks einen großen Einfluss auf die Qualität der Erfahrung. Unterschiedliche Anwendungen und Bildschirmauflösungen erfordern unterschiedliche Netzwerkkonfigurationen, daher ist es wichtig, sicherzustellen, dass das Netzwerk entsprechend den Anforderungen konfiguriert ist.

>[!NOTE]
>Die folgenden Empfehlungen gelten für Netzwerke einem Verlust von weniger als 0,1 %. Diese Empfehlungen gelten unabhängig davon, wie viele Sitzungen du auf deinen virtuellen Computern (VMs) hostest.

## <a name="applications"></a>Anwendungen

In der folgenden Tabelle sind die empfohlenen Mindestbandbreiten für eine reibungslose Benutzererfahrung aufgeführt. Diese Empfehlungen basieren auf den Richtlinien in [Remotedesktop-Workloads](remote-desktop-workloads.md).

| Workloadtyp   | Empfohlene Bandbreite |
|-----------------|-----------------------|
| Leicht           | 1,5 Mbit/s              |
| Medium (Mittel)          | 3 Mbit/s                |
| Schwer           | 5 Mbit/s                |
| Leistung           | 15 Mbit/s               |

Denke daran, dass die Belastung deines Netzwerks sowohl von der Ausgabebildfrequenz deiner App-Workloads als auch von der Bildschirmauflösung abhängt. Wenn entweder die Bildfrequenz oder die Bildschirmauflösung erhöht wird, steigt auch der Bandbreitenbedarf. Beispielsweise benötigt eine geringe Workload bei einer Anzeige mit hoher Auflösung mehr verfügbare Bandbreite als eine geringe Workload bei normaler oder niedriger Auflösung.

In anderen Szenarien können sich die Bandbreitenanforderungen je nach der Art der Nutzung ändern, z. B:

- Telefon- oder Videokonferenzen
- Echtzeitkommunikation
- Streamen von 4-K-Videos

Führe für diese Szenarien in deiner Bereitstellung unbedingt Auslastungstest mit Simulationswerkzeugen wie Login VSI durch. Variiere die Auslastungsgröße, führe Belastungstests durch, und teste gängige Benutzerszenarien in Remotesitzungen, um die Anforderungen an das Netzwerk besser zu verstehen.

## <a name="display-resolutions"></a>Anzeigeauflösungen

Unterschiedliche Anzeigeauflösungen erfordern unterschiedliche verfügbare Bandbreiten. In der folgenden Tabelle sind die Bandbreiten aufgelistet, die wir für eine reibungslose Benutzererfahrung bei typischen Anzeigeauflösungen mit einer Bildfrequenz von 30 Bildern pro Sekunde (FPS) empfehlen. Diese Empfehlungen gelten für Einzel- und Mehrbenutzerszenarien. Beachte, dass Szenarien mit einer Bildfrequenz unter 30 FPS, wie z.B. das Lesen von statischem Text, weniger verfügbare Bandbreite benötigen.

| Typische Anzeigeauflösungen bei 30 FPS    | Empfohlene Bandbreite |
|------------------------------------------|-----------------------|
| Etwa 1024 × 768 px                      | 1,5 Mbit/s              |
| Etwa 1280 × 720 px                      | 3 Mbit/s                |
| Etwa 1920 × 1080 px                     | 5 Mbit/s                |
| Etwa 3840 × 2160 px (4 K)                | 15 Mbit/s               |

## <a name="windows-virtual-desktop-experience-estimator"></a>Einschätzung der Servicequalität für Windows Virtual Desktop

Die Azure-Region, in der du dich befindest, kann die Benutzererfahrung ebenso beeinflussen wie die Netzwerkbedingungen. Unter [Einschätzung der Servicequalität für Windows Virtual Desktop](https://azure.microsoft.com/services/virtual-desktop/assessment/) findest du weitere Informationen.

## <a name="assistive-technologies"></a>Hilfstechnologien

Hilfstechnologieworkloads, wie die Verwendung der Sprachausgabe in der Remotesitzung, erfordern für eine optimale Benutzererfahrung Verbindungen mit einer Roundtripzeit (RTT) von 20 Millisekunden (ms) oder besser.
