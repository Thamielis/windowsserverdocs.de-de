---
title: Übersicht über das Testumgebungsszenario
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: ce584811-b209-48fe-ab2b-4c399bd0bd79
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 39b6212714ebf868b91c1b28f35cc6a5149828ca
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860323"
---
# <a name="overview-of-the-test-lab-scenario"></a>Übersicht über das Testumgebungsszenario

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Der Remote Zugriff ist eine Server Rolle in den Betriebssystemen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, die Remote Benutzern den sicheren Zugriff auf interne Netzwerkressourcen über DirectAccess oder virtuelle private Netzwerke (Virtual Private Networks, VPNs) mit dem RRAS (Routing and Remote Access Service). Diese Anleitung enthält Schritt-für-Schritt-Anweisungen zum Erweitern der [Test Umgebungs Anleitung: veranschaulichen der Einrichtung von DirectAccess Single Server mit gemischtem IPv4 und IPv6](https://go.microsoft.com/fwlink/p/?LinkId=237004) , um eine Konfiguration des einmaligen Zugriffs per Remote Zugriff zu veranschaulichen.  
  
> [!WARNING]  
> Der Entwurf dieser Test Umgebungs Anleitung umfasst Infrastruktur Server, z. b. einen Domänen Controller und eine Zertifizierungsstelle (Certification Authority, ca), auf denen entweder Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Die Verwendung dieser Test Umgebungs Anleitung zum Konfigurieren von Infrastruktur Servern, auf denen andere Betriebssysteme ausgeführt werden, wurde nicht getestet, und Anweisungen zum Konfigurieren anderer Betriebssysteme sind in diesem Handbuch nicht enthalten.  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Der Remote Zugriff in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 bietet Unterstützung für die Client Authentifizierung mit OTP. Im Rahmen dieser Testumgebung wird nur RSA SecurID verwendet, um die OTP-Funktionalität mit Remote Zugriff zu veranschaulichen. Andere auf RADIUS basierende OTP-Lösungen werden ebenfalls unterstützt, sind jedoch außerhalb des Umfangs dieses Testlabors. Diese Anleitung enthält Anweisungen zum Konfigurieren und Veranschaulichen des Remotezugriffs mit sechs Servern und zwei Clientcomputern. Der abgeschlossene Remote Zugriff mit OTP-Test Labor simuliert ein Intranet, das Internet und ein Heimnetzwerk und veranschaulicht die Remote Zugriffs Funktionalität in verschiedenen Internetverbindungs Szenarien.  
  
> [!IMPORTANT]  
> Diese Testumgebung ist eine Machbarkeitsstudie mit der minimalen Anzahl an Computern. Die in dieser Anleitung beschriebene Konfiguration ist nur für Testzwecke geeignet und sollte nicht in einer Produktionsumgebung verwendet werden.  
  


