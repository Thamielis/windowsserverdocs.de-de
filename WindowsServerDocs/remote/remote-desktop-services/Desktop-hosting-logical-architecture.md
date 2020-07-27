---
title: Architektur der Remotedesktopdienste
description: Architekturdiagramme für RDS
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 02/10/2017
ms.topic: article
ms.assetid: 7f73bb0a-ce98-48a4-9d9f-cf7438936ca1
author: lizap
manager: dongill
ms.openlocfilehash: 2635302c79f5bfb8ca446f78d543e19656644102
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966712"
---
# <a name="remote-desktop-services-architecture"></a>Architektur der Remotedesktopdienste

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Im Anschluss findest du verschiedene Konfigurationen für die Bereitstellung der Remotedesktopdienste zum Hosten von Windows-Apps und -Desktops für Endbenutzer.

>[!NOTE]
> Die folgenden Architekturdiagramme zeigen die Verwendung von RDS in Azure. Die Remotedesktopdienste können aber auch lokal und in anderen Clouds bereitgestellt werden. Diese Diagramme sollen in erster Linie die Zusammenstellung der RDS-Rollen und die Verwendung anderer Dienste veranschaulichen.

## <a name="standard-rds-deployment-architectures"></a>Standardarchitekturen für die RDS-Bereitstellung

Für die Remotedesktopdienste stehen zwei Standardarchitekturen zur Verfügung:
-    Einfache Bereitstellung: Enthält die erforderliche Mindestanzahl von Servern für eine effektive RDS-Umgebung.
-    Hoch verfügbare Bereitstellung: Enthält alle erforderlichen Komponenten, um die höchstmögliche garantierte Betriebszeit für deine RDS-Umgebung zu erzielen.

### <a name="basic-deployment"></a>Einfache Bereitstellung

![Einfache RDS-Bereitstellung](./media/basic-rds.png)

### <a name="highly-available-deployment"></a>Hoch verfügbare Bereitstellung

![Hoch verfügbare RDS-Bereitstellung](./media/ha-rds.png)

## <a name="rds-architectures-with-unique-azure-paas-roles"></a>RDS-Architekturen mit eindeutigen Azure-PaaS-Rollen

Die Standardarchitekturen für die RDS-Bereitstellung sind zwar für die meisten Szenarien geeignet, Azure investiert jedoch weiter in PaaS-Erstanbieterlösungen, um den Nutzen für Kunden noch weiter zu erhöhen. Im Anschluss folgen einige Architekturen zur Veranschaulichung der RDS-Integration.

### <a name="rds-deployment-with-azure-ad-domain-services"></a>RDS-Bereitstellung mit Azure AD Domain Services

Die beiden Standardarchitekturdiagramme von weiter oben basieren auf einer traditionellen AD-Bereitstellung (Active Directory) auf einem virtuellen Windows Server-Computer. Wenn du allerdings über keine traditionelle AD-Bereitstellung und nur über einen einzelnen Azure AD-Mandanten (über Dienste wie Office 365) verfügst, RDS aber trotzdem nutzen möchtest, kannst du mithilfe von [Azure AD Domain Services](/azure/active-directory-domain-services/active-directory-ds-overview) in deiner Azure-IaaS-Umgebung eine vollständig verwaltete Domäne erstellen, die die gleichen Benutzer verwendet, die auch in deinem Azure AD-Client vorhanden sind. Dadurch entfällt die Komplexität durch die manuelle Synchronisierung von Benutzern und die Verwaltung weiterer virtueller Computer. Azure AD Domain Services können sowohl in einer einfachen als auch in einer hoch verfügbaren Bereitstellung verwendet werden.

![Bereitstellung mit Azure AD und RDS](./media/aadds-rds.png)

### <a name="rds-deployment-with-azure-ad-application-proxy"></a>RDS-Bereitstellung mit Azure AD-Anwendungsproxy

In den beiden Standardarchitekturdiagrammen von weiter oben werden RD-Webserver/Gatewayserver als internetseitiger Einstiegspunkt für das RDS-System verwendet. Bei manchen Umgebungen möchten Administratoren allerdings ihre eigenen Server lieber aus der Umgebung entfernen und stattdessen Technologien mit zusätzlicher Sicherheit durch Reverseproxytechnologien verwenden. Die PaaS-Rolle [Azure AD-Anwendungsproxy](/azure/active-directory/active-directory-application-proxy-get-started) ist für ein solches Szenario wie geschaffen.

Informationen zu unterstützten Szenarien sowie zur Einrichtung findest du unter [Veröffentlichen des Remotedesktops per Azure AD-Anwendungsproxy](/azure/active-directory/application-proxy-publish-remote-desktop).

![RDS mit Azure AD-Anwendungsproxy](./media/aadappproxy-rds.png)
