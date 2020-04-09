---
title: WinSAT-Arbeitsspeicher
description: Windows-Befehls Artikel für WinSAT-Arbeitsspeicher, bei dem die Systemspeicher Bandbreite auf eine Weise überprüft wird, die den umfangreichen Arbeitsspeichers und Speicherpuffer Kopien reflektiert, wie bei der Multimedia-Verarbeitung.
ms.prod: windows-server
ms.technology: manage-windows-commands
winms.topic: article
ms.assetid: cda017bf-6193-43c1-b71f-e379c23e1152
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20d7a67ebc6ee623ed7cba41e98bc0105465bdcc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829113"
---
# <a name="winsat-mem"></a>WinSAT-Arbeitsspeicher



Testet die Systemspeicher Bandbreite auf eine Weise, die große Arbeitsspeicher-und Arbeitsspeicher Puffer Kopien reflektiert, wie Sie bei der Multimedia-Verarbeitung verwendet werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
winsat mem <parameters>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|nach oben|Erzwingen Sie Speichertests nur mit einem einzigen Thread. Der Standardwert besteht darin, einen Thread pro physischer CPU oder Kern auszuführen.|
|-RN|Geben Sie an, dass die Threads der Bewertung mit normaler Priorität ausgeführt werden sollen. Der Standardwert besteht darin, mit der Priorität 15 auszuführen.|
|-NC|Geben Sie an, dass die Bewertung Speicher zuweisen und als nicht zwischengespeicherte markieren soll. Dies bedeutet, dass die Caches des Prozessors bei Kopier Vorgängen umgangen werden. Der Standardwert ist die Durchführung im zwischengespeicherten Speicherplatz.|
|-Do \<n >|Geben Sie den Abstand zwischen dem Ende des Quell Puffers und dem Anfang des Ziel Puffers in Bytes an. Der Standardwert ist 64 Bytes. Der maximal zulässige Ziel Offset beträgt 16 MB. Das Angeben eines ungültigen Ziel Offsets führt zu einem Fehler.</br>Hinweis: NULL ist ein gültiger Wert für **\<n >** , aber negative Zahlen nicht.|
|-Mint \<n >|Geben Sie die minimale Laufzeit (in Sekunden) für die Bewertung an. Der Standardwert ist 2,0. Der Minimalwert ist 1,0. Der Höchstwert ist 30,0.</br>Hinweis: Wenn Sie einen **-Mint-** Wert angeben, der größer ist als der **-maxt-** Wert, wenn die beiden Parameter in Kombination verwendet werden, führt dies zu einem Fehler.|
|-maxt \<n >|Geben Sie die maximale Laufzeit (in Sekunden) für die Bewertung an. Der Standardwert ist 5,0. Der Minimalwert ist 1,0. Der Höchstwert ist 30,0. Wenn Sie in Kombination mit dem **-Mint-** Parameter verwendet wird, beginnt die Bewertung nach dem in **-Mint**angegebenen Zeitraum regelmäßige statistische Prüfungen der Ergebnisse. Wenn die statistischen Überprüfungen bestanden werden, wird die Bewertung beendet, bevor der in **-maxt** angegebene Zeitraum verstrichen ist. Wenn die Bewertung für den in **-maxt** angegebenen Zeitraum ausgeführt wird, ohne die statistischen Prüfungen zu erfüllen, wird die Bewertung zu diesem Zeitpunkt abgeschlossen, und die gesammelten Ergebnisse werden zurückgegeben.|
|-bufferSize \<n >|Geben Sie die Puffergröße an, die vom Speicher Kopier Test verwendet werden soll. Zweimal wird dieser Betrag pro CPU zugeordnet, der die Menge der Daten bestimmt, die von einem Puffer in einen anderen kopiert werden. Der Standardwert ist 16 MB. Dieser Wert wird auf die nächste Grenze von 4 KB gerundet. Der Höchstwert beträgt 32 MB. Der Minimalwert ist 4 KB. Das Angeben einer ungültigen Puffergröße führt zu einem Fehler.|
|-v|Senden Sie eine ausführliche Ausgabe an stdout, einschließlich Status-und Fortschrittsinformationen. Alle Fehler werden auch in das Befehlsfenster geschrieben.|
|-XML \<Dateiname >|Speichert die Ausgabe der Bewertung als die angegebene XML-Datei. Wenn die angegebene Datei vorhanden ist, wird sie überschrieben.|
|-idiskinfo|Speichern Sie Informationen zu physischen Volumes und logischen Datenträgern als Teil des **\<SystemConfig->** Abschnitts in der XML-Ausgabe.|
|-iguid|Erstellen Sie eine Globally Unique Identifier (GUID) in der XML-Ausgabedatei.|
|-Hinweis Text|Fügen Sie den Hinweis Text zum **\<Notiz >** Abschnitt in der XML-Ausgabedatei hinzu.|
|-ICN|Fügen Sie den Namen des lokalen Computers in die XML-Ausgabedatei ein.|
|-EEF|Listet zusätzliche Systeminformationen in der XML-Ausgabedatei auf.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

- Im folgenden Beispiel wird die Bewertung für mindestens 4 Sekunden und nicht länger als 12 Sekunden ausgeführt. dabei wird eine Puffergröße von 32 MB verwendet, und die Ergebnisse werden im XML-Format in der Datei **memtest. XML**gespeichert.  
  ```
  winsat mem -mint 4.0 -maxt 12.0 -buffersize 32MB -xml memtest.xml
  ```

## <a name="remarks"></a>Hinweise

-   Sie müssen mindestens Mitglied der lokalen Gruppe Administratoren oder einer entsprechenden Gruppe sein, um **WinSAT**verwenden zu können. Der Befehl muss von einem Eingabe Aufforderungs Fenster mit erhöhten Rechten ausgeführt werden.
-   Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten auf **Start**und auf **Zubehör**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.

## <a name="additional-references"></a>Weitere Verweise

