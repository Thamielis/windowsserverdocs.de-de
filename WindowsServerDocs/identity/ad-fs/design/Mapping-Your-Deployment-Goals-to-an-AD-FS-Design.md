---
ms.assetid: 68979914-8a1c-465a-bd37-08df30722d69
title: Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4154f46bdb1a7b3a2c81eba6882a6a095a16ee45
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853053"
---
# <a name="mapping-your-deployment-goals-to-an-ad-fs-design"></a>Zuordnen der Bereitstellungsziele zu einem AD FS-Entwurf


Nachdem Sie die vorhandenen Active Directory-Verbunddienste (AD FS) \(AD FS\) Bereitstellungs Ziele überprüft und bestimmt haben, welche Ziele mit Ihrer Bereitstellung in Zusammenhang stehen, können Sie diese Ziele einem bestimmten AD FS Entwurf zuordnen. Weitere Informationen zu AD FS vordefinierten Bereitstellungs Zielen finden [Sie unter Ermitteln Ihrer AD FS Bereitstellungs Ziele](Identifying-Your-AD-FS-Deployment-Goals.md).  
  
Verwenden Sie die folgende Tabelle, um zu bestimmen, welcher AD FS Entwurf der entsprechenden Kombination von AD FS Bereitstellungs Zielen für Ihre Organisation entspricht. Diese Tabelle bezieht sich nur auf die beiden primären AD FS Entwürfe, wie in diesem Handbuch beschrieben. Sie können jedoch einen Hybrid-oder benutzerdefinierten AD FS Entwurf erstellen, indem Sie eine beliebige Kombination der AD FS Bereitstellungs Ziele verwenden, um die Anforderungen Ihrer Organisation zu erfüllen.  
  
|AD FS Bereitstellungs Ziel|[Web-SSO-Entwurf](Web-SSO-Design.md)|[Federated-Web-SSO-Entwurf](Federated-Web-SSO-Design.md)|  
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|[Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)|Nein|Ja, im Kontopartner|  
|[Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)|Nein|Nein, optional im Kontopartner|  
|[Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für die Benutzer anderer Organisationen](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)|Ja|Ja|  

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
  

