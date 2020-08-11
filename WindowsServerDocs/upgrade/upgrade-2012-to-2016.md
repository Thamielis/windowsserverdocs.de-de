---
title: Upgrade von Windows Server 2012 auf Windows Server 2016 | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie ein direktes Upgrade von Windows Server 2012 auf Windows Server 2016 durchführen.
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: ea67496a0e094c68133dfd9315d070bb87c99dbc
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997234"
---
# <a name="upgrade-windows-server-2012-to-windows-server-2016"></a>Upgrade von Windows Server 2012 auf Windows Server 2016

Wenn Sie die Hardware und alle eingerichteten Serverrollen beibehalten möchten, bietet sich ein direktes Upgrade an. Bei einem klassischen Upgrade wird von einem älteren Betriebssystem zu einem neueren gewechselt, und Ihre Einstellungen, Serverrollen und Daten bleiben erhalten. Dieser Artikel unterstützt Sie bei der Umstellung von Windows Server 2012 auf Windows Server 2016.

Wenn Sie ein Upgrade auf Windows Server 2019 durchführen möchten, verwenden Sie zunächst dieses Thema, um auf Windows Server 2016 zu aktualisieren, und [dann ein Upgrade von Windows Server 2016 auf Windows Server 2019 auszuführen](upgrade-2016-to-2019.md).

## <a name="before-you-begin-your-in-place-upgrade"></a>Bevor Sie mit dem direkten Upgrade beginnen

Bevor Sie mit dem Windows Server-Upgrade beginnen, wird empfohlen, dass Sie zur Diagnose und Problembehandlung Informationen von ihren Geräten sammeln. Da diese Informationen nur für den Fall eines Fehlers beim Upgrade vorgesehen sind, müssen Sie sicherstellen, dass Sie die Informationen an einem Speicherort speichern, auf den Sie ohne Ihr Gerät zugreifen können.

### <a name="to-collect-your-info"></a>So sammeln Sie Informationen

1. Öffnen Sie eine Eingabeaufforderung, navigieren Sie zu `c:\Windows\system32`, und geben Sie **systeminfo.exe** ein.

2. Die dann angezeigten Systeminformationen können Sie kopieren, einfügen und an einem Speicherort außerhalb Ihres Systems speichern.

3. Geben Sie an der Eingabeaufforderung **ipconfig /all** ein, kopieren Sie dann die angezeigten Konfigurationsinformationen, und fügen Sie sie an dem gleichen Speicherort wie oben ein.

4. Öffnen Sie den Registrierungs-Editor, wechseln Sie zum Hive „HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion“, kopieren Sie die Angaben zu Windows Server **BuildLabEx** (Version) und **EditionID** (Edition) an den gleichen Speicherort wie oben.

Nachdem Sie alle mit Windows Server zusammenhängenden Informationen gesammelt haben, raten wir dringend zu einer Sicherung Ihres Betriebssystems, Ihrer Apps und Ihrer virtuellen Computer. Ferner müssen Sie alle virtuellen Computer, die aktuell auf dem Server ausgeführt werden **herunterfahren** oder für sie eine **Schnellmigration** oder **Livemigration** ausführen. Während des direkten Upgrades können keine virtuellen Computer ausgeführt werden.

## <a name="to-perform-the-upgrade"></a>So führen Sie das Upgrade aus

1. Vergewissern Sie sich, dass der Wert von **BuildLabEx** besagt, dass Sie Windows Server 2012 ausführen.

2. Suchen Sie die Windows Server 2016-Setupmedien, und wählen Sie dann **setup.exe** aus.

    ![Windows-Explorer mit der Datei „setup.exe“](media/upgrade-2012-2016/setup-2016.png)

3. Wählen Sie **Ja** aus, um den Setupvorgang zu starten.

    ![Die Benutzerkontensteuerung bittet um die Berechtigung zum Starten des Setups](media/upgrade-2012-2016/start-setup-uac-box.png)

4. Wählen Sie auf dem Bildschirm „Windows Server 2016“ **Jetzt installieren** aus.

5. Wählen Sie für Geräte mit Internetverbindung **Updates herunterladen und installieren (empfohlen)** aus.

    ![Bildschirm mit der Option zum Herstellen einer Onlineverbindung zum Abrufen wichtiger Windows-Updates](media/upgrade-2012-2016/imp-updates-win-setup.png)

6. Setup überprüft Ihre Gerätekonfiguration; warten Sie bis zum Abschluss der Überprüfung, und wählen Sie dann **Weiter** aus.

7. Je nach dem Verteilungskanal, über den Sie Ihre Windows Server-Medien erhalten haben (Einzelhandel, Volumenlizenz, OEM, ODM usw.), und der Lizenz für den Server, werden Sie möglicherweise aufgefordert, einen Lizenzschlüssel einzugeben, bevor Sie fortfahren können.

    ![Bildschirm, auf dem Sie Ihren ProductKey eingeben können](media/upgrade-2012-2016/enter-product-key.png)

8. Wählen Sie die Windows Server 2016-Edition aus, die Sie installieren möchten, und wählen Sie dann **Weiter** aus.

    ![Auswahlbildschirm für die zu installierende Windows Server 2016-Edition](media/upgrade-2012-2016/select-os-edition.png)

9. Wählen Sie **Ich stimme zu** aus, um den Bedingungen Ihres Lizenzvertrags zuzustimmen, abhängig von Ihrem Verteilungskanal (wie etwa Einzelhandel, Volumenlizenz, OEM, ODM usw).

    ![Bildschirm zur Annahme Ihres Lizenzvertrags](media/upgrade-2012-2016/license-terms.png)

10. Wählen Sie **Persönliche Dateien und Apps beibehalten** aus, um ein direktes Upgrade festzulegen, und wählen Sie dann **Weiter** aus.

    ![Bildschirm zur Auswahl Ihres Installationstyps](media/upgrade-2012-2016/choose-install-upgrade.png)

11. Wenn eine Seite angezeigt wird, die Sie informiert, dass ein Upgrade nicht empfohlen wird, können Sie sie ignorieren und **Bestätigen** auswählen. Sie wurde eingefügt, um zur Neuinstallation aufzufordern, dies ist jedoch nicht erforderlich.

    ![Bildschirm mit der Bestätigen-Schaltfläche für die Sicherheitsabfrage, ob Sie das Upgrade ausführen möchten](media/upgrade-2012-2016/confirm-upgrade-process.png)

12. Setup weist Sie an, Microsoft Endpoint Protection mithilfe von **Programme hinzufügen/entfernen** zu entfernen.

    Diese Funktion ist nicht mit Windows 10 kompatibel.

13. Nachdem Setup Ihr Gerät analysiert hat, werden Sie aufgefordert, den Upgradevorgang fortzusetzen, indem Sie **Installieren** auswählen.

    ![Bildschirm, der anzeigt, dass Sie zum Starten des Upgrades bereit sind](media/upgrade-2012-2016/ready-to-install.png)

    Das direkte Upgrade beginnt und zeigt den Bildschirm **Windows-Upgrade wird durchgeführt** mit seinem Status an. Nach dem Abschluss des Upgrades wird der Server neu gestartet.

    ![Bildschirm mit dem Upgradestatus](media/upgrade-2012-2016/upgrading-windows-with-progress.png)

## <a name="after-your-upgrade-is-done"></a>Nach dem Abschluss des Upgrades

Nachdem das Upgrade abgeschlossen ist, müssen Sie sich vergewissern, dass das Upgrade auf Windows Server 2016 erfolgreich war.

### <a name="to-make-sure-your-upgrade-was-successful"></a>So überprüfen Sie, ob das Upgrade erfolgreich war

1. Öffnen Sie den Registrierungs-Editor, wechseln Sie zum Hive HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion, und sehen Sie sich den **ProductName** an. Sie sollten Ihre Edition von Windows Server 2016 sehen, beispielsweise **Windows Server 2016 Datacenter**.

2. Vergewissern Sie sich, dass alle Ihre Anwendungen ausgeführt werden, und dass Ihre Clientverbindungen mit den Anwendungen erfolgreich sind.

Wenn Sie der Ansicht sind, dass während des Upgrades ein Fehler aufgetreten ist, kopieren Sie das `%SystemRoot%\Panther`-Verzeichnis (in der Regel `C:\Windows\Panther`), und wenden Sie sich an den Microsoft Support.

## <a name="next-steps"></a>Nächste Schritte

Sie können die Umstellung von Windows Server 2016 auf Windows Server 2019 mit einem oder mehreren Upgrades durchführen. Ausführliche Anweisungen finden Sie unter [Upgrade von Windows Server 2016 auf Windows Server 2019](upgrade-2016-to-2019.md).

## <a name="related-articles"></a>Verwandte Artikel

- Weitere Details und Informationen zu Windows Server 2016 finden Sie unter [Erste Schritte mit Windows Server 2016](../get-started/server-basics.md).