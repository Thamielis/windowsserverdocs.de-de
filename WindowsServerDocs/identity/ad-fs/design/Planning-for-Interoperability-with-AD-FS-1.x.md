---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: Planen der Interoperabilität mit AD FS 1.x
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0bbf64a7bf110e3d73084dd047c84b2b83be8d9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858613"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>Planen der Interoperabilität mit AD FS 1.x

Active Directory-Verbunddienste (AD FS) \(AD FS\) Verbund Servern, auf denen Windows Server&reg; 2012 ausgeführt wird, mit einer AD FS 1,0-\(zusammenarbeiten können, die mit Windows Server 2003 R2\) Verbunddienst installiert wurde, und AD FS 1,1 \(mit Windows Server 2008 oder Windows Server 2008 R2\) Verbunddienst installiert wurde. Eine der folgenden Interoperabilitätskombinationen werden unterstützt:  

-   Alle AD FS 1. *x* Verbunddienst können einen Anspruch senden, der von einem AD FS Verbunddienst in Windows Server 2012 verwendet werden kann. Weitere Informationen finden Sie unter Prüfliste [: Konfigurieren von AD FS für die Nutzung von Ansprüchen AD FS 1. x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md).  

-   Alle AD FS Verbunddienst in Windows Server 2012 können eine AD FS 1 senden. *x*\-kompatibler Anspruch, der von einem AD FS 1 verwendet werden kann. *x* -Verbunddienst. Weitere Informationen finden Sie unter [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md).  

-   Alle AD FS Verbunddienst in Windows Server 2012 können eine AD FS 1 senden. *x*\-kompatibler Anspruch, der von einem oder mehreren Webservern genutzt werden kann, auf denen die AD FS 1 ausgeführt wird. *x* Claims\-aware Web Agent. Weitere Informationen finden Sie unter [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md).  

> [!NOTE]  
> AD FS unterstützt oder interagiert nicht mit AD FS 1. *x* Windows NT Token – basierter Web-Agent.  

Eine AD FS 1. *x*\-kompatibler Anspruch ist ein Anspruch, der von einem AD FS Verbunddienst in Windows Server 2012 gesendet und durch einen AD FS 1 interpretiert werden kann. *x* -Verbunddienst. Ein AD FS 1. *x* Verbunddienst die von einem Verbunddienst AD FS gesendeten Ansprüche verarbeiten können, muss eine namens Kennung \(ID\) Anspruchstyp gesendet werden.  

## <a name="understanding-the-name-id-claim-type"></a>Grundlegendes zum Namensbezeichner (ID)-Anspruchstyp  
Der Namensbezeichner (ID)-Anspruchstyp ist die Entsprechung des Identitätsanspruchstyps, der von AD FS 1.*x* verwendet wird. Dieser Typ muss verwendet werden, wenn die Interoperabilität mit AD FS 1.*x*gewünscht wird. Der Anspruchstyp Name ID aktiviert entweder eine AD FS 1. *x* Verbunddienst oder die AD FS 1. *x* beansprucht\-fähigen Web-Agent, um Ansprüche zu verarbeiten, die in Windows Server 2012-Sendungen AD FS, solange diese Ansprüche in einem der namens-ID-Formate in der folgenden Tabelle gesendet werden.  


|      Namensbezeichnerformat       |               Entsprechender URI                |
|---------------------------|------------------------------------------------|
| AD FS 1.*x* -E-Mailadresse | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* -E-Mail-UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        Allgemeiner Name        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           Gruppe           |    http://schemas.xmlsoap.org/claims/Group     |

Es muss nur ein Anspruch im entsprechenden Namensbezeichnerformat gesendet werden. Wenn dieses Kriterium erfüllt ist, können viele andere Ansprüche auch gesendet werden, vorausgesetzt, dass sie den in der Tabelle beschriebenen Einschränkungen entsprechen.  

> [!NOTE]  
> Eine AD FS 1. *x* Verbunddienst kann nur eingehende Anspruchs Typen interpretieren, die mit dem Uniform Resource Identifier \(-URI\) von http://schemas.xmlsoap.org/claims/beginnen.  

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
