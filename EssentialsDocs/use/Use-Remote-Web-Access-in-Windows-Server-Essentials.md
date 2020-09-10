---
title: Verwalten des Remotewebzugriffs in Windows Server 2012 Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 47ea21a0-5e05-4b4b-8fa4-338c82601276
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 25b3bf64672356027742858399d1e2cbc7037194
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624906"
---
# <a name="use-remote-web-access-in-windows-server-essentials"></a>Verwalten des Remotewebzugriffs in Windows Server 2012 Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

  Remote Webzugriff ist ein Feature von Windows Server Essentials, mit dem Sie über einen Webbrowser von einem beliebigen Standort mit Internet Verbindung auf Dateien/Ordner und Computer in Ihrem Netzwerk zugreifen können.

  Remotewebzugriff bietet die Möglichkeit, auch unterwegs mit dem Windows Server Essentials-Netzwerk in Verbindung zu bleiben. Wenn Sie sich bei Remote Webzugriff anmelden, können Sie eine Verbindung mit den Computern in Ihrem Windows Server Essentials-Netzwerk herstellen, das Dashboard zum Verwalten Ihres Windows Server Essentials-Netzwerks öffnen und auf alle freigegebenen Ordner und Mediendateien auf dem Server zugreifen.

 Dieses Thema enthält die folgenden Abschnitte:

-   [Verbinden mit dem Remotewebzugriff](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Connect)

-   [Dateien und Ordner freigeben](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SharedFolders)

-   [Verbinden über ein Mobilgerät](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ConnectMobile)

##  <a name="connect-to-remote-web-access"></a><a name="BKMK_Connect"></a> Verbindung mit Remote Webzugriff herstellen

-   [Anmelden bei Remote Webzugriff](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)

-   [Remotezugriff auf den Computer](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1.5)

-   [Verbinden mit dem Remotewebzugriff](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_Connect)

-   [Dateien und Ordner freigeben](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_SharedFolders)

-   [Verbinden über ein Mobilgerät](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_ConnectMobile)

##  <a name="connect-to-remote-web-access"></a><a name="BKMK_Connect"></a> Verbindung mit Remote Webzugriff herstellen

-   [Anmelden bei Remote Webzugriff](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1)

-   [Remotezugriff auf den Computer](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_1.5)


###  <a name="log-on-to-remote-web-access"></a><a name="BKMK_1"></a> Anmelden bei Remote Webzugriff
 Wenn Sie sich auf einem lokalen Computer oder einem Remote Computer an einer Remote Webzugriff anmelden, können Sie auf Ressourcen auf Ihrem Server mit Windows Server Essentials und Computern in Ihrem Netzwerk zugreifen.

##### <a name="to-log-on-to-remote-web-access-from-a-network-computer"></a>So melden Sie sich beim Remotewebzugriff über einen Netzwerkcomputer an

1.  Öffnen Sie einen Webbrowser, geben Sie **https://** _<yourservername \> _**/Remote** in der Adressleiste ein, und drücken Sie dann die EINGABETASTE.

    > [!NOTE]
    >  Stellen Sie sicher, dass Sie die s in HTTPS einschließen.

2.  Geben Sie auf der Seite Remote Webzugriff Anmeldung Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, und klicken Sie dann auf den Pfeil.

##### <a name="to-log-on-to-remote-web-access-from-a-remote-computer"></a>So melden Sie sich beim Remotewebzugriff über einen Remotecomputer an

1.  Öffnen Sie einen Webbrowser, geben Sie **https://** _<yourDomainName \> _**/Remote** in der Adressleiste ein, und drücken Sie dann die EINGABETASTE.

    > [!NOTE]
    >  Ihre Domänennamensinformationen können Sie von Ihrem Netzwerkadministrator abrufen. Stellen Sie sicher, dass Sie die s in HTTPS einschließen.

2.  Geben Sie auf der Seite Remote Webzugriff Anmeldung Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, und klicken Sie dann auf den Pfeil.

###  <a name="remotely-access-your-computer"></a><a name="BKMK_1.5"></a> Remote Zugriff auf Ihren Computer
 Wenn Sie nicht im Büro sind, können Sie sich mit Ihrem Webbrowser bei der Remote Webzugriff-Website anmelden, um per Remote Zugriff auf Ihr Windows Server Essentials-Dashboard, freigegebene Ordner und Computer in Ihrem Netzwerk zuzugreifen.

 Wenn Sie mit dem Dashboard eine Verbindung herstellen, können Sie Windows Server Essentials so verwalten, als würden Sie sich im Büro befinden. Sie können alle gewöhnlichen Verwaltungsaufgaben vornehmen. Dazu zählt auch das Hinzufügen von Benutzerkonten, das Hinzufügen von freigegebenen Ordnern, das Festlegen des Zugriffs auf freigegebene Ordner usw. Wenn Sie eine Verbindung zu Computern in Ihrem Netzwerk herstellen, können Sie so auf deren Desktops zugreifen, als würden Sie sich direkt vor ihnen im Büro befinden.

 Anhand der Spalte **Status** wird ersichtlich, ob Sie eine Verbindung mit einem Computer in Ihrem Netzwerk herstellen können, und Sie können die folgenden Werte einbeziehen:

-   **Verfügbar**

     Der Computer ist eingeschaltet ist und für eine Remoteverbindung verfügbar. Auch wenn dieser Status angezeigt wird, können Sie möglicherweise trotzdem keine Verbindung mit diesem Computer herstellen, wenn eine Drittanbieterfirewall die Verbindung blockiert.

-   **Offline oder im Ruhezustand**

     Der Computer ist ausgeschaltet oder befindet sich im Standbymodus oder im Ruhezustandmodus. Wenn ein Computer offline oder im Ruhezustand ist, wird der Status in Echtzeit aktualisiert, damit Sie wissen, wenn der Computer verfügbar ist.

-   **Nicht unterstütztes Betriebssystem**

     Remotedesktop wird vom Betriebssystem auf dem Computer nicht unterstützt. Es kann bis zu sechs Stunden dauern, bis der Status auf dem Server aktualisiert wird, wenn eine Änderung durchgeführt wird.

-   **Verbindung ist deaktiviert.**

     Die Computerverbindung wird entweder durch eine Firewall blockiert, oder der Remotedesktop ist auf dem Computer oder durch eine Gruppenrichtlinie deaktiviert. Es kann bis zu sechs Stunden dauern, bis der Status auf dem Server aktualisiert wird, wenn eine Änderung durchgeführt wird.

#### <a name="to-connect-to-a-computer-on-your-network"></a>So verbinden Sie sich mit einem Computer in Ihrem Netzwerk
 Klicken Sie auf der Registerkarte **GERÄTE** auf den Namen Ihres Computers. Sie können ausschließlich Computer mit dem Status **Verfügbar** auswählen.

#### <a name="to-connect-to-the-server-dashboard"></a>So verbinden Sie sich mit dem Serverdashboard
 Klicken Sie auf der Registerkarte **GERÄTE** auf den Namen Ihres Servers. Sie können ausschließlich Computer mit dem Status **Verfügbar** auswählen. Sie müssen ein Administratorbenutzerkonto und -kennwort auf Ihrem Server bereitstellen können, um das Dashboard verwenden zu können.

##  <a name="share-files-and-folders"></a><a name="BKMK_SharedFolders"></a> Freigeben von Dateien und Ordnern


-   [Hochladen und Herunterladen von Dateien mit Remotewebzugriff](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_UploadRWA)

-   [Erstellen, Umbenennen, Verschieben, Löschen oder Kopieren von Dateien und Ordnern mit Remotewebzugriff](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2)


###  <a name="upload-and-download-files-in-remote-web-access"></a><a name="BKMK_UploadRWA"></a> Hochladen und Herunterladen von Dateien in Remote Webzugriff
 Auf der Registerkarte für die freigegebenen Ordner**** im Remotewebzugriff können Sie Folgendes vornehmen:

-   Hochladen (Senden) von Dateien von Ihrem Computer aus zu Windows Server Essentials.

    > [!NOTE]
    >  Sie können nur Dateien und keine Ordner zum Remotewebzugriff hochladen. Wenn Sie möchten, dass dieselbe Datei- und Ordnerhierarchie in den freigegebenen Ordnern**** auf dem Server wie auf Ihrem Computer verwendet wird, müssen Sie die Ordner auf dem Server im Remotewebzugriff erstellen und dann die Dateien in den von Ihnen erstellten Ordner hochladen. Informationen über das Erstellen eines Serverordners finden Sie im Thema zum [Hinzufügen oder Verschieben eines Serverordners](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5).

-   Laden (Empfangen) Sie Dateien und Ordner aus Windows Server Essential auf Ihren Computer herunter.

-   Erstellen Sie einen Ordner in einem freigegebenen Ordner auf Windows Server Essentials.


-   Verschieben, löschen und benennen Sie Dateien und Ordner auf Windows Server Essentials um. Weitere Informationen finden Sie unter [erstellen, umbenennen, verschieben, löschen oder Kopieren von Dateien und Ordnern in Remote Webzugriff](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2).

-   Verschieben, löschen und benennen Sie Dateien und Ordner auf Windows Server Essentials um. Weitere Informationen finden Sie unter [erstellen, umbenennen, verschieben, löschen oder Kopieren von Dateien und Ordnern in Remote Webzugriff](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_2).


#### <a name="upload-files"></a>Hochladen von Dateien

##### <a name="to-upload-files"></a>So laden Sie Dateien hoch

1. Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2. Klicken Sie in der Liste der freigegebenen Ordner der Dateien und Ordner auf den Ordner, in den die Datei hochgeladen werden soll, und klicken Sie dann auf **Hochladen**.

3. Wenn das standardmäßige Uploadtool nicht bereits geladen ist, klicken Sie auf die Option zur Verwendung der Standardmethode für Uploads****.

4. Klicken Sie auf **Durchsuchen**  , um die entsprechende Datei auf Ihrem Computer zu finden.

5. Navigieren Sie zwischen den Ordnern auf Ihrem Computer, um die hochzuladende Datei zu finden, und klicken Sie dann auf **Öffnen**.

6. Wiederholen Sie die Schritte 2 und 3 für jede Datei, die Sie hochladen möchten.

7. Klicken Sie nach dem Hinzufügen sämtlicher hochzuladender Datei auf **Hochladen**.

   Das Tool „Einfacher Dateiupload“ optimiert das Hochladen von Dateien auf Ihrem Server unter Windows Server Essentials. Sie können mithilfe des Tools „Einfacher Dateiupload“ beliebig viele Dateien unter Verwendung des Drag-and-drop-Features hinzufügen und sie anschließend als freigegebene Ordner auf dem Server hochladen.

> [!NOTE]
>  Das Hochladen mehrerer Dateien wird in Webbrowsern, die mit HTML5 kompatibel sind, nativ unterstützt. Dieses Tool ist nur erforderlich, wenn der Webbrowser HTML5 nicht unterstützt.

##### <a name="to-upload-files-using-the-easy-file-upload-tool"></a>So laden Sie Dateien mithilfe des Tools „Einfacher Dateiupload“ hoch

1.  Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2.  Klicken Sie in der Liste der freigegebenen Ordner der Dateien und Ordner auf den Ordner, in den die Dateien hochgeladen werden sollen, und klicken Sie dann auf **Upload**. Wenn der Ordner, zu dem Sie den Upload vornehmen möchten, nicht vorhanden ist, klicken Sie auf **Neuer Ordner**, geben Sie den Namen des neuen Ordners im Dialogfeld ein, und klicken Sie dann auf **OK**.

3.  Sie müssen möglicherweise das Add-On für Windows Server-Lösungen ausführen. Wenn dies der Fall sein sollte, klicken Sie auf den gelben Streifen oben auf dem Bildschirm, klicken Sie auf **Add-On**, und klicken Sie dann auf das Dialogfeld **Ausführen**.

4.  Klicken Sie auf **Verwenden Sie das Tool 'Einfacher Dateiupload'**, wenn das Tool „Einfacher Dateiupload“ nicht bereits geladen wurde.

5.  Sie können Dateien per Drag-and-drop aus dem Windows-Explorer im Tool „Einfacher Dateiupload“ ablegen oder auf **auf 'Durchsuchen' klicken, um Dateien auszuwählen** klicken.

6.  Wenn Sie das Hinzufügen der Dateien, die Sie in den ausgewählten Ordner hochladen möchten, abgeschlossen haben, klicken Sie auf **Hochladen**.

7.  Klicken Sie auf **Schließen**, wenn die Dateien erfolgreich hochgeladen wurden.

#### <a name="download-files-or-folders"></a>Herunterladen von Dateien oder Ordnern

##### <a name="to-download-a-single-file"></a>So laden Sie eine einzelne Datei herunter

1. Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2. Aktivieren Sie in der Dateiliste für den freigegebenen Ordner das Kontrollkästchen neben der Datei, die Sie auf Ihren physischen Computer herunterladen möchten.

3. Klicken Sie auf **Download**, um den Download zu starten.

4. Klicken Sie im Dialogfeld **Dateidownload** auf **Speichern**, um die Datei auf Ihrem Computer zu speichern.

5. Wählen Sie im Dialogfeld **Speichern unter** den Speicherort für das Speichern der Datei aus, und klicken Sie dann auf **Speichern**. Eine einzelne Datei wird nicht komprimiert, bevor sie heruntergeladen wird.

   Es gibt zwei Optionen zum Herunterladen mehrerer Dateien oder Ordner. Wählen Sie die für Ihre Anforderungen geeignete Option aus:

> [!NOTE]
>  Diese Optionen stehen nur zur Verfügung, wenn Sie mehrere Dateien oder Ordner auf Ihren Computer herunterladen.

- **Selbstextrahierende ausführbare Datei (.exe)**

  > [!NOTE]
  >   Dieser Abschnitt gilt für einen Server, auf dem Windows Server Essentials ausgeführt wird.

   Eine selbstextrahierende ausführbare Datei ist eine herunterladbare Datei, die das Dekomprimierungsprogramm (ausführbare Datei) mit den komprimierten Dateien kombiniert. Wenn Sie das ausführbare Programm ausführen, dekomprimiert es automatisch die komprimierten Dateien (selbstextrahierend). Mit diesem gängigen Verfahren können komprimierte Daten verteilt werden, ohne dass der Empfänger über das nötige Dekomprimierungshilfsprogramm verfügen muss.

  > [!NOTE]
  >  Diese Option unterstützt Unicode-Zeichen.

- **Komprimierter Windows-Ordner (.zip)**

   Durch das Zippen einer Datei wird eine komprimierte Dateiversion erstellt, die kleiner als die Originaldatei ist. Die komprimierte Dateiversion verfügt über die Dateierweiterung ".zip". Dateitypen, die am stärksten verpackt werden, sind textorientierte Dateitypen wie TXT,- DOC-, XLS- und grafische Dateien, die nicht komprimierte Dateitypen wie .bmp verwenden. Einige Grafikdateien wie JPG- und GIF-Dateien nutzen bereits die Komprimierung, sodass sich die Dateigröße durch das Komprimieren nur geringfügig verkleinert. Darüber hinaus reduziert sich die Dateigröße eines Word-Dokuments mit vielen Grafiken nicht in dem Maße wie ein Dokument, das hauptsächlich Text enthält.

  > [!NOTE]
  >  Diese Option bietet eingeschränkte Unterstützung für internationale Dateinamen in Windows Server Essentials.

  Vor dem Beginn des tatsächlichen Herunterladens wird die EXE- oder ZIP-Datei erstellt. Abhängig von der Anzahl der Dateien und der Gesamtgröße der Downloaddateien kann dies einige Minuten dauern. Nachdem die Downloaddatei erstellt wurde, erfolgt das Herunterladen der Datei im Hintergrund. Dadurch können Sie weiterarbeiten, während der Downloadvorgang ausgeführt wird.

##### <a name="to-download-multiple-files-or-folders"></a>So laden Sie mehrere Dateien oder Ordner herunter

1.  Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2.  Aktivieren Sie in der Dateiliste für den freigegebenen Ordner das Kontrollkästchen neben den Dateien oder Ordnern, die Sie auf Ihren physischen Computer herunterladen möchten.

3.  Klicken Sie auf **Download**, um den Download zu starten.

4.  Klicken Sie im Dialogfeld **Downloadformat auswählen**, um die von Ihnen bevorzugte Downloadformatoption auszuwählen, und klicken Sie dann auf **OK**. Die komprimierte Datei wird anhand der von Ihnen ausgewählten Formatoption vorbereitet.

5.  Klicken Sie im Dialogfeld **Dateidownload** auf **Speichern**, um die Datei auf Ihrem Computer zu speichern.

6.  Wählen Sie im Dialogfeld **Speichern unter** den Speicherort für das Speichern der Datei aus, und klicken Sie dann auf **Speichern**.

#### <a name="retrieve-compressed-files-downloaded-to-your-computer"></a>Abrufen von auf Ihren Computer heruntergeladener komprimierter Dateien

> [!NOTE]
>   Dieser Abschnitt gilt für einen Server, auf dem Windows Server Essentials ausgeführt wird.

 Wenn Sie auswählen, mehrere Dateien oder Ordner herunterzuladen, erhalten Sie eine selbstextrahierende komprimierte ausführbare Datei (EXE) oder eine komprimierte Datei (ZIP).

##### <a name="to-retrieve-a-file-from-the-compressed-exe-file"></a>So rufen Sie eine Datei aus der komprimierten Datei (EXE) ab

1.  Doppelklicken Sie auf Ihrem Computer auf die komprimierte Datei, um sie zu öffnen.

2.  Befolgen Sie die Anweisungen, um die Dateien in einem Ordner auf Ihrem Computer zu extrahieren.

##### <a name="to-retrieve-a-file-from-the-compressed-zip-file"></a>So rufen Sie eine Datei aus der komprimierten Datei (ZIP) ab

1.  Doppelklicken Sie auf Ihrem Computer auf die komprimierte Datei, um sie zu öffnen.

2.  Wählen Sie die abzurufenden Dateien aus, und ziehen Sie die Dateien anschließend in einen Ordner auf Ihrem Computer, in dem Sie sie speichern möchten.

    > [!NOTE]
    >  Wenn Sie ein Drittanbieter-Komprimierungsprogramm verwenden, befolgen Sie die Vorgehensweisen für das Programm, um Ihre Dateien aus der komprimierten Datei zu extrahieren.

###  <a name="create-rename-move-delete-or-copy-files-and-folders-in-remote-web-access"></a><a name="BKMK_2"></a> Erstellen, umbenennen, verschieben, löschen oder Kopieren von Dateien und Ordnern in Remote Webzugriff
 Sie können den Remotewebzugriff verwenden, um neue Ordner in einem vorhandenen freigegebenen Ordner zu erstellen, um Dateien und Ordner umzubenennen und um Dateien und Ordner auf Ihrem Server zu löschen.

> [!NOTE]
> Zum Hinzufügen neuer freigegebener Ordner auf einem Server unter Windows Server Essentials müssen Sie das Dashboard verwenden. Klicken Sie zum Herstellen einer Verbindung zur Serverkonsole über den Remotewebzugriff auf die Registerkarte **Computer**, klicken Sie auf den Servernamen, klicken Sie auf **Verbinden**, und befolgen Sie dann die Anweisungen für das Anmelden beim Server. Informationen über das Erstellen freigegebener Ordner finden Sie im Thema zum [Hinzufügen oder Verschieben eines Serverordners](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5).

#### <a name="to-create-a-new-folder"></a>So erstellen Sie einen neuen Ordner

1.  Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2.  Klicken Sie auf der Aufgabenleiste auf **Neuer Ordner**.

3.  Geben Sie einen Namen für den Ordner ein, und klicken Sie dann auf **OK**.

##### <a name="to-rename-a-file-or-folder"></a>So benennen Sie eine Datei oder einen Ordner um

1.  Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2.  Klicken Sie mit der rechten Maustaste auf die Datei oder den Ordner, die bzw. den Sie umbenennen möchten, und klicken Sie dann auf **Umbenennen**.

3.  Geben Sie einen neuen Namen in das Textfeld ein, und klicken Sie dann auf **OK**.

#### <a name="to-move-files-or-folders"></a>So verschieben Sie Dateien oder Ordner

1.  Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2.  Aktivieren Sie das Kontrollkästchen neben den Dateien oder Ordnern, die Sie verschieben möchten, klicken Sie mit der rechten Maustaste auf eine bzw. einen der ausgewählten Dateien bzw. Ordner, und klicken Sie dann auf **Ausschneiden**.

3.  Klicken Sie mit der rechten Maustaste auf den Ordner, in den die Dateien oder Ordner verschoben werden sollen, und klicken Sie dann auf **Einfügen**.

##### <a name="to-delete-a-file-or-folder"></a>So löschen Sie eine Datei oder einen Ordner

1.  Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2.  Aktivieren Sie das Kontrollkästchen neben den Dateien oder Ordnern, die Sie löschen möchten, klicken Sie mit der rechten Maustaste auf eine bzw. einen der ausgewählten Dateien bzw. Ordner, und klicken Sie dann auf **Löschen**.

3.  Klicken Sie auf **Ja**, um zu bestätigen, dass Sie die ausgewählten Dateien und Ordner löschen möchten.

##### <a name="to-copy-files-or-folders"></a>So kopieren Sie Dateien oder Ordner

1.  Klicken Sie im Remotewebzugriff auf die Registerkarte für die freigegebenen**** Ordner, und klicken Sie dann auf die Verknüpfung eines freigegebenen Ordners. Eine Liste der Dateien und Ordner in diesem freigegebenen Ordner wird angezeigt.

2.  Aktivieren Sie das Kontrollkästchen neben den Dateien oder Ordnern, die Sie kopieren möchten, klicken Sie mit der rechten Maustaste auf eine bzw. einen der ausgewählten Dateien bzw. Ordner, und klicken Sie dann auf **Kopieren**.

3.  Klicken Sie mit der rechten Maustaste auf den Ordner, in den die Dateien oder Ordner kopiert werden sollen, und klicken Sie dann auf **Einfügen**.

##  <a name="connect-from-a-mobile-device"></a><a name="BKMK_ConnectMobile"></a> Herstellen einer Verbindung von einem mobilen Gerät aus


-   [Verwenden des Remotewebzugriffs über ein Mobilgerät](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_8)

-   [Unterstützte Webbrowser für Mobilgeräte](Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_9)

-   [Verwenden des Remotewebzugriffs über ein Mobilgerät](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_8)

-   [Unterstützte Webbrowser für Mobilgeräte](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md#BKMK_9)


###  <a name="use-remote-web-access-from-a-mobile-device"></a><a name="BKMK_8"></a> Remote Webzugriff von einem mobilen Gerät aus verwenden
 Sie können sich auf Ihrem Smartphone beim Remotewebzugriff anmelden, um die Dateien und Ordner in den freigegebenen Ordnern auf dem Server anzuzeigen.

> [!NOTE]
>  Sie können auch die My Server-App für Windows Server Essential aus dem [Windows Phone Marketplace](http://www.windowsphone.com/apps/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a) herunterladen und verwenden, um auf Ihre freigegebenen Ordner und Mediendateien zuzugreifen, die auf dem Server gespeichert sind.

##### <a name="to-log-on-to-remote-web-access-from-a-mobile-device"></a>So melden Sie sich beim Remotewebzugriff über einen Mobilgerät an

1.  Öffnen Sie einen Webbrowser, und geben Sie **https://** _<yourDomainName \> _**/Remote** in der Adressleiste ein.  Stellen Sie sicher, dass Sie die s in HTTPS einschließen.

2.  Geben Sie auf der Seite Remote Webzugriff Anmeldung Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, und klicken Sie dann auf den Pfeil. Sie werden in der mobilen Version des Remotewebzugriffs angemeldet.

##### <a name="to-switch-to-the-desktop-version-of-remote-web-access"></a>So wechseln Sie zur Desktopcomputerversion des Remotewebzugriffs

1.  Öffnen Sie einen Webbrowser, und geben Sie **https://** _<yourDomainName \> _**/Remote** in der Adressleiste ein.  Stellen Sie sicher, dass Sie die s in HTTPS einschließen.

2.  Geben Sie auf der Seite Remote Webzugriff Anmeldung Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, klicken Sie auf **Desktop Version anzeigen**, und klicken Sie dann auf den Pfeil. Sie werden in der Desktopversion des Remotewebzugriffs angemeldet.

##### <a name="to-return-to-the-mobile-version-of-remote-web-access"></a>So kehren Sie zur mobilen Version des Remotewebzugriffs zurück

1. Melden Sie sich ab.

2. Öffnen Sie einen Webbrowser, und geben Sie **https://** _<yourDomainName \> _**/Remote/m** in der Adressleiste ein. Stellen Sie sicher, dass Sie die s in HTTPS einschließen.

3. Die Mobile Version von Remote Webzugriff wird angezeigt. Geben Sie auf der Seite Remote Webzugriff Anmeldung Ihren Benutzernamen und Ihr Kennwort in die Textfelder ein, und klicken Sie dann auf den Pfeil. Sie sind bei der mobilen Version von Remote Webzugriff angemeldet.

   Sie können nach Dateien und Ordnern in den freigegebenen Ordnern auf dem Server suchen.

###  <a name="supported-web-browsers-for-mobile-devices"></a><a name="BKMK_9"></a> Unterstützte Webbrowser für mobile Geräte
 Unterstützte Webbrowser für Mobilgeräte umfassen:

-   Internet Explorer Mobile 6.0 oder höher

-   Safari

-   BlackBerry

-   Symbian 6.0 oder höher

-   Android

-   Google Chrome

-   Firefox

## <a name="additional-references"></a>Weitere Verweise

-   [Verwalten der Remotewebzugriffs](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)


-   [Remote arbeiten](Work-Remotely-in-Windows-Server-Essentials.md)

-   [Verwenden von Windows Server Essentials](Use-Windows-Server-Essentials.md)

-   [Remote arbeiten](../use/Work-Remotely-in-Windows-Server-Essentials.md)

-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)

