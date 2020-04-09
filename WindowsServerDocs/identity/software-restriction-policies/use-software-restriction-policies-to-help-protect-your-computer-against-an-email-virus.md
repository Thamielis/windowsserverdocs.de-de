---
title: Verwenden von Richtlinien für die Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: 02f23979-f832-4e46-bdea-21fd77db35b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 680d0435d77164e101f045b439be6ccb6601dfef
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855733"
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>Verwenden von Richtlinien für die Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält Informationen zum Festlegen von Anwendungs Steuerungs Richtlinien mithilfe von Software Einschränkungs Richtlinien (Software Einschränkungs Richtlinien, Software Einschränkungs Richtlinien) zum Schutz Ihres Computers vor einem e-Mail-Virus ab Windows Server 2008 und Windows Vista.

## <a name="introduction"></a>Einführung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in der Sie ausschließlich die Ausführung explizit angegebener Anwendungen zulassen. Diese sind in Microsoft Active Directory Domain Services und Gruppenrichtlinie integriert, können aber auch auf eigenständigen Computern konfiguriert werden. Einen Ausgangspunkt für SRP finden Sie in den [Richtlinien für Software Einschränkung](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7 kann Windows AppLocker anstelle von oder in zusammen mit SRP für einen Teil ihrer Anwendungs Steuerungsstrategie verwendet werden. 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>Konfigurieren von SRP zum Schutz vor einem e-Mail-Virus

1.  Informieren Sie sich über die bewährten Methoden für Software Einschränkungs Richtlinien, um zu verstehen, wie SRP funktioniert.

    -   [Empfohlene Methoden](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [Funktionsweise von Software Einschränkungs Richtlinien](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

    -   [Für den lokalen Computer](administer-software-restriction-policies.md#BKMK_1)

    -   [Für eine Domäne, Site oder Organisationseinheit, und Sie befinden sich auf einem Mitglieds Server oder einer Arbeitsstation, die mit einer Domäne verknüpft ist](administer-software-restriction-policies.md#BKMK_2)

3.  Wenn Sie zuvor keine Software Einschränkungs Richtlinien definiert haben, erstellen Sie neue Richtlinien für Software Einschränkung.

    -   [So erstellen Sie neue Richtlinien für Software Einschränkung](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  Erstellen Sie eine Pfadregel für den Ordner, den Ihr e-Mail-Programm zum Ausführen von e-Mail-Anlagen verwendet, und legen Sie dann die Sicherheits **Stufe auf unzulässig**fest

    -   [Arbeiten mit Pfad Regeln](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  Geben Sie die Dateitypen an, für die die Regel gilt.

    -   [So können Sie einen bestimmten Dateityp hinzufügen oder löschen](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  Ändern Sie die Richtlinien Einstellungen so, dass Sie auf die gewünschten Benutzer und Gruppen angewendet werden:

    -   Geben Sie Benutzer oder Gruppen an, für die die Richtlinien Einstellungen des Gruppenrichtlinie Objekts (GPO) nicht gelten sollen.

    -   Schließen Sie lokale Administratoren aus den Richtlinien für Software Einschränkung einer bestimmten Richtlinien Einstellung in Gruppenrichtlinie aus, und lassen Sie die übrigen Gruppenrichtlinie auf die Administratoren anwenden.

        -   [So verhindern Sie, dass Software Einschränkungs Richtlinien auf lokale Administratoren angewendet werden](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  Testen Sie die Richtlinie.


