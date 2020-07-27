---
title: Unterstützte Windows 10-Sicherheitskonfigurationen für Remotedesktopdienste-VDI
description: Enthält Informationen zu unterstützten Konfigurationen für Windows 10-VDI mit RDS in Windows Server 2016.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 10/27/2016
ms.topic: article
ms.assetid: 8f164f5d-a498-4f91-a12f-3e01d554f810
author: lizap
manager: dongill
ms.openlocfilehash: 4ecd290a910ddbb1aba85b26764fb86e30731172
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86963352"
---
# <a name="supported-windows-10-security-configurations-for-remote-desktop-services-vdi"></a>Unterstützte Windows 10-Sicherheitskonfigurationen für Remotedesktopdienste-VDI

> Gilt für: Windows Server 2016

Windows 10 und Windows Server 2016 verfügen über neue, in das Betriebssystem integrierte Schutzebenen, die Sie vor Sicherheitslücken schützen, böswillige Angriffe blockieren helfen und die Sicherheit von virtuellen Computern, Anwendungen und Daten verbessern.

> [!NOTE]
> Lesen Sie unbedingt die [Informationen zu unterstützten Konfigurationen der Remotedesktopdienste](rds-supported-config.md).

Die folgende Tabelle zeigt, welche dieser neuen Features in einer VDI-Bereitstellung mithilfe von RDS unterstützt werden.

|  VDI-Sammlungstyp               |  Verwaltet – gepoolt |  Verwaltet – persönlich |  Nicht verwaltet – gepoolt                                     |  Nicht verwaltet – persönlich                                    |
|-------------------------------------|------------------|--------------------|--------------------------------------------------------|--------------------------------------------------------|
| [Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard)                    | Ja              | Ja                | Ja                                                    | Ja                                                    |
| [Device Guard](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)                        | Ja              | Ja                | Ja                                                    | Ja                                                    |
| [Remote Credential Guard](/windows/security/identity-protection/remote-credential-guard)             | Nein               | Nein                 | Nein                                                     | Nein                                                     |
| [Abgeschirmte VMs und VMs mit Verschlüsselungsunterstützung](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) | Nein               | Nein                 | VMs mit Verschlüsselungsunterstützung mit zusätzlicher Konfiguration | VMs mit Verschlüsselungsunterstützung mit zusätzlicher Konfiguration |

## <a name="remote-credential-guard"></a>Remote Credential Guard:

Remote Credential Guard wird nur für direkte Verbindungen mit den Zielcomputern unterstützt, nicht für Verbindungen über den Remotedesktop-Verbindungsbroker und das Remotedesktop-Gateway.
> [!NOTE]
> Wenn Sie einen Verbindungsbroker in einer Einzelinstanzumgebung betreiben und der DNS-Name mit dem Computernamen übereinstimmt, sind Sie möglicherweise in der Lage, Remote Credential Guard zu verwenden, jedoch wird dies nicht unterstützt.

## <a name="shielded-vms-and-encryption-supported-vms"></a>Abgeschirmte VMs und VMs mit Verschlüsselungsunterstützung: 

- Abgeschirmte VMs werden in Remotedesktopdienste-VDI nicht unterstützt 

Um VMs mit Verschlüsselungsunterstützung zu nutzen:
- Verwenden Sie eine nicht verwaltete Sammlung und eine Bereitstellungstechnologie außerhalb des Prozesses zur Sammlungserstellung in den Remotedesktopdiensten, um die virtuellen Computer bereitzustellen. 
- Benutzerprofil-Datenträger werden nicht unterstützt, da sie differenzielle Datenträger benötigen 
