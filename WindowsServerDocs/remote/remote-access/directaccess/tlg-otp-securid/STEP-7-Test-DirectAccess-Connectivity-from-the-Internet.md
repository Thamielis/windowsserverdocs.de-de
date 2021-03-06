---
title: Schritt 7 Testen der DirectAccess-Konnektivität über das Internet
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.topic: article
ms.assetid: ed2a1616-30c6-482a-9a02-4a5023621f58
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 18cf11af84ab43e7fe0fd4ea93f10e61159048a8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963966"
---
# <a name="step-7-test-directaccess-connectivity-from-the-internet"></a>Schritt 7 Testen der DirectAccess-Konnektivität über das Internet

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Die Bereitstellung des einmaligen Kennworts für DirectAccess wurde aus dem homenet-Subnetz getestet und kann nun über das Internet getestet werden.

### <a name="to-test-otp-functionality-from-the-internet-on-client1"></a>So testen Sie die OTP-Funktionalität über das Internet auf CLIENT1

1. Auf CLIENT1 stellen Sie sicher, dass Sie als **User1**angemeldet sind. Verbinden Sie CLIENT1 mit dem Corpnet-Subnetz.

2. Geben Sie auf dem **Start** Bildschirm**powershell.exe**ein, klicken Sie mit der rechten Maustaste auf **PowerShell**, klicken Sie auf **erweitert**, und klicken Sie dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.

3. Geben Sie im Windows PowerShell-Fenster **gpupdate/force** ein, und drücken Sie die EINGABETASTE.

4. Entfernen Sie die CLIENT1 aus dem homenet-Subnetz, verbinden Sie Sie mit dem Internet, und starten Sie den Computer neu.

5. Öffnen Sie auf CLIENT1 Internet Explorer, geben Sie in der Adressleiste ein, **https://app1.corp.contoso.com/** und drücken Sie die EINGABETASTE. Drücken Sie F5.

   Die Site sollte nicht geöffnet werden.

6. Geben Sie auf dem **Start** Bildschirm**RSA**ein, und klicken Sie auf **RSA SecurID Token**.

7. Warten Sie, bis der RSA SecurID-Token das einmalige Kennwort ändert, und klicken Sie dann auf **Kopieren**.

8. Klicken Sie auf die**Netzwerkverbindungen**-Symbol im Infobereich angezeigt, DA Medien-Manager zugreifen.

9. Klicken Sie auf **Arbeitsplatz Verbindung**und dann auf **weiter**.

10. Drücken Sie STRG + ALT + ENTF, und klicken Sie auf die Kachel **einmal Kennwort (OTP)** .

11. Fügen Sie die zuvor kopierte achtstellige Ziffer in den Code ein, und klicken Sie auf **OK**. Warten Sie, bis die Authentifizierung fertiggestellt ist. Der Status der DirectAccess-Arbeitsplatz Verbindung wird nun **verbunden**.

12. Geben Sie in Internet Explorer in der Adressleiste ein, **https://app1.corp.contoso.com/** und drücken Sie die EINGABETASTE. Drücken Sie F5. Die Standard-IIS-Website auf APP1 wird angezeigt.

13. Geben Sie in der Internet Explorer-Adressleiste ein, **https://app2.corp.contoso.com/** und drücken Sie die EINGABETASTE. Drücken Sie F5. Die IIS-Standard Website wird auf APP2 angezeigt.

14. Geben Sie auf dem **Start** Bildschirm<strong> \\ \app1\files</strong>ein, und drücken Sie die EINGABETASTE.

15. Doppelklicken Sie im Fenster freigegebene Ordner **Dateien** auf die **Example.txt** Datei. Der Inhalt der Example.txt Datei wird angezeigt.

16. Geben Sie auf dem **Start** Bildschirm<strong> \\ \app2\files</strong>ein, und drücken Sie die EINGABETASTE.

17. Doppelklicken Sie im Fenster freigegebene Ordner **Dateien** auf den **neuen Text #b0** Datei. Der Inhalt der neuen Text Document.txt Datei wird angezeigt.



