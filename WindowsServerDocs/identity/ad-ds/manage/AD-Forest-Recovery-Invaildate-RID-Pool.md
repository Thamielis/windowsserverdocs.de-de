---
title: 'AD-Gesamtstruktur Wiederherstellung: der RID-Pool wird ungültig.'
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.openlocfilehash: 36919eb4f4e67129446975f9c8c4d60fd64cc499
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939640"
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>AD-Gesamtstruktur Wiederherstellung: der aktuelle RID-Pool wird ungültig.

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren für Windows PowerShell, um den aktuellen RID-Pool auf einem Domänen Controller ungültig zu machen. Windows PowerShell ist standardmäßig unter Windows Server 2012 und Windows Server 2008 R2 aktiviert, jedoch nicht unter Windows Server 2008, wo Sie mithilfe von **Features hinzufügen**installiert werden muss. Sie kann [heruntergeladen](https://www.microsoft.com/download/details.aspx?id=20020) werden, um unter Windows Server 2003 ausgeführt zu werden.

Um zu überprüfen, ob der Befehl erfolgreich abgeschlossen wurde, überprüfen Sie die Ereignis-ID 16654 (Quelle ist Verzeichnisdienst-Sam) im System Protokoll in Ereignisanzeige in Windows Server 2012. In früheren Versionen von Windows wird dieses Ereignis nicht protokolliert.

> [!NOTE]
> Nachdem Sie den RID-Pool ungültig gemacht haben, wird beim ersten Versuch, den Sicherheits Prinzipal (Benutzer, Computer oder Gruppe) zu erstellen, eine Fehlermeldung angezeigt. Der Versuch, ein Objekt zu erstellen, löst eine Anforderung für einen neuen RID-Pool aus. Die Wiederholung des Vorgangs ist erfolgreich, da der neue RID-Pool zugeordnet wird.

## <a name="to-invalidate-the-current-rid-pool"></a>So machen Sie den aktuellen RID-Pool ungültig

- Öffnen Sie eine Windows PowerShell-Sitzung mit erhöhten Rechten, führen Sie den folgenden Befehl aus, und drücken Sie Eingabe

   ```powershell
   $Domain = New-Object System.DirectoryServices.DirectoryEntry
   $DomainSid = $Domain.objectSid
   $RootDSE = New-Object System.DirectoryServices.DirectoryEntry("LDAP://RootDSE")
   $RootDSE.UsePropertyCache = $false
   $RootDSE.Put("invalidateRidPool", $DomainSid.Value)
   $RootDSE.SetInfo()
   ```

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
