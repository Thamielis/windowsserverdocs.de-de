---
title: What's New for Managed Service Accounts
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 2f2a8b6b-c152-4c40-b712-bfabff0e408b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: f3b003ebe9ce766f39e10a21e0fa4002db562773
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639591"
---
# <a name="what39s-new-for-managed-service-accounts"></a>Neues für verwaltete Dienst Konten&#39;

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Experten werden die Funktionsänderungen für verwaltete Dienst Konten mit der Einführung des Gruppen verwalteten Dienst Kontos (Group Managed Service Account, GMSA) in Windows Server 2012 und Windows 8 beschrieben.

Das verwaltete Dienstkonto wurde entwickelt, damit Dienste und Aufgaben wie Windows-Dienste und ISS-Anwendungspools eigene Domänenkonten zur Verfügung stellen und dabei die Anforderung an Administratoren wegfällt, diesen Konten manuell Kennwörter zuweisen zu müssen. Die automatische Kennwortverwaltung wird von verwalteten Domänenkonten bereitgestellt.

## <a name="whats-new-for-managed-service-accounts-in-windows-server-2012-and-windows-8"></a><a name="versions"></a>Neues für verwaltete Dienst Konten unter Windows Server 2012 und Windows 8
Im folgenden wird beschrieben, welche Änderungen an der Funktionalität von MSA in Windows Server 2012 und Windows 8 vorgenommen wurden.

### <a name="group-managed-service-accounts"></a>Gruppenverwaltete Dienstkonten
Wenn ein Domänenkonto für einen Server in einer Domäne konfiguriert wird, kann sich der Clientcomputer bei diesem Gerät authentifizieren und eine Verbindung dazu herstellen. Zuvor stellen nur zwei Kontotypen eine Identität zur Verfügung, ohne dass die Kennwortverwaltung erforderlich war. Diese Kontotypen haben jedoch Einschränkungen:

-   Das Computerkonto ist auf einen Domänenserver beschränkt und die Kennwörter werden vom Computer verwaltet.

-   Das verwaltete Dienstkonto ist auf einen Domänenserver beschränkt und die Kennwörter werden vom Computer verwaltet.

Diese Konten können nicht über mehrere Systeme hinweg freigegeben werden. Aus diesem Grund muss das Konto im Hinblick auf alle Dienste auf allen Systemen regelmäßig gewartet werden, um zu verhindern, dass das Kennwort unbeabsichtigterweise abläuft.

**Welchen Nutzen bietet diese Änderung?**

Das Gruppen verwaltete Dienst Konto löst dieses Problem, da das Konto Kennwort von Windows Server 2012-Domänen Controllern verwaltet wird und von mehreren Windows Server 2012-Systemen abgerufen werden kann. Das minimiert den administrativen Mehraufwand eines Dienstkontos, indem Windows gestattet wird, die Kennwortverwaltung für diese Konten zu übernehmen.

**Worin bestehen die Unterschiede?**

Auf Computern, auf denen Windows Server 2012 oder Windows 8 ausgeführt wird, kann eine Gruppen-MSA über den Dienststeuerungs-Manager erstellt und verwaltet werden, sodass zahlreiche Instanzen des Dienstanbieter, z. b. über eine Serverfarm bereitgestellt, von einem Server aus verwaltet werden können. Tools und Hilfsprogramme zur Verwaltung von verwalteten Dienstkonten, etwa der ISS-Anwendungspoolmanager, können mit gruppenverwalteten Dienstkonten verwendet werden. Domänenadministratoren können die Dienstverwaltung an Dienstadministratoren delegieren, die den gesamten Lebenszyklus eines verwalteten oder gruppenverwalteten Dienstkontos verwalten können. Bestehende Clientcomputer können sich bei allen solchen Diensten authentifizieren, ohne zu wissen, bei welcher Dienstinstanz sie das tun.

### <a name="removed-or-deprecated-functionality"></a><a name="interoperability"></a>Entfernte oder veraltete Funktionen
Für Windows Server 2012 werden die Windows PowerShell-Cmdlets standardmäßig für die Verwaltung der Gruppen verwalteten Dienst Konten anstelle der Server verwalteten Dienst Konten verwendet.

## <a name="additional-references"></a>Weitere Verweise

-   [Übersicht über Gruppen verwaltete Dienst Konten](group-managed-service-accounts-overview.md)

-   [Übersicht über die Active Directory Domain Services](active-directory-domain-services-overview.md)

-   [Verwaltete Dienstkonten: Grundlegendes, Implementierung, bewährte Methoden und Problembehandlung](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/managed-service-accounts-understanding-implementing-best/ba-p/397009)


