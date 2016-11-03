---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP-REST-API für Geräte
{: #api}
Letzte Aktualisierung: 9. September 2016
{: .last-updated}

**Wichtig:** Die {{site.data.keyword.iot_full}}-Funktion 'HTTP-REST-API für Geräte' steht nur als Bestandteil des eingeschränkten Beta-Programms zur Verfügung. Zukünftige Aktualisierungen enthalten möglicherweise Änderungen, die mit der aktuellen Version dieser Funktion nicht kompatibel sind. Starten Sie einen Versuch und [senden Sie uns Ihren Erfahrungsbericht](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Zugriff auf HTTP-REST-API
{: #api_link}

Für den Zugriff auf die {{site.data.keyword.iot_short_notm}}-HTTP-REST-API und zum Abrufen weiterer Informationen zur Vorgehensweise bei der Integration von Geräten in Ihre Organisation rufen Sie die Webadresse 'https://docs.internetofthings.ibmcloud.com/swagger/v0002.html' auf.

Die einzige unterstützte {{site.data.keyword.iot_short_notm}}-HTTP-REST-API ist Version 2. Stellen Sie sicher, dass Ihre {{site.data.keyword.iot_short_notm}}-Lösungen Version 2 verwenden.

# HTTP-REST-Messaging-API für Geräte
{: #rest_messaging_api}

## Ereignisse publizieren
{: #event_publication}

Zusätzlich zum MQTT-Nachrichtenprotokoll können Sie Ihre Geräte auch so konfigurieren, dass Ereignisse in {{site.data.keyword.iot_short_notm}} über HTTP mithilfe von HTTP-REST-API-Befehlen publiziert werden.

Verwenden Sie eine der folgenden URLs, um eine `POST`-Anforderung von einem Gerät zu übergeben, das mit {{site.data.keyword.iot_short_notm}} verbunden ist:

### Nicht sichere POST-Anforderung
<pre class="pre">http://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

### Sichere POST-Anforderung
<pre class="pre">https://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

Wenn Sie eine Verbindung zwischen einem Gerät oder einer Anwendung und dem Quickstart-Service herstellen, verwenden Sie stattdessen eine der folgenden URLs:

### Nicht sichere POST-Anforderung an Quickstart
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

### Sichere POST-Anforderung an Quickstart
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

**Wichtige Hinweise:**
- In der aktuellen Version der HTTP-REST-API können Sie Geräteereignisse nur mithilfe der HTTP-Nachrichtenübertragung übergeben. Verwenden Sie das MQTT-Nachrichtenprotokoll, um Anforderungen nach anderen Gerätemanagement- und Steuerfunktionen zu übergeben.
- HTTP-Verbindungen können nur wiederverwendet werden, um Ereignisse für dasselbe Gerät zu publizieren, da der HTTP-Header für die Berechtigung nicht geändert werden kann.

### Authentifizierung

Alle Anforderungen müssen einen Berechtigungsheader enthalten. Die Basisauthentifizierung ist die einzige Methode, die unterstützt ist. Wenn ein Gerät eine HTTP-Anforderung über die {{site.data.keyword.iot_short_notm}}-HTTP-REST-API übergibt, sind folgende Berechtigungsnachweise erforderlich:

```
username = "use-token-auth"
password = Authentication token
```

### Anforderungsheader des Typs 'Content-Type'

Zusammen mit der Anforderung muss ein Anforderungsheader des Typs `Content-Type` ('Inhaltstyp') angegeben werden. Die folgende Tabelle zeigt die Zuordnung der unterstützten Typen zu den internen {{site.data.keyword.iot_short_notm}}-Formaten.

|Header des Typs 'Content-Type'|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### Servicequalität

Ähnlich der Servicestufe 0 der MQTT-Servicequalität (Zustellung höchstens einmal) bietet das HTTP-REST-Messaging die Zustellung nicht persistenter Nachrichten, prüft aber, ob die Anforderung richtig ist und an den Server gesendet werden kann, bevor es die HTTP-Antwort sendet. Durch eine Antwort, die den HTTP-Statuscode 200 enthält, wird bestätigt, dass die Nachricht an den Server übermittelt wurde. Wenn Sie entweder die MQTT-Servicequalitätsstufe 'höchstens einmal' oder das HTTP-Äquivalent zum Zustellen von Ereignisnachrichten verwenden, muss das Gerät oder die Anwendung Wiederholungslogik implementieren, damit die Zustellung garantiert ist.

Weitere Informationen zum MQTT-Protokoll und den Servicequalitätsstufen für {{site.data.keyword.iot_short_notm}} finden Sie in [MQTT-Messaging](../reference/mqtt/index.html).
