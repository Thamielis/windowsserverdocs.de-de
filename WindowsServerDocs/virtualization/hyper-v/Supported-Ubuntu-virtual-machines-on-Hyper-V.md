---
title: Unterstützte virtuelle Ubuntu-Computer auf Hyper-V
description: Listet die in jeder Version enthaltenen Linux-Integrationsdienste und-Funktionen auf.
ms.topic: article
ms.assetid: 95ea5f7c-25c6-494b-8ffd-2a77f631ee94
ms.author: benarm
author: BenjaminArmstrong
ms.date: 08/29/2020
ms.openlocfilehash: cc59a9c45a1dee797196c8a12550945d3d834cd7
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746575"
---
# <a name="supported-ubuntu-virtual-machines-on-hyper-v"></a>Unterstützte virtuelle Ubuntu-Computer auf Hyper-V

>Gilt für: Windows Server 2019, Hyper-v Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows 10, Windows 8.1

Die folgende featureverteilungszuordnung gibt die Features in den einzelnen Versionen an. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach der Tabelle aufgelistet.

## <a name="table-legend"></a>Tabellen Legende

* **Integrierte** -LIS sind als Teil dieser Linux-Distribution enthalten. Das von Microsoft bereitgestellte LIS-Downloadpaket funktioniert für diese Verteilung nicht. Installieren Sie es also nicht. Die Kernel-Modul Versionsnummern für die integrierten Lis (z. **b. lsmod**) unterscheiden sich von der Versionsnummer des von Microsoft bereitgestellten LIS-Download Pakets. Ein Konflikt weist nicht darauf hin, dass der integrierte LIS veraltet ist.

* &#10004;-Feature verfügbar

* (*leer*): Feature nicht verfügbar

|**Feature**|**Windows Server-Betriebssystemversion**|**20.04 LTS**|**18.04 LTS**|**16.04 LTS**|**14.04 LTS**|
|-|-|-|-|-|-|
|**Verfügbarkeit**||Integriert|Integriert|Integriert|Integriert|
|**[Kernspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 genaue Zeit|2019, 2016|&#10004;|&#10004;|&#10004;||
|**[Netzwerk](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||
|Großrahmen|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN-Tagging und-Abschneiden|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injektion|2019, 2016, 2012 R2|&#10004; Hinweis 1|&#10004; Hinweis 1|&#10004; Hinweis 1|&#10004; Hinweis 1|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|TCP-Segmentierung und Prüfsummen Offloads|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|SR-IOV|2019, 2016|&#10004;|&#10004;|&#10004;||
|**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**|||||
|Vhdx-Größe ändern|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Virtueller Fibre Channel|2019, 2016, 2012 R2|&#10004; Hinweis 2|&#10004; Hinweis 2|&#10004; Hinweis 2|&#10004; Hinweis 2|
|Sicherung virtueller Computer|2019, 2016, 2012 R2|&#10004; Hinweis 3, 4, 5|&#10004; Hinweis 3, 4, 5|&#10004; Hinweis 3, 4, 5|&#10004; Hinweis 3, 4, 5|
|Trim-Unterstützung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|SCSI-WWN|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|||||
|Unterstützung für den unterstützten Kernel|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|MMIO-Lücke konfigurieren|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher-Hot-Add|2019, 2016, 2012 R2|&#10004; Hinweis 6, 7, 8|&#10004; Hinweis 6, 7, 8|&#10004; Hinweis 6, 7, 8|&#10004; Hinweis 6, 7, 8|
|Dynamischer Arbeitsspeicher-Ballooning|2019, 2016, 2012 R2|&#10004; Hinweis 6, 7, 8|&#10004; Hinweis 6, 7, 8|&#10004; Hinweis 6, 7, 8|&#10004; Hinweis 6, 7, 8|
|Größenänderung des Lauf Zeit Speichers|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||
|Hyper-V-spezifisches Videogerät|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|**[Verschiedenes](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**|||||
|Schlüssel-Wert-Paar|2019, 2016, 2012 R2|&#10004; Hinweis 5, 9|&#10004; Hinweis 5, 9|&#10004; Hinweis 5, 9|&#10004; Hinweis 5, 9|
|Nicht mastbare Unterbrechung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Dateikopie von Host zu Gast|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|lsvmbus-Befehl|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Hyper-V-Sockets|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|
|PCI-Passthrough/DDA|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|||||
|Starten mithilfe von UEFI|2019, 2016, 2012 R2|&#10004; Notiz 10, 11|&#10004; Notiz 10, 11|&#10004; Notiz 10, 11|&#10004; Notiz 10, 11|
|Sicherer Start|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|

## <a name="notes"></a>Hinweise

1. Die statische IP-Injektion funktioniert möglicherweise nicht, wenn der **Netzwerk-Manager** für einen bestimmten, für Hyper-V spezifischen Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Stellen Sie sicher, dass der Netzwerk-Manager vollständig ausgeschaltet ist oder für einen bestimmten Netzwerkadapter über seine **ifcfg-ethX-** Datei ausgeschaltet wurde, um eine reibungslose Funktionsweise der statischen IP-Injektion sicherzustellen.

2. Stellen Sie bei der Verwendung von Virtual Fiber Channel-Geräten sicher, dass die logische Gerätenummer 0 (LUN 0) aufgefüllt wurde. Wenn LUN 0 nicht aufgefüllt wurde, kann ein virtueller Linux-Computer möglicherweise keine systemeigenen Fiber-Fibre Channel-Geräte einbinden.

3. Wenn während eines Sicherungs Vorgangs für virtuelle Computer geöffnete Datei Handles vorhanden sind, müssen die gesicherten VHDs in einigen Fällen möglicherweise bei der Wiederherstellung einer Dateisystem Konsistenzprüfung () unterzogen werden `fsck` .

4. Bei Live Sicherungs Vorgängen kann ein Fehler auftreten, wenn der virtuelle Computer über ein angefügtes iSCSI-Gerät oder einen direkt angeschlossenen Speicher (auch als Pass-Through-Datenträger bezeichnet) verfügt.

5. Bei LTS-Releases (Long Term Support) wird der neueste HWE-Kernel (Virtual Hardware Enablement) für aktuelle Linux-Integration Services verwendet.

   Führen Sie die folgenden Befehle als root (or sudo) aus, um den mit Azure optimierten Kernel auf 16,04, 18,04 und 20,04 zu installieren:

   ```bash
   # apt-get update
   # apt-get install linux-azure
   ```
6. Die Unterstützung dynamischer Arbeitsspeicher ist nur auf virtuellen 64-Bit-Computern verfügbar.

7. Dynamischer Arbeitsspeicher Vorgänge können fehlschlagen, wenn für das Gast Betriebssystem zu wenig Arbeitsspeicher verfügbar ist. Im folgenden finden Sie einige bewährte Methoden:

   * Start Speicher und minimaler Arbeitsspeicher müssen größer oder gleich dem vom Verteilungs Anbieter empfohlenen Arbeitsspeicher sein.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System belegen, können bis zu 80 Prozent des verfügbaren Arbeitsspeichers verbrauchen.

8. Wenn Sie dynamischer Arbeitsspeicher unter den Betriebssystemen Windows Server 2019, Windows Server 2016 oder Windows Server 2012/2012 R2 verwenden, geben Sie den **Start Speicher**, den **minimalen Arbeitsspeicher**und den **maximalen Arbeitsspeicher** Parameter in Vielfachen von 128 Megabyte (MB) an. Wenn dies nicht der Fall ist, kann dies zu Fehlern beim Hinzufügen von Fehlern führen, und es wird möglicherweise keine Arbeitsspeicher Zunahme für ein Gast Betriebssystem angezeigt.

9. In Windows Server 2019, Windows Server 2016 oder Windows Server 2012 R2 funktioniert die Schlüssel-Wert-Paar-Infrastruktur ohne Linux-Software Update möglicherweise nicht ordnungsgemäß. Wenden Sie sich an Ihren Verteilungs Hersteller, um das Software Update zu erhalten, falls Probleme mit diesem Feature auftreten.

10. Auf virtuellen Computern der Generation 2 auf Windows Server 2012 R2 ist der sichere Start standardmäßig aktiviert, und einige virtuelle Linux-Computer werden erst gestartet, wenn die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Abschnitt **Firmware** der Einstellungen für den virtuellen Computer im **Hyper-V-Manager** deaktivieren, oder Sie können ihn mithilfe von PowerShell deaktivieren:

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

11. Führen Sie die folgenden Schritte aus, bevor Sie versuchen, die VHD eines vorhandenen virtuellen Computers der Generation 2 zu kopieren, um neue virtuelle Maschinen der Generation 2 zu erstellen:

    1. Melden Sie sich bei dem vorhandenen virtuellen Computer der Generation 2 an.

    2. Wechseln Sie in das Verzeichnis für das Start-EFI:

       ```bash
       # cd /boot/efi/EFI
       ```

    3. Kopieren Sie das Ubuntu-Verzeichnis in ein neues Verzeichnis mit dem Namen Boot:

       ```bash
       # sudo cp -r ubuntu/ boot
       ```

    4. Wechseln Sie in das neu erstellte Start Verzeichnis:

       ```bash
       # cd boot
       ```

    5. Benennen Sie die Datei shimx64. EFI um:

       ```bash
       # sudo mv shimx64.efi bootx64.efi
       ```

## <a name="see-also"></a>Weitere Informationen

* [Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle SuSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Set-vmfirmware](/powershell/module/hyper-v/set-vmfirmware?view=win10-ps)

* [Ubuntu 14,04 in einem virtuellen Computer der Generation 2, den virtualisierungsblog von Ben Armstrong](/archive/blogs/virtual_pc_guy/ubuntu-14-04-in-a-generation-2-vm)
