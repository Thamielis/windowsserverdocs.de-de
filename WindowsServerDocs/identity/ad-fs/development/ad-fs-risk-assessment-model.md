---
title: Erstellen von Plug-Ins mit dem Risikobewertungsmodell von AD FS 2019
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 05/05/2020
ms.topic: article
ms.openlocfilehash: c70c117716f5e60a75182a7529a39daa46c796b1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942925"
---
# <a name="build-plug-ins-with-ad-fs-2019-risk-assessment-model"></a>Erstellen von Plug-Ins mit dem Risikobewertungsmodell von AD FS 2019

Sie können jetzt Ihre eigenen Plug-ins zum Blockieren oder Zuweisen einer Risikobewertung zu Authentifizierungsanforderungen in verschiedenen Phasen – Anforderung empfangen, vor der Authentifizierung und nach der Authentifizierung. Dies kann mit dem neuen Risiko Bewertungsmodell erreicht werden, das mit AD FS 2019 eingeführt wurde.

## <a name="what-is-the-risk-assessment-model"></a>Was ist das Risiko Bewertungsmodell?

Das Risiko Bewertungsmodell besteht aus einer Reihe von Schnittstellen und Klassen, die es Entwicklern ermöglichen, Authentifizierungs Anforderungs Header zu lesen und ihre eigene Risiko Bewertungs Logik zu implementieren. Der implementierte Code (Plug-in) wird dann in Übereinstimmung mit AD FS Authentifizierungsprozess ausgeführt. Wenn Sie z. b. die Schnittstellen und Klassen verwenden, die im Modell enthalten sind, können Sie Code implementieren, um eine Authentifizierungsanforderung auf der Grundlage der im Anforderungs Header enthaltenen Client-IP-Adresse zu blockieren oder zuzulassen. AD FS führt den Code für jede Authentifizierungsanforderung aus und führt gemäß der implementierten Logik entsprechende Maßnahmen durch.

Das Modell ermöglicht das Plug-in-Code in drei Phasen AD FS Authentifizierungs Pipeline, wie unten gezeigt.

![model](media/ad-fs-risk-assessment-model/risk1.png)

1.    **Stufe "empfangene Anforderung** " – ermöglicht die Erstellung von Plug-ins zum Zulassen oder Blockieren von Anforderungen, wenn AD FS die Authentifizierungsanforderung empfängt, d.h. bevor der Benutzer Anmelde Informationen eingibt Sie können den Anforderungs Kontext (z. b. Client-IP, HTTP-Methode, Proxy Server-DNS usw.) verwenden, der in dieser Phase verfügbar ist, um die Risikobewertung durchzuführen. Sie können z. b. ein Plug-in erstellen, um die IP-Adresse aus dem Anforderungs Kontext zu lesen und die Authentifizierungsanforderung zu blockieren, wenn die IP-Adresse in der vordefinierten Liste der riskanten IPS enthalten ist.

2.    **Phase vor der Authentifizierung** – ermöglicht das aufbauen von Plug-ins, um Anforderungen an den Punkt zuzulassen oder zu blockieren, an dem der Benutzer die Anmelde Informationen bereitstellt, aber bevor AD FS Sie auswertet Zu diesem Zeitpunkt haben Sie zusätzlich zum Anforderungs Kontext auch Informationen zum Sicherheitskontext (z. b. Benutzer Token, Benutzer Bezeichner usw.) und zum Protokoll Kontext (z. b. Authentifizierungsprotokoll, ClientID, ResourceId usw.), der in ihrer Risiko Bewertungs Logik verwendet werden kann. Sie können z. b. ein Plug-in erstellen, um Kenn Wort Manipulationen zu verhindern, indem Sie das Benutzer Kennwort aus dem Benutzer Token lesen und die Authentifizierungsanforderung blockieren, wenn das Kennwort in der vordefinierten Liste der riskanten Kenn Wörter enthalten ist.

3.    **Nach Authentifizierung** – ermöglicht die Erstellung von Plug-ins, um das Risiko zu bewerten, nachdem der Benutzer Anmelde Informationen eingegeben hat und AD FS die Authentifizierung durchgeführt hat. Zu diesem Zeitpunkt haben Sie zusätzlich zum Anforderungs Kontext, Sicherheitskontext und Protokoll Kontext auch Informationen zum Authentifizierungs Ergebnis (Erfolg oder Fehler). Das Plug-in kann die Risikobewertung basierend auf den verfügbaren Informationen auswerten und die Risikobewertung an die Anspruchs-und Richtlinien Regeln übergeben, um die Auswertung zu erhöhen.

Um besser zu verstehen, wie ein Plug-in für die Risikobewertung erstellt und in AD FS Prozess ausgeführt wird, erstellen wir ein Beispiel-Plug-in, das die Anforderungen von bestimmten **Extranet** -IPS, die als riskant identifiziert werden, blockieren, das Plug-in mit AD FS registrieren und schließlich die Funktionalität testen.

>[!NOTE]
>Alternativ dazu können Sie ein [riskantes Benutzer-Plug-in](https://github.com/microsoft/adfs-sample-block-user-on-adfs-marked-risky-by-AzureAD-IdentityProtection)erstellen, ein Beispiel-Plug-in, das die von Azure AD Identity Protection festgelegte Benutzer Risikostufe nutzt, um die Authentifizierung zu blockieren oder Multi-Factor Authentication (MFA) zu erzwingen. Schritte zum Erstellen eines riskanten Benutzer-Plug-ins sind [hier](https://github.com/microsoft/adfs-sample-block-user-on-adfs-marked-risky-by-AzureAD-IdentityProtection) verfügbar.

## <a name="building-a-sample-plug-in"></a>Aufbau eines Beispiel-Plug-ins

>[!NOTE]
>In dieser exemplarischen Vorgehensweise wird nur gezeigt, wie Sie ein Beispiel-Plug-in erstellen können. Das heißt, wir erstellen eine Lösung für Unternehmen.

### <a name="pre-requisites"></a>Voraussetzungen
Im folgenden finden Sie eine Liste der Voraussetzungen, die zum Erstellen dieses Beispiel-Plug-Ins erforderlich sind.

- AD FS 2019 installiert und konfiguriert
- .NET Framework 4,7 und höher
- Visual Studio

### <a name="build-plug-in-dll"></a>Plug-in-dll erstellen
Das folgende Verfahren führt Sie durch die Schritte zum Aufbau einer Beispiel-Plug-in-dll.

1. Laden Sie das Beispiel-Plug-in herunter, verwenden Sie git bash, und geben Sie Folgendes ein:

   ```
   git clone https://github.com/Microsoft/adfs-sample-RiskAssessmentModel-RiskyIPBlock
   ```

2. Erstellen Sie eine **CSV** -Datei an einem beliebigen Speicherort auf dem AD FS Server (in meinem Fall habe ich die **authconfigdb.csv** Datei unter " **c:\extensions**" erstellt), und fügen Sie die IP-Adressen, die Sie blockieren möchten, dieser Datei hinzu.

   Das Beispiel-Plug-in blockiert alle Authentifizierungsanforderungen aus den in dieser Datei aufgeführten **Extranet-IPS** .

   >{! Hinweis] Wenn Sie über eine AD FS-Farm verfügen, können Sie die Datei auf einem beliebigen oder allen AD FS Servern erstellen. Alle Dateien können verwendet werden, um die riskanten IPS in AD FS zu importieren. Der Import Vorgang wird im folgenden Abschnitt im Abschnitt [Registrieren der Plug-in-dll mit AD FS](#register-the-plug-in-dll-with-ad-fs) ausführlich erläutert.

3. Öffnen des Projekts `ThreatDetectionModule.sln` mit Visual Studio

4. Entfernen Sie aus dem Projektmappen- `Microsoft.IdentityServer.dll` Explorer, wie unten gezeigt:</br>
   ![model](media/ad-fs-risk-assessment-model/risk2.png)

5. Fügen Sie einen Verweis auf die Ihres AD FS hinzu, `Microsoft.IdentityServer.dll` wie unten gezeigt.

   a.    Klicken Sie mit der rechten Maustaste auf **Verweise** im Projektmappen- **Explorer** und wählen Sie **Verweis hinzufügen**</br>
   ![model](media/ad-fs-risk-assessment-model/risk3.png)

   b.    Wählen Sie im Fenster **Verweis-Manager** die Option **Durchsuchen**. **Wählen Sie im Abschnitt wählen Sie die zu referendenen Dateien aus..** . Dialog: Wählen Sie `Microsoft.IdentityServer.dll` aus Ihrem AD FS Installationsordner (in meinem Fall " **c:\windows\adfs**") aus, und klicken Sie auf **Hinzufügen**.

   >[!NOTE]
   >In meinem Fall erstelle ich das Plug-in auf dem AD FS Server selbst. Wenn sich Ihre Entwicklungsumgebung auf einem anderen Server befindet, kopieren Sie die `Microsoft.IdentityServer.dll` aus dem AD FS-Installationsordner auf AD FS Server in in das Entwicklungsfeld.</br>

   ![model](media/ad-fs-risk-assessment-model/risk4.png)

   c.    Klicken Sie im Fenster **Verweis-Manager** auf **OK** , nachdem Sie das `Microsoft.IdentityServer.dll` Kontrollkästchen aktiviert haben.</br>
   ![model](media/ad-fs-risk-assessment-model/risk5.png)

6. Alle Klassen und Verweise sind jetzt für einen Build vorhanden.   Da es sich bei der Ausgabe dieses Projekts jedoch um eine DLL handelt, muss Sie im **globalen Assemblycache**(GAC) des AD FS Servers installiert werden, und die dll muss zuerst signiert werden. Gehen Sie dazu folgendermaßen vor:

   a.    **Klicken Sie mit der rechten Maustaste** auf den Namen des Projekts, und klicken Sie dann auf. Klicken Sie im Menü auf **Eigenschaften**.</br>
   ![model](media/ad-fs-risk-assessment-model/risk6.png)

   b.    Klicken Sie auf der Seite **Eigenschaften** auf der linken Seite auf **Signierung**, und aktivieren Sie dann das Kontrollkästchen **Assembly signieren**. Wählen Sie im Dropdown Menü **Schlüsseldatei mit starkem Namen auswählen**die Option **<neu... aus >**</br>
   ![model](media/ad-fs-risk-assessment-model/risk7.png)

   c.    Geben Sie im Dialogfeld Schlüssel für einen **starken Namen erstellen**einen Namen (Sie können einen beliebigen Namen auswählen) für den Schlüssel ein, deaktivieren Sie das Kontrollkästchen **meine Schlüsseldatei mit Kennwort schützen**. Klicken Sie dann auf **OK**.</br>
   ![model](media/ad-fs-risk-assessment-model/risk8.png)

   d.    Speichern Sie das Projekt, wie unten gezeigt.</br>
   ![model](media/ad-fs-risk-assessment-model/risk9.png)

7. Erstellen Sie das Projekt, indem Sie auf **Erstellen** und dann auf Projekt Mappe **neu** erstellen klicken.</br>
   ![model](media/ad-fs-risk-assessment-model/risk10.png)

   Überprüfen Sie das **Ausgabefenster**unten auf dem Bildschirm, um festzustellen, ob Fehler aufgetreten sind.</br>
   ![model](media/ad-fs-risk-assessment-model/risk11.png)


Das Plug-in (dll) ist jetzt einsatzbereit und befindet sich im Ordner " **\bin\debug** " des Projekt Ordners (in meinem Fall **C:\extensions\ThreatDetectionModule\bin\Debug\ThreatDetectionModule.dll**).

Der nächste Schritt besteht darin, diese DLL bei AD FS zu registrieren, sodass Sie mit AD FS Authentifizierungsprozess ausgeführt wird.

### <a name="register-the-plug-in-dll-with-ad-fs"></a>Registrieren Sie die Plug-in-dll bei AD FS

Wir müssen die dll in AD FS registrieren, indem wir den `Register-AdfsThreatDetectionModule` PowerShell-Befehl auf dem AD FS Server verwenden. vor der Registrierung müssen wir jedoch das Token des öffentlichen Schlüssels erhalten. Dieses öffentliche Schlüssel Token wurde erstellt, als der Schlüssel erstellt und die DLL mit diesem Schlüssel signiert wurde. Um zu erfahren, was das Token des öffentlichen Schlüssels für die dll ist, können Sie die **SN.exe** wie folgt verwenden:

1. Kopieren Sie die DLL-Datei aus dem Ordner " **\bin\debug** " an einen anderen Speicherort (in meinem Fall kopieren Sie Sie in " **c:\extensions**")

2. Starten Sie den **Developer-Eingabeaufforderung** für Visual Studio, und navigieren Sie zu dem Verzeichnis, das die **sn.exe** enthält (in meinem Fall das Verzeichnis **c:\Programme (x86) \Microsoft sdks\windows\v10.0a\bin\netfx 4.7.2 Tools** ![ ).](media/ad-fs-risk-assessment-model/risk12.png)

3. Führen Sie den **SN** -Befehl mit dem Parameter " **-T** " und dem Speicherort der Datei (in meinem Fall) aus. `SN -T "C:\extensions\ThreatDetectionModule.dll"` ![](media/ad-fs-risk-assessment-model/risk13.png)</br>
   Mit dem Befehl wird das Token des öffentlichen Schlüssels bereitgestellt (für mich **ist das Token des öffentlichen Schlüssels 714697626ef96b35**).

4. Fügen Sie die dll dem **globalen Assemblycache** des AD FS Servers hinzu. die bewährte Vorgehensweise besteht darin, dass Sie ein geeignetes Installationsprogramm für Ihr Projekt erstellen und das Installationsprogramm verwenden, um die Datei dem GAC hinzuzufügen. Eine weitere Lösung ist die Verwendung von **Gacutil.exe** (Weitere Informationen zuGacutil.exe[verfügbaren](/dotnet/framework/tools/gacutil-exe-gac-tool) **Gacutil.exe** ) auf Ihrem Entwicklungs Computer.  Da ich Visual Studio auf demselben Server wie AD FS verwende, verwende ich **Gacutil.exe** wie folgt.

   a.    Wechseln Sie auf Developer-Eingabeaufforderung für Visual Studio, und navigieren Sie zu dem Verzeichnis, das die **Gacutil.exe** enthält (in meinem Fall lautet das Verzeichnis " **c:\Programme (x86) \Microsoft sdks\windows\v10.0a\bin\netfx 4.7.2 Tools**").

   b.    Ausführen des Befehls " **Gacutil** " (in meinem Fall `Gacutil /IF C:\extensions\ThreatDetectionModule.dll` ) ![](media/ad-fs-risk-assessment-model/risk14.png)

   >[!NOTE]
   >Wenn Sie über eine AD FS-Farm verfügen, muss die obige Ausführung auf jedem AD FS Server in der Farm ausgeführt werden.

5. Öffnen Sie **Windows PowerShell** , und führen Sie den folgenden Befehl zum Registrieren der dll aus.
   ```
   Register-AdfsThreatDetectionModule -Name "<Add a name>" -TypeName "<class name that implements interface>, <dll name>, Version=10.0.0.0, Culture=neutral, PublicKeyToken=< Add the Public Key Token from Step 2. above>" -ConfigurationFilePath "<path of the .csv file>"
   ```
   In meinem Fall lautet der Befehl wie folgt:
   ```
   Register-AdfsThreatDetectionModule -Name "IPBlockPlugin" -TypeName "ThreatDetectionModule.UserRiskAnalyzer, ThreatDetectionModule, Version=10.0.0.0, Culture=neutral, PublicKeyToken=714697626ef96b35" -ConfigurationFilePath "C:\extensions\authconfigdb.csv"
   ```

   >[!NOTE]
   >Sie müssen die dll nur einmal registrieren, auch wenn Sie über eine AD FS-Farm verfügen.

6. Neustarten des AD FS Dienstanbieter nach dem Registrieren der dll

Die dll ist nun in AD FS registriert und einsatzbereit!

 >[!NOTE]
 > Wenn Änderungen am Plug-in vorgenommen und das Projekt neu erstellt wird, muss die aktualisierte dll erneut registriert werden. Vor der Registrierung müssen Sie die Registrierung der aktuellen dll mit dem folgenden Befehl aufheben:</br></br>
 >`
  UnRegister-AdfsThreatDetectionModule -Name "<name used while registering the dll in 5. above>"
 >`</br></br>
 >In meinem Fall lautet der Befehl wie folgt:
 >```
 >UnRegister-AdfsThreatDetectionModule -Name "IPBlockPlugin"
 >```

### <a name="testing-the-plug-in"></a>Testen des Plug-ins

1. Öffnen Sie die **authconfig.csv** Datei, die Sie zuvor erstellt haben (in meinem Fall an Speicherort **c:\extensions**), und fügen Sie die **Extranet-IPS** hinzu, die Sie blockieren möchten. Jede IP-Adresse muss sich in einer separaten Zeile befinden, und am Ende dürfen keine Leerzeichen vorhanden sein.</br>
   ![model](media/ad-fs-risk-assessment-model/risk18.png)

2. Speichern und schließen Sie die Datei.

3. Importieren Sie die aktualisierte Datei in AD FS, indem Sie den folgenden PowerShell-Befehl ausführen.

   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "<name given while registering the dll>" -ConfigurationFilePath "<path of the .csv file>"
   ```

   In meinem Fall lautet der Befehl wie folgt:
   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "IPBlockPlugin" -ConfigurationFilePath "C:\extensions\authconfigdb.csv")
   ```

4. Initiieren Sie eine Authentifizierungsanforderung vom Server mit derselben IP-Adresse, die Sie in **authconfig.csv**hinzugefügt haben.

   Für diese Demonstration verwende ich das [X-Ray-Tool AD FS Help Claims](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) , um eine Anforderung zu initiieren. Wenn Sie das X-Ray-Tool verwenden möchten, befolgen Sie die Anweisungen.

   Schaltfläche "Verbund Serverinstanz und Treffer **Test Authentifizierung** " eingeben.</br>
   ![model](media/ad-fs-risk-assessment-model/risk15.png)

5. Die Authentifizierung wird wie unten dargestellt blockiert.</br>
   ![model](media/ad-fs-risk-assessment-model/risk16.png)

Nachdem Sie nun wissen, wie das Plug-in erstellt und registriert wird, können Sie den Plug-in-Code durchlaufen, um die Implementierung mithilfe der neuen Schnittstellen und Klassen zu verstehen, die mit dem Modell eingeführt wurden.

## <a name="plug-in-code-walkthrough"></a>Exemplarische Vorgehensweise zum Plug-in-Code

Öffnen Sie das Projekt `ThreatDetectionModule.sln` mit Visual Studio, und öffnen Sie dann die Hauptdatei **UserRiskAnalyzer.cs** im Projektmappen- **Explorer** auf der rechten Seite des Bildschirms.</br>
![model](media/ad-fs-risk-assessment-model/risk17.png)

Die Datei enthält die Hauptklasse "userriskanalyzer", die die abstrakte Klasse " [" und die](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019) Schnittstelle " [irequestreceived-detectionmodule](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019) " implementiert, um die IP-Adresse aus dem Anforderungs Kontext zu lesen, die abgerufene IP-Adresse mit den von AD FS DB geladenen IPS zu vergleichen und die Anforderung zu blockieren, wenn eine IP-Adresse vorliegt Diese Typen werden ausführlicher erläutert.

### <a name="threatdetectionmodule-abstract-class"></a>Abstrakte Klasse von "ererkenctionmodule"

Diese abstrakte Klasse lädt das Plug-in in AD FS Pipeline, sodass der Plug-in-Code in der AD FS Prozess ausgeführt werden kann.

```
public abstract class ThreatDetectionModule
{
    protected ThreatDetectionModule();

    public abstract string VendorName { get; }
    public abstract string ModuleIdentifier { get; }

 public abstract void OnAuthenticationPipelineLoad(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData);
 public abstract void OnAuthenticationPipelineUnload(ThreatDetectionLogger logger);
  public abstract void OnConfigurationUpdate(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData);
 }
```
Die-Klasse enthält die folgenden Methoden und Eigenschaften.

|Methode |type|Definition|
|-----|-----|-----|
|[Onauthenticationpipelineload](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) |Void|Wird von AD FS aufgerufen, wenn das Plug-in in seine Pipeline geladen wird.|
|[Onauthenticationpipelineentladen](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineunload?view=adfs-2019) |Void|Wird von AD FS aufgerufen, wenn das Plug-in aus seiner Pipeline entladen wird.|
|[Onconfigurationupdate](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)| Void|Wird von AD FS auf Konfigurationsupdate aufgerufen |
|**Property** |**Type** |**Definition**|
|[VendorName](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.vendorname?view=adfs-2019)|String |Ruft den Namen des Anbieters ab, der das Plug-in besitzt.|
|[Moduleidentifier](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.moduleidentifier?view=adfs-2019)|String |Ruft den Bezeichner des Plug-ins ab.|

In unserem Beispiel-Plug-in verwenden wir die Methoden [onauthenticationpipelineload](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) und [onconfigurationupdate](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) , um die vordefinierten IPS aus AD FS DB zu lesen. [Onauthenticationpipelineload](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) wird aufgerufen, wenn das Plug-in mit AD FS registriert wird, während [onconfigurationupdate](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) aufgerufen wird, wenn die CSV-Datei mithilfe des `Import-AdfsThreatDetectionModuleConfiguration` Cmdlets importiert wird.

#### <a name="irequestreceivedthreatdetectionmodule-interface"></a>Irequestreceivedseerkenctionmodule-Schnittstelle

Diese [Schnittstelle](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019) ermöglicht Ihnen das Implementieren der Risikobewertung an dem Punkt, an dem AD FS die Authentifizierungsanforderung empfängt, aber bevor der Benutzer Anmelde Informationen eingibt, d. h. die Phase der empfangenen Anforderung des Authentifizierungs Vorgangs.

```
public interface IRequestReceivedThreatDetectionModule
{
Task<ThrottleStatus> EvaluateRequest (
ThreatDetectionLogger logger,
RequestContext requestContext );
}
```

Die-Schnittstelle enthält die [evaluaterequest](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019) -Methode, die es Ihnen ermöglicht, den Kontext der Authentifizierungsanforderung zu verwenden, die im RequestContext-Eingabeparameter übergeben wird, um Ihre Risiko Bewertungs Logik zu schreiben. Der RequestContext-Parameter ist vom Typ " [RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)".

Der andere übergebene Eingabeparameter ist "Logger", [d. h](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019) Der-Parameter kann verwendet werden, um die Fehler-, Überwachungs-und/oder Debugmeldungen in AD FS Protokolle zu schreiben.

Die-Methode gibt [throttlestatus](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) zurück (0, wenn notevaluated, 1 bis Block und 2), um zu AD FS, wodurch die Anforderung entweder blockiert oder zugelassen wird.

In unserem Beispiel-Plug-in analysiert die [evaluaterequest](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019) -Methoden Implementierung die [clientipaddress](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext.clientipaddresses?view=adfs-2019#Microsoft_IdentityServer_Public_ThreatDetectionFramework_RequestContext_ClientIpAddresses) aus dem [RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019) -Parameter und vergleicht sie mit allen IPS, die aus der AD FS DB geladen werden. Wenn eine Entsprechung gefunden wird, gibt die Methode 2 für **Block**zurück, andernfalls wird 1 für **Allow**zurückgegeben. Basierend auf dem zurückgegebenen Wert AD FS entweder blockiert oder lässt die Anforderung zu.

>[!NOTE]
>Das oben beschriebene Beispiel-Plug-in implementiert nur die irequestreceived-detectionmodule-Schnittstelle. Das Risiko Bewertungsmodell bietet jedoch zwei zusätzliche Schnittstellen – ipreauthenticationerdetectionmodule (zur Implementierung der Risikobewertung vor der Authentifizierungs Phase) und ipostauthenticationgefährdetectionmodule (zur Implementierung der Risiko Bewertungs Logik während der nach der Authentifizierung). Die Details zu den beiden Schnittstellen werden unten bereitgestellt.

#### <a name="ipreauthenticationthreatdetectionmodule-interface"></a>Ipreauthentication-detectionmodule-Schnittstelle

Diese [Schnittstelle](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule?view=adfs-2019) ermöglicht Ihnen die Implementierung von Risiko Bewertungs Logik an dem Punkt, an dem der Benutzer die Anmelde Informationen bereitstellt, aber bevor AD FS Sie auswertet, z.b. vor der Authentifizierung.

```
public interface IPreAuthenticationThreatDetectionModule
{
Task<ThrottleStatus> EvaluatePreAuthentication (
ThreatDetectionLogger logger,
RequestContext requestContext,
SecurityContext securityContext,
ProtocolContext protocolContext,
IList<Claim> additionalClams
);
}
```
Die-Schnittstelle enthält die [evaluatepreauthentication](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule.evaluatepreauthentication?view=adfs-2019) -Methode, mit der Sie die in den Eingabe Parametern [RequestContext requestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext SecurityContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), [protocolcontext protocolcontext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)und [IList <Claim> additionalclams](/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) übergebenen Informationen verwenden können, um die Logik zur Risikobewertung vor der Authentifizierung zu schreiben.

>[!NOTE]
>Eine Liste der Eigenschaften, die mit den einzelnen Kontext Typen übermittelt werden, finden Sie unter [RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)und [protocolcontext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019) -Klassendefinitionen.

Der andere übergebene Eingabeparameter ist "Logger", [d. h](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019) Der-Parameter kann verwendet werden, um die Fehler-, Überwachungs-und/oder Debugmeldungen in AD FS Protokolle zu schreiben.

Die-Methode gibt [throttlestatus](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) zurück (0, wenn notevaluated, 1 bis Block und 2), um zu AD FS, wodurch die Anforderung entweder blockiert oder zugelassen wird.

#### <a name="ipostauthenticationthreatdetectionmodule-interface"></a>Ipostauthentication-detectionmodule-Schnittstelle

Diese [Schnittstelle](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule?view=adfs-2019) ermöglicht es Ihnen, die Risiko Bewertungs Logik zu implementieren, nachdem der Benutzer Anmelde Informationen bereitgestellt hat und AD FS eine Authentifizierung durchgeführt hat, z.

```
public interface IPostAuthenticationThreatDetectionModule
{
Task<RiskScore> EvaluatePostAuthentication (
ThreatDetectionLogger logger,
RequestContext requestContext,
SecurityContext securityContext,
ProtocolContext protocolContext,
AuthenticationResult authenticationResult,
IList<Claim> additionalClams
);
}
```

Die-Schnittstelle enthält die [evaluatepostauthentication](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule.evaluatepostauthentication?view=adfs-2019) -Methode, mit der Sie die in den Eingabe Parametern [RequestContext requestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext SecurityContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), [protocolcontext protocolcontext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)und [IList <Claim> additionalclams](/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) übergebenen Informationen verwenden können, um die Logik zur Risikobewertung nach der Authentifizierung zu schreiben.

>[!NOTE]
> Eine umfassende Liste der Eigenschaften, die mit jedem Kontexttyp übergebenen werden, finden Sie unter [RequestContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)und [protocolcontext](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019) -Klassendefinitionen.

Der andere übergebene Eingabeparameter ist "Logger", [d. h](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019) Der-Parameter kann verwendet werden, um die Fehler-, Überwachungs-und/oder Debugmeldungen in AD FS Protokolle zu schreiben.

Die-Methode gibt die [Risikobewertung](/dotnet/api/microsoft.identityserver.authentication.riskscoreconstants?view=adfs-2019) zurück, die in AD FS Richtlinie und Anspruchs Regeln verwendet werden kann.

>[!NOTE]
>Damit das Plug-in funktioniert, muss die Hauptklasse (in diesem Fall userriskanalyzer) [die abstrakte Klasse](/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019) "-Klasse" von "" und "" mindestens eine der drei oben beschriebenen Schnittstellen implementieren. Nachdem die dll registriert wurde, überprüft AD FS, welche der Schnittstellen implementiert sind, und ruft Sie in der entsprechenden Phase in der Pipeline auf.

### <a name="faqs"></a>Häufig gestellte Fragen

**Warum sollten diese Plug-Ins erstellt werden?**</br>
**A:** Diese Plug-ins bieten Ihnen nicht nur zusätzliche Funktionen, um Ihre Umgebung vor Angriffen wie Kenn Wort Spritzen Angriffen zu schützen. Sie bieten Ihnen außerdem die Flexibilität, eine eigene Risiko Bewertungs Logik basierend auf Ihren Anforderungen zu erstellen.

**Wo werden die Protokolle aufgezeichnet?**</br>
**A:** Sie können Fehlerprotokolle mithilfe der Methode "Write-adminlogerrormessage" in das Ereignisprotokoll "AD FS/admin" schreiben, mithilfe der Methode "Write-AuditMessage" Überwachungs Protokolle in "AD FS Auditing" und mithilfe der Methode "Write-debugmessage" in das Debugprotokoll "AD FS Ablauf Verfolgung" schreiben.

**Können diese Plug-ins durch Hinzufügen AD FS Authentifizierungsprozess Latenz erhöht werden?**</br>
**A:** Die Latenzzeit wird durch die Zeit bestimmt, die zum Ausführen der von Ihnen implementierten Logik zur Risikobewertung benötigt wird. Es wird empfohlen, die Latenzzeiten zu bewerten, bevor Sie das Plug-in in der Produktionsumgebung bereitstellen.

**Warum kann AD FS die Liste der riskanten IPS, Benutzer usw. nicht vorschlagen?**</br>
**A:** Obwohl es zurzeit nicht verfügbar ist, arbeiten wir an der Bildung von Informationen, um riskante IPS, Benutzer usw. im austauschbaren Risiko Bewertungsmodell vorzuschlagen. Wir werden die Startdaten bald freigeben.

**Welche anderen Plug-in-Beispiele sind verfügbar?**</br>
**A:** Die folgenden Beispiel-Plug-ins sind verfügbar:

|Name|BESCHREIBUNG|
|-----|-----|
|[Riskantes Benutzer-Plug-in](https://github.com/microsoft/adfs-sample-block-user-on-adfs-marked-risky-by-AzureAD-IdentityProtection)|Beispiel-Plug-in, das die Authentifizierung blockiert oder die MFA auf Grundlage der durch Azure AD Identity Protection festgelegten Benutzer Risikostufe erzwingt.|
