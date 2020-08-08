---
title: Erstellen von Hyper-V-VHD-Satz Dateien
description: Schritte zum Erstellen einer vhdset-Datei unter Hyper-v 2016
author: jiwool
ms.author: jiwool
manager: senthilr
ms.date: 01/26/2017
ms.topic: article
ms.assetid: 444e1496-9e5a-41cf-bfbc-306e2ed8e00a
audience: IT Pros
ms.reviewer: kathydav
ms.openlocfilehash: a2c4b2ff3ca4dda2cb2989c629c5dac5f529cac0
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991451"
---
# <a name="create-hyper-v-vhd-set-files"></a>Erstellen von Hyper-V-VHD-Satz Dateien
VHD-Set-Dateien sind ein neues frei gegebenes virtuelles Datenträger Modell für Gast Cluster in Windows Server 2016. VHD-Set-Dateien unterstützen die Online Größe von freigegebenen virtuellen Datenträgern, unterstützen das Hyper-V-Replikat und können in Anwendungs konsistente Prüfpunkte eingeschlossen werden.

VHD-Satz Dateien verwenden den neuen VHD-Dateityp. VHDs. VHD-Set-Dateien speichern Prüf Punkt Informationen über den virtuellen Gruppen Datenträger, der in Gast Clustern verwendet wird, in Form von Metadaten.

Hyper-V übernimmt alle Aspekte der Verwaltung der Prüf Punkt Ketten und das Zusammenführen des freigegebenen VHD-Satzes. Verwaltungssoftware kann Datenträger Vorgänge wie die Online Änderung der Größe von VHD-Dateien auf die gleiche Weise wie für ausführen. Vhdx-Dateien. Dies bedeutet, dass Verwaltungssoftware nicht über das VHD-Dateiformat informiert werden muss.

> [!NOTE]
> Es ist wichtig, die Auswirkungen von VHD-Dateien vor der Bereitstellung in der Produktion auszuwerten. Stellen Sie sicher, dass Ihre Umgebung keine Leistungs-oder Funktions Verschlechterung hat, wie z. b. die Datenträger Latenz.

## <a name="create-a-vhd-set-file-from-hyper-v-manager"></a>Erstellen einer VHD-Datei im Hyper-V-Manager

1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.
2.  Klicken Sie im Aktionsbereich auf **Neu**, und klicken Sie dann auf **Festplatte**.
3.  Wählen Sie auf der Seite Datenträger **Format auswählen** die Option **VHD-Satz** als Format der virtuellen Festplatte aus.
4.  Gehen Sie auf den Seiten des Assistenten, um die virtuelle Festplatte anzupassen. Sie können auf **Weiter** klicken, um alle Seiten des Assistenten nacheinander zu bearbeiten. Sie können aber auch im linken Bereich auf den Namen einer Seite klicken, um direkt zu einer Seite zu wechseln.
5.  Wenn Sie mit dem Konfigurieren der virtuellen Festplatte fertig sind, klicken Sie auf **Fertig stellen**.

## <a name="create-a-vhd-set-file-from-windows-powershell"></a>Erstellen einer VHD-Satz Datei aus Windows PowerShell

Verwenden Sie das Cmdlet [New-VHD](/powershell/module/hyper-v/new-vhd?view=win10-ps) mit dem Dateityp. VHDs im Dateipfad. In diesem Beispiel wird eine VHD-Datei mit dem Namen base. VHDs erstellt, die 10 Gigabyte groß ist.

``` PowerShell
PS c:\>New-VHD -Path c:\base.vhds -SizeBytes 10GB
```

## <a name="migrate-a-shared-vhdx-file-to-a-vhd-set-file"></a>Migrieren einer freigegebenen vhdx-Datei in eine VHD-Datei

Zum Migrieren einer vorhandenen freigegebenen vhdx-Datei zu VHDs muss der virtuelle Computer offline geschaltet werden. Dies ist der empfohlene Prozess mithilfe von Windows PowerShell:

1. Entfernen Sie das vhdx von der VM. Führen Sie zum Beispiel aus:
   ``` PowerShell
   PS c:\>Remove-VMHardDiskDrive existing.vhdx
   ```

2. Konvertieren Sie die vhdx-Datei in eine VHDs. Führen Sie zum Beispiel aus:
   ``` PowerShell
   PS c:\>Convert-VHD existing.vhdx new.vhds
   ```

3. Fügen Sie die VHDs der VM hinzu. Führen Sie zum Beispiel aus:
   ``` PowerShell
   PS c:\>Add-VMHardDiskDrive new.vhds
   ```