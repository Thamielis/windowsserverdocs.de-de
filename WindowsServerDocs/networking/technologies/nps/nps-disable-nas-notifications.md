---
title: Deaktivieren der NAS-Benachrichtigungs Weiterleitung in NPS
description: Dieses Thema enthält Anweisungen zum Konfigurieren der gleichzeitigen Authentifizierungen von Netzwerk Richtlinien Servern in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: a09bfb03-95fc-4534-bf3c-97078ef6b07e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 72ac7d13005fef609df437ce3fcb4e12f617a400
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946974"
---
# <a name="disable-nas-notification-forwarding-in-nps"></a>Deaktivieren der NAS-Benachrichtigungs Weiterleitung in NPS

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe dieses Verfahrens können Sie die Weiterleitung von Nachrichten zum Starten und Abbrechen von Netzwerk Zugriffs Servern (nass) an Mitglieder einer Remote-RADIUS-Server Gruppe deaktivieren, die in NPS konfiguriert ist.

Wenn Sie Remote-RADIUS-Server Gruppen konfiguriert haben und Sie in NPS- **Verbindungs Anforderungs Richtlinien**das Kontrollkästchen **Buchhaltungs Anforderungen an diese Remote-RADIUS-Server Gruppe weiterleiten** deaktivieren, werden diese Gruppen weiterhin vom NAS-Start-und-Beenden von Benachrichtigungs Meldungen gesendet.

Dadurch wird unnötiger Netzwerk Datenverkehr erstellt. Deaktivieren Sie die NAS-Benachrichtigungs Weiterleitung für einzelne Server in jeder RADIUS-Remote Server Gruppe, um diesen Datenverkehr auszuschließen.

Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.

### <a name="to-disable-nas-notification-forwarding"></a>Deaktivieren der NAS-Benachrichtigungs Weiterleitung

1. Klicken Sie im Server-Manager auf **Tools** und dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und-Server**, klicken Sie auf Remote-RADIUS- **Server Gruppen**, und doppelklicken Sie dann auf die Remote-RADIUS-Server Gruppe, die Sie konfigurieren möchten. Das Dialogfeld Remote-RADIUS-Server Gruppen **Eigenschaften** wird geöffnet.

3. Doppelklicken Sie auf das Gruppenmitglied, das Sie konfigurieren möchten, und klicken Sie dann auf die Registerkarte **Authentifizierung/Buchhaltung** .

4. Deaktivieren Sie in der **Buchhaltung**das Kontrollkästchen **Netzwerk Zugriffs Server-Benachrichtigungen an diesen Server starten und beenden** , und klicken Sie dann auf **OK**.

5. Wiederholen Sie die Schritte 3 und 4 für alle Mitglieder der Gruppe, die Sie konfigurieren möchten.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerk Richtlinien Servers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
