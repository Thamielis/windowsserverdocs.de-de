---
title: logman Create Counter
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e214c32-b704-43c1-b548-e1cf43b583c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: feff7ad1597232ad441e2ad23ee73638b4ad68ea
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724385"
---
# <a name="logman-create-counter"></a>logman Create Counter

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellen Sie einen Counter-Datensammler.  

## <a name="syntax"></a>Syntax  
```  
logman create counter <[-n] <name>> [options]  
```  
### <a name="parameters"></a>Parameter  

|                    Parameter                     |                                                                               BESCHREIBUNG                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    Zeigt die kontextbezogene Hilfe an.                                                                     |
|                -s<computer name>                |                                                          Führen Sie den Befehl auf dem angegebenen Remote Computer aus.                                                          |
|                 -config <value>                  |                                                         Gibt die Einstellungsdatei an, die Befehlsoptionen enthält.                                                         |
|                   [-n]<name>                    |                                                                       Name des Zielobjekts                                                                        |
| -f <bin&#124;bincirc&#124;CSV&#124;TSV&#124;SQL> |                                                            Gibt das Protokoll Format für den Datensammler an.                                                             |
|             -[-] u <Benutzer [Kennwort] >              | Gibt den Benutzer an, der als ausgeführt werden soll. Wenn Sie \* einen als Kennwort eingeben, wird eine Eingabeaufforderung für das Kennwort ausgegeben. Das Kennwort wird nicht angezeigt, wenn Sie es an der Eingabeaufforderung eingeben. |
|    -m < [Start] [Ende] [[Start] [Ende] [...]] >    |                                                Wechseln Sie zu "manueller Start" oder "beenden" anstelle eines geplanten Anfangs-oder Endzeit Zeitraums.                                                 |
|                -RF < [[hh:] mm:] SS>                |                                                        Führt den Datensammler für den angegebenen Zeitraum aus.                                                         |
|        -b <M/d/yyyy h:mm: SS [am&#124;pm] >         |                                                              Beginnt mit dem Sammeln von Daten zum angegebenen Zeitpunkt.                                                               |
|        -e <M/d/yyyy h:mm: SS [am&#124;pm] >         |                                                               Beenden Sie die Datensammlung zum angegebenen Zeitpunkt.                                                                |
|                -Si < [[hh:] mm:] SS>                |                                                 Gibt das Stichproben Intervall für Leistungsdaten Sammler an.                                                  |
|              -o <Pfad&#124;DSN! Log>              |                                              Gibt die Ausgabeprotokoll Datei oder den DSN-und Protokoll Satz Namen in einer SQL-Datenbank an.                                               |
|                      -[-] r                       |                                                  Wiederholen Sie den Datensammler täglich zu den angegebenen Anfangs-und Endzeiten.                                                  |
|                      -[-] a                       |                                                                     Fügen Sie an eine vorhandene Protokolldatei an.                                                                     |
|                      -[-] OW                      |                                                                     Hiermit wird eine vorhandene Protokolldatei überschrieben.                                                                     |
|           -[-] v <nnnnnn&#124;mmddhhmm>           |                                                   Fügen Sie Datei Versionsinformationen an das Ende des Protokoll Dateinamens an.                                                   |
|                  -[-] RC<task>                   |                                                         Führen Sie den Befehl aus, der bei jedem Schließen des Protokolls angegeben wird.                                                          |
|                 -[-] max. <value>                  |                                                 Maximale Protokolldatei Größe in MB oder maximale Anzahl von Datensätzen für SQL-Protokolle.                                                  |
|              -[-] cnf-< [[hh:] mm:] SS>              |     Wenn Time angegeben ist, wird eine neue Datei erstellt, wenn die angegebene Zeit abgelaufen ist. Wenn Time nicht angegeben ist, erstellen Sie eine neue Datei, wenn die maximale Größe überschritten wird.     |
|                        -y                        |                                                             Antworten Sie auf Ja, um alle Fragen zu beantworten.                                                              |
|                  -CF<filename>                  |                       Gibt die zu sammelnden Leistungsindikatoren zum Auflisten von Dateien an. Die Datei sollte einen Leistungs Leistungs beendenamen pro Zeile enthalten.                        |
|               -c <Pfad [Pfad []] >               |                                                              Gibt die zu sammelnden Leistungs Zählers an.                                                               |
|                   -SC <value>                    |                                      Gibt die maximale Anzahl von Stichproben an, die mit einem Leistungsdaten Sammler erfasst werden sollen.                                      |

## <a name="remarks"></a>Bemerkungen  
Wenn [-] aufgeführt ist, wird die-Option durch ein extra negiert.  
## <a name="examples"></a>Beispiele  
Der folgende Befehl erstellt einen Counter-Wert mit dem Namen "perf_log" unter Verwendung des Zählers "Prozessorzeit (%)" aus der Prozessor-(_Total)  
```  
logman create counter perf_log -c \Processor(_Total)\% Processor time  
```  
Der folgende Befehl erstellt einen Counter mit dem Namen "perf_log" unter Verwendung des Zählers "Prozessorzeit (%)" aus der Kategorie "Prozessor" (_Total), wobei eine Protokolldatei mit einer maximalen Größe von 10 MB erstellt und Daten für 1 Minute und 0 Sekunden gesammelt werden.  
```  
logman create counter perf_log -c \Processor(_Total)\% Processor time -max 10 -rf 01:00  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
[logman](logman.md)  
