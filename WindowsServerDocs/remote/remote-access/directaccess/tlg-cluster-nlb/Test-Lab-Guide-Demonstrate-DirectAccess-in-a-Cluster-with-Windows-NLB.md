---
title: 'Test Umgebungs Anleitung: veranschaulichen von DirectAccess in einem Cluster mit Windows NLB'
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: db15dcf5-4d64-48d7-818a-06c2839e1289
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c39111755af922a477475de180302da226966859
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951075"
---
# <a name="test-lab-guide-demonstrate-directaccess-in-a-cluster-with-windows-nlb"></a>Testumgebungsanleitung: Vorführung von DirectAccess in einem Cluster mit Windows-Netzwerklastausgleich

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Der Remote Zugriff ist eine Server Rolle in den Betriebssystemen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, die Remote Benutzern den sicheren Zugriff auf interne Netzwerkressourcen über DirectAccess oder RRAS-VPN ermöglicht. Diese Anleitung enthält schrittweise Anweisungen zum Erweitern der [Testumgebungsanleitung zum Veranschaulichen von DirectAccess Single Server-Setup mit gemischten IPv4 und IPv6.](https://go.microsoft.com/fwlink/p/?LinkId=237004), die den Netzwerklastenausgleich und die Clusterkonfiguration für DirectAccess veranschaulicht.

## <a name="about-this-guide"></a>Über diesen Leitfaden
Diese Anleitung enthält Anweisungen zum Konfigurieren und Veranschaulichen des Remotezugriffs mit sechs Servern und zwei Clientcomputern. Die vollständige Remotezugriffs-Testumgebung mit NLB simuliert ein Intranet, das Internet sowie ein Heimnetzwerk und veranschaulicht die Remotezugriffsfunktionalität in verschiedenen Internetverbindungsszenarios.

> [!IMPORTANT]
> Diese Testumgebung ist eine Machbarkeitsstudie mit der minimalen Anzahl an Computern. Die in dieser Anleitung beschriebene Konfiguration ist nur für Testzwecke geeignet und sollte nicht in einer Produktionsumgebung verwendet werden.

## <a name="known-issues"></a><a name="KnownIssues"></a>Bekannte Probleme
Im Folgenden finden Sie bekannte Probleme beim Konfigurieren eines Clusterszenarios:

-   Nach dem Konfigurieren von DirectAccess in einer ausschließlichen IPv4-Bereitstellung mit einem einzelnen Netzwerkadapter und nach automatischem Konfigurieren von Standard-DNS64 (die IPv6-Adresse mit „:3333::“) auf dem Netzwerkadapter wird der Benutzer bei dem Versuch, den Lastenausgleich über die Remotezugriffs-Verwaltungskonsole zu aktivieren, zur Eingabe einer IPv6-DIP-Adresse aufgefordert. Wenn eine IPv6-DIP-Adresse angegeben wird, tritt nach dem Klicken auf **Commit ausführen** ein Konfigurationsfehler mit folgender Fehlermeldung auf: Der Parameter ist falsch.

    So lösen Sie das Problem:

    1.  Laden Sie die Sicherung herunter, und stellen Sie Skripts aus [Back up and Restore Remote Access Configuration](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)wieder her.

    2.  Sichern Sie die Remotezugriffs-GPOs mit dem heruntergeladenen Skript „Backup-RemoteAccess.ps1“.

    3.  Versuchen Sie, den Lastenausgleich bis zu dem Schritt zu aktivieren, bei dem ein Fehler auftritt. Erweitern Sie den Detailbereich im Dialogfeld „Lastenausgleich aktivieren“, klicken Sie mit der rechten Maustaste in den Detailbereich, und klicken Sie auf **Skript kopieren**.

    4.  Öffnen Sie Editor, und fügen Sie den Inhalt der Zwischenablage ein. Zum Beispiel:

        ```
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19/255.255.255.0','fdc4:29bd:abde:3333::2/128') -InternetVirtualIPAddress @('fdc4:29bd:abde:3333::1/128', '10.244.4.21/255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose
        ```

    5.  Schließen Sie alle offenen Remotezugriffs-Dialogfelder und die Remotezugriffs-Verwaltungskonsole.

    6.  Bearbeiten Sie den eingefügten Text, und entfernen Sie die IPv6-Adressen. Zum Beispiel:

        ```
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19/255.255.255.0') -InternetVirtualIPAddress @('10.244.4.21/255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose
        ```

    7.  Führen Sie den Befehl aus dem vorherigen Schritt in einem PowerShell-Fenster mit erhöhten Rechten aus.

    8.  Wenn während der Ausführung des Cmdlets ein Fehler auftritt (nicht durch falsche Eingabewerte), führen Sie den Befehl „Restore-RemoteAccess.ps1“ aus, und befolgen Sie die Anweisungen, um sicherzustellen, dass die Integrität der ursprünglichen Konfiguration beibehalten wird.

    9. Nun können Sie die Remotezugriffs-Verwaltungskonsole wieder öffnen.



