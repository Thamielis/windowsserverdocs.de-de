---
title: Neues im DNS-Client unter Windows Server
description: Dieses Thema bietet einen Überblick über die neuen Features im DNS-Client unter Windows Server und Windows 10.
manager: brianlic
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 772fedf497691834e6b894f61bd01c284ec24c16
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971807"
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>Neues im DNS-Client unter Windows Server 2016

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden die Funktionen des Domain Name System (DNS) beschrieben, die in Windows 10 und Windows Server 2016 und höheren Versionen dieser Betriebssysteme neu sind oder geändert wurden.

## <a name="updates-to-dns-client"></a>Updates für den DNS-Client

**DNS-Client Dienst Bindung**: in Windows 10 bietet der DNS-Client Dienst eine verbesserte Unterstützung für Computer mit mehr als einer Netzwerkschnittstelle. Bei mehrfach vernetzten Computern wird die DNS-Auflösung wie folgt optimiert:

-   Wenn ein DNS-Server, der auf einer bestimmten Schnittstelle konfiguriert ist, verwendet wird, um eine DNS-Abfrage aufzulösen, wird der DNS-Client Dienst vor dem Senden der DNS-Abfrage an diese Schnittstelle gebunden.

    Durch die Bindung an eine bestimmte Schnittstelle kann der DNS-Client die Schnittstelle, an der die Namensauflösung erfolgt, eindeutig angeben, sodass Anwendungen die Kommunikation mit dem DNS-Client über diese Netzwerkschnittstelle optimieren können.

-   Wenn der verwendete DNS-Server durch eine Gruppenrichtlinie Einstellung aus der Richtlinien Tabelle für die Namensauflösung (Name Resolution Policy Table, NRPT) bestimmt wird, wird der DNS-Client Dienst nicht an eine bestimmte Schnittstelle gebunden.

> [!NOTE]
> Änderungen am DNS-Client Dienst in Windows 10 sind auch auf Computern vorhanden, auf denen Windows Server 2016 und höhere Versionen ausgeführt werden.

## <a name="additional-references"></a>Weitere Verweise

-   [Neues in DNS-Server unter Windows Server 2016](What-s-New-in-DNS-Server.md)


