---
title: Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V
description: Listet die Versionen der Linux-Integrationsdienste für unterstützte CentOS-und Red Hat Enterprise-Distributionen auf.
ms.prod: windows-server
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 4bf8783d-dee5-4b3e-8cce-2b11b117c189
author: danihalfin
ms.author: vichen
ms.date: 04/06/2020
ms.openlocfilehash: 5d30f373390ffa61ebe8710de82d20107456462b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855983"
---
# <a name="supported-centos-and-red-hat-enterprise-linux-virtual-machines-on-hyper-v"></a>Unterstützte virtuelle Computer der CentOS-und Red Hat Enterprise Linux auf Hyper-V

>Gilt für: Windows Server 2019, Hyper-v Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows 10, Windows 8.1

Die folgenden featureverteilungszuordnungen zeigen die Funktionen an, die in integrierten und herunterladbaren Versionen von Linux-Integration Services vorhanden sind. Die bekannten Probleme und Problem Umgehungen für die einzelnen Verteilungen werden nach den Tabellen aufgelistet.

Die integrierten Red Hat Enterprise Linux Integration Services Treiber für Hyper-v (verfügbar seit Red Hat Enterprise Linux 6,4) sind für Red Hat Enterprise Linux Gäste ausreichend, damit Sie mit den hochleistungsfähigen synthetischen Geräten auf Hyper-v-Hosts ausgeführt werden können. Diese integrierten Treiber werden für diese Verwendung von Red hat zertifiziert. Zertifizierte Konfigurationen können auf der red hat-Webseite angezeigt werden: [red hat Certification Catalog](https://access.redhat.com/ecosystem/search/#/ecosystem/Red%20Hat%20Enterprise%20Linux?sort=sortTitle%20asc&vendors=Microsoft&category=Server). Es ist nicht erforderlich, Linux-Integration Services Pakete aus dem Microsoft Download Center herunterzuladen und zu installieren. Dadurch kann der red hat-Support eingeschränkt werden, wie in red hat Knowledge dgebase-Artikel 1067: [red hat Knowledge dgebase 1067](https://access.redhat.com/articles/1067)beschrieben.

Da bei der Aktualisierung des Kernels mögliche Konflikte zwischen der integrierten LIS-Unterstützung und der herunterladbaren LIS-Unterstützung auftreten, deaktivieren Sie automatische Updates, deinstallieren Sie die von Lis herunterladbaren Pakete, aktualisieren Sie den Kernel, starten Sie, und installieren Sie dann die neueste Version von Lis und starten Sie erneut.

> [!NOTE]
> Offizielle Red Hat Enterprise Linux Zertifizierungs Informationen sind im [red hat-Kunden Portal](https://access.redhat.com/ecosystem/search/#/category/Server?sort=sortTitle%20asc&query=windows%20server&ecosystem=Red%20Hat%20Enterprise%20Linux)verfügbar.

In diesem Abschnitt:

* [RHEL/CentOS 8. x-Serie](#rhelcentos-8x-series)

* [RHEL/CentOS 7. x-Serie](#rhelcentos-7x-series)

* [RHEL/CentOS 6. x-Reihe](#rhelcentos-6x-series)

* [RHEL/CentOS 5. x-Reihe](#rhelcentos-5x-series)

* [Hinweise](#notes)

## <a name="table-legend"></a>Tabellen Legende

* **Integrierte** -LIS sind als Teil dieser Linux-Distribution enthalten. Die Kernel-Modul Versionsnummern für die integrierten Lis (z. **b. lsmod**) unterscheiden sich von der Versionsnummer des von Microsoft bereitgestellten LIS-Download Pakets. Ein Konflikt weist nicht darauf hin, dass der integrierte LIS veraltet ist.

* &#10004;-Feature verfügbar

* (*leer*): Feature nicht verfügbar

## <a name="rhelcentos-8x-series"></a>RHEL/CentOS 8. x-Serie

|       **Feature**     |       **Windows Server-Version**      |       **8,1**     |       **8,0**     | 
|-----------------------|---------------------------------------|-------------------|-------------------|
|       **Verfügbarkeit**        |   |   |
|       **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019, 2016, 2012 R2 | &#10004; | &#10004;
|       Windows Server 2016 genaue Zeit       | 2019, 2016 | &#10004; | &#10004; 
|       **[Ungs](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   |  |
|       Großrahmen        | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       VLAN-Tagging und-Abschneiden       | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Livemigration      | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       Statische IP-Injektion     |  2019, 2016, 2012 R2 | &#10004;Hinweis 2 | &#10004;Hinweis 2|
|       vRSS     | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       TCP-Segmentierung und Prüfsummen Offloads | 2019, 2016, 2012 R2 | &#10004;|  &#10004; |
|       SR-IOV  | 2019, 2016 |  &#10004;   | &#10004; |
|       **[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  |  |
|       Vhdx-Größe ändern  | 2019, 2016, 2012 R2 | &#10004; | &#10004; |
|       Virtueller Fibre Channel | 2019, 2016, 2012 R2 | &#10004;Hinweis 3  | &#10004;Hinweis 3 |
|       Sicherung virtueller Computer  | 2019, 2016, 2012 R2 | &#10004;Hinweis 5 | &#10004;Hinweis 5|
|       Trim-Unterstützung | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       SCSI-WWN | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       **[Gedenkens](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |  |
|       Unterstützung für den unterstützten Kernel  | 2019, 2016, 2012 R2 |  N/V | N/V
|       MMIO-Lücke konfigurieren  | 2019, 2016, 2012 R2 | &#10004; | &#10004;  |
|       Dynamischer Arbeitsspeicher-Hot-Add | 2019, 2016, 2012 R2  | &#10004;Notiz 8, 9, 10 | &#10004;Notiz 8, 9, 10 |
|       Dynamischer Arbeitsspeicher-Ballooning | 2019, 2016, 2012 R2 | &#10004;Notiz 8, 9, 10 | &#10004;Notiz 8, 9, 10 |
|       Größenänderung des Lauf Zeit Speichers | 2019, 2016  | &#10004;  | &#10004; |
|       **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | | |
|       Hyper-V-spezifisches Videogerät | 2019, 2016, 2012 R2 | &#10004;   | &#10004; |
|       **[Verschiedensten](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | | |
|       Schlüssel-Wert-Paar  | 2019, 2016, 2012 R2 | &#10004;   | &#10004;  |
|       Nicht mastbare Unterbrechung | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Dateikopie von Host zu Gast | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       lsvmbus-Befehl | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Hyper-V-Sockets | 2019, 2016 | &#10004;  | &#10004; |
|       PCI-Passthrough/DDA | 2019, 2016 | &#10004; | &#10004; |
| **[Virtuelle Maschinen der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       Starten mithilfe von UEFI | 2019, 2016, 2012 R2 |  &#10004;Hinweis 14  | &#10004;Hinweis 14   
|       Sicherer Start | 2019, 2016 |  &#10004; |  &#10004; |


## <a name="rhelcentos-7x-series"></a>RHEL/CentOS 7. x-Serie

Diese Reihe hat nur 64-Bit-Kernel.


|                                                                 **Feature**                                                                  |     **Windows Server-Version**     |                             **7.5-7.8**                             |                             **7.3-7.4**                             |                             **7.0-7.2**                             |     **7.5-7.8**     |       **7,4**       |       **7,3**       |       **7,2**       |       **7,1**       |        **7,0**         |
|----------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|---------------------|---------------------|---------------------|---------------------|---------------------|------------------------|
|                                                               **Verfügbarkeit**                                                               |                                    | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) |      Integriert       |      Integriert       |      Integriert       |      Integriert       |      Integriert       |        Integriert        |
|                          **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                          | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                      Windows Server 2016 genaue Zeit                                                       |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                                                                     |                     |                     |                     |                     |                     |                        |
|                    **[Ungs](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                    |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                                 Großrahmen                                                                 | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                          VLAN-Tagging und-Abschneiden                                                           | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                                Livemigration                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                             Statische IP-Injektion                                                              |     2019, 2016, 2012 R2      |                           &#10004;Hinweis 2                           |                           &#10004;Hinweis 2                           |                           &#10004;Hinweis 2                           |   &#10004;Hinweis 2   |   &#10004;Hinweis 2   |   &#10004;Hinweis 2   |   &#10004;Hinweis 2   |   &#10004;Hinweis 2   |    &#10004;Hinweis 2     |
|                                                                     vRSS                                                                     |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                        |
|                                                    TCP-Segmentierung und Prüfsummen Offloads                                                    | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                        |
|                                                                    SR-IOV                                                                    |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                                                                     |      &#10004;       |      &#10004;       |      &#10004;       |                     |                     |                        |
|                       **[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                       |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                                 Vhdx-Größe ändern                                                                  |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                     |                        |
|                                                            Virtueller Fibre Channel                                                             |        2019, 2016, 2012 R2         |                           &#10004;Hinweis 3                           |                           &#10004;Hinweis 3                           |                           &#10004;Hinweis 3                           |   &#10004;Hinweis 3   |   &#10004;Hinweis 3   |   &#10004;Hinweis 3   |   &#10004;Hinweis 3   |   &#10004;Hinweis 3   |    &#10004;Hinweis 3     |
|                                                         Sicherung virtueller Computer                                                          |        2019, 2016, 2012 R2         |                           &#10004;Hinweis 5                           |                           &#10004;Hinweis 5                           |                           &#10004;Hinweis 5                           |  &#10004;Hinweis 4, 5  | &#10004;Hinweis 4, 5  | &#10004;Hinweis 4, 5  | &#10004;Hinweis 4, 5  | &#10004;Hinweis 4, 5  |   &#10004;Hinweis 4, 5   |
|                                                                 Trim-Unterstützung                                                                 |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                     |                        |
|                                                                   SCSI-WWN                                                                   |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |                     |                     |                     |                     |                        |
|                        **[Gedenkens](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                        |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                              Unterstützung für den unterstützten Kernel                                                              | 2019, 2016, 2012 R2 |                                 N/V                                 |                                 N/V                                 |                                 N/V                                 |         N/V         |         N/V         |         N/V         |         N/V         |         N/V         |          N/V           |
|                                                          MMIO-Lücke konfigurieren                                                           |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                           Dynamischer Arbeitsspeicher-Hot-Add                                                           |     2019, 2016, 2012 R2      |                       &#10004;Notiz 8, 9, 10                        |                       &#10004;Notiz 8, 9, 10                        |                       &#10004;Notiz 8, 9, 10                        | &#10004;Hinweis 9, 10 | &#10004;Hinweis 9, 10 | &#10004;Hinweis 9, 10 | &#10004;Hinweis 9, 10 | &#10004;Hinweis 9, 10 | &#10004;Notiz 8, 9, 10 |
|                                                         Dynamischer Arbeitsspeicher-Ballooning                                                          |     2019, 2016, 2012 R2      |                       &#10004;Notiz 8, 9, 10                        |                       &#10004;Notiz 8, 9, 10                        |                       &#10004;Notiz 8, 9, 10                        | &#10004;Hinweis 9, 10 | &#10004;Hinweis 9, 10 | &#10004;Hinweis 9, 10 | &#10004;Hinweis 9, 10 | &#10004;Hinweis 9, 10 | &#10004;Notiz 8, 9, 10 |
|                                                            Größenänderung des Lauf Zeit Speichers                                                             |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |                     |                     |                     |                     |                     |                        |
|                         **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                         |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                        Hyper-V-spezifisches Videogerät                                                         | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                 **[Verschiedensten](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                 |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                                Schlüssel-Wert-Paar                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                            Nicht mastbare Unterbrechung                                                            |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |
|                                                         Dateikopie von Host zu Gast                                                         |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |                        |
|                                                               lsvmbus-Befehl                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |                     |                     |                     |                     |                     |                        |
|                                                               Hyper-V-Sockets                                                                |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |                     |                     |                     |                     |                     |                        |
|                                                             PCI-Passthrough/DDA                                                              |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                                                                     |      &#10004;       |      &#10004;       |      &#10004;       |                     |                     |                        |
| **[Virtuelle Maschinen der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                    |                                                                     |                                                                     |                                                                     |                     |                     |                     |                     |                     |                        |
|                                                               Starten mithilfe von UEFI                                                                |        2019, 2016, 2012 R2         |                          &#10004;Hinweis 14                           |                          &#10004;Hinweis 14                           |                          &#10004;Hinweis 14                           |  &#10004;Hinweis 14   |  &#10004;Hinweis 14   |  &#10004;Hinweis 14   |  &#10004;Hinweis 14   |  &#10004;Hinweis 14   |    &#10004;Hinweis 14    |
|                                                                 Sicherer Start                                                                  |             2019, 2016             |                              &#10004;                               |                              &#10004;                               |                              &#10004;                               |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |      &#10004;       |        &#10004;        |


## <a name="rhelcentos-6x-series"></a>RHEL/CentOS 6. x-Reihe

Der 32-Bit-Kernel für diese Reihe ist "PE" aktiviert. Es gibt keine integrierte LIS-Unterstützung für RHEL/CentOS 6.0-6.3.

|  **Feature**  | **Windows Server-Version** |  **6.7-6.10** |  **6.4-6.6** | **6.0-6.3** |   **6,10, 6,9, 6,8**   |       **6,6, 6,7**        |          **6,5**          |          **6,4**           |
|---------------|----------------------------|---------------|--------------|-------------|------------------------|---------------------------|----------------------------|---------------------------|
|  **Verfügbarkeit** |   | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) |        Integriert        |         Integriert          |         Integriert          |          Integriert          |
|  **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)** | 2019, 2016, 2012 R2 |  &#10004; | &#10004;  | &#10004;  | &#10004; | &#10004; | &#10004;| &#10004; |
|  Windows Server 2016 genaue Zeit | 2019, 2016 | |  | |  |  |   |   |
|  **[Ungs](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**  | |   |  | |  |  |   |  |
|  Großrahmen | 2019, 2016, 2012 R2 | &#10004; |  &#10004; | &#10004; | &#10004; | &#10004; | &#10004; | &#10004; |
|  VLAN-Tagging und-Abschneiden | 2019, 2016, 2012 R2 | &#10004;Hinweis 1 | &#10004;Hinweis 1 | &#10004;Hinweis 1 | &#10004;Hinweis 1 | &#10004;Hinweis 1|  &#10004;Hinweis 1 |&#10004;Hinweis 1 |
|  Livemigration | 2019, 2016, 2012 R2 | &#10004; | &#10004; | &#10004;| &#10004; | &#10004; | &#10004;  | &#10004; |
|  Statische IP-Injektion |  2019, 2016, 2012 R2 | &#10004;Hinweis 2 |  &#10004;Hinweis 2  | &#10004;Hinweis 2 | &#10004;Hinweis 2 | &#10004;Hinweis 2 | &#10004;Hinweis 2  | &#10004;Hinweis 2 |
|  vRSS  | 2019, 2016, 2012 R2 | &#10004; | &#10004; |  &#10004; | &#10004; | &#10004;  |   |   |
|  TCP-Segmentierung und Prüfsummen Offloads | 2019, 2016, 2012 R2 | &#10004; | &#10004; | &#10004; | &#10004; | &#10004;  |   |    |
|  SR-IOV   | 2019, 2016 |    |  |   |   |   |   |  |
|  **[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**  |  |   |   |  | |  |  | |
|  Vhdx-Größe ändern | 2019, 2016, 2012 R2| &#10004; | &#10004; | &#10004; | &#10004; | &#10004; | &#10004; |  |
|  Virtueller Fibre Channel  | 2019, 2016, 2012 R2 |  &#10004;Hinweis 3  | &#10004;Hinweis 3  | &#10004;Hinweis 3  | &#10004;Hinweis 3 | &#10004;Hinweis 3  | &#10004;Hinweis 3  |    |
|  Sicherung virtueller Computer | 2019, 2016, 2012 R2 | &#10004;Hinweis 5  | &#10004;Hinweis 5  | &#10004;Hinweis 5 | &#10004;Hinweis 4, 5 | &#10004;Hinweis 4, 5 | &#10004;Hinweis 4, 5, 6 | &#10004;Hinweis 4, 5, 6 |
|  Trim-Unterstützung  | 2019, 2016, 2012 R2  | &#10004; | &#10004; | &#10004; | &#10004; |  |  |  |
|  SCSI-WWN  | 2019, 2016, 2012 R2  | &#10004; | &#10004;  | &#10004;  |  |   |  |  |
|  **[Gedenkens](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |  | | |  | |  |  |
|  Unterstützung für den unterstützten Kernel | 2019, 2016, 2012 R2 | &#10004;  | &#10004;  | &#10004; | &#10004; |  &#10004;  |  &#10004; |  &#10004; |
|  MMIO-Lücke konfigurieren  | 2019, 2016, 2012 R2 | &#10004;  | &#10004;  | &#10004;  |  &#10004;  | &#10004;  |  &#10004; |  &#10004; |
|  Dynamischer Arbeitsspeicher-Hot-Add | 2019, 2016, 2012 R2 |  &#10004;Hinweis 7, 9, 10  | &#10004;Hinweis 7, 9, 10 | &#10004;Hinweis 7, 9, 10 | &#10004;Hinweis 7, 9, 10 | &#10004;Hinweis 7, 8, 9, 10 | &#10004;Hinweis 7, 8, 9, 10 | |
|  Dynamischer Arbeitsspeicher-Ballooning | 2019, 2016, 2012 R2 | &#10004;Hinweis 7, 9, 10  | &#10004;Hinweis 7, 9, 10  | &#10004;Hinweis 7, 9, 10 | &#10004;Hinweis 7, 9, 10 |  &#10004;Hinweis 7, 9, 10   |  &#10004;Hinweis 7, 9, 10   | &#10004;Hinweis 7, 9, 10, 11 |
| Größenänderung des Lauf Zeit Speichers | 2019, 2016  |  |   |  |  | |  |  |
| **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** || | | |  |  |  | |
| Hyper-V-spezifisches Videogerät | 2019, 2016, 2012 R2 | &#10004;  | &#10004;  | &#10004;  | &#10004; | &#10004; | &#10004; | |
| **[Verschiedensten](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** |  |  |  |   |  | |  |  |
| Schlüssel-Wert-Paar | 2019, 2016, 2012 R2 | &#10004; | &#10004;| &#10004; | &#10004;Hinweis 12 | &#10004;Hinweis 12 | &#10004;Hinweis 12, 13 | &#10004;Hinweis 12, 13 |
| Nicht mastbare Unterbrechung | 2019, 2016, 2012 R2 | &#10004;  | &#10004;  | &#10004; | &#10004; | &#10004;  |  &#10004;| &#10004; |
| Dateikopie von Host zu Gast | 2019, 2016, 2012 R2 | &#10004;  |  &#10004; | &#10004; | &#10004; | &#10004; | |  |
| lsvmbus-Befehl | 2019, 2016, 2012 R2 |  &#10004; |  &#10004;  |  &#10004; |   |   |    |  |
| Hyper-V-Sockets | 2019, 2016  | &#10004;  |  &#10004;  |  &#10004; |  |   |   |  |
| PCI-Passthrough/DDA | 2019, 2016 | &#10004;  | |   |  |  | |   |
| **[Virtuelle Maschinen der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  | | | | | | |
| Starten mithilfe von UEFI  | 2012 R2 |  |  |  |  |  | |
|  |2019, 2016 | &#10004;Hinweis 14 | &#10004;Hinweis 14| &#10004;Hinweis 14 |    &#10004;Hinweis 14    |  | |  |
|Sicherer Start| 2019, 2016|  ||  |  |  | ||



## <a name="rhelcentos-5x-series"></a>RHEL/CentOS 5. x-Reihe

Für diese Reihe ist ein 32-Bit-PE-Kernel verfügbar. Vor 5,9 gibt es keine integrierte LIS-Unterstützung für RHEL/CentOS.


|                                                                 **Feature**                                                                  |     **Windows Server-Version**     |                              5,2-5,11                              |                            **5.2-5.11**                             |    **5,9-5,11**     |
|----------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|-----------------------|
|                                                               **Verfügbarkeit**                                                               |                                    | [LIS 4,3](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4,1](https://www.microsoft.com/download/details.aspx?id=51612) |       Integriert        |
|                          **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                          | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                      Windows Server 2016 genaue Zeit                                                       |             2019, 2016             |                                                                     |                                                                     |                       |
|                    **[Ungs](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                    |                                    |                                                                     |                                                                     |                       |
|                                                                 Großrahmen                                                                 | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                          VLAN-Tagging und-Abschneiden                                                           | 2019, 2016, 2012 R2 |                           &#10004;Hinweis 1                           |                           &#10004;Hinweis 1                           |    &#10004;Hinweis 1    |
|                                                                Livemigration                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                             Statische IP-Injektion                                                              |     2019, 2016, 2012 R2      |                           &#10004;Hinweis 2                           |                           &#10004;Hinweis 2                           |    &#10004;Hinweis 2    |
|                                                                     vRSS                                                                     |        2019, 2016, 2012 R2         |                                                                     |                                                                     |                       |
|                                                    TCP-Segmentierung und Prüfsummen Offloads                                                    | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                       |
|                                                                    SR-IOV                                                                    |             2019, 2016             |                                                                     |                                                                     |                       |
|                       **[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                       |                                    |                                                                     |                                                                     |                       |
|                                                                 Vhdx-Größe ändern                                                                  |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                       |
|                                                            Virtueller Fibre Channel                                                             |        2019, 2016, 2012 R2         |                           &#10004;Hinweis 3                           |                           &#10004;Hinweis 3                           |                       |
|                                                         Sicherung virtueller Computer                                                          |        2019, 2016, 2012 R2         |                         &#10004;Hinweis 5, 15                         |                           &#10004;Hinweis 5                           | &#10004;Hinweis 4, 5, 6 |
|                                                                 Trim-Unterstützung                                                                 |        2019, 2016, 2012 R2         |                                                                     |                                                                     |                       |
|                                                                   SCSI-WWN                                                                   |        2019, 2016, 2012 R2         |                                                                     |                                                                     |                       |
|                        **[Gedenkens](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                        |                                    |                                                                     |                                                                     |                       |
|                                                              Unterstützung für den unterstützten Kernel                                                              | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                          MMIO-Lücke konfigurieren                                                           |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                           Dynamischer Arbeitsspeicher-Hot-Add                                                           |     2019, 2016, 2012 R2      |                                                                     |                                                                     |                       |
|                                                         Dynamischer Arbeitsspeicher-Ballooning                                                          |     2019, 2016, 2012 R2      |                     &#10004;Hinweis 7, 9, 10, 11                      |                     &#10004;Hinweis 7, 9, 10, 11                      |                       |
|                                                            Größenänderung des Lauf Zeit Speichers                                                             |             2019, 2016             |                                                                     |                                                                     |                       |
|                         **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                         |                                    |                                                                     |                                                                     |                       |
|                                                        Hyper-V-spezifisches Videogerät                                                         | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                       |
|                 **[Verschiedensten](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                 |                                    |                                                                     |                                                                     |                       |
|                                                                Schlüssel-Wert-Paar                                                                | 2019, 2016, 2012 R2 |                              &#10004;                               |                              &#10004;                               |                       |
|                                                            Nicht mastbare Unterbrechung                                                            |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |       &#10004;        |
|                                                         Dateikopie von Host zu Gast                                                         |        2019, 2016, 2012 R2         |                              &#10004;                               |                              &#10004;                               |                       |
|                                                               lsvmbus-Befehl                                                                | 2019, 2016, 2012 R2 |                                                                     |                                                                     |                       |
|                                                               Hyper-V-Sockets                                                                |             2019, 2016             |                                                                     |                                                                     |                       |
|                                                             PCI-Passthrough/DDA                                                              |             2019, 2016             |                                                                     |                                                                     |                       |
| **[Virtuelle Maschinen der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                    |                                                                     |                                                                     |                       |
|                                                               Starten mithilfe von UEFI                                                                |        2019, 2016, 2012 R2         |                                                                     |                                                                     |                       |
|                                                                 Sicherer Start                                                                  |             2019, 2016             |                                                                     |                                                                     |                       |

## <a name="notes"></a>Hinweise

1. Für diese RHEL/CentOS-Version funktioniert das VLAN-Tagging, aber VLAN-abkürzen nicht.

2. Die statische IP-Injektion funktioniert möglicherweise nicht, wenn der Netzwerk-Manager für einen bestimmten synthetischen Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Stellen Sie für eine reibungslose Verwendung statischer IP-Einschleusung sicher, dass entweder der Netzwerk-Manager entweder vollständig ausgeschaltet ist oder für einen bestimmten Netzwerkadapter über seine ifcfg-ethX-Datei ausgeschaltet wurde.

3. Stellen Sie unter Windows Server 2012 R2 bei der Verwendung von virtuellen Fibre Channel-Geräten sicher, dass die logische Gerätenummer 0 (LUN 0) aufgefüllt wurde. Wenn LUN 0 nicht aufgefüllt wurde, kann ein virtueller Linux-Computer möglicherweise keine systemeigenen Fibre Channel-Geräte einbinden.

4. Für integrierte LIS muss das "HyperV-Daemons"-Paket für diese Funktionalität installiert werden.

5. Wenn während eines Sicherungs Vorgangs für virtuelle Computer geöffnete Datei Handles vorhanden sind, müssen die gesicherten VHDs in einigen Fällen möglicherweise bei der Wiederherstellung eine Dateisystem Konsistenzprüfung (fsck) durchlaufen. Bei Live Sicherungs Vorgängen kann ein Fehler auftreten, wenn der virtuelle Computer über ein angefügtes iSCSI-Gerät oder einen direkt angeschlossenen Speicher (auch als Pass-Through-Datenträger bezeichnet) verfügt.

6. Während der herunterladen von Linux-Integration Services bevorzugt wird, ist die Unterstützung der Live Sicherung für RHEL/CentOS 5,9-5.11/6.4/6.5 auch über [Hyper-V Backup Essentials für Linux](https://github.com/LIS/backupessentials/tree/1.0)verfügbar.

7. Die Unterstützung dynamischer Arbeitsspeicher ist nur auf virtuellen 64-Bit-Computern verfügbar.

8. Die Unterstützung von "Hot-Add" ist in dieser Verteilung standardmäßig nicht aktiviert. Um die Unterstützung für "Hot-Add" zu aktivieren, müssen Sie eine udev-Regel unter/etc/udev/rules.d/wie folgt hinzufügen:

   1. Erstellen Sie eine Datei **/etc/udev/rules.d/100-Balloon.Rules**. Sie können einen beliebigen anderen gewünschten Namen für die Datei verwenden.

   2. Fügen Sie der Datei den folgenden Inhalt hinzu: `SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Starten Sie das System neu.

   Während das Herunterladen von Linux-Integration Services diese Regel bei der Installation erstellt, wird die Regel auch entfernt, wenn LIS deinstalliert wird. Daher muss die Regel neu erstellt werden, wenn dynamischer Arbeitsspeicher nach der Installation benötigt wird.

9. Dynamische Arbeitsspeicher Vorgänge können fehlschlagen, wenn für das Gast Betriebssystem zu wenig Arbeitsspeicher verfügbar ist. Im folgenden finden Sie einige bewährte Methoden:

   * Start Speicher und minimaler Arbeitsspeicher müssen größer oder gleich dem vom Verteilungs Anbieter empfohlenen Arbeitsspeicher sein.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System belegen, können bis zu 80 Prozent des verfügbaren Arbeitsspeichers verbrauchen.

10. Wenn Sie dynamischer Arbeitsspeicher auf einem Windows Server 2016-oder Windows Server 2012 R2-Betriebssystem verwenden, geben Sie den **Start Speicher**, den **minimalen Arbeitsspeicher**und den **maximalen Arbeitsspeicher** Parameter in Vielfachen von 128 Megabyte (MB) an. Wenn dies nicht der Fall ist, kann dies zu Fehlern beim Hinzufügen von Fehlern führen, und in einem Gast Betriebssystem wird möglicherweise keine Erhöhung des Arbeitsspeichers angezeigt.

11. Bestimmte Verteilungen, einschließlich derjenigen, die LIS 4,0 und 4,1 verwenden, bieten nur Unterstützung für die Bereitstellung und bieten keine Unterstützung für das heiße hinzufügen. In einem solchen Szenario kann die Funktion "dynamischer Arbeitsspeicher" verwendet werden, indem der Start Speicher Parameter auf einen Wert festgelegt wird, der gleich dem maximalen Arbeitsspeicher Parameter ist. Dies führt dazu, dass der gesamte erforderliche Arbeitsspeicher dem virtuellen Computer zum Startzeitpunkt hinzugefügt wird und später abhängig von den Arbeitsspeicher Anforderungen des Hosts, dass Hyper-V Arbeitsspeicher vom Gast mithilfe von hoch Skalierung frei zuweisen oder deren Zuweisung aufgehoben werden kann. Konfigurieren Sie den **Start Speicher** und den **minimalen Arbeitsspeicher** um bzw. über dem empfohlenen Wert für die Verteilung.

12. Um die KVP-Infrastruktur (Key/Value Pair) zu aktivieren, installieren Sie das Paket hypervkvpd oder HyperV-Daemons RPM von der RHEL-ISO-Datei. Alternativ kann das Paket direkt aus RHEL-Repository installiert werden.

13. Die KVP-Infrastruktur (Key/Value-Paar) funktioniert möglicherweise ohne Linux-Software Update nicht ordnungsgemäß. Wenden Sie sich an Ihren Verteilungs Hersteller, um das Software Update zu erhalten, falls Probleme mit diesem Feature auftreten.

14. Auf virtuellen Computern der Windows Server 2012 R2-Generation 2 ist der sichere Start standardmäßig aktiviert, und einige virtuelle Linux-Computer werden erst gestartet, wenn die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Abschnitt **Firmware** der Einstellungen für den virtuellen Computer im **Hyper-V-Manager** deaktivieren, oder Sie können ihn mithilfe von PowerShell deaktivieren:

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    Der Download der Linux-Integration Services kann auf vorhandene VMS der Generation 2 angewendet werden, aber nicht die Funktion der Generation 2.

15. In Red Hat Enterprise Linux oder CentOS 5,2, 5,3 und 5,4 ist die Funktion zum Einfrieren des Dateisystems nicht verfügbar, daher ist die Sicherung virtueller Computer auch nicht verfügbar.

Weitere Informationen

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Unterstützte virtuelle Debian-Computer in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux virtuellen Maschinen auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle SuSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle Ubuntu-Computer auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte virtuelle FreeBSD-Maschinen auf Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Funktionsbeschreibungen für virtuelle Linux-und FreeBSD-Computer auf Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux unter Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Red hat-Hardware Zertifizierung](https://hardware.redhat.com/&quicksearch=Microsoft)
