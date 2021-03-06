---
title: Ändern eines Laufwerkbuchstabens
description: Hier erfährst du, wie du unter Windows mithilfe der Datenträgerverwaltung einen Laufwerkbuchstaben änderst oder zuweist.
ms.date: 06/08/2020
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 52665f239bec56ad81d0300ed3312ec57b32cb1f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936071"
---
# <a name="change-a-drive-letter"></a>Ändern eines Laufwerkbuchstabens

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn du einem Laufwerk einen anderen Laufwerkbuchstaben zuweisen möchtest oder ein Laufwerk ohne Laufwerkbuchstaben besitzt, kannst du den Laufwerkbuchstaben mithilfe der Datenträgerverwaltung ändern oder zuweisen. Wenn Sie das Laufwerk stattdessen in einem leeren Ordner bereitstellen möchten, sodass es nur als ein weiterer Ordner angezeigt wird, finden Sie unter [Bereitstellen eines Laufwerks in einem Ordner](assign-a-mount-point-folder-path-to-a-drive.md) weitere Informationen.

> [!IMPORTANT]
> Falls du den Laufwerkbuchstaben eines Laufwerks mit Windows- oder App-Installation änderst, können Apps unter Umständen nicht richtig ausgeführt werden oder das Laufwerk möglicherweise nicht finden. Aus diesem Grund wird empfohlen, den Laufwerkbuchstaben des Laufwerks nicht zu ändern, auf dem Windows oder Apps installiert ist bzw. sind.

Hier erfahren Sie, wie Sie den Laufwerkbuchstaben ändern können:

1. Öffne die Datenträgerverwaltung mit Administratorberechtigungen.
    Halten Sie dazu die Startschaltfläche gedrückt (oder klicken Sie mit der rechten Maustaste darauf), und wählen Sie dann **Datenträgerverwaltung** aus.
1. Halten Sie in „Datenträgerverwaltung“ das Volume gedrückt (oder klicken Sie mit der rechten Maustaste darauf), für das Sie den Laufwerkbuchstaben ändern oder hinzufügen möchten, und wählen Sie dann **Laufwerkbuchstaben und -pfade ändern** aus.

    ![Datenträgerverwaltung mit angezeigtem Laufwerk](media/change-drive-letter.png)
    > [!TIP]
    > Wird die Option **Laufwerkbuchstaben und -pfade ändern...** nicht oder abgeblendet angezeigt, kann dem Volume möglicherweise kein Laufwerkbuchstabe zugewiesen werden. Dies ist der Fall, wenn das Laufwerk nicht zugeordnet ist und [initialisiert](initialize-new-disks.md) werden muss. Vielleicht soll der Zugriff auch gar nicht möglich sein – etwa im Fall von EFI-Systempartitionen oder Wiederherstellungspartitionen. Wenn du sichergestellt hast, dass du ein formatiertes Volume mit einem Laufwerkbuchstaben besitzt, auf das du zugreifen, dessen Laufwerkbuchstaben du aber nicht ändern kannst, findest du in diesem Thema wahrscheinlich keine hilfreichen Informationen. Wende dich in diesem Fall an [Microsoft](https://support.microsoft.com/contactus/) oder den Hersteller deines PCs, um weitere Unterstützung zu erhalten.

1. Wähle zum Ändern des Laufwerkbuchstaben die Option **Ändern** aus. Wähle **Hinzufügen** aus, um einen Laufwerkbuchstaben zuzuweisen, sofern das Laufwerk noch keinen besitzt.

    ![Dialogfeld „Laufwerkbuchstaben und -pfade ändern...“](media/change-drive-letter2.png)
1. Wähle den neuen Laufwerkbuchstaben und dann **OK** aus. Wenn die Meldung angezeigt wird, dass Programme, die den Laufwerkbuchstaben verwenden, möglicherweise nicht ordnungsgemäß ausgeführt werden, wähle **Ja** aus.

    ![Dialogfeld „Laufwerkbuchstaben und -pfade ändern...“: Ändern des Laufwerkbuchstabens](media/change-drive-letter3.png)
