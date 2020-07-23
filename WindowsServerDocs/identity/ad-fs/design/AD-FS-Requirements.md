---
ms.assetid: 8ce6e7c4-cf8e-4b55-980c-048fea28d50f
title: Verbundserverfarm mit SQL Server
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 93f99ef40897007dbe73a3309459b543700b244a
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961942"
---
# <a name="ad-fs-requirements"></a>AD FS-Anforderungen

Im folgenden sind die verschiedenen Anforderungen aufgeführt, die Sie bei der Bereitstellung von AD FS einhalten müssen:  
  
-   [Zertifikatanforderungen](AD-FS-Requirements.md#BKMK_1)  
  
-   [Hardwareanforderungen](AD-FS-Requirements.md#BKMK_2)  
  
-   [Softwareanforderungen](AD-FS-Requirements.md#BKMK_3)  
  
-   [AD DS-Anforderungen](AD-FS-Requirements.md#BKMK_4)  
  
-   [Anforderungen an die Konfigurationsdatenbank](AD-FS-Requirements.md#BKMK_5)  
  
-   [Browseranforderungen](AD-FS-Requirements.md#BKMK_6)  
  
-   [Extranetanforderungen](AD-FS-Requirements.md#BKMK_extranet)  
  
-   [Netzwerkanforderungen](AD-FS-Requirements.md#BKMK_7)  
  
-   [Anforderungen an den Attributspeicher](AD-FS-Requirements.md#BKMK_8)  
  
-   [Anwendungsanforderungen](AD-FS-Requirements.md#BKMK_9)  
  
-   [Authentifizierungsanforderungen](AD-FS-Requirements.md#BKMK_10)  
  
-   [Anforderungen an den Workplace Join](AD-FS-Requirements.md#BKMK_11)  
  
-   [Kryptografieanforderungen](AD-FS-Requirements.md#BKMK_12)  
  
-   [Berechtigungsanforderungen](AD-FS-Requirements.md#BKMK_13)  
  
## <a name="certificate-requirements"></a><a name="BKMK_1"></a>Zertifikatanforderungen  
Zertifikate spielen die wichtigste Rolle beim Sichern der Kommunikation zwischen Verbund Servern, webanwendungsproxys, Ansprüche unterstützenden \- Anwendungen und Webclients. Die Anforderungen für Zertifikate variieren abhängig davon, ob Sie einen Verbund Server oder einen Proxy Computer einrichten, wie in diesem Abschnitt beschrieben.  
  
**Verbundserverzertifikate**  
  
|||  
|-|-|  
|**Zertifikattyp**|**Anforderungen, Unterstützung & Dinge, die Sie kennen müssen**|  
|**Secure Sockets Layer \( SSL- \) Zertifikat:** hierbei handelt es sich um ein Standardmäßiges SSL-Zertifikat, das zum Sichern der Kommunikation zwischen Verbund Servern und Clients verwendet wird.|: Bei diesem Zertifikat muss es sich um ein öffentlich vertrauenswürdiges \* X509 v3-Zertifikat handeln.<br />-Alle Clients, die auf einen AD FS Endpunkt zugreifen, müssen diesem Zertifikat vertrauen. Es wird dringend empfohlen, Zertifikate zu verwenden, die von einer Zertifizierungsstellen-Zertifizierungsstelle eines öffentlichen Drittanbieters ausgestellt werden \( \- \) \( \) . Sie können ein selbst \- signiertes SSL-Zertifikat erfolgreich auf Verbund Servern in einer Testumgebung verwenden. Bei einer Produktionsumgebung wird jedoch empfohlen, dass Sie das Zertifikat von einer öffentlichen Zertifizierungsstelle beziehen.<br />: Unterstützt alle Schlüsselgrößen, die von Windows Server 2012 R2 für SSL-Zertifikate unterstützt werden.<br />: Unterstützt keine Zertifikate, die CNG-Schlüssel verwenden.<br />-Bei Verwendung mit Workplace Join \/ Geräte Registrierungsdienst muss der alternative Antragsteller Name des SSL-Zertifikats für den AD FS Dienst den Wert enterpriseregistration enthalten, auf den das Benutzer Prinzipal Namen- \( UPN- \) Suffix Ihrer Organisation folgt, z. b. enterpriseregistration.contoso.com.<br />-Platzhalter Zertifikate werden unterstützt. Wenn Sie die AD FS-Farm erstellen, werden Sie aufgefordert, den Dienstnamen für den AD FS Dienst anzugeben \( , z. b. **ADFS.contoso.com**.<br />-Es wird dringend empfohlen, das gleiche SSL-Zertifikat für den webanwendungsproxy zu verwenden. Dies **muss jedoch bei** der Unterstützung der integrierten Windows-Authentifizierungs Endpunkte über den webanwendungsproxy identisch sein, und wenn die erweiterte Schutz Authentifizierung für die \( Standardeinstellung aktiviert ist \) .<br />-Der Antragsteller Name dieses Zertifikats wird verwendet, um den Verbunddienst Namen für jede Instanz von AD FS darzustellen, die Sie bereitstellen. Aus diesem Grund sollten Sie einen Antragsteller Namen für alle neuen von \- der Zertifizierungsstelle ausgestellten Zertifikate auswählen, die den Namen Ihres Unternehmens oder Ihrer Organisation für Partner am besten darstellen.<br />    Die Identität des Zertifikats muss mit dem Verbund Dienstnamen \( , z. b. fs.contoso.com, identisch sein \) . Die Identität ist entweder eine Alternative Alternative Namenserweiterung des Typs DnsName. wenn keine alternativen Antragsteller Namen Einträge vorhanden sind, wird der Antragsteller Name als allgemeiner Name angegeben. Im Zertifikat können mehrere alternative Antragsteller Namen Einträge vorhanden sein, vorausgesetzt, dass eine von Ihnen mit dem Verbund Dienstnamen übereinstimmt.<br />-   **Wichtig:** es wird dringend empfohlen, das gleiche SSL-Zertifikat für alle Knoten Ihrer AD FS Farm sowie für alle webanwendungsproxys in Ihrer AD FS-Farm zu verwenden.|  
|**Dienst Kommunikations Zertifikat:** Mit diesem Zertifikat wird die WCF-Nachrichten Sicherheit zum Sichern der Kommunikation zwischen Verbund Servern aktiviert.|Standardmäßig wird das SSL-Zertifikat als Dienst Kommunikations Zertifikat verwendet.  Sie haben jedoch auch die Möglichkeit, ein anderes Zertifikat als Dienst Kommunikations Zertifikat zu konfigurieren.<br />-   **Wichtig:** Wenn Sie das SSL-Zertifikat als Dienst Kommunikations Zertifikat verwenden und das SSL-Zertifikat abläuft, stellen Sie sicher, dass Sie das erneuerte SSL-Zertifikat als Dienst Kommunikations Zertifikat konfigurieren. Dies geschieht nicht automatisch.<br />-Dieses Zertifikat muss von Clients von AD FS vertraut werden, die WCF-Nachrichten Sicherheit verwenden.<br />-Wir empfehlen die Verwendung eines Server Authentifizierungs Zertifikats, das von einer öffentlichen Zertifizierungsstellen-Zertifizierungsstelle ausgestellt wurde \( \- \) \( \) .<br />-Das Dienst Kommunikations Zertifikat darf kein Zertifikat sein, das CNG-Schlüssel verwendet.<br />-Dieses Zertifikat kann mithilfe der AD FS Management Console verwaltet werden.|  
|** \- Tokensignaturzertifikat:** Dies ist ein Standard-X509-Zertifikat, das zum sicheren Signieren aller Token verwendet wird, die der Verbund Server ausgibt.|-AD FS erstellt standardmäßig ein selbst \- signiertes Zertifikat mit 2048-Bit-Schlüsseln.<br />-Zertifikate, die von der Zertifizierungsstelle ausgestellt wurden, werden ebenfalls unterstützt und können mithilfe des Snap-Ins "AD FS \-<br />-Zertifizierungsstellen Zertifikate müssen gespeichert werden, & über einen CSP-Kryptografieanbieter zugegriffen wird.<br />-Das Tokensignaturzertifikat darf kein Zertifikat sein, das CNG-Schlüssel verwendet.<br />-AD FS für die Tokensignierung extern registrierte Zertifikate nicht benötigt.<br />    AD FS diese selbst \- signierten Zertifikate vor dem Ablauf automatisch erneuern, konfigurieren Sie zunächst die neuen Zertifikate als sekundäre Zertifikate, damit Sie von Partnern genutzt werden können, und kippen Sie dann in einem Prozess, der als automatisches zertifikatrol Lover bezeichnet wird, in das primäre Objekt. Es wird empfohlen, die automatisch generierten Standardzertifikate für die Tokensignierung zu verwenden.<br />    Wenn in Ihrer Organisation Richtlinien vorhanden sind, für die unterschiedliche Zertifikate für die Tokensignierung konfiguriert werden müssen, können Sie die Zertifikate zur Installationszeit mithilfe von PowerShell angeben, indem Sie \( den Parameter – signingcertifigatethrebprint des \- Cmdlets install adfsfarm verwenden \) .  Nach der Installation können Sie Tokensignaturzertifikate mithilfe der AD FS Management Console oder mithilfe der PowerShell-Cmdlets " \- adfscertificate" und "get \- adfscertificate" anzeigen und verwalten.<br />    Wenn Extern registrierte Zertifikate für die Tokensignierung verwendet werden, führt AD FS keine automatische Zertifikat Erneuerung oder einen Rollover durch.  Dieser Prozess muss von einem Administrator ausgeführt werden.<br />    Um einen zertifikatrol Lover zuzulassen, wenn ein Zertifikat fast abgelaufen ist, kann in AD FS ein sekundäres Tokensignaturzertifikat konfiguriert werden. Standardmäßig werden alle Tokensignaturzertifikate in Verbund Metadaten veröffentlicht, aber nur das primäre \- Tokensignaturzertifikat wird von AD FS verwendet, um Token tatsächlich zu signieren.|  
|** \- \/ Verschlüsselungs Zertifikat für die tokenentschlüsselung:** hierbei handelt es sich um ein Standard-X509-Zertifikat, das verwendet wird, um die \/ Verschlüsselung eingehender Token zu entschlüsseln. Es wird außerdem in den Verbundmetadaten veröffentlicht.|-AD FS erstellt standardmäßig ein selbst \- signiertes Zertifikat mit 2048-Bit-Schlüsseln.<br />-Zertifikate, die von der Zertifizierungsstelle ausgestellt wurden, werden ebenfalls unterstützt und können mithilfe des Snap-Ins "AD FS \-<br />-Zertifizierungsstellen Zertifikate müssen gespeichert werden, & über einen CSP-Kryptografieanbieter zugegriffen wird.<br />-Das \- Verschlüsselungs Zertifikat für die tokenentschlüsselung \/ darf kein Zertifikat sein, das CNG-Schlüssel verwendet.<br />Standardmäßig generiert AD FS eigene, intern generierte und selbst \- signierte Zertifikate für die tokenentschlüsselung und verwendet diese.  Für diesen Zweck werden AD FS nicht extern registrierte Zertifikate benötigt.<br />    Außerdem erneuert AD FS diese selbst \- signierten Zertifikate automatisch, bevor Sie ablaufen.<br />    **Es wird empfohlen, die automatisch generierten Standardzertifikate für die tokenentschlüsselung zu verwenden.**<br />    Wenn in Ihrer Organisation Richtlinien vorhanden sind, für die verschiedene Zertifikate für die tokenentschlüsselung konfiguriert werden müssen, können Sie die Zertifikate zur Installationszeit mithilfe von PowerShell angeben, indem Sie \( den Parameter – decryptioncertifigatethrebprint des \- Cmdlets install adfsfarm verwenden \) .  Nach der Installation können Sie tokenentschlüsselungszertifikate mithilfe der AD FS Management Console oder PowerShell-Cmdlets für " \- adfscertificate" und "get \- adfscertificate" anzeigen und verwalten.<br />    **Wenn Extern registrierte Zertifikate für die tokenentschlüsselung verwendet werden, führt AD FS keine automatische Zertifikat Erneuerung aus.  Dieser Prozess muss von einem Administrator ausgeführt werden**.<br />-Das AD FS-Dienst Konto muss auf den \- privaten Schlüssel des Tokensignaturzertifikats im persönlichen Speicher des lokalen Computers zugreifen können. Dies wird vom-Setup erledigt. Sie können das Snap-in AD FS Verwaltung auch verwenden \- , um diesen Zugriff zu gewährleisten, wenn Sie anschließend das \- Tokensignaturzertifikat ändern.|  
  
> [!CAUTION]  
> Zertifikate, die für die Tokensignatur und die Tokenentschlüsselung bzw. -verschlüsselung verwendet werden, sind wichtig für die Stabilität des Verbunddiensts. Kunden, die ihre eigenen Zertifikate für Tokensignatur und Tokenentschlüsselung bzw. -verschlüsselung verwalten, sollten sicherstellen, dass diese Zertifikate gesichert werden und während eines Wiederherstellungsereignisses unabhängig voneinander verfügbar sind.  
  
> [!NOTE]  
> In AD FS Sie die SHA-Ebene des Secure-Hash-Algorithmus \( \) , die für digitale Signaturen verwendet wird, entweder in Sha \- 1 oder SHA 256 sicherer ändern \- \( \) . AD FS unterstützt die Verwendung von Zertifikaten mit anderen Hash Methoden, wie z. b. MD5, \( dem Standard Hash Algorithmus, der mit dem Makecert.exe Befehls \- Zeilen Tool verwendet wird \) . Als bewährte Sicherheitsmaßnahme empfiehlt es sich, SHA \- 256 zu verwenden, \( das standardmäßig \) für alle Signaturen festgelegt wird. SHA \- 1 wird nur in Szenarien empfohlen, in denen Sie mit einem Produkt interoperieren müssen, das keine Kommunikation über SHA 256 unterstützt \- , wie z. b. ein nicht- \- Microsoft-Produkt oder Legacy Versionen von AD FS.  
  
> [!NOTE]  
> Nachdem Sie ein Zertifikat von einer Zertifizierungsstelle erhalten haben, stellen Sie sicher, dass alle Zertifikate in den persönlichen Zertifikatspeicher auf dem lokalen Computer importiert werden. Zertifikate können mit dem MMC-Snap-in "Zertifikate" in den persönlichen Speicher importiert werden \- .  
  
## <a name="hardware-requirements"></a><a name="BKMK_2"></a>Hardwareanforderungen  
Die folgenden Mindestanforderungen und empfohlenen Hardwareanforderungen gelten für die AD FS Verbund Server in Windows Server 2012 R2:  
  
||||  
|-|-|-|  
|**Hardwareanforderung**|**Mindestanforderung**|**Empfohlene Anforderung**|  
|CPU-Geschwindigkeit|1,4 GHz 64- \- Bit-Prozessor|\-Vierkern, 2 GHz|  
|RAM|512 MB|4 GB|  
|Speicherplatz|32 GB|100 GB|  
  
## <a name="software-requirements"></a><a name="BKMK_3"></a>Softwareanforderungen  
Die folgenden AD FS Anforderungen gelten für die Serverfunktionen, die in das &reg; Betriebssystem Windows Server 2012 R2 integriert sind:  
  
-   Für den Extranetzugriff müssen Sie den webanwendungsproxy-Rollen Dienst \- Teil der Windows Server &reg; 2012 R2-Remote Zugriffs-Server Rolle bereitstellen. Frühere Versionen eines Verbund Server Proxys werden bei AD FS in Windows Server 2012 R2 nicht unterstützt &reg; .  
  
-   Ein Verbundserver und der Webanwendungsproxy-Rollendienst können nicht auf demselben Computer installiert werden.  
  
## <a name="ad-ds-requirements"></a><a name="BKMK_4"></a>AD DS-Anforderungen  
**Anforderungen an den Domänencontroller**  
  
Auf Domänen Controllern in allen Benutzer Domänen und in der Domäne, der die AD FS Server beitreten, muss Windows Server 2008 oder höher ausgeführt werden.  
  
> [!NOTE]  
> Die Unterstützung für Umgebungen mit Windows Server 2003-Domänen Controllern endet nach dem Enddatum des erweiterten Supports für Windows Server 2003. Kunden wird dringend empfohlen, die Domänen Controller so bald wie möglich zu aktualisieren. Besuchen Sie [Diese Seite](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) , um weitere Informationen zu Microsoft-Support Lebenszyklus zu erhalten. Für Probleme, die für Windows Server 2003-Domänen Controller Umgebungen spezifisch sind, werden Korrekturen nur für Sicherheitsprobleme ausgegeben, und wenn vor dem Ablauf des erweiterten Supports für Windows Server 2003 eine Korrektur ausgegeben werden kann.  



>[!NOTE]
> AD FS erfordert, dass ein voll Schreib geschützter Domänen Controller im Gegensatz zu einem schreibgeschützten Domänen Controller funktioniert. Wenn eine geplante Topologie einen schreibgeschützten Domänen Controller enthält, kann der schreibgeschützte Domänen Controller für die Authentifizierung verwendet werden, die LDAP-Anspruchs Verarbeitung erfordert jedoch eine Verbindung mit dem beschreibbaren Domänen Controller.
  
**Anforderungen auf Domänenfunktionsebene**  
  
Alle Benutzerkontodomänen und die Domäne, mit der die AD FS-Server verbunden sind, müssen auf der Domänenfunktionsebene von Windows Server 2003 oder höher betrieben werden.  
  
Die meisten AD FS Features erfordern nicht, dass AD DS \- funktionsebenenänderungen erfolgreich ausgeführt werden. Allerdings ist die Windows Server 2008-Domänenfunktionsebene oder höher erforderlich, damit die Clientzertifikatauthentifizierung erfolgreich betrieben werden kann, wenn das Zertifikat explizit einem Benutzerkonto in AD DS zugeordnet ist.  
  
**Schemaanforderungen**  
  
-   AD FS erfordert keine Schema Änderungen oder \- Änderungen an der Funktionsebene an AD DS.  
  
-   Um Workplace Join Funktionalität verwenden zu können, muss das Schema der Gesamtstruktur, mit der AD FS Server verknüpft werden, auf Windows Server 2012 R2 festgelegt werden.  
  
**Dienstkontenanforderungen**  
  
-   Jedes Standard Dienst Konto kann als Dienst Konto für AD FS verwendet werden. Über Gruppen verwaltete Dienstkonten werden ebenfalls unterstützt. Hierfür ist mindestens ein Domänen Controller erforderlich \( . es wird empfohlen, mindestens zwei Domänen Controller bereitzustellen \) , auf denen Windows Server 2012 oder höher ausgeführt wird.  
  
-   Damit die Kerberos-Authentifizierung zwischen in \- die Domäne eingefügten Clients und AD FS funktioniert, muss der "Host \/<ADFS- \_ Dienst \_ Name>" als SPN für das Dienst Konto registriert werden. Standardmäßig konfiguriert AD FS diese, wenn Sie eine neue AD FS Farm erstellt, wenn Sie über ausreichende Berechtigungen zum Ausführen dieses Vorgangs verfügt.  
  
-   Das AD FS-Dienst Konto muss in jeder Benutzer Domäne vertrauenswürdig sein, die Benutzer enthält, die sich für den AD FS-Dienst authentifizieren.  
  
**Domänenanforderungen**  
  
-   Alle AD FS-Server müssen einer AD DS-Domäne beigetreten sein.  
  
-   Alle AD FS Server innerhalb einer Farm müssen in einer einzelnen Domäne bereitgestellt werden.  
  
-   Die Domäne, der die AD FS Server beitreten, muss jeder Benutzerkonto Domäne vertrauen, die Benutzer enthält, die sich für den AD FS-Dienst authentifizieren.  
  
**Anforderungen für mehrere Gesamtstrukturen**  
  
-   Die Domäne, der die AD FS Server angehören, muss jeder Benutzerkonto Domäne oder-Gesamtstruktur vertrauen, die Benutzer enthält, die sich für den AD FS-Dienst authentifizieren.  
  
-   Das AD FS-Dienst Konto muss in jeder Benutzer Domäne vertrauenswürdig sein, die Benutzer enthält, die sich für den AD FS-Dienst authentifizieren.  
  
## <a name="configuration-database-requirements"></a><a name="BKMK_5"></a>Anforderungen an die Konfigurationsdatenbank  
Nachfolgend sind die Anforderungen und Einschränkungen aufgeführt, die basierend auf dem Typ des Konfigurations Speicher zutreffen:  
  
**WID**  
  
-   Eine wid-Farm hat ein Limit von 30 Verbund Servern, wenn Sie über 100 oder weniger Vertrauens Stellungen der vertrauenden Seite verfügen.  
  
-   Das artefaktauflösungs Profil in SAML 2,0 wird in der wid-Konfigurations Datenbank nicht unterstützt.  Die Erkennung von tokenwiedergabe wird in der wid-Konfigurations Datenbank nicht unterstützt. Diese Funktion wird nur in Szenarien verwendet, in denen AD FS als Verbund Anbieter fungiert und Sicherheits Token von externen Anspruchs Anbietern beansprucht.  
  
-   Das Bereitstellen von AD FS Servern in unterschiedlichen Rechenzentren für Failover oder geografischer Lastenausgleich wird unterstützt, solange die Anzahl der Server 30 nicht überschreitet.  
  
In der folgenden Tabelle finden Sie eine Zusammenfassung zur Verwendung einer wid-Farm.  Verwenden Sie es, um Ihre Implementierung zu planen.  
  
||||  
|-|-|-|  
||1 \- 100 RP-Vertrauens Stellungen|Mehr als 100 RP-Vertrauens Stellungen|  
|1 \- 30 AD FS Knoten|Von WID unterstützt|Nicht unterstützt, wenn wid \- SQL erforderlich ist|  
|Mehr als 30 AD FS Knoten|Nicht unterstützt, wenn wid \- SQL erforderlich ist|Nicht unterstützt, wenn wid \- SQL erforderlich ist|  
  
**SQL Server**  
  
Für AD FS in Windows Server 2012 R2 können Sie SQL Server 2008 und höher verwenden.  
  
## <a name="browser-requirements"></a><a name="BKMK_6"></a>Browseranforderungen  
Wenn die AD FS-Authentifizierung über einen Browser oder ein Browsersteuerelement durchgeführt wird, muss der Browser die folgenden Anforderungen erfüllen:  
  
-   JavaScript muss aktiviert sein  
  
-   Cookies müssen eingeschaltet werden.  
  
-   Die Servernamensanzeige \(Server Name Indicator, SNI\) muss unterstützt werden  
  
-   \( \) Der Browser muss die SSL-Client Zertifikat Authentifizierung unterstützen, um die Funktion für die Arbeitsbereichverknüpfung von Benutzer Zertifikaten &  
  
Mehrere Schlüssel Browser und-Plattformen wurden für das Rendering und die Funktionalität überprüft, die unten aufgeführten Details aufgeführt sind. Browser und Geräte, die nicht in dieser Tabelle behandelt werden, werden weiterhin unterstützt, wenn Sie die oben aufgeführten Anforderungen erfüllen:  
  
|||  
|-|-|  
|**Browser**|**Plattformen**|  
|IE 10,0|Windows 7, Windows 8.1, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2|  
|IE 11,0|Windows7, Windows 8.1, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2|  
|Windows-Webauthentifizierungs Broker|Windows 8.1|  
|Firefox \[ V21\]|Windows 7, Windows 8.1|  
|Safari \[ V7\]|IOS 6, Mac OS \- X 10,7|  
|Chrome- \[ V27\]|Windows 7, Windows 8.1, Windows Server 2012, Windows Server 2012 R2, Mac OS \- X 10,7|  
  
> [!IMPORTANT]  
> Bekanntes Problem \- Firefox: Workplace Join Funktionen, die das Gerät mithilfe des Geräte Zertifikats identifizieren, sind auf Windows-Plattformen nicht funktionsfähig. Firefox unterstützt derzeit keine SSL-Client Zertifikat Authentifizierung mithilfe von Zertifikaten, die im Zertifikat Speicher des Benutzers auf Windows-Clients bereitgestellt werden.  
  
**Cookies**  
  
AD FS erstellt Sitzungs \- basierte und persistente Cookies, die auf Client Computern gespeichert werden müssen, um Anmeldung \- , \- Abmeldung, einmaliges Anmelden ( \- \( SSO) \) und andere Funktionen bereitzustellen. Daher muss der Clientbrowser so konfiguriert sein, dass Cookies akzeptiert werden. Cookies, die für die Authentifizierung verwendet werden, sind immer Secure Hypertext Transfer Protocol \( https- \) Sitzungs Cookies, die für den Ursprungsserver geschrieben werden. Wenn die Konfiguration des Clientbrowsers diese Cookies nicht zulässt, kann AD FS nicht ordnungsgemäß funktionieren. Beständige Cookies werden verwendet, um die Benutzerauswahl des Anspruchsanbieters beizubehalten. Sie können Sie mithilfe einer Konfigurationseinstellung in der Konfigurationsdatei für die AD FS Anmelde Seiten deaktivieren \- . Aus Sicherheitsgründen ist eine Unterstützung für TLS- \/ SSL erforderlich.  
  
## <a name="extranet-requirements"></a><a name="BKMK_extranet"></a>Extranetanforderungen  
Um Extranetzugriff auf den AD FS-Dienst bereitzustellen, müssen Sie den webanwendungsproxy-Rollen Dienst als Extranet-Rolle bereitstellen, die Authentifizierungsanforderungen auf sichere Weise für den AD FS-Dienst proamt. Dies ermöglicht die Isolierung der AD FS Dienst Endpunkte sowie die Isolierung aller Sicherheitsschlüssel \( , wie z. b. Tokensignaturzertifikate \) von Anforderungen, die aus dem Internet stammen. Darüber hinaus erfordern Features wie die vorläufige Konto Sperre für das Extranet die Verwendung des webanwendungsproxys. Weitere Informationen zum webanwendungsproxy finden Sie unter [webanwendungsproxy](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn584107(v=ws.11)).  
  
Wenn Sie einen \- Proxy von Drittanbietern für den Extranetzugriff verwenden möchten, \- muss der Proxy dieses Drittanbieters das in [http: \/ \/ Download.Microsoft.com \/ Download \/ 9 \/ 5 \/ E \/ 95ef05af \- 9026 \- 4bb0 \- A41D \- A4F81802D92C \/ % 5bms \- adfspip% 5d.pdf](https://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/%5bMS-ADFSPIP%5d.pdf)definierte Protokoll unterstützen.  
  
## <a name="network-requirements"></a><a name="BKMK_7"></a>Netzwerkanforderungen  
Die ordnungsgemäß Konfigurierung der folgenden Netzwerkdienste ist wichtig für eine erfolgreiche Bereitstellung von AD FS in Ihrer Organisation:  
  
**Konfigurieren der Unternehmens Firewall**  
  
Sowohl die Firewall zwischen dem Webanwendungsproxy und der Verbundserverfarm als auch die Firewall zwischen den Clients und dem Webanwendungsproxy müssen den TCP-Port 443 für eingehende Daten aktiviert haben.  
  
Wenn außerdem die \( clienttls-Authentifizierung des Client Benutzer Zertifikats mit X509-Benutzer Zertifikaten \) erforderlich ist, erfordert AD FS in Windows Server 2012 R2, dass TCP-Port 49443 in der Firewall zwischen den Clients und dem webanwendungsproxy eingehenden aktiviert ist. Dies ist für die Firewall zwischen dem webanwendungsproxy und den Verbund Servern nicht erforderlich \) .  

> [!NOTE]
> Stellen Sie außerdem sicher, dass Port 49443 nicht von anderen Diensten auf dem AD FS-und webanwendungsproxy-Server verwendet wird.

**Konfigurieren des DNS**  
  
-   Für den Intranetzugriff müssen alle Clients, die auf AD FS Dienst innerhalb des internen Unternehmensnetzwerks zugreifen, \( \) den Namen des AD FS diensnamens \( , der vom SSL-Zertifikat bereitgestellt wird, \) in den Load Balancer für die AD FS Server oder den AD FS Server auflösen können.  
  
-   Für den Extranetzugriff müssen alle Clients, die von außerhalb des Unternehmensnetzwerks \( extranetinternet auf AD FS Dienst zugreifen, \/ den Namen \) des AD FS Diensts, der \( vom SSL-Zertifikat bereitgestellt wird, \) in den Load Balancer für die webanwendungsproxy-Server oder den webanwendungsproxy  
  
-   Damit der Extranetzugriff ordnungsgemäß funktioniert, muss jeder webanwendungsproxy-Server in der DMZ in der Lage sein, AD FS \( vom SSL-Zertifikat bereitgestellte Dienstnamen Name in \) den Load Balancer für die AD FS Server oder den AD FS Server aufzulösen. Dies kann mithilfe eines alternativen DNS-Servers im DMZ-Netzwerk oder durch Ändern der Auflösung des lokalen Servers mithilfe der Hosts-Datei erreicht werden.  
  
-   Damit die integrierte Windows-Authentifizierung innerhalb des Netzwerks und außerhalb des Netzwerks für eine Teilmenge von Endpunkten funktioniert, die über den webanwendungsproxy verfügbar gemacht werden, müssen Sie einen a-Datensatz \( Not CNAME verwenden, \) um auf den Lastenausgleich zu verweisen.  
  
Informationen zum Konfigurieren des Unternehmens-DNS für den Verbund Dienst und den Geräte Registrierungsdienst finden Sie unter [Konfigurieren des Unternehmens-DNS für die Verbunddienst und DRS](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486786(v=ws.11)).  
  
Informationen zum Konfigurieren des Unternehmens-DNS für webanwendungsproxys finden Sie im Abschnitt "Konfigurieren von DNS" in [Schritt 1: Konfigurieren der webanwendungsproxy-Infrastruktur](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383644(v=ws.11))  
  
Informationen zum Konfigurieren einer Cluster-IP-Adresse oder eines Cluster-FQDN mithilfe von NLB finden Sie unter Angeben der Cluster Parameter unter [http: \/ \/ go.Microsoft.com \/ fwlink \/ ? LinkId \= 75282](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
## <a name="attribute-store-requirements"></a><a name="BKMK_8"></a>Anforderungen an den Attributspeicher  
AD FS erfordert mindestens einen Attribut Speicher, der für die Authentifizierung von Benutzern und das Extrahieren von Sicherheitsansprüchen für diese Benutzer verwendet werden muss. Eine Liste der von AD FS unterstützten Attribut Speicher finden Sie unter [der Rolle von Attribut speichern](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
> [!NOTE]  
> AD FS erstellt standardmäßig automatisch einen "Active Directory"-Attribut Speicher. Die Anforderungen an den Attribut Speicher hängen davon ab, ob Ihre Organisation als Konto Partner fungiert, \( der die Verbund Benutzer und den Ressourcen Partner, der als Host für \) \( die Verbund Anwendung fungiert, fungiert \) .  
  
**LDAP-Attribut Speicher**  
  
Wenn Sie mit anderen LDAP-basierten Attribut speichern in Lightweight Directory Access Protocol arbeiten \( \) \- , müssen Sie eine Verbindung mit einem LDAP-Server herstellen, der die integrierte Windows-Authentifizierung unterstützt. Die LDAP-Verbindungszeichenfolge muss außerdem im Format einer LDAP-URL geschrieben sein, wie in RFC 2255 beschrieben.  
  
Außerdem ist es erforderlich, dass das Dienst Konto für den AD FS-Dienst über das Recht zum Abrufen von Benutzerinformationen im LDAP-Attribut Speicher verfügt.  
  
**SQL Server-Attribut Speicher**  
  
Damit AD FS in Windows Server 2012 R2 erfolgreich ausgeführt werden kann, muss auf Computern, auf denen der SQL Server Attribut Speicher gehostet wird, entweder Microsoft SQL Server 2008 oder höher ausgeführt werden. Wenn Sie mit SQL- \- basierten Attribut speichern arbeiten, müssen Sie auch eine Verbindungs Zeichenfolge konfigurieren.  
  
**Benutzerdefinierte Attribut Speicher**  
  
Sie können benutzerdefinierte Attributspeicher entwickeln, um erweiterte Szenarien zu aktivieren.  
  
-   Die in AD FS integrierte Richtiliniensprache kann auf benutzerdefinierte Attributspeicher verweisen, sodass jedes der folgenden Szenarien verbessert werden kann:  
  
    -   Erstellen von Ansprüchen für einen lokal authentifizierten Benutzer  
  
    -   Ergänzen von Ansprüchen für einen lokal authentifizierten Benutzer  
  
    -   Autorisieren eines Benutzers zum Abrufen eines Token  
  
    -   Autorisieren eines Diensts zum Abrufen eines Token zum Verhalten eines Benutzers  
  
    -   Ausgeben zusätzlicher Daten in Sicherheits Token, die von AD FS an vertrauende Seiten ausgegeben werden.  
  
-   Alle benutzerdefinierten Attribut Speicher müssen auf .NET 4,0 oder höher erstellt werden.  
  
Wenn Sie mit einem benutzerdefinierten Attribut Speicher arbeiten, müssen Sie möglicherweise auch eine Verbindungs Zeichenfolge konfigurieren. In diesem Fall können Sie einen benutzerdefinierten Code Ihrer Wahl eingeben, der eine Verbindung mit dem benutzerdefinierten Attribut Speicher ermöglicht. Die Verbindungs Zeichenfolge in dieser Situation ist ein Satz von Name- \/ Wert-Paaren, die vom Entwickler des benutzerdefinierten Attribut Speicher als implementiert interpretiert werden. Weitere Informationen zum entwickeln und Verwenden von benutzerdefinierten Attribut speichern finden Sie unter Übersicht über den [Attribut Speicher](https://go.microsoft.com/fwlink/?LinkId=190782).  
  
## <a name="application-requirements"></a><a name="BKMK_9"></a>Anwendungsanforderungen  
AD FS unterstützt Ansprüche unterstützende \- Anwendungen, die die folgenden Protokolle verwenden:  
  
-   WS \- -Verbund  
  
-   WS- \- Vertrauensstellung  
  
-   SAML 2,0-Protokoll mit idplite, splite & eGov 1.5-Profilen.  
  
-   OAuth 2,0-Autorisierungs Zuweisungs Profil  
  
AD FS unterstützt auch die Authentifizierung und Autorisierung für Anwendungen, die keine Ansprüche unterstützen und \- \- vom webanwendungsproxy unterstützt werden.  
  
## <a name="authentication-requirements"></a><a name="BKMK_10"></a>Authentifizierungsanforderungen  
**Primäre Authentifizierung für AD DS Authentifizierung \(\)**  
  
Für den Intranetzugriff werden die folgenden Standard Authentifizierungsmechanismen für AD DS unterstützt:  
  
-   Integrierte Windows-Authentifizierung unter Verwendung von aushandeln für Kerberos-& NTLM  
  
-   Formular Authentifizierung mit Benutzernamen \/ Kennwörtern  
  
-   Zertifikat Authentifizierung mithilfe von Zertifikaten, die Benutzerkonten in AD DS zugeordnet sind  
  
Für den Extranetzugriff werden die folgenden Authentifizierungsmechanismen unterstützt:  
  
-   Formular Authentifizierung mit Benutzernamen \/ Kennwörtern  
  
-   Zertifikat Authentifizierung mithilfe von Zertifikaten, die Benutzerkonten in AD DS zugeordnet sind  
  
-   Die integrierte Windows-Authentifizierung mit \( der Aushandlung von NTLM nur \) für WS \- Trust-Endpunkte, die die integrierte Windows-Authentifizierung akzeptieren.  
  
Für Zertifikat Authentifizierung:  
  
-   Wird auf Smartcards erweitert, die durch Pin geschützt werden können.  
  
-   Die Benutzeroberfläche für den Benutzer zur Eingabe der PIN wird nicht von AD FS bereitgestellt und muss Teil des Client Betriebssystems sein, das bei Verwendung von Client TLS angezeigt wird.  
  
-   Der Reader und der Kryptografiedienstanbieter- \( CSP \) für die Smartcard müssen auf dem Computer arbeiten, auf dem sich der Browser befindet.  
  
-   Das Smartcardzertifikat muss an einen vertrauenswürdigen Stamm für alle AD FS Server und webanwendungsproxy-Server verkettet sein.  
  
-   Das Zertifikat muss dem Benutzerkonto in AD DS mit einer der folgenden Methoden zugeordnet sein:  
  
    -   Der Antragstellername des Zertifikats entspricht dem definierten LDAP-Namen eines Benutzerkontos in AD DS.  
  
    -   Die Unterordner für den Antragsteller Namen des Zertifikats enthält den Benutzer Prinzipal Namen- \( UPN \) eines Benutzerkontos in AD DS.  
  
Für eine nahtlose integrierte Windows-Authentifizierung mithilfe von Kerberos im Intranet  
  
-   Es ist erforderlich, damit der Dienst Name Teil der vertrauenswürdigen Sites oder der lokalen Intranetsites ist.  
  
-   Außerdem muss der Host \/<ADFS- \_ Dienst \_ Name> SPN für das Dienst Konto festgelegt werden, unter dem die AD FS-Farm ausgeführt wird.  
  
**Multi- \- Factor Authentication**  
  
AD FS unterstützt die zusätzliche Authentifizierung \( über die von AD DS unterstützte primäre Authentifizierung unter \) Verwendung eines Anbieter Modells, bei dem Anbieter \/ Kunden ihren eigenen Multi- \- Factor Authentication-Adapter erstellen können, den ein Administrator bei der Anmeldung Registrieren und verwenden kann.  
  
Jeder MFA-Adapter muss über .NET 4,5 erstellt werden.  
  
Weitere Informationen zu MFA finden Sie unter [Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).  
  
**Geräte Authentifizierung**  
  
AD FS unterstützt die Geräte Authentifizierung mithilfe von Zertifikaten, die vom Geräte Registrierungsdienst bereitgestellt werden, während der Arbeitsplatz eines Endbenutzers an Ihrem Gerät angeschlossen wird.  
  
## <a name="workplace-join-requirements"></a><a name="BKMK_11"></a>Anforderungen an den Workplace Join  
Endbenutzer können Ihre Geräte mit AD FS in eine Organisation einbinden. Dies wird vom Geräte Registrierungsdienst in AD FS unterstützt. Dies hat zur Folge, dass Endbenutzer den zusätzlichen Vorteil von SSO für die von AD FS unterstützten Anwendungen erhalten. Außerdem können Administratoren Risiken verwalten, indem Sie den Zugriff auf Anwendungen beschränken, indem Sie den Zugriff auf Geräte einschränken, die der Organisation hinzugefügt wurden. Im folgenden finden Sie die folgenden Anforderungen für die Aktivierung dieses Szenarios.  
  
-   AD FS unterstützt den Arbeitsplatz Beitritt für Windows 8.1-und IOS 5- \+ Geräte  
  
-   Um Workplace Join Funktionalität verwenden zu können, muss das Schema der Gesamtstruktur, mit der AD FS Server verknüpft sind, Windows Server 2012 R2 sein.  
  
-   Der alternative Antragsteller Name des SSL-Zertifikats für AD FS-Dienst muss den Wert enterpriseregistration enthalten, auf den das UPN-Suffix des Benutzer Prinzipal namens \( \) Ihrer Organisation folgt, z. b. enterpriseregistration.Corp.contoso.com.  
  
## <a name="cryptography-requirements"></a><a name="BKMK_12"></a>Kryptografieanforderungen  
In der folgenden Tabelle finden Sie weitere Informationen zur Kryptografieunterstützung zum AD FS Tokensignierung, zur Entschlüsselung von tokenverschlüsselungsfunktionen \/ :  
  
||||  
|-|-|-|  
|**Algorithmus**|**Schlüssellängen**|**\/Anwendungs \/ Kommentare für Protokolle**|  
|TripleDES – Standard 192 \( unterstützt 192 – 256 \) \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# TripleDES \- CBC](http://www.w3.org/2001/04/xmlenc#tripledes-cbc)|>\=192|Unterstützter Algorithmus für das Entschlüsseln des Sicherheits Tokens. Das Verschlüsseln des Sicherheits Tokens mit diesem Algorithmus wird nicht unterstützt.|  
|AES128 \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# AES128 \- CBC](http://www.w3.org/2001/04/xmlenc#aes128-cbc)|128|Unterstützter Algorithmus für das Entschlüsseln des Sicherheits Tokens. Das Verschlüsseln des Sicherheits Tokens mit diesem Algorithmus wird nicht unterstützt.|  
|AES192 \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# AES192 \- CBC](http://www.w3.org/2001/04/xmlenc#aes192-cbc)|192|Unterstützter Algorithmus für das Entschlüsseln des Sicherheits Tokens. Das Verschlüsseln des Sicherheits Tokens mit diesem Algorithmus wird nicht unterstützt.|  
|AES256 \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# AES256 \- CBC](http://www.w3.org/2001/04/xmlenc#aes256-cbc)|256|**Standard**. Unterstützter Algorithmus zum Verschlüsseln des Sicherheits Tokens.|  
|Tripledeskeywrap \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# kWh \- TripleDES](http://www.w3.org/2001/04/xmlenc#kw-tripledes)|Alle von .NET 4,0 unterstützten Schlüsselgrößen\+|Unterstützter Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der ein Sicherheits Token verschlüsselt.|  
|AES128KeyWrap \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# kW \- AES128](http://www.w3.org/2001/04/xmlenc#kw-aes128)|128|Unterstützter Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheits Token verschlüsselt.|  
|AES192KeyWrap \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# kW \- AES192](http://www.w3.org/2001/04/xmlenc#kw-aes192)|192|Unterstützter Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheits Token verschlüsselt.|  
|AES256KeyWrap \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# kW \- AES256](http://www.w3.org/2001/04/xmlenc#kw-aes256)|256|Unterstützter Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheits Token verschlüsselt.|  
|RsaV15KeyWrap \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# RSA \- 1 \_ 5](http://www.w3.org/2001/04/xmlenc#rsa-1_5)|1024|Unterstützter Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheits Token verschlüsselt.|  
|Rsaoaepkeywrap \- [http: \/ \/ www.w3.org \/ 2001 \/ 04 \/ xmlenc \# RSA \- OAEP \- MGF1P](http://www.w3.org/2001/04/xmlenc#rsa-oaep-mgf1p)|1024|Standard. Unterstützter Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheits Token verschlüsselt.|  
|SHA1 \- [http: \/ \/ www.w3.org \/ PIC \/ dsig \/ SHA1 \_ 1 \_0.html](http://www.w3.org/PICS/DSig/SHA1_1_0.html)|N\/V|Wird von AD FS Server in artefaktquellengenerierung verwendet: in diesem Szenario verwendet der STS SHA1 \( gemäß der Empfehlung im SAML 2,0-Standard \) , um einen kurzen 160-Bit-Wert für das artefaktelement SourceID zu erstellen.<p>Wird auch von der ADFS-Web-Agent- \( Legacy Komponente aus WS2003 Zeitrahmen verwendet \) , um Änderungen in einem "zuletzt aktualisierten" Uhrzeitwert zu identifizieren, sodass er weiß, wann Informationen aus dem STS aktualisiert werden müssen.|  
|SHA1withRSA\-<p>[http: \/ \/ www.w3.org \/ PIC \/ dsig \/ RSA \- SHA1 \_ 1 \_0.html](http://www.w3.org/PICS/DSig/RSA-SHA1_1_0.html)|N\/V|Wird in Fällen verwendet, in denen AD FS Server die Signatur von SAML authenticationrequest überprüft, die artefaktauflösungs Anforderung oder-Antwort Signieren und \- Tokensignaturzertifikat erstellen.<p>In diesen Fällen ist SHA256 der Standardwert, und SHA1 wird nur verwendet, wenn die Partner vertrauende \( Seite \) SHA256 nicht unterstützen kann und SHA1 verwendet werden muss.|  
  
## <a name="permissions-requirements"></a><a name="BKMK_13"></a>Berechtigungsanforderungen  
Der Administrator, der die Installation ausführt, und die Erstkonfiguration AD FS müssen über Domänen Administrator Berechtigungen in der lokalen Domäne verfügen \( , also die Domäne, der der Verbund Server hinzugefügt wird.\)  
  
## <a name="see-also"></a>Weitere Informationen  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  
