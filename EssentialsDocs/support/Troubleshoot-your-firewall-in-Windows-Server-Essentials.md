---
title: Behandeln von Problemen mit der Firewall in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 51d94b67-8b9b-4159-80dd-f652d73a43cb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b20a42c9bf0cf9a7bdb09e120f5bc796451d8030
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180136"
---
# <a name="troubleshoot-your-firewall-in-windows-server-essentials"></a>Behandeln von Problemen mit der Firewall in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Wenn Probleme mit dem Remotezugriff auftreten, führen Sie den Assistenten zur Reparatur von "Zugriff überall" aus.

### <a name="to-run-the-repair-anywhere-access-wizard"></a>Ausführen des Assistenten zur Reparatur von "Zugriff überall"

1. Öffnen Sie das Dashboard.

2. Klicken Sie auf **Einstellungen**, auf die Registerkarte **Zugriff überall** und dann auf **Reparieren**.

3. Folgen Sie den Anweisungen im Assistenten zur Reparatur von "Zugriff überall".

   Wenn Sie eine erweiterte Netzwerkeinrichtung oder eine nicht von Microsoft stammende Firewall verwenden, müssen Sie unter Umständen zusätzliche Ports der Firewall öffnen. Die Ports in der folgenden Tabelle sind bei IANA (Internet Assigned Numbers Authority) registriert.

|Portnummer|BESCHREIBUNG|
|-----------------|-----------------|
|65500|Zertifkatwebdienst|
|65510 und 65515|Website zur Bereitstellung von Clientcomputern|
|65520|Webdienst für Mac-Clientcomputer|
|65532|Anbieterframework für Server-Loopbackkommunikation|
|6602|Anbieterframework für Kommunikation zwischen den Server- und Clientcomputern|

## <a name="see-also"></a>Weitere Informationen

-   [Verwenden des Remotewebzugriffs](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Verwalten der Remotewebzugriffs](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)

-   [Verwalten von %%amp;quot;Zugriff überall%%amp;quot;](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Verwalten von Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)

-   [Unterstützung von Windows Server Essentials](../support/Support-Windows-Server-Essentials.md)

