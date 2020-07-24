---
title: SMB-Datei-und Druckerfreigabe Ports müssen geöffnet sein.
ms.date: 07/02/2012
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: d9d24f1ce66ca691bfa31479a00b9ecf719abe1e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961302"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>SMB: Ports für Datei- und Druckerfreigaben sollten offen sein


Aktualisiert: 2. Februar 2011

Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, Windows Server 2008 R2

*Dieses Thema dient der Behebung eines bestimmten Problems, das durch einen Best Practices Analyzer Scan identifiziert wird. Die Informationen in diesem Thema sollten nur auf Computer angewendet werden, auf denen die Dateidienste Best Practices Analyzer ausgeführt wurden und die in diesem Thema behandelt werden. Weitere Informationen zu bewährten Methoden und Scans finden Sie unter* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?linkid=122786%0d%0a).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Betriebssystem</strong></p></td>
<td><p>Windows Server</p></td>
</tr>
<tr class="even">
<td><p><strong>Produkt/Feature</strong></p></td>
<td><p>Dateidienste</p></td>
</tr>
<tr class="odd">
<td><p><strong>Severity</strong></p></td>
<td><p>Fehler</p></td>
</tr>
<tr class="even">
<td><p><strong>Kategorie</strong></p></td>
<td><p>Konfiguration</p></td>
</tr>
</tbody>
</table>

## <a name="issue"></a>Problem

> *Die Firewallports, die für die Datei-und Druckerfreigabe erforderlich sind, sind nicht geöffnet (Ports 445 und 139).*

## <a name="impact"></a>Auswirkung

> *Computer können nicht auf freigegebene Ordner und andere auf Server Message Block (SMB) basierende Netzwerkdienste auf diesem Server zugreifen.*

## <a name="resolution"></a>Lösung

> *Aktivieren Sie die Datei-und Druckerfreigabe für die Kommunikation über die Firewall des Computers.*

Zum Ausführen dieser Prozedur müssen Sie Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein.

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>So öffnen Sie die Firewallports zum Aktivieren der Datei-und Druckerfreigabe

1.  Öffnen Sie die Systemsteuerung, klicken Sie auf **System und Sicherheit**, und klicken Sie dann auf **Windows-Firewall**.

2.  Klicken Sie im linken Bereich auf **Erweiterte Einstellungen**, und klicken Sie in der Konsolen Struktur auf **Eingehende Regeln**.

3.  Suchen Sie unter **Eingehende Regeln**die Regel **Datei und die Druckerfreigabe (NB-Session-in)** und **Datei-und Druckerfreigabe (SMB-in)**.

4.  Klicken Sie mit der rechten Maustaste auf jede Regel, und klicken Sie dann auf **Regel aktivieren**.

## <a name="additional-references"></a>Zusätzliche Verweise

Grundlegendes [zu freigegebenen Ordnern und der Windows-Firewall](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731402(v=ws.11))(https://technet.microsoft.com/library/cc731402.aspx)
