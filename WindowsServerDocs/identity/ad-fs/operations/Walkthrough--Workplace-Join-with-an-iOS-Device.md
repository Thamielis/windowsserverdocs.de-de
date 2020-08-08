---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: 'Exemplarische Vorgehensweise: Workplace Join mit einem IOS-Gerät'
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 10/18/2018
ms.topic: article
ms.openlocfilehash: 1090c5c79ad0f4b4cf2fa27bf735604ad334b90e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956377"
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem iOS-Gerät


> [!IMPORTANT]
> Diese Methode ist nur für vollständig lokale Kunden relevant. Hybrid-oder cloudkunden dürfen diese Methode nicht verwenden, um Ihre IOS-Geräte zu registrieren. Diese Methode ist nicht kompatibel, wenn die lokalen Kunden eine Umstellung auf die Cloud durchführen. Die Registrierung des Geräts muss aufgehoben werden, und die Registrierung muss bei der Cloud erfolgen.

In diesem Thema wird der Arbeitsplatzbeitritt mit einem iOS-Gerät dargestellt. Sie müssen die Schritte im Abschnitt [Einrichten der Lab-Umgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) ausführen, bevor Sie diese exemplarische Vorgehensweise ausprobieren können. Sie können das Gerät verwenden, um auf dieselbe Unternehmensweb Anwendung zuzugreifen, auf die Sie unter Exemplarische Vorgehensweise [: Workplace Join mit einem Windows-Gerät](Walkthrough--Workplace-Join-with-a-Windows-Device.md)zugegriffen haben.


## <a name="join-an-ios-device-with-workplace-join"></a>Hinzufügen eines iOS-Geräts mit dem Arbeitsplatzbeitritt

> [!IMPORTANT]
> Wenn lokales DRS konfiguriert ist, muss das iOS-Gerät dem SSL-Zertifikat (Secure Socket Layer) vertrauen, das für die Konfiguration von Active Directory-Verbunddienste (AD FS) in [Step 2: Configure the federation server (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)für den Arbeitsplatzbeitritt konfiguriert wurde.
>
> -   Wenn das AD FS-SSL-Zertifikat von einer Testzertifizierungsstelle ausgegeben wurde, müssen Sie das Zertifizierungsstellenzertifikat auf Ihrem iOS-Gerät installieren.
> -   Wenn Ihr Zertifizierungsstellenzertifikat auf einer Website veröffentlicht ist, können Sie von Ihrem iOS-Gerät zu der Website navigieren und das Zertifikat installieren.

In dieser Demo fügen Sie das Gerät dem Arbeitsplatz hinzu.

#### <a name="to-join-an-ios-device-to-a-workplace"></a>So fügen Sie ein iOS-Gerät zu einem Arbeitsplatz hinzu

1. -   **Wenn Azure Active Directory Device Registration Dienst das konfigurierte DRS ist:** Öffnen Sie Apple Safari, und navigieren Sie zu Azure Active Directory Device Registration Service over-the-Air profile Endpoint for IOS Devices, <`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` > WHERE <`yourdomainname`> ist der Domänen Name, den Sie mit Azure Active Directory konfiguriert haben. Wenn Ihr Domänenname z. B. "contoso.com" lautet, ist die URL: `https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`

   -   **Wenn das lokale DRS das konfigurierte DRS ist**: Öffnen Sie Apple Safari, und navigieren Sie zum over-the-Air-Profil Endpunkt des Geräte Registrierungs Dienstanbieter für IOS-Geräte.`https://adf1s.contoso.com/enrollmentserver/otaprofile`

   Es gibt viele Methoden, diese URL Ihren Benutzern mitzuteilen. Ein empfohlenes Verfahren besteht im Veröffentlichen dieser URL in einer benutzerdefinierten Anwendungsmeldung "Zugriff verweigert" in AD FS. Dies wird im nächsten Abschnitt beschrieben: [Erstellen einer Anwendungs Zugriffs Richtlinie und benutzerdefinierte Meldung "Zugriff verweigert](/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message) "

2. Melden Sie sich bei der Webseite mit einem Unternehmens Domänen Konto an: <strong>roberth@contoso.com</strong> und Kennwort: <strong>P@ssword</strong> .

3. Sie werden aufgefordert, ein Profil zu installieren. Klicken Sie auf dem Bildschirm **Profil installieren** auf **Installieren**.

4. Wenn Sie aufgefordert werden, die Installation des Profils zu bestätigen, klicken Sie auf **Jetzt installieren**.

5. Wenn für das Entsperren Ihres Geräts eine PIN erforderlich ist, werden Sie aufgefordert, Ihre PIN einzugeben.

6. Die Profilinstallation ist abgeschlossen, wenn der Bildschirm **Profil installiert** angezeigt wird. Klicken Sie auf **Fertig**.

   Kehren Sie zu Safari zurück. Sie werden in einer Meldung informiert, dass Sie Safari schließen oder verlassen können.

> [!TIP]
> Navigieren Sie zum Anzeigen oder Entfernen des Profils für den Arbeitsplatzbeitritt zu **Einstellungen**, klicken Sie auf **Allgemein**, und klicken Sie dann auf **Profile** auf Ihrem iOS-Gerät.

## <a name="see-also"></a>Weitere Informationen


- [Arbeitsplatzbeitritt von einem beliebigen Gerät für SSO und die nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Einrichten der Laborumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [Exemplarische Vorgehensweise: Arbeitsplatzbeitritt mit einem Windows-Gerät](Walkthrough--Workplace-Join-with-a-Windows-Device.md)
