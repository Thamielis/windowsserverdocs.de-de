---
title: Überwachen der Aktivitäten und des Status von verbundenen Remoteclients
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: beb94475-b21f-46a9-ac51-bf2bb28ca94e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 831b429c69bdeac7a9e0aec69a7f79bf385f321f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970227"
---
# <a name="monitor-connected-remote-clients-for-activity-and-status"></a>Überwachen der Aktivitäten und des Status von verbundenen Remoteclients

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

**Hinweis:** Windows Server 2012 kombiniert DirectAccess und RAS-Dienst (RAS) zu einer einzigen Remote Zugriffs Rolle.

Sie können die-Verwaltungskonsole auf dem Remote Zugriffs Server verwenden, um die Remote Client Aktivität und den Status zu überwachen.

> [!NOTE]
> Sie müssen auf jedem Computer als Mitglied der Gruppe "Domänen-Admins" oder "Administratoren" angemeldet sein, um die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht ausführen können, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Administratoren" ist, versuchen Sie, die Aufgabe auszuführen, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Domänen-Admins" ist.

#### <a name="to-monitor-remote-client-activity-and-status"></a>So überwachen Sie die Remote Client Aktivität und den Status

1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.

2.  Klicken Sie auf **Berichterstattung** , um in der **Remote Zugriffs-Verwaltungskonsole**zur **Remote Zugriffs Berichterstattung** zu navigieren.

3.  Klicken Sie auf **Remote Client Status** , um in der **Remote Zugriffs-Verwaltungskonsole**in der Remote Zugriffs-Verwaltungskonsole zur Remote Client Aktivität und zur Benutzeroberfläche

4.  Es wird eine Liste der Benutzer angezeigt, die mit dem RAS-Server verbunden sind, sowie ausführliche Statistiken zu diesen. Klicken Sie auf die erste Zeile in der Liste, die einem Client entspricht. Wenn Sie eine Zeile auswählen, wird die Remote Benutzeraktivität im Vorschaubereich angezeigt.

![Äquivalente Windows PowerShell-Befehle in Windows](../../../media/Monitor-connected-remote-clients-for-activity-and-status/PowerShellLogoSmall.gif)***<em>PowerShell</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
PS> Get-RemoteAccessConnectionStatistics
```

Die Benutzerstatistiken können mithilfe der Felder in der folgenden Tabelle gefiltert werden, basierend auf der Kriterienauswahl.

|Feldname|Wert|
|-------|-----|
|Username|Der Benutzername oder das Alias des Remotebenutzers. Platzhalter Zeichen können verwendet werden, um eine Gruppe von Benutzern (z. b. "Configuration Manager") oder "\administrator" "auszuwählen. \\ \*|
|Hostname|Der Name des Computerkontos des Remotebenutzers. Außerdem kann eine IPv4-oder IPv6-Adresse angegeben werden.|
|Typ|DirectAccess oder VPN. Wenn DirectAccess ausgewählt ist, werden alle Remote Benutzer, die über DirectAccess verbunden sind, aufgeführt. Wenn VPN ausgewählt wird, werden alle Remote Benutzer aufgelistet, die über VPN verbunden sind.|
|ISP-Adresse|Die IPv4- oder IPv6-Adresse des Remotebenutzers.|
|IPv4-Adresse|Die innere IPv4-Adresse des Tunnels, der den Remote Benutzer mit dem Unternehmensnetzwerk verbindet.|
|IPv6-Adresse|Die interne IPv6-Adresse des Tunnels, über den der Remotebenutzer mit dem Unternehmensnetzwerk verbunden ist.|
|Protokoll//Tunnel|Die Übergangstechnologie, die vom Remote Client verwendet wird. Dies ist Teredo, 6de4 oder IP-HTTPS für DirectAccess-Benutzer, und es ist PPTP, L2TP, SSTP oder IKEv2 für VPN-Benutzer.|
|Aufgerufene Ressource|Alle Benutzer, die auf eine bestimmte Unternehmensressource oder einen bestimmten Unternehmensendpunkt zugreifen. Der Wert, der diesem Feld entspricht, ist der Hostname/die IP-Adresse des Servers.|
|Server|Der RAS-Server, mit dem Clients verbunden sind. Dies ist nur für Clusterbereitstellungen und Bereitstellungen für mehrere Standorte relevant.|





