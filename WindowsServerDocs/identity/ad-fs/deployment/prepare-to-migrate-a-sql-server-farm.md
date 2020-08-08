---
title: Vorbereiten der Migration einer AD FS SQL-Farm
description: Enthält Informationen zum Vorbereiten der Migration einer AD FS Server-SQL-Farm zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: ef166adeb2285efbbcaa40cdce44cb53b4411dde
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940619"
---
# <a name="prepare-to-migrate-a-sql-server-farm"></a>Vorbereiten der Migration einer SQL Server-Farm
 Zum Vorbereiten der Migration von AD FS 2,0-Verbund Servern, die zu einer SQL Server-Farm zu Windows Server 2012 gehören, müssen Sie die AD FS Konfigurationsdaten von diesen Servern exportieren und sichern.

 Führen Sie zum Exportieren der AD FS-Konfigurationsdaten die folgenden Schritte aus:

-   [Schritt 1: Exportieren der Dienst Einstellungen](#step-1-export-service-settings)

-   [Schritt 2: Sichern von benutzerdefinierten Attribut speichern](#step-2-back-up-custom-attribute-stores)

-   [Schritt 3: Sichern von Webseiten Anpassungen](#step-3-back-up-webpage-customizations)

## <a name="step-1-export-service-settings"></a>Schritt 1: Exportieren der Dienst Einstellungen
 Gehen Sie wie folgt vor, um die Diensteinstellungen zu exportieren:

### <a name="to-export-service-settings"></a>So exportieren Sie Diensteinstellungen

1.  Notieren Sie den Antragstellernamen des Zertifikats sowie den Fingerabdruckwert des SSL-Zertifikats, die vom Verbunddienst verwendet werden. Um das SSL-Zertifikat zu finden, öffnen Sie die Internetinformationsdienste (IIS)-Verwaltungskonsole, wählen Sie im linken Bereich **Standard Website** aus, und klicken Sie auf **Bindungen...** auf **Bindungen…** . Navigieren Sie zur HTTPS-Bindung, wählen Sie sie aus, und klicken Sie auf **Bearbeiten**und anschließend auf **Anzeigen**.

> [!NOTE]
>  Optional können Sie auch SSL-Zertifikat und seinen privaten Schlüssel in eine PFX-Datei exportieren. Weitere Informationen finden Sie unter [Export the Private Key Portion of a Server Authentication Certificate](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md).
>
>  Dieser Schritt ist optional, da dieses Zertifikat auf dem lokalen Computer im privaten Zertifikatspeicher gespeichert wird und beim Upgrade des Betriebssystems erhalten bleibt.

2. Exportieren Sie alle sonstigen Zertifikate und Schlüssel für die Tokensignatur, Tokenverschlüsselung oder Dienstkommunikation, die nicht intern von AD FS generiert werden.

Sie können alle auf Ihrem Server von AD FS verwendeten Zertifikate mithilfe von Windows PowerShell anzeigen. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle Zertifikate anzuzeigen, die auf dem Server verwendet werden `PSH:>Get-ADFSCertificate` . Die Ausgabe dieses Befehls umfasst StoreLocation- und StoreName-Werte, die den Speicherort für die einzelnen Zertifikate angeben.

> [!NOTE]
>  Sie können dann optional die Anleitung in [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) verwenden, um die einzelnen Zertifikate und den entsprechenden privaten Schlüssel in eine PFX-Datei zu exportieren. Dieser Schritt ist optional, da alle externen Zertifikate während des Betriebssystemupgrades erhalten bleiben.

3. Sichern Sie die Anwendungskonfigurationsdatei. Neben anderen Einstellungen enthält diese Datei die Verbindungszeichenfolge der Richtliniendatenbank.

Zum Sichern der Anwendungskonfigurationsdatei muss die Datei `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` manuell an einen sicheren Speicherort auf einem Sicherungsserver kopiert werden.

> [!NOTE]
>  Notieren Sie die SQL Server Verbindungs Zeichenfolge nach "policystore ConnectionString =" in der folgenden Datei: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` . Diese Zeichenfolge ist für die Wiederherstellung der ursprünglichen AD FS-Konfiguration auf dem Verbundserver erforderlich.

4. Notieren Sie die Identität des AD FS 2.0-Verbunddienstkontos und das Kennwort für dieses Konto.

Der Identitätswert befindet sich in der Konsole **Dienste** in der Spalte **Anmelden als** unter **AD FS 2.0-Windows-Dienst**. Zeichnen Sie den Wert manuell auf.

## <a name="step-2-back-up-custom-attribute-stores"></a>Schritt 2: Sichern von benutzerdefinierten Attribut speichern
 Informationen zu von AD FS verwendeten benutzerdefinierten Attributspeichern erhalten Sie mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um Informationen zu den benutzerdefinierten Attribut speichern zu finden: `PSH:>Get-ADFSAttributeStore` . Die Schritte zum Aktualisieren oder Migrieren von Attributspeichern variieren.

## <a name="step-3-back-up-webpage-customizations"></a>Schritt 3: Sichern von Webseiten Anpassungen
 Kopieren Sie die AD FS-Webseiten und die Datei **web.config** aus dem zugeordneten Verzeichnis in den virtuellen Pfad **“/adfs/ls”** in IIS, um alle Webseitenanpassungen zu sichern. Standardmäßig befindet sie sich im Verzeichnis **%systemdrive%\inetpub\adfs\ls**.

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) -Verbund Servers [Vorbereiten der Migration des Verbund Server Proxys von AD FS 2,0](prepare-to-migrate-ad-fs-fed-proxy.md) [Migrieren des AD FS 2,0](migrate-the-ad-fs-fed-server.md) Verbund Servers migrieren des [AD FS 2,0](migrate-the-ad-fs-2-fed-server-proxy.md) Verbund Server Proxy [Migrieren der AD FS 1,1-Web-Agents](migrate-the-ad-fs-web-agent.md)