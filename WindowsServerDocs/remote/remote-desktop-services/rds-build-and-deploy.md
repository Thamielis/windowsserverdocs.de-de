---
title: 'RDS: Erstellen und Bereitstellen'
description: Schritte zum Erstellen einer Remotedesktopbereitstellung
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/18/2017
ms.topic: article
ms.assetid: 176ae424-96e9-4c78-88f5-da418e76c3d7
author: lizap
manager: dongill
ms.openlocfilehash: ce8c6e2089c3130d078513287b661a42e5754690
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857603"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>Erstellen und Bereitstellen deiner Remotedesktopdienste-Bereitstellung

Bei einer Remotedesktopdienste-Bereitstellung handelt es sich um die Infrastruktur, die zum Freigeben von Apps und Ressourcen für deine Benutzer verwendet wird. Abhängig von der bereitzustellenden Umgebung kannst du die Infrastruktur nach Bedarf einfach oder komplex gestalten. Remotedesktopbereitstellungen können mühelos skaliert werden. Du kannst nach Belieben Webzugriffs-, Gateway-, Verbindungsbroker- und Sitzungshostserver für Remotedesktop hinzufügen und entfernen. Du kannst den Remotedesktop-Verbindungsbroker zum Verteilen von Workloads verwenden. Dank Active Directory-basierter Authentifizierung wird eine äußerst sichere Umgebung bereitgestellt. 

[Remotedesktopclients](clients/remote-desktop-clients.md) ermöglichen Zugriff von jedem Windows-, Apple- oder Android-Computer, Tablet oder Smartphone aus.

Eine ausführliche Erläuterung der verschiedenen Komponenten, aus denen sich deine Remotedesktopdienste-Bereitstellung zusammensetzt, findest du unter [Architektur der Remotedesktopdienste](desktop-hosting-logical-architecture.md).

Deine vorhandene Remotedesktopbereitstellung basiert auf einer älteren Version von Windows Server? Sieh dir die Optionen für die Migration zu Windows Server 2016 an, und nutze neue und bessere Funktionen für Leistung und Skalierung:

- [Migrate your RDS deployment to Windows Server 2016](migrate-rds-role-services.md) (Migrieren deiner RDS-Bereitstellung zu Windows Server 2016)
- [Upgrade your RDS deployment to Windows Server 2016](upgrade-to-rds-2016.md) (Aktualisieren deiner RDS-Bereitstellung auf Windows Server 2016)

Du möchtest eine neue Remotedesktopbereitstellung erstellen? Du kannst Remotedesktop anhand der folgenden Informationen unter Windows Server 2016 bereitstellen:

- [Deploy the Remote Desktop Services infrastructure](rds-deploy-infrastructure.md) (Bereitstellen der Remotedesktopdienste-Infrastruktur)
- [Create a session collection to hold the apps and resources you want to share](rds-create-collection.md) (Erstellen einer Sitzungssammlung für die freizugebenden Apps und Ressourcen)
- [License your RDS deployment with client access licenses (CALs)](rds-client-access-license.md) (Lizenzieren deiner RDS-Bereitstellung mit Clientzugriffslizenzen (CALs))
- Fordere deine Benutzer auf, einen [Remotedesktopclient](clients/remote-desktop-clients.md) zu installieren, sodass sie auf die Apps und Ressourcen zugreifen können. 
- Ermögliche Hochverfügbarkeit, indem du zusätzliche Verbindungsbroker und Sitzungshosts hinzufügst:
   - [Horizontales Skalieren einer vorhandenen RDS-Sammlung mit einer RD-Sitzungshostfarm](rds-scale-rdsh-farm.md)
   - [Hinzufügen von hoher Verfügbarkeit zur RD Connection Broker-Infrastruktur](rds-connection-broker-cluster.md)
   - [Hinzufügen von hoher Verfügbarkeit zur RD Web- und RD Gateway-Webfront](rds-rdweb-gateway-ha.md)
   - [Bereitstellen eines auf zwei Knoten und „Direkte Speicherplätze“ basierenden Dateisystems für die UPD-Speicherung](rds-storage-spaces-direct-deployment.md)


Wenn du Hostingpartner bist und dich für die Bereitstellung von Apps und Ressourcen für Kunden mithilfe von Remotedesktop interessierst oder ein Kunde auf der Suche nach einer Person bist, die deine Apps hostet, sieh dir den Artikel [Remotedesktopdienste – Hostingpartner](rds-hosting-partners.md) an. Dort findest du Informationen zu einer Bewertung, mit der du die Verwendung von RDS in Azure als Hostingumgebung evaluieren kannst, sowie eine Liste mit Partnern, die diese Bewertung bestanden haben.
