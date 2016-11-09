---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Verbindungen zu {{site.data.keyword.iot_short_notm}} für Anwendungen, Geräte und Gateways 
{: #connect_devices_apps_gw}
Letzte Aktualisierung: 8. September 2016
{: .last-updated}

Anwendungen, Geräte und Gateways können über das MQTT-Protokoll eine Verbindung zu {{site.data.keyword.iot_full}} herstellen. Geräte können auch über die HTTP-API eine Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen und Ereignisse publizieren.
{: shortdesc}


## URLs für Clientverbindungen 
{: #client_connect_url}

Zum Herstellen von Verbindungen zwischen Geräte-, Anwendungs- und Gateway-Clients und Ihrer {{site.data.keyword.iot_short_notm}}-Instanz verwenden Sie folgende Verbindungs-URLs: 

### Nachrichtenadresse 

<pre class="pre"><var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com </pre>
{: codeblock}

### Verbindungs-URL für HTTP-REST-API 

<pre class="pre">https://<var class="keyword varname">Organisations-ID</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var> </pre>
{: codeblock}

**Hinweise** 
- *Organisations-ID* ist die eindeutige Organisations-ID, die Sie beim Registrieren der Serviceinstanz generiert haben. 
- Wenn Sie für ein Gerät oder eine Anwendung eine Verbindung zum Quickstart-Service herstellen, geben Sie 'quickstart' als Wert für *Organisations-ID* an. 

## Portsicherheit 
{: #client_port_security}

Stellen Sie sicher, dass die erforderlichen Ports offen und für die Kommunikation aktiviert sind. 

|Verbindungstyp  |Portnummer |
|:---|:---|
|Nicht sicher |1883 |
|Sicher |8883 |
|Sicher |443 |

MQTT-Clients stellen eine Verbindung unter Verwendung von entsprechenden Berechtigungsnachweisen her, wie beispielsweise Authentifizierungstokens für Geräte bzw. API-Schlüssel und Tokens für Anwendungen. Da diese Berechtigungsnachweise mithilfe der MQTT-Nachrichtenübermittlung in einfachem Text an den nicht sicheren Port 1883 gesendet werden, sollten Sie stattdessen stets die sicheren Alternativen 8883 oder 443 verwenden. Die sicheren Ports erzwingen die Verschlüsselung der TLS-Berechtigungsnachweise. Beachten Sie, dass Sie TLS in der Anwendung über die Methode 'tls_set()' in der Python-MQTT-Bibliothek aktivieren müssen. Andernfalls werden die Daten möglicherweise auf unsichere Weise gesendet. 

Wenn Sie die MQTT-Nachrichtenübermittlung an den Ports 8883 oder 443 schützen, vertrauen neuere Clientbibliotheken automatisch dem Zertifikat, das von {{site.data.keyword.iot_short_notm}} angegeben wird. Wenn dies in Ihrer Clientumgebung nicht der Fall ist, können Sie die Kette des Gesamtzertifikats von [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem) herunterladen und verwenden. 


## TLS-Anforderungen 
{: #tls_requirements}
Einige TLS-Clientbibliotheken (TLS - Transport Layer Security) unterstützen keine Domänen, die ein Platzhalterzeichen enthalten. Inaktivieren Sie die Zertifikatsüberprüfung, wenn das Ändern von Bibliotheken nicht erfolgreich ist. 

{{site.data.keyword.iot_short_notm}} erfordert TLS Version 1.2 und folgende Cipher-Suites: 
- ECDHE-RSA-AES256-GCM-SHA384 
- AES256-GCM-SHA384 
- ECDHE-RSA-AES128-GCM-SHA256 
- AES128-GCM-SHA256 

## MQTT-Clientauthentifizierung 
{: #mqtt_authentication}

**Wichtig:** Für jeden MQTT-Client ist eine eindeutige Client-ID erforderlich. Wenn Sie versuchen, in Ihrer Organisation eine Verbindung für einen Client mithilfe einer Client-ID herzustellen, für die bereits eine Verbindung besteht, wird die zuerst hergestellte Verbindung getrennt. 

Für Geräte und Gateways, die direkt mit {{site.data.keyword.iot_short_notm}} verbunden sind, wird im Dashboard ein Statussymbol angezeigt, mit dem angegeben wird, dass sie verbunden sind. Geräte, die indirekt über ein Gateway verbunden sind, werden als nicht verbunden angezeigt, da das Dashboard über ein Gateway verbundene Geräte nicht erkennt. 

### MQTT-Client-ID 

Definieren Sie jeden MQTT-Client mithilfe der folgenden Client-IDs und des folgenden Formats, um Geräte, Anwendungen und Gateways erfolgreich zu authentifizieren. 

|Clienttyp  |ID |MQTT-ID-Format |
|:---|:---|:---|
|Anwendungen |a |<pre class="pre">a:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Anwendungs-ID</var> </pre>
|Skalierbare Anwendungen |A |<pre class="pre">A:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Anwendungs-ID</var> </pre>
|Geräte |d |<pre class="pre">d:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Gerätetyp</var>:<var class="keyword varname">Geräte-ID</var> </pre>|
|Gateways |g |<pre class="pre">g:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Typ-ID</var>:<var class="keyword varname">Geräte-ID</var> </pre>|

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

<pre class="pre">a-<var class="keyword varname">Organisations-ID</var>-a84ps90Ajs </pre>
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

Weitere Informationen finden Sie in [MQTT-Konnektivität für Geräte](../../devices/mqtt.html) 

#### Kennwörter 
Wenn der Client die tokenbasierte Authentifizierung verwendet, übergeben Sie das Authentifizierungstoken des Geräts als Kennwort für alle MQTT-Verbindungen. 
