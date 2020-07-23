---
title: 'AD FS Problembehandlung: DNS-Auflösung'
description: In diesem Dokument wird beschrieben, wie Sie die Problembehandlung für DNS-Aspekte AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a9be4a72cd60cfdd5807c67132dba837093be4db
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959022"
---
# <a name="ad-fs-troubleshooting---dns"></a>AD FS Problembehandlung: DNS 
Eine der ersten Überprüfungen, wenn AD FS nicht funktioniert oder antwortet, ist die DNS-Namensauflösung.  Dabei handelt es sich um grundlegende Tests, um zu bestimmen, ob die AD FS Server oder WAP-Server in Ihrem Netzwerk gefunden werden.  Bei internen Benutzern sollten diese Tests auf die AD FS Server (STS) aufgelöst werden.    Für externe Benutzer sollten diese Tests auf die WAP-Server aufgelöst werden.

Im restlichen Teil dieses Dokuments erfahren Sie, wie Sie mithilfe von Befehlszeilen Tools einige schnelle namens Auflösungs Prüfungen durchführen.

## <a name="ping-test"></a>Ping-Test
Überprüft die Konnektivität auf IP-Ebene zu einem anderen TCP/IP-Computer, indem ICMP-Echo Anforderungs Nachrichten (Internet Control Message Protocol) gesendet werden. Der Empfang entsprechender Echo Antwort Nachrichten wird zusammen mit Roundtrip-Zeiten angezeigt.  Weitere Informationen finden Sie unter [Ping](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff961503(v=ws.11)).


>[!NOTE]
>Beachten Sie, dass einige Unternehmen diesen Port auf Ihren Servern blockieren, und Sie erhalten möglicherweise eine **Anforderungs Timeout** Antwort.

### <a name="to-use-a-ping-test"></a>So verwenden Sie einen Pingtest
1.  Öffnen Sie eine Eingabeaufforderung.
2. Geben Sie ping <name of adfs server> a ein. Beispiel: Ping STS.contoso.com
3. Es sollte eine Antwort vom Server angezeigt werden.

![Pingen](media/ad-fs-tshoot-dns/dns1.png)

## <a name="nslookup"></a>Nslookup
Zeigt Informationen an, die Sie verwenden können, um Domain Name System (DNS)-Infrastruktur zu diagnostizieren.  Weitere Informationen finden Sie unter [nslookup](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc725991(v=ws.11)).

### <a name="to-use-a-nslookup"></a>So verwenden Sie ein nslookup
1.  Öffnen Sie eine Eingabeaufforderung.
2. Geben Sie ping <name of adfs server> a ein. Beispiel: nslookup STS.contoso.com
3. Die DNS-Informationen für den Server ![ nslookup sollten angezeigt werden.](media/ad-fs-tshoot-dns/dns2.png)

## <a name="tracert"></a>Tracert
Bestimmt den Pfad zu einem Ziel, indem ICMP-Echo Anforderungen (Internet Control Message Protocol) oder ICMPv6-Nachrichten an das Ziel gesendet werden, wobei die Werte für die Gültigkeitsdauer (TTL) inkrementell erhöht werden.   Weitere Informationen finden Sie unter [tracert](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff961507(v=ws.11)).


### <a name="to-use-tracert"></a>So verwenden Sie tracert
1.  Öffnen Sie eine Eingabeaufforderung.
2. Geben Sie tracert <name of adfs server> a ein. Beispiel: tracert STS.contoso.com
3. Der Zielpfad, der zum Erreichen des Server tracert verwendet wird, sollte angezeigt werden. ![](media/ad-fs-tshoot-dns/dns3.png)

## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)
