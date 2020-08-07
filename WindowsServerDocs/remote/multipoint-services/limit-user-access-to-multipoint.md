---
title: Einschränken des Benutzer Zugriffs auf den Server
description: Erfahren Sie, wie Sie den Zugriff auf Multipoint Services für Benutzer und Gruppen gewähren oder verweigern.
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 4cabd4f1-a764-4be6-bc6e-0a5f5566390c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 436ffc0b3056e17aa4cdcc12a2ee38cce68304f3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970487"
---
# <a name="limit-users-access-to-the-multipoint-server"></a>Einschränken des Zugriffs von Benutzern auf den Multipoint-Server
Unabhängig davon, ob Sie einen Multipoint-Server einer Active Directory Domäne hinzufügen oder lokale Benutzerkonten verwenden, haben alle Benutzer standardmäßig Zugriff auf Multipoint Server. Bevor Sie es Benutzern ermöglichen, sich an Stationen in ihrer Multipoint Services-Umgebung anzumelden, sollten Sie den Zugriff auf den Server einschränken.

Alle Benutzer in der Gruppe Remotedesktop Benutzer können sich bei Multipoint Server anmelden. Standardmäßig ist die Benutzergruppe "jeder" Mitglied der Gruppe "Remotedesktop Users". Daher können sich alle lokalen Benutzer und Domänen Benutzer am Multipoint-Server anmelden. Entfernen Sie zum Einschränken des Zugriffs auf Multipoint Server die Gruppe Jeder Benutzer aus der Gruppe Remotedesktop Benutzer, und fügen Sie dann der Gruppe Remotedesktop Benutzer bestimmte Benutzer oder Gruppen hinzu.

## <a name="add-or-remove-users-or-groups-to-the-remote-desktop-users-group"></a>Hinzufügen oder Entfernen von Benutzern oder Gruppen zur Gruppe "Remotedesktop Benutzer"

1.  Öffnen Sie auf dem **Start** Bildschirm die **Computer Verwaltung**.

2.  Klicken Sie in der Konsolen Struktur unter **lokale Benutzer und Gruppen**auf **Gruppen**.

3.  Doppelklicken Sie auf **Remotedesktop Benutzer**, und befolgen Sie die Anweisungen zum Hinzufügen oder Entfernen von Benutzern.

    -   Entfernen Sie die Gruppe Jeder, um den allgemeinen Zugriff auf den Server einzuschränken.

    -   Fügen Sie der Gruppe Remotedesktop Benutzer jedes lokale Konto oder jedes Domänen Benutzer-oder Gruppenkonto hinzu, um den Multipoint Server-Benutzern Zugriff auf Stationen zu geben.