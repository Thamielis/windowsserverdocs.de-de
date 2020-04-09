---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: AD FS-Entwurfshandbuch in Windows Server 2012
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6a9a3e5c8e32b74e059f7a7bbc64c85092a5f047
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853953"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>AD FS Entwurfs Handbuch in Windows Server 


  
> [!NOTE]  
> Informationen zum Bereitstellen von AD FS in Windows Server 2012 R2 finden Sie im [Bereitstellungs Handbuch für Windows Server 2012 R2 AD FS](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md).  
  
Sie können Active Directory&reg; Verbund Dienste \(AD FS\) mit dem Betriebssystem Windows Server&reg; 2012 in einer Verbund Dienstanbieter-Rolle verwenden, um Ihre Benutzer nahtlos bei allen Web\-basierten Diensten oder Anwendungen zu authentifizieren, die sich in einer Ressourcen Partnerorganisation befinden. es ist nicht erforderlich, dass Administratoren externe Vertrauens Stellungen oder Gesamtstruktur-Vertrauens Stellungen zwischen den Netzwerken beider Organisationen erstellen oder verwalten, und ohne dass die Benutzer sich ein zweites Mal anmelden müssen. Der Prozess der Authentifizierung bei einem Netzwerk beim Zugriff auf Ressourcen in einem anderen Netzwerk – ohne die Belastung wiederholter Anmeldeaktionen durch Benutzer – wird als einmaliges\-anmelden auf \(SSO-\)bezeichnet.  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Dieses Handbuch enthält Empfehlungen zum Planen einer neuen Bereitstellung von AD FS, basierend auf den Anforderungen Ihres Unternehmens \(die in diesem Handbuch auch als Bereitstellungs Ziele bezeichnet werden\) und einem bestimmten Entwurf, den Sie erstellen möchten. Dieses Handbuch ist für die Verwendung durch einen Infrastrukturspezialisten oder Systemarchitekten vorgesehen. Es hebt die wichtigsten Entscheidungspunkte hervor, wenn Sie Ihre AD FS Bereitstellung planen. Bevor Sie dieses Handbuch lesen, sollten Sie wissen, wie AD FS auf einer Funktionsebene funktioniert. Außerdem sollten Sie über ein gutes Verständnis der Organisations Anforderungen verfügen, die in Ihrem AD FS Entwurf berücksichtigt werden.  
  
In dieser Anleitung wird eine Reihe von Bereitstellungs Zielen beschrieben, die auf drei primären AD FS Entwürfen basieren, und Sie können Ihnen dabei helfen, den am besten geeigneten Entwurf für Ihre Umgebung zu treffen. Sie können diese Bereitstellungs Ziele verwenden, um einen der folgenden umfassenden AD FS Entwürfe oder einen benutzerdefinierten Entwurf zu bilden, der den Anforderungen Ihrer Umgebung entspricht:  
  
-   Federated-Web-SSO zur Unterstützung von Geschäfts\-für\-Business \(B2B-\) Szenarien und zur Unterstützung der Zusammenarbeit zwischen Geschäftseinheiten mit unabhängigen Gesamtstrukturen  
  
-   Web-SSO zur Unterstützung des Kunden Zugriffs auf Anwendungen in Business\-auf\-Consumer \(B2C\) Szenarien  
  
Sie finden zu jedem Entwurf Richtlinien für das Erfassen der erforderlichen Daten zu Ihrer Umgebung. Anschließend können Sie diese Richtlinien verwenden, um Ihre AD FS-Bereitstellung zu planen und zu entwerfen. Nachdem Sie dieses Handbuch gelesen und das erfassen, dokumentieren und Mapping der Anforderungen Ihrer Organisation abgeschlossen haben, verfügen Sie über die erforderlichen Informationen, um mit der Bereitstellung von AD FS zu beginnen, indem Sie die Anleitung im [Bereitstellungs Handbuch für Windows Server 2012 AD FS bereit](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md)stellen.  
  
## <a name="in-this-guide"></a>In diesem Handbuch  
  
-   [Identifizieren der AD FS-Bereitstellungsziele](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [Bestimmen der AD FS-Bereitstellungstopologie](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [Planen Ihrer Bereitstellung](Planning-Your-Deployment.md)  
  
-   [Planen der Verbundserverplatzierung](Planning-Federation-Server-Placement.md)  
  
-   [Planen der Verbundserverproxy-Platzierung](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [Planen der AD FS-Serverkapazität](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [Anhang A: Überprüfen der AD FS Anforderungen](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

