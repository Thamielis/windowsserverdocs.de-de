---
title: Initialisieren des HGS-Clusters mit dem TPM-Modus in einer neuen dedizierten Gesamtstruktur (Standard)
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 47e0780eb846e690c766dd241060d2687587c7ff
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961644"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-a-new-dedicated-forest-default"></a>Initialisieren des HGS-Clusters mit dem TPM-Modus in einer neuen dedizierten Gesamtstruktur (Standard)

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  Führen Sie [Initialize-hgsserver](https://technet.microsoft.com/library/mt652185.aspx) in einem PowerShell-Fenster mit erhöhten Rechten auf dem ersten HGS-Knoten aus. Die Syntax dieses Cmdlets unterstützt viele verschiedene Eingaben, aber die zwei häufigsten Aufrufe sind unten aufgeführt:

    -   Wenn Sie PFX-Dateien für Ihre Signatur-und Verschlüsselungs Zertifikate verwenden, führen Sie die folgenden Befehle aus:

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
        ```

    -   Wenn Sie nicht exportierbare Zertifikate verwenden, die im lokalen Zertifikat Speicher installiert sind, führen Sie den folgenden Befehl aus. Wenn Sie die Fingerabdrücke ihrer Zertifikate nicht kennen, können Sie die verfügbaren Zertifikate auflisten, indem Sie Ausführen `Get-ChildItem Cert:\LocalMachine\My` .

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' -TrustTpm
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Installieren von TPM-Stammzertifikaten](guarded-fabric-install-trusted-tpm-root-certificates.md)
