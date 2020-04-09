---
title: Always On VPN bereitstellen
description: Dieses Thema enthält ausführliche Anweisungen zum Bereitstellen von Always on-VPN in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.openlocfilehash: 0889c8a3472509ec3e3a9d013ba649df7ac63d24
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860053"
---
# <a name="deploy-always-on-vpn"></a>Always On VPN bereitstellen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Erfahren Sie mehr über die erweiterten Features für Always on-VPN](always-on-vpn-adv-options.md)
- [**Weiter:** Schritt 1: Beginnen der Planung der Always on-VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

In diesem Abschnitt erfahren Sie mehr über den Workflow für die Bereitstellung von Always on-VPN-Verbindungen für in die Domäne eingebundenen Windows 10-Client Computern. Wenn Sie den **bedingten Zugriff konfigurieren** möchten, um zu optimieren, wie VPN-Benutzer auf Ihre Ressourcen zugreifen, finden Sie unter [bedingter Zugriff für VPN-Konnektivität mithilfe von Azure AD](../../ad-ca-vpn-connectivity-windows10.md)Weitere Informationen. Weitere Informationen zum bedingten Zugriff für VPN-Konnektivität mithilfe von Azure AD finden Sie unter [bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). 

Das folgende Diagramm veranschaulicht den Workflow Prozess für die verschiedenen Szenarien beim Bereitstellen Always on VPN:

[![Flussdiagramm des Workflows für die Always on-VPN-Bereitstellung](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow.png)

> [!IMPORTANT]
> Für diese Bereitstellung ist es nicht erforderlich, dass auf Ihren Infrastruktur Servern, z. b. Computern, auf denen Active Directory Domain Services, Active Directory Zertifikat Dienste und Netzwerk Richtlinien Server ausgeführt wird, Windows Server 2016 ausgeführt wird. Sie können frühere Versionen von Windows Server, wie z. b. Windows Server 2012 R2, für die Infrastruktur Server und für den Server verwenden, auf dem Remote Zugriff ausgeführt wird.

## <a name="step-1-plan-the-always-on-vpn-deployment"></a>[Schritt 1: Planen der Always on VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

In diesem Schritt beginnen Sie mit der Planung und Vorbereitung ihrer Always on-VPN-Bereitstellung. Vor der Installation der Remote Zugriffs-Server Rolle auf dem Computer, den Sie als VPN-Server verwenden möchten. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.

## <a name="step-2-configure-the-always-on-vpn-server-infrastructure"></a>[Schritt 2: Konfigurieren der Always on VPN-Server Infrastruktur](vpn-deploy-server-infrastructure.md)

In diesem Schritt installieren und konfigurieren Sie die serverseitigen Komponenten, die zur Unterstützung des VPN erforderlich sind. Zu den serverseitigen Komponenten gehört das Konfigurieren der PKI für die Verteilung der Zertifikate, die von Benutzern, dem VPN-Server und dem NPS-Server verwendet werden.  Außerdem konfigurieren Sie RRAS für die Unterstützung von IKEv2-Verbindungen und den NPS-Server zum Ausführen der Autorisierung für die VPN-Verbindungen.

Zum Konfigurieren der Serverinfrastruktur müssen Sie die folgenden Aufgaben ausführen:

- **Auf einem mit Active Directory Domain Services konfigurierten Server:** Aktivieren Sie die automatische Zertifikat Registrierung in Gruppenrichtlinie für Computer und Benutzer, erstellen Sie die Gruppe "VPN-Benutzer", die Gruppe "VPN-Server" und die Gruppe "NPS-Server", und fügen Sie jeder Gruppe Mitglieder hinzu.
- **Auf einer Active Directory Zertifikat Server-Zertifizierungsstelle:** Erstellen Sie die Zertifikat Vorlagen Benutzerauthentifizierung, VPN-Server Authentifizierung und NPS-Server Authentifizierung.
- **Auf in die Domäne eingebundenen Windows 10-Clients:** Registrieren und Validieren von Benutzer Zertifikaten

## <a name="step-3-configure-the-remote-access-server-for-always-on-vpn"></a>[Schritt 3. Konfigurieren des Remote Zugriffs Servers für die Always on-VPN](vpn-deploy-ras.md)

In diesem Schritt konfigurieren Sie das RAS-VPN, um IKEv2-VPN-Verbindungen zuzulassen, Verbindungen von anderen VPN-Protokollen zu verweigern und einen statischen IP-Adresspool für die Ausstellung von IP-Adressen für die Verbindung mit autorisierten VPN-Clients zuzuweisen.

Zum Konfigurieren von RAS müssen Sie die folgenden Aufgaben ausführen:

- Registrieren und Validieren des VPN-Serverzertifikats
- Installieren und Konfigurieren des RAS-VPN

## <a name="step-4-install-and-configure-the-nps-server"></a>[Schritt 4: Installieren und Konfigurieren des NPS-Servers](vpn-deploy-nps.md)

In diesem Schritt installieren Sie den Netzwerk Richtlinien Server (Network Policy Server, NPS) mithilfe von Windows PowerShell oder dem Server-Manager Assistenten zum Hinzufügen von Rollen und Features. Außerdem können Sie NPS so konfigurieren, dass alle Authentifizierungs-, Autorisierungs-und Buchhaltungsaufgaben für Verbindungsanforderungen verarbeitet werden, die vom VPN-Server empfangen werden.

Zum Konfigurieren von NPS müssen Sie die folgenden Aufgaben ausführen:

- Registrieren des NPS-Servers in Active Directory
- Konfigurieren der RADIUS-Kontoführung für Ihren NPS-Server
- Hinzufügen des VPN-Servers als RADIUS-Client in NPS
- Konfigurieren der Netzwerk Richtlinie in NPS
- Automatische Registrierung des NPS-Server Zertifikats

## <a name="step-5-configure-dns-and-firewall-settings-for-always-on-vpn"></a>[Schritt 5: Konfigurieren von DNS-und Firewalleinstellungen für Always on-VPN](vpn-deploy-dns-firewall.md)

In diesem Schritt konfigurieren Sie DNS-und Firewalleinstellungen. Wenn Remote-VPN-Clients eine Verbindung herstellen, verwenden Sie die gleichen DNS-Server, die von den internen Clients verwendet werden. auf diese Weise können Namen auf die gleiche Weise wie die übrigen internen Arbeitsstationen aufgelöst werden. 

## <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>[Schritt 6: Konfigurieren von Windows 10-Client Always on-VPN-Verbindungen](vpn-deploy-client-vpn-connections.md)

In diesem Schritt konfigurieren Sie die Windows 10-Client Computer für die Kommunikation mit dieser Infrastruktur über eine VPN-Verbindung. Sie können verschiedene Technologien zum Konfigurieren von Windows 10-VPN-Clients verwenden, einschließlich Windows PowerShell, Microsoft Endpoint Configuration Manager und InTune. Alle drei erfordern ein XML-VPN-Profil, um die entsprechenden VPN-Einstellungen zu konfigurieren.

## <a name="step-7-optional-configure-conditional-access-for-vpn-connectivity"></a>[Schritt 7: Optionale Konfigurieren des bedingten Zugriffs für VPN-Konnektivität](../../ad-ca-vpn-connectivity-windows10.md)

In diesem optionalen Schritt können Sie optimieren, wie autorisierte VPN-Benutzer auf Ihre Ressourcen zugreifen. Mit Azure AD bedingten Zugriff für VPN-Konnektivität können Sie die VPN-Verbindungen schützen. Der bedingte Zugriff ist eine Richtlinien basierte Evaluierungs-Engine, mit der Sie Zugriffsregeln für alle Azure AD verbundenen Anwendungen erstellen können. Weitere Informationen finden Sie unter [Azure Active Directory (Azure AD) bedingtem Zugriff](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).

## <a name="next-step"></a>Nächster Schritt

[Schritt 1: Planen Sie die Always on-VPN-Bereitstellung](always-on-vpn-deploy-planning.md): vor der Installation der RAS-Server Rolle auf dem Computer, den Sie als VPN-Server verwenden möchten. Nach dem ordnungsgemäßen Planen können Sie Always On VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mit Azure AD konfigurieren.  
