---
title: Einrichten der E-Mail-Erkennung zum Abonnieren deines RDS-Feeds
description: Hier erfährst du, wie du Azure Active Directory Domain Services in deine RDS-Bereitstellung integrierst.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: c56a233adf28270aac809dc960e32b5363e4b8ab
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "71387510"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>Einrichten der E-Mail-Erkennung zum Abonnieren deines RDS-Feeds

Hattest du jemals Schwierigkeiten, für deine Endbenutzer eine Verbindung mit dem veröffentlichten RDS-Feed herzustellen, weil entweder in der Feed-URL ein einzelner Buchstabe gefehlt hat oder weil die E-Mail mit der URL verloren gegangen ist? Nahezu alle Remotedesktop-Clientanwendungen unterstützen die Suche nach deinem Abonnement durch Eingabe deiner E-Mail-Adresse. So kannst du deine Endbenutzer leichter als je zuvor mit ihren RemoteApps und Desktops verbinden.

>[!IMPORTANT]
>Die Microsoft-Remotedesktop-App im Microsoft Store unterstützt das Abonnieren von E-Mail-Adressen derzeit nicht.

Führe vor dem Einrichten der E-Mail-Erkennung die folgenden Schritte aus:

- Vergewissere dich, dass du über Berechtigungen zum Hinzufügen eines TXT-Eintrags zu der mit deiner E-Mail verknüpften Domäne verfügst. (Beispiel: Wenn deine Benutzer E-Mail-Adressen vom Typ @contoso.com besitzen, benötigst du Berechtigungen für die Domäne „contoso.com“.)
- Erstelle eine RD-Feed-URL (https://\<RDWeb-DNS-Name\>.Domäne/RDWeb/Feed/webfeed.aspx, etwa https://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx).

Führe nun die folgenden Schritte zum Einrichten der E-Mail-Erkennung aus:

1. Öffne im Browser die Website der Domänennamen-Registrierungsstelle, bei der deine Domäne registriert ist.
2. Navigiere zur entsprechenden Seite für deine registrierte Domäne, auf der du DNS-Einträge anzeigen, hinzufügen und bearbeiten kannst.
3. Gib einen neuen DNS-Eintrag mit den folgenden Eigenschaften ein:
   - **Host:** _msradc
   - **Text:** \<RD-Feed-URL\>
   - **TTL:** 300

   Die Namen der Felder für DNS-Einträge variieren je nach Domänennamen-Registrierungsstelle, mit diesen Schritten erhältst du jedoch einen TXT-Eintrag namens „_msradc.\<Domänenname\> (etwa „_msradc.contoso.com“) mit einem Wert des vollständigen RD-Feeds.

Das war's. Starte jetzt die Remotedesktopanwendung auf deinem Gerät, und abonniere deinen eigenen Feed!