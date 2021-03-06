---
title: Konfigurieren der Benachrichtigungsgrenze
description: In diesem Artikel wird beschrieben, wie Sie verschiedenen Benachrichtigungs Typen Zeitlimits hinzufügen.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 969c950d3a925afac400d128ac21ed0923f07ffa
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950654"
---
# <a name="configure-notification-limits"></a>Konfigurieren der Benachrichtigungsgrenze

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Um die Anzahl der Benachrichtigungen zu verringern, die sich für das wiederholte überschreiten eines Kontingent Schwellenwerts oder des Versuchs, eine nicht autorisierte Datei zu speichern, wendet der Datei Server Ressourcen-Manager Zeitlimits auf die folgenden Benachrichtigungs Typen an

-   E-Mail
-   Ereignisprotokoll
-   Befehl
-   Bericht

Jede Grenze gibt einen Zeitraum an, bevor eine andere konfigurierte Benachrichtigung desselben Typs für ein identisches Problem generiert wird.

Für jeden Benachrichtigungstyp wird ein Standard Limit von 60 Minuten festgelegt. Sie können diese Limits jedoch ändern. Das Limit gilt für alle Benachrichtigungen eines bestimmten Typs, unabhängig davon, ob Sie durch Kontingent Schwellenwerte oder durch Datei Überprüfungs Ereignisse generiert werden.

## <a name="to-specify-a-standard-notification-limit-for-each-notification-type"></a>So geben Sie ein Standard Benachrichtigungs Limit für jeden Benachrichtigungstyp an

1.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Datei Server Ressourcen-Manager**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.

2.  Geben Sie auf der Registerkarte **Benachrichtigungs Limits** für jeden angezeigten Benachrichtigungstyp einen Wert in Minuten ein.

3.  Klicken Sie auf **OK**.

> [!Note]
> Zum Anpassen von Zeitlimits, die Benachrichtigungen für ein bestimmtes Kontingent oder einen bestimmten Datei Bildschirm zugeordnet sind, können Sie den Dateiserver Ressourcen-Manager Befehlszeilen Tools **Dirquota.exe** und **Filescrn.exe**verwenden oder die [Dateiserver Ressourcen-Manager](/powershell/module/fileserverresourcemanager/?view=win10-ps) -Cmdlets verwenden.

## <a name="additional-references"></a>Weitere Verweise

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Befehlszeilentools](command-line-tools.md)
