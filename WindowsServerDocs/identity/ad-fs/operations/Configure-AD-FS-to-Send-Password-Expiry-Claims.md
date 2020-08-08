---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: Konfigurieren von AD FS Kennwort Ablauf Ansprüche senden
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e53c33f1fef30570db46cf658bd1481343e846cd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962544"
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>Konfigurieren von AD FS Kennwort Ablauf Ansprüche senden


Sie können Active Directory-Verbunddienste (AD FS) (AD FS) konfigurieren, um Kenn Wort Ablauf Ansprüche an die Vertrauens Stellungen der vertrauenden Seite (Anwendungen) zu senden, die durch AD FS geschützt werden. Wie diese Ansprüche verwendet werden, hängt von der jeweiligen Anwendung ab. Beispiel: Bei Office 365 als vertrauende Seite werden Updates in Exchange und Outlook implementiert, damit Verbundbenutzer über ihre bald ablaufenden Kennwörter benachrichtigt werden.

Um AD FS zum Senden von Kenn Wort Ablauf Ansprüchen an eine Vertrauensstellung der vertrauenden Seite zu konfigurieren, müssen Sie der Vertrauensstellung der vertrauenden Seite die folgenden Anspruchs Regeln hinzufügen:

```
@RuleName = "Issue Password Expiry Claims"
c1:[Type == "http://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
 => issue(store = "_PasswordExpiryStore", types = ("http://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "http://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "http://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> Ansprüche zum Ablauf von Kenn Wörtern sind nur für Benutzername-und Kennwort-und Microsoft Passport for Work Authentifizierungs Typen verfügbar.  Wenn sich der Benutzer mit der integrierten Windows-Authentifizierung authentifiziert und Passport nicht konfiguriert ist, sind die Ansprüche nicht verfügbar, und den Benutzern werden keine Benachrichtigungen zum Ablauf des Kennworts angezeigt.

> [!NOTE]
> Es gibt ein Fenster von 14 Tagen, sodass die gesendeten Ansprüche nur aufgefüllt werden, wenn das Kennwort innerhalb von 14 Tagen abläuft.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Vorgänge](../ad-fs-operations.md)
