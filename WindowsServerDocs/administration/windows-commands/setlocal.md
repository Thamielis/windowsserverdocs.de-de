---
title: setlocal
description: Referenz Artikel für SETLOCAL, mit dem die Lokalisierung von Umgebungsvariablen in einer Batchdatei gestartet wird.
ms.topic: reference
ms.assetid: e4e4b6d3-3f1a-4851-a782-25ee2470e16e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 807bcb1d5694617f9632e88a4bc200a714048cc9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639470"
---
# <a name="setlocal"></a>setlocal

Startet die Lokalisierung von Umgebungsvariablen in einer Batchdatei. Die Lokalisierung wird fortgesetzt, bis ein entsprechender **endlocal** -Befehl gefunden wird oder das Ende der Batchdatei erreicht wird.



## <a name="syntax"></a>Syntax

```
setlocal [enableextensions | disableextensions] [enabledelayedexpansion | disabledelayedexpansion]
```

## <a name="arguments"></a>Argumente

|Argument|BESCHREIBUNG|
|--------|-----------|
|ENABLEEXTENSIONS|Aktiviert die Befehls Erweiterungen, bis der entsprechende **endlocal** -Befehl gefunden wird, unabhängig von der Einstellung, bevor der Befehl " **setlocal** " ausgeführt wurde.|
|DISABLEEXTENSIONS|Deaktiviert die Befehls Erweiterungen, bis der entsprechende **endlocal** -Befehl gefunden wird, unabhängig von der Einstellung, bevor der Befehl " **setlocal** " ausgeführt wurde.|
|enabledelayedexpansion|Ermöglicht die verzögerte Erweiterung der Umgebungsvariablen, bis der entsprechende **endlocal** -Befehl gefunden wird, unabhängig von der Einstellung, bevor der Befehl " **setlocal** " ausgeführt wurde.|
|disabledelayedexpansion|Deaktiviert die Erweiterung der verzögerten Umgebungsvariablen, bis der entsprechende **endlocal** -Befehl gefunden wird, unabhängig von der Einstellung, bevor der Befehl " **setlocal** " ausgeführt wurde.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Verwenden von **setlocal**

    Wenn Sie **setlocal** außerhalb eines Skripts oder einer Batchdatei verwenden, hat dies keine Auswirkungen.
-   Ändern von Umgebungsvariablen

    Verwenden Sie **setlocal** , um Umgebungsvariablen zu ändern, wenn Sie eine Batchdatei ausführen. Umgebungs Änderungen, die nach der Ausführung von **setlocal** vorgenommen werden, sind lokal in der Batchdatei. Das Cmd.exe Programm stellt vorherige Einstellungen wieder her, wenn es auf einen **endlocal** -Befehl stößt oder das Ende der Batchdatei erreicht.
-   Schachteln von Befehlen

    Sie können in einem Batch-Programm mehr als einen Befehl " **setlocal** " oder " **endlocal** " haben (d. h. in einem Batch-Programm).
-   Testen von Befehls Erweiterungen in Batch Dateien

    Mit dem Befehl **setlocal** wird die ERRORLEVEL-Variable festgelegt. Wenn Sie {**ENABLEEXTENSIONS**  |  **DISABLEEXTENSIONS**} oder {**enabledelayedexpansion**  |  **disabledelayedexpansion**} übergeben, wird die ERRORLEVEL-Variable auf **0** (null) festgelegt. Andernfalls wird Sie auf **1**festgelegt. Sie können diese Informationen in Batch Skripts verwenden, um zu bestimmen, ob die Erweiterungen verfügbar sind, wie im folgenden Beispiel gezeigt:
    ```
    setlocal enableextensions
    verify other 2>nul
    if errorlevel 1 echo Unable to enable extensions
    ```
    Da **cmd** die ERRORLEVEL-Variable nicht festgelegt, wenn die Befehls Erweiterungen deaktiviert sind, initialisiert der **Verify** -Befehl die ERRORLEVEL-Variable auf einen Wert ungleich 0 (null), wenn Sie Sie mit einem ungültigen Argument verwenden. Wenn Sie den Befehl **setlocal** mit den Argumenten {**ENABLEEXTENSIONS**  |  **DISABLEEXTENSIONS**} oder {**enabledelayedexpansion**  |  **disabledelayedexpansion**} verwenden und die ERRORLEVEL-Variable nicht auf **1**festgelegt ist, sind keine Befehls Erweiterungen verfügbar.

## <a name="examples"></a>Beispiele

Sie können Umgebungsvariablen in einer Batchdatei lokalisieren, wie im folgenden Beispielskript gezeigt:
```
rem *******Begin Comment**************
rem This program starts the superapp batch program on the network,
rem directs the output to a file, and displays the file
rem in Notepad.
rem *******End Comment**************
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)