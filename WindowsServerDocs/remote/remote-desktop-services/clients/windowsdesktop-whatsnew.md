---
title: Neuigkeiten im Windows-Desktopclient
description: Hier erfährst du mehr über aktuelle Änderungen am Remotedesktopclient für Windows-Desktop
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 03/24/2020
ms.localizationpriority: medium
ms.openlocfilehash: 38b779b12b841e276d8f807af6f6332469c20817
ms.sourcegitcommit: 9e8fddf683c9a36aad330ebef9b80d57f75ffb43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233308"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Neuigkeiten im Windows-Desktopclient

Ausführlichere Informationen über den Windows-Desktopclient findest du unter [Erste Schritte mit dem Windows-Desktopclient](windowsdesktop.md). Die neuesten Updates für den Client findest du nachstehend.

## <a name="latest-client-versions"></a>Neueste Clientversionen

Der Client kann für verschiedene [Benutzergruppen](windowsdesktop-admin.md#configure-user-groups) konfiguriert werden. In der folgenden Tabelle sind die aktuellen Versionen aufgelistet, die für jede Benutzergruppe verfügbar sind:

|Benutzergruppe |Version  |
|-----------|---------|
|Öffentlich     |1.2.790  |
|Insider    |1.2.790  |

## <a name="updates-for-version-12790"></a>Updates für Version 1.2.790

*Veröffentlicht am: 24.03.2020*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4siSh), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4siSi), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4sllb)

- Die Aktion „Update“ für Arbeitsbereiche wurde in „Aktualisieren“ umbenannt, um Konsistenz mit anderen Remotedesktopclients zu gewährleisten.
- Ein Arbeitsbereich kann jetzt direkt über das zugehörige Kontextmenü aktualisiert werden.
- Durch manuelles Aktualisieren eines Arbeitsbereichs wird sichergestellt, dass alle lokalen Inhalte aktualisiert werden.
- Die Benutzerdaten des Clients können jetzt über die Seite „Info“ zurückgesetzt werden, ohne die App deinstallieren zu müssen.
- Die Benutzerdaten des Clients können jetzt auch mit „msrdcw.exe /reset“ und einem optionalen „/f“-Parameter zurückgesetzt werden, um die Eingabeaufforderung zu überspringen.
- Bei der Navigation zur Seite „Info wird jetzt automatisch nach einem Clientupdate gesucht.
- Die Farbe der Schaltflächen wurde aus Konsistenzgründen aktualisiert.

## <a name="updates-for-version-12675"></a>Updates für Version 1.2.675

*Veröffentlicht am: 25.02.2020*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qeak), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qm7h), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qm7g)

- Verbindungen mit Windows Virtual Desktop werden jetzt blockiert, wenn der RDP-Datei die Signatur fehlt oder eine der signscope-Eigenschaften geändert wurde.
- Wenn ein Arbeitsbereich leer ist oder entfernt wurde, scheint das Verbindungscenter nicht mehr leer zu sein.
- Trennungsmeldungen wurden die Aktivitäts-ID und der Fehlercode hinzugefügt, um die Problembehandlung zu verbessern. Du kannst die Dialogmeldung mit **STRG+C** kopieren.
- Ein Problem wurde behoben, das dazu geführt hat, dass die Desktopverbindungseinstellungen keine Anzeigen erkannt haben.
- Der PC wird von Clientupdates nicht mehr automatisch neu gestartet.
- Auf der Taskleiste sollten keine fensterlosen Symbole mehr angezeigt werden.

## <a name="updates-for-version-12605"></a>Updates für Version 1.2.605

*Veröffentlicht am: 29.01.2020*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oHrD), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oJZs), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oXhD)

- Du kannst jetzt auswählen, welche Anzeigen für Desktopverbindungen verwendet werden sollen. Zum Ändern dieser Einstellung klicke mit der rechten Maustaste auf das Symbol der Desktopverbindung, und wähle **Einstellungen** aus.
- Es wurde ein Problem behoben, bei dem in den Verbindungseinstellungen nicht die richtigen verfügbaren Skalierungsfaktoren angezeigt wurden.
- Es wurde ein Problem behoben, bei dem die Sprachausgabe den beim Initiieren der Verbindung gezeigten Dialog nicht lesen konnte.
- Es wurde ein Problem behoben, bei dem der falsche Benutzername angezeigt wurde, wenn die Namen von Azure Active Directory und Active Directory nicht übereinstimmten.
- Es wurde ein Problem behoben, durch das der Client beim Initiieren einer Verbindung nicht mehr reagierte, wenn keine Netzwerkverbindung vorlag.
- Es wurde ein Problem behoben, das dazu führte, dass der Client beim Anschließen eines Headsets nicht mehr reagierte.

## <a name="updates-for-version-12535"></a>Updates für Version 1.2.535

*Veröffentlicht am: 04.12.2019*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k7jH), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k7jL), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k27O)

- Sie können jetzt direkt über die Schaltfläche „Weitere Optionen“ in der Befehlsleiste am oberen Rand des Clients auf Informationen über Updates zugreifen.
- Außerdem können Sie nun Feedback über die Befehlsleiste des Clients mitteilen.
- Die Feedbackoption wird jetzt nur angezeigt, wenn der Feedback-Hub verfügbar ist.
- Gewährleistet, dass die Updatebenachrichtigung nicht angezeigt wird, wenn Benachrichtigungen per Richtlinie deaktiviert sind.
- Es wurde ein Problem behoben, das das Starten einiger RDP-Dateien verhindert hat.
- Es wurde ein Absturz beim Starten des Clients behoben, der durch die Beschädigung einiger persistenter Einstellungen verursacht wurde.

## <a name="updates-for-version-12431"></a>Updates für Version 1.2.431

*Veröffentlicht am: 12.11.2019*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48kow), [Windows 32-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48koA), [Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48zYj)

- Die 32-Bit-Version und die ARM64-Version des Clients sind nun verfügbar.
- Der Client speichert jetzt alle an der Verbindungsleiste vorgenommenen Änderungen (z.B. Position, Größe und angehefteter Zustand), und wendet diese Änderungen sitzungsübergreifend an.
- Aktualisierte Dialogfelder für Gatewayinformationen und Verbindungsstatus.
- Es wurde ein Problem behoben, das dazu führte, dass beim Verbindungsversuch nach Ablauf des Azure Active Directory-Token gleichzeitig zwei Mal Anmeldeinformationen angefordert wurden.
- Unter Windows 7 werden die Benutzer nun ordnungsgemäß zur Eingabe von Anmeldeinformationen aufgefordert, wenn sie Anmeldeinformationen gespeichert hatten und der Server dies nicht zulässt.
- Die Azure Active Directory-Eingabeaufforderung wird jetzt beim Wiederherstellen der Verbindung vor dem Verbindungsfenster angezeigt.
- Elemente, die an die Taskleiste angeheftet wurden, werden jetzt während einer Feedaktualisierung aktualisiert.
- Verbessertes Scrollen im Connection Center bei Verwendung der Toucheingabe.
- Die leere Zeile wurde aus dem Dropdownmenü „Auflösung“ entfernt.
- Unnötige Einträge in der Windows-Anmeldeinformationsverwaltung wurden entfernt.
- Beim Beenden des Vollbildmodus erfolgt nun eine ordnungsgemäße Größenanpassung der Desktopsitzungen.
- Das Dialogfeld zum Trennen der RemoteApp wird jetzt im Vordergrund angezeigt, wenn eine Sitzung aus dem Energiesparmodus wieder aufgenommen wird.
- Barrierefreiheitsprobleme, z.B. bei der Tastaturnavigation, wurden behoben.

## <a name="updates-for-version-12247"></a>Updates für Version 1.2.247

*Veröffentlicht am: 17.09.2019*

Download: [Windows 64-Bit](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE3LkSa)

- Verbesserung der Reservesprachen für lokalisierte Versionen. (Beispielsweise wird FR-CA ordnungsgemäß in Französisch anstelle von Englisch angezeigt.)
- Beim Entfernen eines Abonnements entfernt der Client nun die gespeicherten Anmeldeinformationen ordnungsgemäß aus der Anmeldeinformationsverwaltung.
- Der Updatevorgang des Clients erfolgt jetzt nach dem Starten ohne Benutzereingriff, und der Client wird nach Abschluss neu gestartet.
- Der-Client kann jetzt unter Windows 10 im S-Modus verwendet werden.
- Es wurde ein Problem behoben, das für Benutzer mit einem Leerzeichen im Benutzernamen zu einem Fehler beim Update führte.
- Es wurde ein Absturz korrigiert, der vorkam, wenn während einer Verbindung eine Authentifizierung vorgenommen wurde.
- Es wurde ein Absturz korrigiert, der vorkam, wenn der Client geschlossen wurde.
