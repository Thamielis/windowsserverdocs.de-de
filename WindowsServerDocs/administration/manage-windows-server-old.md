---
title: Verwalten von Windows Server
description: Erfahren Sie mehr über Tools, Empfehlungen und Anleitungen zur Verwaltung von Windows Server
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 03/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 55b33c7ab74ac9295d42ef884540d551b1ad6ec4
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992429"
---
# <a name="manage-windows-server"></a>Verwalten von Windows Server

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

>[!TIP]
> Suchen Sie nach Informationen zu älteren Versionen von Windows Server? Sehen Sie sich unsere [Windows Server-Bibliotheken](/previous-versions/windows/) auf „docs.microsoft.com“ an. Sie können auch nach bestimmten Informationen [auf dieser Website suchen](/search/index?dataSource=previousVersions&search=Windows+Server).

 <ul class="cardse panelContent cols cols3">
    <li>
        <a href="https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback-hub">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="manage icon" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h2>Verwalten</h2>
                <p>Nachdem Sie Windows Server in Ihrer Umgebung bereitgestellt haben, einschließlich der spezifischen Rollen für die benötigten Features und Funktionen, besteht der nächste Schritt darin, diese Server zu verwalten. Windows Server enthält eine Reihe von Tools, mit denen Sie Ihre Windows Server-Umgebung besser verstehen, bestimmte Server verwalten, die Leistung optimieren und viele Verwaltungsaufgaben automatisieren können. </p>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

## <a name="manage-windows-server-systems-and-environments"></a>Verwalten von Windows Server-Systemen und -Umgebungen
Die Tools, die Sie zum Verwalten von Windows Server-Instanzen verwenden, hängen in hohem Maße von den bereitgestellten Systemtypen (Windows Server mit Desktopdarstellung oder Server Core), physischen und virtuellen Computern sowie dem Standort der Server ab. Verwenden Sie die folgenden Informationen, um grundlegende Verwaltungsaufgaben unter Windows Server auszuführen.

Verwenden Sie die folgende Tabelle, um ermitteln, welche Tools wann zu verwenden sind.

| Ich bin   | Installieren und Ausführen von Windows Admin Center | Server Manager unter Windows Server ausführen | Server Manager in RSAT unter Windows 10 ausführen |
|--------|----------------------|--------------------------------------|------------------------------------------|
| Benutzer an einem Windows 10-PC | X  |                                      | X                                        |
| Benutzer an einem Windows Server-System, das mit der Desktopdarstellung arbeitet | X | X | X |
| Benutzer an einem Windows Server-System, das mit Server Core arbeitet |X (unter Windows 10 installieren, zum Verwalten von Server Core verwenden) | | X |
| Von meinem Windows Server-System weit entfernt |X | | X |
| Von meinem Windows Server-System, das mit der Desktopdarstellung arbeitet, weit entfernt |X | Verwendung von RDS für die Remoteverbindung mit dem Server, dann Verwendung von Server-Manager | X |

Zusätzlich zu den unten aufgeführten Tools können Sie auch [Remotedesktopdienste](../remote/remote-desktop-services/welcome-to-rds.md) für den Zugriff auf lokale, remote und virtuelle Server verwenden. Dann können Sie mit Server-Manager Verwaltungsaufgaben ausführen.

### <a name="manage-on-premises-systems-remote-systems-and-systems-without-ui-with-windows-admin-center"></a>Verwalten von lokalen Systemen, Remotesystemen und Systemen ohne Benutzeroberfläche mit Windows Admin Center
[Windows Admin Center](../manage/windows-admin-center/overview.md) ist eine browserbasierte Verwaltungs-APP, die die lokale Verwaltung von Windows-Servern ohne Azure-oder cloudabhängigkeit ermöglicht. Das Windows Admin Center bietet Ihnen vollständige Kontrolle über alle Aspekte Ihrer Serverinfrastruktur und ist besonders nützlich für die Verwaltung von privaten Netzwerken, die nicht mit dem Internet verbunden sind. Sie können Windows Admin Center unter Windows 10, auf einem Gatewayserver oder direkt auf dem Windows Server-System installieren, das Sie verwalten möchten.

>[!NOTE]
>Windows Admin Center ist der offizielle Name von dem, was wir zum Anrufen von "Project Honolulu" verwendet haben.

### <a name="manage-on-premises-systems-with-server-manager"></a>Verwalten von lokalen Systemen mit Server-Manager
[Server-Manager](server-manager/server-manager.md) ist eine Verwaltungskonsole, die in der vollständigen Installation von Windows Server enthalten ist. (Es ist nicht verfügbar bei Installationen ohne Benutzeroberfläche – in Server Core ist Server-Manager nicht enthalten). Verwenden Sie Server-Manager zum Installieren und Entfernen von Serverrollen, Hinzufügen und Entfernen von Remoteservern, Starten und Beenden von Diensten sowie zum Anzeigen von Daten, die über Ihre Umgebung gesammelt wurden.

### <a name="manage-remote-systems-and-systems-without-ui-with-remote-server-administration-tools-rsat"></a>Verwalten von Remotesystemen und Systemen ohne Benutzeroberfläche mit Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT)
Wenn Ihre Umgebung Installationen von Server Core-oder Remote Servern (lokale oder virtuelle Computer) umfasst, können Sie die [Remote Server-Verwaltungs Tools (Remote Server Administration Tools, RSAT)](../remote/remote-server-administration-tools.md) verwenden, um diese Systeme zu verwalten. RSAT enthält Server-Manager, sodass Sie alle Ihre Server damit verwalten können.

> [!IMPORTANT]
> RSAT wird unter Windows 10 ausgeführt. RSAT kann nicht unter Windows Server Core installiert werden.

Server Core-Installationen können auch über die Befehlszeile verwaltet werden. Informationen finden Sie [Untergrund Legende Verwaltungsaufgaben in Server Core](server-core/server-core-administer.md).

### <a name="manage-updates-to-windows-server-systems"></a>Verwalten von Updates für Windows Server-Systeme
Sie können [Windows Server Update Services (WSUS)](windows-server-update-services/get-started/windows-server-update-services-wsus.md) verwenden, um Updates für die Systeme in Ihrer Windows Server-Umgebung zu verwalten und bereitzustellen.

## <a name="gather-information-about-your-environment"></a>Sammeln von Informationen über Ihre Umgebung
Viele der Entscheidungen, die Sie als Administrator treffen, sind von Daten über die Systeme und Benutzer in Ihrer Umgebung abhängig. Verwenden Sie die folgenden Informationen und Tools, um diese Daten zu erfassen.

Beginnen [Sie mit Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](/windows/configuration/configure-windows-diagnostic-data-in-your-organization) , um Informationen zu den Diagnosedaten zu erhalten, die von Windows 10 und Windows Server gesammelt werden können.

### <a name="setup-and-boot-event-collection"></a>[Ereignissammlung für Setup und Start](get-started-with-setup-and-boot-event-collection.md)
Mit „Ereignissammlung für Setup und Start“ können Sie einen Computer zum „Sammeln“ angeben, der eine Vielzahl von wichtigen Ereignissen erfasst, die auf anderen Computern auftreten, wenn sie starten oder den Installationsvorgang durchlaufen. Die erfassten Ereignisse können Sie später mit der Ereignisanzeige, Message Analyzer, Wevtutil oder Windows PowerShell-Cmdlets analysieren.

### <a name="software-inventory-logging-sil"></a>[Protokollierung des Softwarebestands (Software Inventory Logging, SIL)](software-inventory-logging/get-started-with-software-inventory-logging.md)

Die Protokollierung des Softwarebestands in Windows Server ist ein Feature mit einer Reihe einfacher PowerShell-Cmdlets, über die Serveradministratoren eine Liste der auf Servern installierten Microsoft-Software abrufen können. Darüber hinaus bietet sie die Möglichkeit, diese Daten für die Aggregation in regelmäßigen Abständen mithilfe des HTTPS-Protokolls über das Netzwerk zu sammeln und an einen Zielwebserver weiterzuleiten. Zum Verwalten des Features – in erster Linie zum stündlichen Sammeln und Weiterleiten – werden ebenfalls PowerShell-Befehle verwendet.

### <a name="user-access-logging-ual"></a>[Benutzerzugriffsprotokollierung (User Access Logging, UAL)](user-access-logging/get-started-with-user-access-logging.md)

Die Benutzerzugriffsprotokollierung aggregiert eindeutige Ereignisse auf Clientgeräten sowie Benutzeranforderungsereignisse, die auf einem Computer unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 in einer lokalen Datenbank protokolliert wurden. Diese Datensätze werden dann (über die Abfrage eines Serveradministrators) zur Verfügung gestellt, um Mengen und Instanzen nach Serverrolle, Benutzer, Gerät, lokalem Server und Datum abzurufen. Außerdem bietet UAL auch Nicht-Microsoft-Softwareentwicklern die Möglichkeit, ihre UAL-Ereignisse für die Aggregierung zu instrumentieren.

## <a name="tune-your-windows-server-environment-for-performance"></a>Leistungsoptimierung für die Windows Server-Umgebung
Verwenden Sie die folgenden Informationen, um die Leistung Ihrer Umgebung zu optimieren.

### <a name="performance-tuning-guidelines"></a>[Richtlinien zur Leistungsoptimierung](performance-tuning/index.md)
Informieren Sie sich über eine Reihe von Richtlinien, die Sie verwenden können, um die Servereinstellungen in Windows Server 2016 zu optimieren und inkrementelle Leistungs-oder Energieeffizienzsteigerungen zu erzielen. Dies gilt insbesondere, wenn die Art der Arbeitsauslastung wenig Zeit

### <a name="microsoft-server-performance-advisor"></a>[Microsoft Server Performance Advisor](server-performance-advisor/microsoft-server-performance-advisor.md)

Mit Microsoft Server Performance Advisor (SPA) können Sie Messdaten sammeln, um Leistungsprobleme auf Windows-Servern unauffällig zu diagnostizieren, ohne Softwareagenten hinzuzufügen oder Produktionsserver neu zu konfigurieren. SPA generiert umfassende Berichte und historische Diagramme mit Empfehlungen.


## <a name="automate-windows-server-management"></a>Automatisieren der Windows Server-Verwaltung

Windows Server umfasst eine Reihe von Befehlen und Windows PowerShell-Modulen, die Sie zum Automatisieren von Verwaltungsaufgaben verwenden können.

### <a name="windows-powershell"></a>[Windows PowerShell](/powershell/scripting/powershell-scripting?view=powershell-5.1)
Winows PowerShell ist eine Befehlszeilenshell und Skriptsprache, mit der Sie administrative Aufgaben schnell automatisieren können.

### <a name="windows-commands"></a>[Windows-Befehle](windows-commands/windows-commands.md)

Die Windows-Befehlszeilentools dienen zum Ausführen von Verwaltungsaufgaben in Windows. Anhand der Befehlsreferenz können Sie sich mit den Befehlszeilentools vertraut machen, mehr über die Befehlsshell erfahren und Befehlszeilenaufgaben mithilfe von Stapeldateien oder Skripting-Tools automatisieren.

## <a name="windows-server-insider-preview"></a>Windows Server Insider Preview
### <a name="system-insights"></a>[Systemdaten](../manage/system-insights/overview.md)
System Insights ist ein neues Feature, das Predictive Analytics nativ in Windows Server einführt. Diese Vorhersagefunktionen analysieren lokal Windows Server-Systemdaten (z. b. Leistungsindikatoren oder ETW-Ereignisse) und unterstützen IT-Administratoren dabei, das problematische Verhalten in ihren bereit Stellungen proaktiv zu erkennen und zu beheben