---
ms.assetid: 39ecc468-77c5-4938-827e-48ce498a25ad
title: 'Anhang A: Überprüfen von AD FS Anforderungen'
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ad3184dbe43cfa108aa1b178421102880b3ef4d7
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994983"
---
# <a name="appendix-a-reviewing-ad-fs-requirements"></a>Anhang A: Überprüfen der AD FS-Anforderungen

Damit die Organisations Partner in Ihrer Active Directory-Verbunddienste (AD FS)-Bereitstellung (AD FS) erfolgreich zusammenarbeiten können, müssen Sie zunächst sicherstellen, dass Ihre Unternehmensnetzwerk Infrastruktur für die Unterstützung von AD FS Anforderungen für Konten, Namensauflösung und Zertifikate konfiguriert ist. Für AD FS müssen die folgenden Anforderungen erfüllt sein:

> [!TIP]
> Weitere AD FS Ressourcen Verknüpfungen finden Sie Untergrund Legendes zu [Schlüssel AD FS Konzepten](../technical-reference/understanding-key-ad-fs-concepts.md).

## <a name="hardware-requirements"></a>Hardwareanforderungen
Die folgenden Mindestanforderungen und empfohlenen Hardwareanforderungen gelten für die Verbund Server-und Verbund Server Proxy-Computer.

|Hardwareanforderung|Mindestanforderung|Empfohlene Anforderung|
|------------------------|-----------------------|---------------------------|
|CPU-Geschwindigkeit|Single-Core, 1 Gigahertz (GHz)|Vierkern, 2 GHz|
|RAM|1 GB|4 GB|
|Speicherplatz|50 MB|100 MB|

## <a name="software-requirements"></a>Softwareanforderungen
AD FS stützt sich auf Serverfunktionen, die in das Betriebssystem Windows Server 2012 integriert sind &reg; .

> [!NOTE]
> Die Verbunddienst- und Verbunddienstproxy-Rollendienste können nicht auf demselben Computer installiert werden.

## <a name="certificate-requirements"></a>Zertifikatanforderungen
Zertifikate spielen eine äußerst wichtige Rolle beim Sichern der Kommunikation zwischen Verbundservern, Verbundproxyservern, Ansprüche unterstützenden Anwendungen und Webclients. Die Anforderungen für Zertifikate sind unterschiedlich, je nachdem, ob Sie einen Verbundserver- oder Verbundserverproxy-Computer einrichten, wie in diesem Abschnitt beschrieben.

### <a name="federation-server-certificates"></a>Verbundserverzertifikate
Für Verbundserver sind die in der folgenden Tabelle beschriebenen Zertifikate erforderlich.

|Zertifikattyp|BESCHREIBUNG|Was Sie vor der Bereitstellung wissen müssen|
|--------------------|---------------|------------------------------------------|
|SSL (Secure Sockets Layer)-Zertifikat|Dieses Standard-SSL-Zertifikat wird für das Sichern der Kommunikation zwischen Verbundservern und Clients verwendet.|Das Zertifikat muss auf die Standardwebsite in den Internetinformationsdiensten (IIS) für einen Verbundserver oder Verbundserverproxy begrenzt sein.  Bei einem Verbundserverproxy muss die Begrenzung in IIS konfiguriert werden, bevor der Assistent für die Konfiguration eines Verbundserverproxys erfolgreich ausgeführt werden kann.<p>**Empfehlung:** Da dieses Zertifikat für Clients von AD FS vertrauenswürdig sein muss, verwenden Sie ein Serverauthentifizierungszertifikat, das von einer öffentlichen (Drittanbieter) Zertifizierungsstelle wie VeriSign ausgestellt wurde. **Tipp:** Der Antragstellername dieses Zertifikats wird verwendet, um den Namen des Verbunddiensts für jede von Ihnen bereitgestellte Instanz von AD FS darzustellen. Aus diesem Grund sollten Sie einen Antragsstellernamen für jedes neue von einer Zertifizierungsstelle ausgestellte Zertifikat in Betracht ziehen, der den Namen Ihres Unternehmens oder Ihrer Organisation gegenüber Partnern am besten widerspiegelt.|
|Dienstkommunikationszertifikat|Mit diesem Zertifikat wird die WCF-Nachrichtensicherheit für das Sichern der Kommunikation zwischen Verbundservern aktiviert.|Standardmäßig wird das SSL-Zertifikat als Dienstkommunikationszertifikat verwendet.  Dies kann über die AD FS-Verwaltungskonsole geändert werden.|
|Tokensignaturzertifikat|Dies ist ein Standard-X509-Zertifikat, das für die sichere Signierung aller Token verwendet wird, die der Verbungsserver ausstellt.|Das Tokensignaturzertifikat muss einen privaten Schlüssel enthalten und sollte an einen vertrauenswürdigen Stamm im Verbunddienst gebunden sein. Standardmäßig erstellt AD FS ein selbstsigniertes Zertifikat. Sie können dies jedoch später je nach Anforderungen Ihrer Organisation über das AD FS-Verwaltungs-Snap-In in ein von einer Zertifizierungsstelle ausgestelltes Zertifikat ändern.|
|Tokenentschlüsselungszertifikat|Dies ist ein Standard-SSL-Zertifikat, das für die Entschlüsselung aller eingehenden Token verwendet wird, die von einem Partnerverbundserver verschlüsselt werden. Es wird außerdem in den Verbundmetadaten veröffentlicht.|Standardmäßig erstellt AD FS ein selbstsigniertes Zertifikat. Sie können dies jedoch später je nach Anforderungen Ihrer Organisation über das AD FS-Verwaltungs-Snap-In in ein von einer Zertifizierungsstelle ausgestelltes Zertifikat ändern.|

> [!CAUTION]
> Zertifikate, die für die Tokensignatur und die Tokenentschlüsselung verwendet werden, sind wichtig für die Stabilität des Verbunddiensts. Da der Verlust oder die ungeplante Entfernung von Zertifikaten, die für diesen Zweck konfiguriert sind, den Dienst unterbrechen kann, sollten Sie alle für diesen Zweck konfigurierten Zertifikate sichern.

Weitere Informationen zu den von Verbundservern verwendeten Zertifikaten finden Sie unter [Zertifikatanforderungen für Verbundserver](Certificate-Requirements-for-Federation-Servers.md).

### <a name="federation-server-proxy-certificates"></a>Verbundserverproxy-Zertifikate
Für Verbundserverproxies sind die in der folgenden Tabelle beschriebenen Zertifikate erforderlich.

|Zertifikattyp|BESCHREIBUNG|Was Sie vor der Bereitstellung wissen müssen|
|--------------------|---------------|------------------------------------------|
|Serverauthentifizierungszertifikat|Dieses Standard-SSL-Zertifikat wird für das Sichern der Kommunikation zwischen einem Verbundserverproxy und Internetclientcomputern verwendet.|Das Zertifikat muss auf die Standardwebsite in den Internetinformationsdiensten (IIS) begrenzt sein, bevor Sie den Assistenten für die Konfiguration eines Verbundserverproxys erfolgreich ausführen können.<p>**Empfehlung:** Da dieses Zertifikat für Clients von AD FS vertrauenswürdig sein muss, verwenden Sie ein Serverauthentifizierungszertifikat, das von einer öffentlichen (Drittanbieter) Zertifizierungsstelle wie VeriSign ausgestellt wurde.<p>**Tipp:** Der Antragstellername dieses Zertifikats wird verwendet, um den Namen des Verbunddiensts für jede von Ihnen bereitgestellte Instanz von AD FS darzustellen. Aus diesem Grund sollten Sie einen Antragstellernamen in Betracht ziehen, der den Namen Ihres Unternehmens oder Ihrer Organisation gegenüber Partnern am besten widerspiegelt.|

Weitere Informationen zu den von Verbundserverproxies verwendeten Zertifikaten finden Sie unter [Zertifikatanforderungen für Verbundserverproxies](Certificate-Requirements-for-Federation-Server-Proxies.md).

## <a name="browser-requirements"></a>Browseranforderungen
Auch wenn jeder aktuelle Webbrowser mit JavaScript-Funktion als ein AD FS-Client funktionieren kann, wurden die standardmäßig bereitgestellten Webseiten nur in Internet Explorer 7.0, 8.0 und 9.0 sowie Mozilla Firefox 3.0 und Safari 3.1 unter Windows getestet. JavaScript und Cookies für die browserbasierte An- und Abmeldung müssen aktiviert sein, damit dies ordnungsgemäß funktioniert.

Das AD FS-Produktteam bei Microsoft hat die Browser-und Betriebs Systemkonfigurationen in der folgenden Tabelle erfolgreich getestet.

|Browser|Windows 7|Windows Vista|
|-----------|-------------|-----------------|
|Internet Explorer 7.0|X|X|
|Internet Explorer 8.0|X|X|
|Internet Explorer 9.0|X|Nicht getestet|
|FireFox 3.0|X|X|
|Safari 3.1|X|X|

> [!NOTE]
> AD FS unterstützt sowohl die 32-Bit- als auch die 64-Bit-Versionen aller in der obigen Tabelle aufgeführten Browser.

### <a name="cookies"></a>Cookies
AD FS erstellt sitzungsbasierte und beständige Cookies, die auf Clientcomputern gespeichert werden müssen, um Anmeldung, Abmeldung, einmaliges Anmelden (SSO) und andere Funktionen bereitzustellen. Daher muss der Clientbrowser so konfiguriert sein, dass Cookies akzeptiert werden. Für die Authentifizierung verwendete Cookies sind immer Secure Hypertext Transfer Protocol (HTTPS)-Sitzungscookies, die für den Ursprungsserver geschrieben werden. Wenn die Konfiguration des Clientbrowsers diese Cookies nicht zulässt, kann AD FS nicht ordnungsgemäß funktionieren. Beständige Cookies werden verwendet, um die Benutzerauswahl des Anspruchsanbieters beizubehalten. Sie können diese über eine Konfigurationseinstellung in der Konfigurationsdatei für die AD FS-Anmeldeseiten deaktivieren.

Aus Sicherheitsgründen ist eine Unterstützung für TLS/SSL erforderlich.

## <a name="network-requirements"></a>Netzwerkanforderungen
Das ordnungsgemäße Konfigurieren der folgenden Netzwerkdienste ist für eine erfolgreiche Bereitstellung von AD FS in Ihrer Organisation entscheidend.

### <a name="tcpip-network-connectivity"></a>TCP/IP-Netzwerkkonnektivität
Damit AD FS funktioniert, muss TCP/IP-Netzwerk Konnektivität zwischen dem Client vorhanden sein. ein Domänen Controller; und die Computer, auf denen die Verbunddienst gehostet werden, die Verbunddienstproxy (bei Verwendung) und die AD FS-Web-Agent.

### <a name="dns"></a>DNS
Der primäre Netzwerkdienst, der für den Betrieb von AD FS wichtig ist, außer Active Directory Domain Services (AD DS), ist Domain Name System (DNS). Wenn DNS bereitgestellt wird, können Benutzer einfach zu merkende Computeranzeigenamen verwenden, um eine Verbindung zu Computern und anderen Ressourcen in IP-Netzwerken herzustellen.

 Windows Server 2008 verwendet DNS für die Namensauflösung anstelle der Windows Internet Name Service (WINS)-NetBIOS-Namensauflösung, die in Windows NT 4.0 – basierten Netzwerken verwendet wurde. Es ist immer noch möglich, WINS für Anwendungen zu verwenden, für die der Dienst erforderlich ist. Für AD DS und AD FS ist jedoch die DNS-Namensauflösung erforderlich.

Der Prozess der Konfiguration von DNS zur Unterstützung von AD FS variiert abhängig davon, ob:

-   Ihre Organisation verfügt bereits über eine vorhandene DNS-Infrastruktur. In den meisten Szenarien ist DNS bereits im gesamten Netzwerk konfiguriert, sodass die Browserclients in Ihrem Unternehmensnetzwerk Zugriff auf das Internet haben. Da der Internet Zugriff und die Namensauflösung Anforderungen AD FS sind, wird davon ausgegangen, dass diese Infrastruktur für Ihre AD FS Bereitstellung eingerichtet ist.

-   Sie beabsichtigen, Ihrem Unternehmensnetzwerk einen Verbundserver hinzuzufügen. Für den Zweck der Authentifizierung von Benutzern im Unternehmensnetzwerk müssen interne DNS-Server in der Unternehmensnetzwerkgesamtstruktur so konfiguriert werden, dass der CNAME des internen Servers zurückgegeben wird, auf dem der Verbunddienst ausgeführt wird. Weitere Informationen finden Sie unter [Anforderungen an die Namensauflösung für Verbundserver](Name-Resolution-Requirements-for-Federation-Servers.md).

-   Sie beabsichtigen, Ihrem Unternehmensnetzwerk einen Verbundserverproxy hinzuzufügen. Wenn Sie Benutzerkonten authentifizieren möchten, die sich im Unternehmensnetzwerk Ihrer Identitäts Partnerorganisation befinden, müssen die internen DNS-Server in der Unternehmensnetzwerk Gesamtstruktur so konfiguriert werden, dass der CNAME des internen Verbund Server Proxys zurückgegeben wird. Informationen zum Konfigurieren von DNS für das Hinzufügen von Verbund Server Proxys finden Sie unter [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.

-   Sie richten DNS für eine Testumgebung ein. Wenn Sie beabsichtigen, AD FS in einer Testumgebung zu verwenden, in der kein einzelner Stamm-DNS-Server autoritativ ist, müssen Sie wahrscheinlich DNS-Weiterleitungen einrichten, damit die Namen von Abfragen zwischen zwei oder mehr Gesamtstrukturen entsprechend weitergeleitet werden. Allgemeine Informationen zum Einrichten einer AD FS Testumgebung finden Sie unter [AD FS Schritt-für-Schritt-Anleitungen und Anleitungen](https://go.microsoft.com/fwlink/?LinkId=180357).

## <a name="attribute-store-requirements"></a>Anforderungen an den Attributspeicher
AD FS erfordert mindestens einen Attribut Speicher, der für die Authentifizierung von Benutzern und das Extrahieren von Sicherheitsansprüchen für diese Benutzer verwendet werden muss. Eine Liste der von AD FS unterstützten Attributspeicher finden Sie unter [Die Rolle von Attributspeichern](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md) im AD FS-Entwurfshandbuch.

> [!NOTE]
> AD FS erstellt standardmäßig automatisch einen Active Directory-Attributspeicher.

Die Anforderungen an den Attributspeicher hängen davon ab, ob Ihre Organisation als Kontopartner (der die Verbundbenutzer hostet) oder als Ressourcenpartner (der die Verbundanwendung hostet) agiert.

### <a name="adds"></a>AD DS
Damit AD FS erfolgreich ausgeführt werden kann, muss auf Domänen Controllern in der Konto Partnerorganisation oder der Ressourcen Partnerorganisation Windows Server 2003 SP1, Windows Server 2003 R2, Windows Server 2008 oder Windows Server 2012 ausgeführt werden.

Wenn AD FS auf einem Computer installiert und konfiguriert ist, der einer Domäne angehört, wird der Active Directory-Benutzerkontenspeicher für diese Domäne als auswählbarer Attributspeicher zur Verfügung gestellt.

> [!IMPORTANT]
> Da AD FS die Installation von Internetinformationsdienste (IIS) erfordert, wird empfohlen, die AD FS Software aus Sicherheitsgründen nicht auf einem Domänen Controller in einer Produktionsumgebung zu installieren. Für diese Konfiguration erhalten Sie jedoch Support vom Microsoft-Kundendienst.

#### <a name="schema-requirements"></a>Schemaanforderungen
AD FS erfordert weder Schema Änderungen noch Änderungen auf funktionaler Ebene in AD DS.

#### <a name="functional-level-requirements"></a>Anforderungen an die Funktionsebene
Für die meisten AD FS-Features sind für einen erfolgreichen Betrieb keine Änderungen auf der AD DS-Funktionsebene erforderlich. Allerdings ist die Windows Server 2008-Domänenfunktionsebene oder höher erforderlich, damit die Clientzertifikatauthentifizierung erfolgreich betrieben werden kann, wenn das Zertifikat explizit einem Benutzerkonto in AD DS zugeordnet ist.

#### <a name="service-account-requirements"></a>Dienstkontenanforderungen
Wenn Sie eine Verbundserverfarm erstellen, müssen Sie zunächst ein dediziertes domänenbasiertes Dienstkonto in AD DS erstellen, dass der Verbunddienst verwenden kann. Später legen Sie in Konfiguration jedes Verbundservers in der Farm fest, dass dieses Konto verwendet wird. Weitere Informationen dazu finden Sie unter [Manuelle Konfiguration eines Dienstkontos für eine Verbundserverfarm](../../ad-fs/deployment/Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) im AD FS-Bereitstellungshandbuch.

### <a name="ldap"></a>LDAP
Wenn Sie mit anderen Lightweight Directory Access Protocol (LDAP)-basierten Attributspeichern arbeiten, müssen Sie eine Verbindung zu einem LDAP-Server herstellen, der die integrierte Windows-Authentifizierung unterstützt. Die LDAP-Verbindungszeichenfolge muss außerdem im Format einer LDAP-URL geschrieben sein, wie in RFC 2255 beschrieben.

### <a name="sql-server"></a>SQL Server
Damit AD FS erfolgreich ausgeführt werden können, müssen Computer, auf denen der strukturierte Abfragesprache (SQL)-Server Attribut Speicher gehostet wird, entweder Microsoft SQL Server 2005 oder SQL Server 2008 ausgeführt werden. Wenn Sie mit SQL-basierten Attributspeichern arbeiten, müssen Sie außerdem eine Verbindungszeichenfolge konfigurieren.

### <a name="custom-attribute-stores"></a>Benutzerdefinierte Attributspeicher
Sie können benutzerdefinierte Attributspeicher entwickeln, um erweiterte Szenarien zu aktivieren. Die in AD FS integrierte Richtiliniensprache kann auf benutzerdefinierte Attributspeicher verweisen, sodass jedes der folgenden Szenarien verbessert werden kann:

-   Erstellen von Ansprüchen für einen lokal authentifizierten Benutzer

-   Ergänzen von Ansprüchen für einen lokal authentifizierten Benutzer

-   Autorisieren eines Benutzers zum Abrufen eines Token

-   Autorisieren eines Diensts zum Abrufen eines Token zum Verhalten eines Benutzers

Wenn Sie mit einem benutzerdefinierten Attributspeicher arbeiten, müssen Sie möglicherweise außerdem eine Verbindungszeichenfolge konfigurieren. In dieser Situation können Sie einen beliebigen Code eingeben, der eine Verbindung zur Ihrem benutzerdefinierten Attributspeicher ermöglicht. In dieser Situation ist die Verbindungszeichenfolge ein Satz von Werten aus Name/Wert, der vom Entwickler des benutzerdefinierten Attributspeichers als implementiert interpretiert wird.

Weitere Informationen zum entwickeln und Verwenden von benutzerdefinierten Attribut speichern finden Sie unter Übersicht über den [Attribut Speicher](https://go.microsoft.com/fwlink/?LinkId=190782).

## <a name="application-requirements"></a>Anwendungsanforderungen
Verbundserver können mit Verbundanwendungen wie Ansprüche unterstützende Anwendungen kommunizieren und diese schützen.

## <a name="authentication-requirements"></a>Authentifizierungsanforderungen
AD FS ist auf natürliche Weise in die vorhandene Windows-Authentifizierung integriert, z. b. Kerberos-Authentifizierung, NTLM, Smartcards und Client seitige X. 509 v3-Zertifikate. Verbundserver verwenden die Standard-Kerberos-Authentifizierung, um einen Benutzer bei einer Domäne zu authentifizieren. Clients können je nach Ihrer Authentifizierungskonfiguration über eine formularbasierte Authentifizierung, eine Authentifizierung mit Smartcards und die integrierte Windows-Authentifizierung authentifiziert werden.

Die AD FS-Verbundserverproxy-Rolle ermöglicht ein Szenario, indem der Benutzer extern über die SSL-Clientauthentifizierung authentifiziert wird. Sie können die Verbundserverrolle außerdem so konfigurieren, dass eine SSL-Clientauthentifizierung erforderlich ist, obwohl die nahtloseste Benutzererfahrung in der Regel durch eine Konfiguration des Kontoverbundservers für die integrierte Windows-Authentifizierung erreicht wird. In dieser Situation hat AD FS keine Kontrolle darüber, welche Anmeldeinformationen der Benutzer für die Windows-Desktopanmeldung verwendet.

### <a name="smart-card-logon"></a>Anmeldung mit Smartcards
Obwohl AD FS den Typ der Anmelde Informationen, die für die Authentifizierung verwendet werden (Kenn Wörter, SSL-Client Authentifizierung oder integrierte Windows-Authentifizierung) erzwingen kann, wird die Authentifizierung mit Smartcards nicht direkt erzwungen. Daher stellt AD FS keine Client seitige Benutzeroberfläche bereit, um Smartcard-PIN-Anmelde Informationen (Personal Identification Number, PIN) abzurufen. Dies liegt daran, dass Windows-basierte Clients absichtlich keine Benutzer Anmelde Informationen für Verbund Server oder Webserver bereitstellen.

### <a name="smart-card-authentication"></a>Authentifizierung mit Smartcards
Bei der Smartcard-Authentifizierung wird das Kerberos-Protokoll für die Authentifizierung bei einem Konto Verbund Server verwendet. AD FS kann nicht erweitert werden, um neue Authentifizierungsmethoden hinzuzufügen. Das Zertifikat in der Smartcard muss an einen vertrauenswürdigen Stamm auf dem Clientcomputer gebunden werden. Die Verwendung eines smartcardbasierten Zertifikats mit AD FS erfordert die folgenden Bedingungen:

-   Der Leser und der Kryptografiedienstanbieter (CSP) für die Smartcard müssen auf dem Computer arbeiten, auf dem sich der Browser befindet.

-   Das Smartcardzertifikat muss an einen vertrauenswürdigen Stamm auf dem Konto Verbund Server und dem Konto Verbund Server Proxy verkettet sein.

-   Das Zertifikat muss dem Benutzerkonto in AD DS mit einer der folgenden Methoden zugeordnet sein:

    -   Der Antragstellername des Zertifikats entspricht dem definierten LDAP-Namen eines Benutzerkontos in AD DS.

    -   Die Erweiterung für den Zertifikatantragsteller-AlternatNamen verfügt über den Benutzerprinzipalnamen eines Benutzerkontos AD DS.

Zur Unterstützung der Anforderungen an bestimmte Authentifizierungsstärken in einigen Szenarien können Sie AD FS auch für die Erstellung eines Anspruchs konfigurieren, der anzeigt, wie ein Benutzer authentifiziert wurde. Eine vertrauende Seite kann diesen Anspruch dann verwenden, um eine Autorisierungsentscheidung zu treffen.

## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)