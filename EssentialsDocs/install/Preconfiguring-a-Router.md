---
title: Vorkonfigurieren eines Routers
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 9153ac90-bb0c-4b8d-93b2-e2121ed13636
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 79ffa14cfabc26afd87c0771f7412c98e661421d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626153"
---
# <a name="preconfiguring-a-router"></a>Vorkonfigurieren eines Routers

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Normalerweise erfordert eine neue Installation des Betriebssystems einen internetfähigen Router und eine Firewall, um das interne Netzwerk des Kunden mit dem Internet zu verbinden. Wenn Sie zusätzlich zu einem Router einen vorkonfigurierten Server zur Verfügung stellen, können Sie weitere Schritte ausführen, um den Router benutzerfreundlicher zu konfigurieren.

 Auf dem Router sollte DHCP aktiviert sein. Dem Server sollte eine statische IP-Adresse zugewiesen sein. Dazu können Sie eine DHCP-Reservierung einer IP-Adresse verwenden oder eine IP-Adresse zuweisen, die nicht im DHCP-Adressbereich liegt.

 Sie sollten auf dem Router auch die Einstellungen für die Portweiterleitung vorkonfigurieren, um bestimmte Ports von der externen Schnittstelle des Routers an die Adresse des Servers im internen Netzwerk weiterzuleiten. Die folgende Tabelle listet die empfohlene Konfiguration auf.

|Konfigurationseinstellung|Details|
|---------------------------|-------------|
|DHCP|Ein|
|Portweiterleitung|Sie sollten die folgenden Ports an die Adresse des Servers weiterleiten:<br /><br /> -80 (bei gehosteter Konfiguration nur 443 verwenden)<br />-443|
|UPnP-Unterstützung|Sie sollten die UPnP-Unterstützung aktivieren, um die einfachste Routerkonfiguration für den Kunden und die beste Kundenfreundlichkeit bei der Installation bereitzustellen.<br /><br /> **Warnung:** Die UPnP-Architektur kann ein Sicherheitsrisiko darstellen, wenn Sie aktiviert ist.|

 Neben den grundlegenden Einstellungen für die Routervorkonfiguration können Sie die folgenden Aufgaben ausführen, um das Verwalten des Routers benutzerfreundlicher zu gestalten:

-   Erweitern Sie das Dashboard, indem Sie auf dem Server ein Add-In bereitstellen, mit dem die Benutzer den Router über eine angepasste Benutzeroberfläche verwalten können.

-   Erweitern Sie die Integritätswarnungen, damit alle Warnungen vom Router in der Meldungsanzeige angezeigt werden.

-   Wenn der Router mehrere Subnetze unterstützt, muss die IP-Adresse des Servers als ein DNS-Server über DHCP ausgegeben werden.

-   Wenn der Router über eine integrierte Zugriffs Steuerungsfunktion für Active Directory- &reg; Domänen Dienste verfügt, können Sie die Active Directory Integration während der Erstkonfiguration des Servers automatisieren. Sie sollten diese Funktion auch über das Add-In für die Routerverwaltung im Dashboard verfügbar machen.

> [!NOTE]
>  Weitere Informationen zum Konfigurieren von Funkverbindungen finden Sie unter [Konfigurieren der Unterstützung für ein Funknetzwerk](Configure-Support-for-a-Wireless-Network.md).

## <a name="see-also"></a>Weitere Informationen
 Informationen zu den ersten Schritten [mit dem Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Images für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)