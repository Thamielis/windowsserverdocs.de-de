---
ms.assetid: 8890ccc9-068d-4da2-bd51-8a2964173ff1
title: Verbundserverfarm mit WID und Proxys
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9c6dba880b80de43bb713d1b4495f0e03d56a695
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853093"
---
# <a name="federation-server-farm-using-wid-and-proxies"></a>Verbundserverfarm mit WID und Proxys

Diese Bereitstellungs Topologie für Active Directory-Verbunddienste (AD FS) \(AD FS\) ist mit der Verbund Serverfarm mit der internen Windows-Datenbank \(wid\) Topologie identisch, fügt jedoch Verbund Server Proxys zum Umkreis Netzwerk hinzu, um externe Benutzer zu unterstützen. Die Verbund Server Proxys leiten Client Authentifizierungsanforderungen, die von außerhalb Ihres Unternehmensnetzwerks stammen, an die Verbund Serverfarm weiter.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Bereitstellungs Topologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit 100 oder weniger konfigurierten Vertrauens Stellungen, die sowohl interne als auch externe Benutzer \(, die bei Computern angemeldet sind, die sich physisch außerhalb des Unternehmensnetzwerks befinden\) mit einmaligem\-anmelden \(SSO\) Zugriff auf Verbund Anwendungen oder-Dienste.  
  
-   Organisationen, die sowohl internen als auch externen Benutzern SSO-Zugriff auf Microsoft Office 365 bereitstellen müssen  
  
-   Kleinere Unternehmen, die externe Benutzer haben und redundante, skalierbare Dienste benötigen  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Die gleichen Vorteile wie für die Verbund [Server Farm mit der wid](Federation-Server-Farm-Using-WID-2012.md) -Topologie sowie die Vorteile der Bereitstellung von zusätzlichem Zugriff für externe Benutzer.  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Die gleichen Einschränkungen wie für die Verbund [Server Farm werden mithilfe der wid](Federation-Server-Farm-Using-WID-2012.md) -Topologie aufgelistet.  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Empfehlungen zur Server Platzierung und zum Netzwerk Layout  
Um diese Topologie zusätzlich zum Hinzufügen von zwei Verbund Server Proxys bereitzustellen, müssen Sie sicherstellen, dass Ihr Umkreis Netzwerk auch Zugriff auf eine Domain Name System \(DNS-\) Servers und auf einen zweiten Netzwerk Lastenausgleich \(NLB-\) Host bereitstellen kann. Der zweite NLB-Host muss mit einem NLB-Cluster konfiguriert werden, der eine IP-Adresse für den Internet\-zugänglichen Cluster verwendet, und er muss die gleiche DNS-Namen Einstellung des Clusters wie der vorherige NLB-Cluster verwenden, den Sie im Unternehmensnetzwerk \(FS.fabrikam.com\)konfiguriert haben. Die Verbund Server Proxys sollten auch mit Internet\-zugänglichen IP-Adressen konfiguriert werden.  
  
In der folgenden Abbildung wird die vorhandene Verbund Serverfarm mit der zuvor beschriebenen wid-Topologie gezeigt und erläutert, wie das fiktive Fabrikam, Inc. Unternehmen Zugriff auf einen DNS-Umkreis Server bereitstellt, einen zweiten NLB-Host mit dem gleichen DNS-Cluster Namen \(FS.fabrikam.com\)hinzufügt und dem Umkreis Netzwerk zwei Verbund Server Proxys \(fsp1-und fsp2-\) hinzufügt.  
  
![Serverfarm mit wid](media/FarmWIDProxies.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbund Servern oder Verbund Server Proxys finden Sie unter Anforderungen für die [Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Servers.md) oder [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
