---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-05"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Anwendungen, Geräte und Gateways mithilfe der API verbinden
{: #connect_devices_apps_gw}

Anwendungen, Geräte und Gateways können über das MQTT-Protokoll eine Verbindung zu {{site.data.keyword.iot_full}} herstellen. Sie können auch die HTTP-REST-API verwenden, um Geräte mit {{site.data.keyword.iot_short_notm}} zu verbinden.
{: shortdesc}


## URLs für Clientverbindungen
{: #client_connect_url}

Zum Herstellen von Verbindungen zwischen Geräte-, Anwendungs- und Gateway-Clients und Ihrer {{site.data.keyword.iot_short_notm}}-Instanz verwenden Sie folgende Verbindungs-URLs:

### Nachrichtenadresse

<pre class="pre"><var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com</pre>
{: codeblock}

### Verbindungs-URL für HTTP-REST-API

<pre class="pre"><code class="hljs">https://<var class="keyword varname">Organisations-ID</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></code></pre>
{: codeblock}

**Hinweise**
- Dabei ist *orgId* die eindeutige Organisations-ID, die beim Registrieren der Serviceinstanz generiert wurde.
- Wenn Sie für ein Gerät oder eine Anwendung eine Verbindung zum Quickstart-Service herstellen, geben Sie 'quickstart' als Wert für *Organisations-ID* an.

## Portsicherheit
{: #client_port_security}

Stellen Sie sicher, dass die erforderlichen Ports offen und für die Kommunikation aktiviert sind. Die Ports 8883 und 443 unterstützen sichere Verbindungen über TLS mit dem MQTT- und dem HTTP-Protokoll. Der Port 1883 unterstützt nicht gesicherte Verbindungen mit dem MQTT- und dem HTTP-Protokoll. Informationen zum Verbindungstyp und zu den zugehörigen Portnummern sind in der folgenden Tabelle zusammengefasst:   

|Verbindungstyp |Portnummer|
|:---|:---|
|Nicht sicher|1883|
|Sicher|8883|
|Sicher|443|

MQTT wird über TCP und WebSockets unterstützt. MQTT-Clients stellen eine Verbindung unter Verwendung von entsprechenden Berechtigungsnachweisen her, wie beispielsweise Authentifizierungstokens für Geräte bzw. API-Schlüssel und Tokens für Anwendungen. Da diese Berechtigungsnachweise mithilfe der MQTT-Nachrichtenübermittlung in einfachem Text an den nicht sicheren Port 1883 gesendet werden, sollten Sie stattdessen stets die sicheren Alternativen 8883 oder 443 verwenden. Die TLS-Berechtigungsnachweise werden immer verschlüsselt über sichere Ports gesendet. Beachten Sie, dass Sie TLS in der Anwendung mithilfe der Methode 'tls_set()' in der Python-MQTT-Bibliothek aktivieren müssen. Andernfalls werden die Daten möglicherweise auf unsichere Weise gesendet.

Wenn Sie die MQTT-Nachrichtenübermittlung an den Ports 8883 oder 443 schützen, vertrauen neuere Clientbibliotheken automatisch dem Zertifikat, das von {{site.data.keyword.iot_short_notm}} angegeben wird. Wenn dies in Ihrer Clientumgebung nicht der Fall ist, können Sie die Kette des Gesamtzertifikats von [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem) herunterladen und verwenden.


## TLS-Anforderungen
{: #tls_requirements}

Einige TLS-Clientbibliotheken (TLS - Transport Layer Security) unterstützen keine Domänen, die ein Platzhalterzeichen enthalten. Inaktivieren Sie die Zertifikatsüberprüfung, wenn das Ändern von Bibliotheken nicht erfolgreich ist.

Ihre TLS-Anforderungen sind davon abhängig, ob Sie eine Verbindung zu {{site.data.keyword.iot_short_notm}} über das MQTT- oder das HTTP-Protokoll herstellen. In den folgenden Abschnitten wird angegeben, welche Cipher-Suites bei Verwendung des Standardserverzertifikats unterstützt werden. Wenn Sie ein eigenes Clientzertifikat verwenden, hängt es vom verwendeten Zertifikat ab, welche Cipher-Suites unterstützt werden.

### TLS-Anforderungen für MQTT-Verbindungen

{{site.data.keyword.iot_short_notm}} erfordert TLS Version 1.2 und die folgenden Cipher-Suites:


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

### TLS-Anforderungen für HTTP-Verbindungen

Wenn Sie das Standardserverzertifikat verwenden, sind für {{site.data.keyword.iot_short_notm}} TLS Version 1, TLS Version 1.1 oder TLS Version 1.2 und die folgenden Cipher-Suites erforderlich:


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384


## MQTT-Clientauthentifizierung
{: #mqtt_authentication}

**Wichtig:** Für jeden MQTT-Client ist eine eindeutige Client-ID erforderlich. Wenn Sie versuchen, in Ihrer Organisation eine Verbindung für einen Client mithilfe einer Client-ID herzustellen, für die bereits eine Verbindung besteht, wird die zuerst hergestellte Verbindung getrennt.

Für Geräte und Gateways, die direkt mit {{site.data.keyword.iot_short_notm}} verbunden sind, wird im Dashboard ein Statussymbol angezeigt, mit dem angegeben wird, dass sie verbunden sind. Geräte, die indirekt über ein Gateway verbunden sind, werden als nicht verbunden angezeigt, da das Dashboard über ein Gateway verbundene Geräte nicht erkennt.

### MQTT-Client-ID

Definieren Sie jeden MQTT-Client mithilfe der folgenden Client-IDs und des folgenden Formats, um Geräte, Anwendungen und Gateways erfolgreich zu authentifizieren.

|Clienttyp |ID|MQTT-ID-Format|
|:---|:---|:---|
|Anwendungen|a|<pre class="pre">a:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Anwendungs-ID</var></pre>
|Skalierbare Anwendungen|A|<pre class="pre">A:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Anwendungs-ID</var></pre>
|Geräte|d|<pre class="pre">d:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Gerätetyp</var>:<var class="keyword varname">Geräte-ID</var></pre>|
|Gateways|g|<pre class="pre">g:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Typ-ID</var>:<var class="keyword varname">Geräte-ID</var></pre>|

Dabei gilt:
- *Organisations-ID* ist die aus sechs Zeichen bestehende eindeutige Organisations-ID, die beim Registrieren des Service generiert wurde.
- *appId* ist eine benutzerdefinierte eindeutige Zeichenfolge-ID für den Client.
- *Geräte-ID* gibt ein Gerät oder Gateway unter allen Typen analog zu einer Seriennummer eindeutig an.
- *Gerätetyp* ist die ID für den Typ des Geräts, für das eine Verbindung aufgebaut wird, und sie ist analog zu einer Modellnummer.
- *Type-ID* ist eine ID für den Typ des Gateways, für das eine Verbindung aufgebaut wird, und sie ist analog zu einer Modellnummer.

Die Werte für *Anwendungs-ID*, *Typ-ID*, *Gerätetyp* und *Geräte-ID* dürfen nicht länger als 36 Zeichen sein und sie dürfen nur folgende Zeichen enthalten:
- Alphanumerische Zeichen (a-z, A-Z, 0-9)
- Gedankenstriche (-)
- Unterstreichungszeichen (_)
- Punkte (.)

**Hinweise:**
- Wenn Sie eine Verbindung zum Quickstart-Service herstellen, ist eine Authentifizierung nicht erforderlich.
- Sie müssen eine Anwendung nicht registrieren, bevor Sie eine Verbindung für diese Anwendung herstellen.


### Verbindungen für Anwendungen mithilfe von MQTT herstellen

{{site.data.keyword.iot_short_notm}}-Anwendungen erfordern einen API-Schlüssel, um eine Verbindung zu einer Organisation herzustellen. Nach Registrierung eines API-Schlüssels wird ein Token generiert, das zusammen mit diesem API-Schlüssel verwendet werden muss.

Der folgende Code zeigt ein Beispiel eines API-Schlüssels:

<pre class="pre">a-<var class="keyword varname">Organisations-ID</var>-a84ps90Ajs</pre>
{: codeblock}

Das folgende Beispiel zeigt ein typisches Authentifizierungstoken:

```
 MP$08VKz!8rXwnR-Q*
```

Wenn Sie mithilfe eines API-Schlüssels eine MQTT-Verbindung herstellen, müssen Sie sicherstellen, dass folgende Anforderungen erfüllt werden:

- Die MQTT-Client-ID hat das folgende Format: a:*Organisations-ID*:*Anwendungs-ID*
- Der MQTT-Benutzername ist der API-Schlüssel, zum Beispiel: a-*Organisations-ID*-a84ps90Ajs.
- Das MQTT-Kennwort ist das Authentifizierungstoken, zum Beispiel: *MP$08VKz!8rXwnR-Q*.

Weitere Informationen finden Sie in [MQTT-Konnektivität für Anwendungen](../../applications/mqtt.html).

### Geräteauthentifizierung

#### Benutzernamen
Der {{site.data.keyword.iot_short_notm}}-Service unterstützt nur die tokenbasierte Authentifizierung für Geräte; daher hat jedes Gerät nur einen einzigen Benutzernamen, der gültig ist.
Der Wert `use-token-auth` gibt für den Service an, dass das Authentifizierungstoken für das Gateway oder das Gerät als Kennwort für die MQTT-Verbindung verwendet wird.

Weitere Informationen finden Sie in [MQTT-Konnektivität für Geräte](../../devices/mqtt.html).

#### Kennwörter
Wenn der Client die tokenbasierte Authentifizierung verwendet, übergeben Sie das Authentifizierungstoken des Geräts als Kennwort für alle MQTT-Verbindungen.
