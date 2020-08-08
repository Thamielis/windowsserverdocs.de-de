---
title: Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: dougkim
ms.topic: article
ms.assetid: f77a3989-9f92-41ef-92a8-031651dd73a8
ms.author: lizross
author: eross-msft
ms.date: 07/26/2018
ms.openlocfilehash: 86c6bb664fc011be4f08e792118f3ff232f8410f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969637"
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie die Zertifikat Sperr Listen-Verteilungs Punkte (CRL) und die AIA-Einstellungen (Authority Information Access) auf CA1 konfigurieren.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.

#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>So konfigurieren Sie die CDP-und AIA-Erweiterungen auf CA1

1.  Klicken Sie in Server-Manager auf **Extras** und dann auf **Zertifizierungsstelle**.

2.  Klicken Sie in der Konsolen Struktur der Zertifizierungsstelle mit der rechten Maustaste auf **Corp-CA1-ca**, und klicken Sie dann auf **Eigenschaften**.

    > [!NOTE]
    > Der Name der Zertifizierungsstelle ist anders, wenn Sie den Computer nicht benennen CA1 und der Domänen Name unterscheidet sich von dem in diesem Beispiel. Der Name der Zertifizierungsstelle hat das Format *Domäne* - *CAComputername*-ca.

3.  Klicken Sie auf die Registerkarte **Erweiterungen** . Stellen Sie sicher, dass **Erweiterung auswählen** auf **CRL-Verteilungs Punkt (CRL Distribution Point, CDP)** festgelegt ist, und führen Sie in den Speicher **Orten, von denen Benutzer eine Zertifikat Sperr Liste abrufen können**die folgenden Schritte aus:

    1.  Wählen Sie den Eintrag aus `file://\\<ServerDNSName>\CertEnroll\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl` , und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.

    2.  Wählen Sie den Eintrag aus `http://<ServerDNSName>/CertEnroll/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl` , und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.

    3.  Wählen Sie den Eintrag aus, der mit dem Pfad beginnt `ldap:///CN=<CATruncatedName><CRLNameSuffix>,CN=<ServerShortName>` , und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.

4.  Klicken Sie in Speicher **Orte angeben, von denen Benutzer eine Zertifikat Sperr Liste abrufen können (CRL)** auf **Hinzufügen**. Das Dialogfeld **Speicherort hinzufügen** wird geöffnet.

5.  Geben Sie unter **Speicherort hinzufügen**in **Speicherort**ein `http://pki.corp.contoso.com/pki/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl` , und klicken Sie dann auf **OK**. Dadurch wird das Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.

6.  Aktivieren Sie auf der Registerkarte **Erweiterungen** die folgenden Kontrollkästchen:

    -   **In CRLs einschließen. Clients verwenden diese, um die Delta-CRL-Speicherorte zu suchen.**

    -   **In die CDP-Erweiterung der ausgestellten Zertifikate einbeziehen**

7.  Klicken Sie in Speicher **Orte angeben, von denen Benutzer eine Zertifikat Sperr Liste abrufen können (CRL)** auf **Hinzufügen**. Das Dialogfeld **Speicherort hinzufügen** wird geöffnet.

8.  Geben Sie unter **Speicherort hinzufügen**in **Speicherort**ein `file://\\pki.corp.contoso.com\pki\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl` , und klicken Sie dann auf **OK**. Dadurch wird das Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.

9. Aktivieren Sie auf der Registerkarte **Erweiterungen** die folgenden Kontrollkästchen:

    -   **Veröffentlichen von CRLs an diesem Ort**

    -   **Delta-CRLs an diesem Speicherort veröffentlichen**

10. Ändern **Sie SELECT Extension** to **Authority Information Access (AIA)**, und führen Sie in den Speicher **Orten, von denen Benutzer eine Zertifikat Sperr Liste abrufen können**, die folgenden Schritte aus:

    1.  Wählen Sie den Eintrag aus, der mit dem Pfad beginnt `ldap:///CN=<CATruncatedName>,CN=AIA,CN=Public Key Services` , und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.

    2.  Wählen Sie den Eintrag aus `http://<ServerDNSName>/CertEnroll/<ServerDNSName>_<CaName><CertificateName>.crt` , und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.

    3.  Wählen Sie den Eintrag aus `file://\\<ServerDNSName>\CertEnroll\<ServerDNSName><CaName><CertificateName>.crt` , und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.

11. Klicken Sie in Speicher **Orte angeben, von denen Benutzer das Zertifikat für diese Zertifizierungsstelle abrufen können**auf **Hinzufügen**. Das Dialogfeld **Speicherort hinzufügen** wird geöffnet.

12. Geben Sie unter **Speicherort hinzufügen**in **Speicherort**ein `http://pki.corp.contoso.com/pki/<ServerDNSName>_<CaName><CertificateName>.crt` , und klicken Sie dann auf **OK**. Dadurch wird das Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.

13. Wählen Sie auf der Registerkarte **Erweiterungen** **in den AIA der ausgestellten Zertifikate einbeziehen aus**.

14. Wenn Sie zum Neustart Active Directory Zertifikat Dienste aufgefordert werden, klicken Sie auf **Nein**. Der Dienst wird zu einem späteren Zeitpunkt neu gestartet.


