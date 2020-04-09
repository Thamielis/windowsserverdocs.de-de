---
ms.assetid: 6e711a96-9055-4508-b6d4-318d6aa95fd1
title: Anwendungsbereiche für Identitätsdelegierung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7a594332900c8b3afb95c139bcde8458a10f186b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858463"
---
# <a name="when-to-use-identity-delegation"></a>Anwendungsbereiche für Identitätsdelegierung
  
## <a name="what-is-identity-delegation"></a>Was ist Identitätsdelegierung?  
Die Identitäts Delegierung ist ein Feature von Active Directory-Verbunddienste (AD FS) \(AD FS\), das es Administrator\-angegebenen Konten ermöglicht, die Identität von Benutzern anzunehmen. Das Konto, das die Identität des Benutzer annimmt, wird als *Delegat* bezeichnet. Diese Delegierungsmöglichkeit ist für viele verteilte Anwendungen entscheidend, bei denen mehrere Zugriffssteuerungsprüfungen nacheinander für jede Anwendung, Datenbank oder jeden Dienst in der Autorisierungskette für die ursprüngliche Anforderung durchgeführt werden müssen. Viele reale Szenarien in der\-Welt sind vorhanden, in denen die "Front-End"-Webanwendung Daten von einem sichereren "Back-End" abrufen muss, z. b. einem Webdienst, der mit einer Microsoft SQL Server-Datenbank verbunden ist.  
  
So kann z. b. ein vorhandener Teil\-Bestell Website Programm gesteuert erweitert werden, sodass Partnerorganisationen ihren eigenen Kauf Verlauf und den Konto Status einsehen können. Aus Sicherheitsgründen werden alle Partner Finanzdaten in einer sicheren Datenbank auf einem dedizierten strukturierte Abfragesprache \(SQL\)-Server gespeichert. In dieser Situation kennt der Code in der Front\-End-Anwendung nichts über die Finanzdaten der Partnerorganisation. Daher müssen diese Daten von einem anderen Computer an anderer Stelle im Netzwerk abgerufen werden, das hostet \(in diesem Fall\) der Webdienst für die Teile Datenbank \(das Back-End-\).  
  
Damit dieser Daten\-Abruf Vorgang erfolgreich ist, muss eine Abfolge von Autorisierungs "Hand\-schütteln" zwischen der Webanwendung und dem Webdienst für die Teile Datenbank stattfinden, wie in der folgenden Abbildung dargestellt.  
  
![Identitäts Delegierung](media/adfs2_identitydelegationconcept.gif)  
  
Da die ursprüngliche Anforderung an den Webserver selbst gerichtet war, der sich möglicherweise in einer ganz anderen Organisation befindet als der zugreifende Benutzer, entspricht das mit der Anforderung gesendete Sicherheitstoken nicht den Autorisierungskriterien, die für den Zugriff auf andere Computer als den Webserver erforderlich sind. Daher besteht die einzige Möglichkeit, die Anforderung des zugreifenden Benutzers zu erfüllen, in der Bereitstellung eines zwischengeschalteten Verbundservers innerhalb der Ressourcenpartnerorganisation, der ein neues Sicherheitstoken mit den erforderlichen Zugriffsrechten ausstellt.  
  
## <a name="how-does-identity-delegation-work"></a>Wie funktioniert die Identitätsdelegierung?  
Webanwendungen mit Multi-Tier-Anwendungsarchitektur rufen oft Webdienste auf, um gemeinsam genutzte Daten und Funktionen abzurufen. Es ist wichtig für diese Webdienste, die Identität des ursprünglichen Benutzers zu kennen, damit der Dienst Autorisierungsentscheidungen treffen kann und eine Überwachung ermöglicht wird. In diesem Fall stellt die Front\-End-Webanwendung den Benutzer für den Webdienst als Delegat dar. AD FS vereinfacht dieses Szenario, indem es Active Directory Konten ermöglicht, als Benutzer für eine andere vertrauende Seite zu fungieren. Die folgende Abbildung stellt ein solches Szenario mit Identitätsdelegierung dar.  
  
![Identitäts Delegierung](media/adfs2_identitydelegationsteps.gif)  
  
1.  Frank versucht, über eine Webanwendung in einer anderen Organisation auf einen Teil\-Bestellverlauf zuzugreifen. Der Client Computer fordert ein Token von AD FS für den Front\-End-Part\-Order-Webanwendung an und empfängt dieses.  
  
2.  Der Client Computer sendet eine Anforderung an die Webanwendung, einschließlich des in Schritt 1 erhaltenen Tokens, um die Identität des Clients nachzuweisen.  
  
3.  Die Webanwendung muss mit dem Webdienst kommunizieren, um die Transaktion mit dem Client abschließen zu können. Die Webanwendung kontaktiert AD FS, um ein Delegierungs Token für die Interaktion mit dem Webdienst zu erhalten. Delegierungstoken sind Sicherheitstoken, die auf einen Delegaten ausgestellt werden, damit dieser als Benutzer auftritt. AD FS gibt ein Delegierungs Token mit Ansprüchen für den Client zurück, das für den Webdienst vorgesehen ist.  
  
4.  Die Webanwendung verwendet das Token, das in Schritt 3 aus AD FS abgerufen wurde, um auf den Webdienst zuzugreifen, der als Client fungiert. Durch Untersuchen des Delegierungstokens kann der Webdienst erkennen, dass die Webanwendung als Client auftritt. Der Webdienst führt seine Autorisierungsrichtlinie aus, protokolliert die Anforderung und gibt die ursprünglich von Frank angeforderten Teileverlaufsdaten an die Webanwendung und somit an Frank aus.  
  
Bei einem bestimmten Delegaten können AD FS die Webdienste beschränken, für die die Webanwendung möglicherweise ein Delegierungs Token anfordert. Der Clientcomputer muss nicht über ein Active Directory-Konto verfügen, damit dieser Vorgang möglich ist. Der Webdienst kann also problemlos die Identität des Delegaten ermitteln, der als der Benutzer fungiert. Somit können Webdienste unterschiedliches Verhalten zeigen, je nachdem, ob sie direkt mit dem Clientcomputer kommunizieren oder über einen Delegaten.  
  
## <a name="configuring-ad-fs-for-identity-delegation"></a>Konfigurieren von AD FS für die Identitätsdelegierung  
Sie können das\-Snap-in "AD FS Verwaltung" in verwenden, um AD FS für die Identitäts Delegierung zu konfigurieren, wenn Sie den Datenabruf Vorgang vereinfachen müssen. Nachdem Sie Sie konfiguriert haben, können AD FS neue Sicherheits Token generieren, die den Autorisierungs Kontext enthalten, den der Back\-End-Dienst möglicherweise benötigt, bevor er Zugriff auf die geschützten Daten bereitstellen kann.  
  
AD FS schränkt nicht ein, welche Benutzer einen Identitätswechsel durchgeführt haben. Nachdem Sie AD FS für die Identitäts Delegierung konfiguriert haben, werden folgende Aktionen durchführt:  
  
-   Es wird festgelegt, an welche Server die Autorität delegiert werden kann, Token anzufordern, mit denen die Identität von Benutzern angenommen werden kann.  
  
-   Der Identitätskontext für das delegierte Clientkonto und der Server, der als Delegat auftritt, werden festgelegt und separat behandelt.  
  
Sie können die Identitäts Delegierung konfigurieren, indem Sie einer Vertrauensstellung der vertrauenden Seite in der AD FS-Verwaltungs-Snap\-in hinzufügen. Weitere Informationen hierzu finden Sie unter [Checklist: Creating Claim Rules for a Relying Party Trust](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md).  
  
## <a name="configuring-the-front-end-web-application-for-identity-delegation"></a>Konfigurieren der Front\-End-Webanwendung für die Identitäts Delegierung  
Entwicklern stehen verschiedene Optionen zur Verfügung, mit denen Sie die Web-Front\-End-Anwendung oder den Dienst ordnungsgemäß programmieren können, um Delegierungs Anfragen an einen AD FS Computer umzuleiten. Weitere Informationen zum Anpassen von Webanwendungen an die Identitätsdelegierung finden Sie im [Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
