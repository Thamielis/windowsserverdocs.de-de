---
title: Domänennamenserver (DNS)
description: Dieses Thema enthält eine Übersicht über DNS in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1117e523e23bfc5415754484385d290eb2375d91
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954096"
---
# <a name="domain-name-system-dns"></a>Domänennamenserver (DNS)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Domain Name System (DNS) ist eine der branchenüblichen Protokolle von Protokollen, aus denen TCP/IP besteht. der DNS-Client und der DNS-Server stellen zusammen mit dem DNS-Client und dem DNS-Server Computername-zu-IP-Adress Dienste für Computer und Benutzer bereit.

> [!NOTE]
> Zusätzlich zu diesem Thema ist der folgende DNS-Inhalt verfügbar.
>
> -   [Neues im DNS-Client](What-s-New-in-DNS-Client.md)
> -   [Neues beim DNS-Server](What-s-New-in-DNS-Server.md)
> -   [Handbuch zu DNS-Gruppenrichtlinienszenarien](deploy/DNS-Policy-Scenario-Guide.md)
> -   Video: [Windows Server 2016: DNS-Verwaltung in IPAM](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)

In Windows Server 2016 ist DNS eine Server Rolle, die Sie mithilfe von Server-Manager oder Windows PowerShell-Befehlen installieren können. Wenn Sie eine neue Active Directory Gesamtstruktur und Domäne installieren, wird DNS automatisch mit Active Directory als globaler Katalogserver für die Gesamtstruktur und Domäne installiert.

Active Directory Domain Services (AD DS) verwendet DNS als Domänen Controller-Speicherort Mechanismus. Wenn einer der Prinzipal Active Directory Vorgänge ausgeführt wird, z. b. Authentifizierung, Aktualisierung oder Suche, verwenden Computer DNS, um Active Directory Domänen Controller zu suchen. Außerdem verwenden Domänen Controller DNS, um sich gegenseitig zu suchen.

Der DNS-Client Dienst ist in allen Client-und Serverversionen des Windows-Betriebssystems enthalten und wird standardmäßig bei der Installation des Betriebssystems ausgeführt. Wenn Sie eine TCP/IP-Netzwerkverbindung mit der IP-Adresse eines DNS-Servers konfigurieren, fragt der DNS-Client den DNS-Server ab, um Domänen Controller zu ermitteln und Computernamen in IP-Adressen aufzulösen. Wenn sich beispielsweise ein Netzwerk Benutzer mit einem Active Directory Benutzerkonto bei einer Active Directory Domäne anmeldet, fragt der DNS-Client Dienst den DNS-Server ab, um einen Domänen Controller für die Active Directory Domäne zu suchen. Wenn der DNS-Server auf die Abfrage antwortet und die IP-Adresse des Domänen Controllers für den Client bereitstellt, kontaktiert der Client den Domänen Controller, und der Authentifizierungs Vorgang kann beginnen.

Der DNS-Server für Windows Server 2016 und die DNS-Client Dienste verwenden das DNS-Protokoll, das in der TCP/IP-Protokoll Suite enthalten ist. DNS ist Teil der Anwendungsebene des TCP/IP-Referenzmodells, wie in der folgenden Abbildung dargestellt.

![DNS in TCP/IP](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)


