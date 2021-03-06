---
title: Verwalten der rollenbasierten Zugriffssteuerung mit Windows PowerShell
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 4f13f78e-0114-4e41-9a28-82a4feccecfc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 61daa0e76fdd5f8db5d81a9709d3bc8ee31c78e2
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997576"
---
# <a name="manage-role-based-access-control-with-windows-powershell"></a>Verwalten der rollenbasierten Zugriffssteuerung mit Windows PowerShell

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie IPAM zum Verwalten der rollenbasierten Zugriffs Steuerung mit Windows PowerShell verwenden.

>[!NOTE]
>Die IPAM-Windows PowerShell-Befehlsreferenz finden Sie unter [ipamserver-Cmdlets in Windows PowerShell](/powershell/module/ipamserver/?view=win10-ps).

Mit den neuen Windows PowerShell-IPAM-Befehlen können Sie die Zugriffs Bereiche von DNS-und DHCP-Objekten abrufen und ändern. Die folgende Tabelle veranschaulicht den korrekten Befehl, der für die einzelnen IPAM-Objekte verwendet werden soll.

|IPAM-Objekt|Befehl|BESCHREIBUNG|
|---------------|-----------|---------------|
|DNS-Server|Get-ipamdnsserver|Mit diesem Cmdlet wird das DNS-Server Objekt in IPAM zurückgegeben.|
|DNS-Zone|Get-ipamdnszone|Mit diesem Cmdlet wird das DNS-Zonen Objekt in IPAM zurückgegeben.|
|DNS-Ressourcen Daten Satz|Get-ipamresourcerecord|Dieses Cmdlet gibt das DNS-Ressourcen Daten Satz Objekt in IPAM zurück.|
|Bedingte DNS-Weiterleitung|Get-ipamdnsconditionalforwarder|Dieses Cmdlet gibt das DNS-Objekt für die bedingte Weiterleitung in IPAM zurück.|
|DHCP-Server|Get-ipamdhcpserver|Dieses Cmdlet gibt das DHCP-Server Objekt in IPAM zurück.|
|DHCP-Bereichsgruppierung|Get-ipamdhcpsuperscope|Dieses Cmdlet gibt das DHCP-Bereichs Gruppierung-Objekt in IPAM zurück.|
|DHCP-Bereich|Get-ipamdhcpscope|Dieses Cmdlet gibt das DHCP-Bereichs Objekt in IPAM zurück.|

Im folgenden Beispiel der Befehlsausgabe `Get-IpamDnsZone` Ruft das Cmdlet die **Dublin.contoso.com** -DNS-Zone ab.

```
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com

ZoneName             : dublin.contoso.com
ZoneType             : Forward
AccessScopePath      : \Global\Dublin
IsSigned             : False
DynamicUpdateStatus  : None
ScavengeStaleRecords : False
```

## <a name="setting-access-scopes-on-ipam-objects"></a>Festlegen von Zugriffs Bereichen für IPAM-Objekte
Mithilfe des-Befehls können Sie Zugriffs Bereiche für IPAM-Objekte festlegen `Set-IpamAccessScope` . Sie können diesen Befehl verwenden, um den Zugriffs Bereich auf einen bestimmten Wert für ein Objekt festzulegen oder um zu bewirken, dass die Objekte den Zugriffs Bereich von übergeordneten Objekten erben. Im folgenden finden Sie die Objekte, die Sie mit diesem Befehl konfigurieren können.

-   DHCP-Bereich

-   DHCP-Server

-   DHCP-Bereichsgruppierung

-   Bedingte DNS-Weiterleitung

-   DNS-Ressourcen Einträge

-   DNS-Server

-   DNS-Zone

-   IP-Adressblock

-   IP-Adressbereich

-   IP-Adressraum

-   IP-Adresssubnetz

Im folgenden finden Sie die Syntax für den `Set-IpamAccessScope` Befehl.

```
NAME
    Set-IpamAccessScope

SYNTAX
    Set-IpamAccessScope [-IpamRange] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Set-IpamAccessScope [-IpamDnsServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDhcpServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDhcpSuperscope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDhcpScope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDnsConditionalForwarder] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDnsResourceRecord] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamDnsZone] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamAddressSpace] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]
    [<CommonParameters>]

    Set-IpamAccessScope [-IpamSubnet] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]

    Set-IpamAccessScope [-IpamBlock] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]
```

Im folgenden Beispiel wird der Zugriffs Bereich der DNS-Zone **Dublin.contoso.com** von **Dublin** in **Europa**geändert.

```
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com

ZoneName             : dublin.contoso.com
ZoneType             : Forward
AccessScopePath      : \Global\Dublin
IsSigned             : False
DynamicUpdateStatus  : None
ScavengeStaleRecords : False

PS C:\Users\Administrator.CONTOSO> $a = Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com
PS C:\Users\Administrator.CONTOSO> Set-IpamAccessScope -IpamDnsZone -InputObject $a -AccessScopePath \Global\Europe -PassThru

ZoneName             : dublin.contoso.com
ZoneType             : Forward
AccessScopePath      : \Global\Europe
IsSigned             : False
DynamicUpdateStatus  : None
ScavengeStaleRecords : False
```