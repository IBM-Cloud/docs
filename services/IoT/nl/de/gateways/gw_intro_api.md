---

copyright:
 years: 2015, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP-Messaging-APIs für Gateway-Geräte (Beta)
{: #api}

**Wichtig:** Die {{site.data.keyword.iot_full}}-Funktion 'HTTP-API für Gateway-Geräte' steht nur als Bestandteil des eingeschränkten Beta-Programms zur Verfügung. Zukünftige Aktualisierungen enthalten möglicherweise Änderungen, die mit der aktuellen Version dieser Funktion nicht kompatibel sind. Starten Sie einen Versuch und [senden Sie uns Ihren Erfahrungsbericht ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}.

## Zugriff auf die Dokumentation der HTTP-Messaging-API für Gateway-Geräte
{: #rest_messaging_api}

Weitere Informationen zum Zugriff auf die Dokumentation der {{site.data.keyword.iot_short_notm}}-HTTP-Messaging-API und zur Vorgehensweise beim Senden von Ereignissen von Gateway-Geräten finden Sie in [{{site.data.keyword.iot_short_notm}}-HTTP-Messaging-API ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.


## Clientverbindungen
{: #client_connections}

Informationen zur Clientsicherheit und zur Vorgehensweise beim Herstellen von Verbindungen zwischen Clients und Gateway-Geräten in {{site.data.keyword.iot_short_notm}} finden Sie in [Anwendungen, Geräte und Gateways mit {{site.data.keyword.iot_short_notm}} verbinden](../reference/security/connect_devices_apps_gw.html).


## Ereignisse publizieren
{: #event_publication}

Zusätzlich zum MQTT-Nachrichtenprotokoll können Sie Ihre Gateway-Geräte auch so konfigurieren, dass Ereignisse in {{site.data.keyword.iot_short_notm}} über HTTP mithilfe von HTTP-Messaging-API-Befehlen publiziert werden.

Verwenden Sie eine der folgenden URLs, um eine `POST`-Anforderung von einem Gerät zu übergeben, das mit {{site.data.keyword.iot_short_notm}} verbunden ist:

### Nicht sichere POST-Anforderung
<pre class="pre"><code class="hljs">http://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></code></pre>

### Sichere POST-Anforderung
<pre class="pre"><code class="hljs">https://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></code></pre>

**Wichtige Hinweise:**
- Sie können Gateway-Geräteereignisse nur mithilfe von HTTP-Messaging übergeben. Verwenden Sie das MQTT-Nachrichtenprotokoll, um Anforderungen nach anderen Gateway-Gerätemanagement- und Steuerfunktionen zu übergeben.
- Port 443, der SSL-Standardport, kann auch für sichere HTTP-API-Aufrufe angegeben werden.
- Falls einem Gateway nicht die Rolle *Standardgateway* zugewiesen ist, kann es Ereignisse im Namen aller Geräte in der Organisation publizieren. Falls das mit dem Gateway verbundene Gerät nicht registriert ist, führt das Gateway automatisch eine Registrierung für dieses Gerät durch.
- Weisen Sie die Rolle *Standardgateway* zu, wenn Sie Geräteberechtigungsstufen prüfen möchten.

Weitere Informationen zur Rolle von Gateways und Ressourcengruppen finden Sie in [Gateway Access Control (Beta)](../gateways/gateway-access-control.html).

### Authentifizierung

Alle Anforderungen müssen einen Berechtigungsheader enthalten. Die Basisauthentifizierung ist die einzige Methode, die unterstützt ist. Wenn ein Gerät eine HTTP-Anforderung mithilfe der {{site.data.keyword.iot_short_notm}}-HTTP-REST-API übergibt, sind folgende Berechtigungsnachweise erforderlich:

|Berechtigungsnachweis|Erforderliche Eingabe|
|:---|:---|
|Benutzername| `g/{orgId}/{gwType}/{gwDevId}` or `g-{orgId}-{gwType}-{gwDevId}`
|Kennwort| Das Authentifizierungstoken, das beim Registrieren des Gateway-Geräts entweder automatisch generiert oder manuell angegeben wurde.

Dabei gilt:

<dl>
<dt>orgId</dt>  
<dd>Der Name der Organisation, der mit dem im Host-Header angegebenen Namen übereinstimmen muss.</dd>

<p></p>
<dt>gwType</dt>  
<dd>Der Typ von Gateway. </dd>
<dd>Wenn Sie Bindestriche ("-") als Trennzeichen im Benutzernamen verwenden, darf dieser Wert keinen Bindestrich enthalten. </dd>
<p></p>
<dt>gwDevId</dt>  
<dd>Die Gerätekennung des Gateways. </dd>
</dl>


### Anforderungsheader des Typs 'Content-Type'

Zusammen mit der Anforderung muss ein Anforderungsheader des Typs `Content-Type` ('Inhaltstyp') angegeben werden. Die folgende Tabelle zeigt die Zuordnung der unterstützten Typen zu den internen {{site.data.keyword.iot_short_notm}}-Formaten:

|Header des Typs 'Content-Type'|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### Servicequalität

Ähnlich der Servicestufe 0 der MQTT-Servicequalität (Zustellung höchstens einmal) bietet das HTTP-REST-Messaging eine Zustellung nicht persistenter Nachrichten, prüft aber, ob die Anforderung richtig ist und an den Server gesendet werden kann, bevor es die HTTP-Antwort sendet. Durch eine Antwort, die den HTTP-Statuscode 200 enthält, wird bestätigt, dass die Nachricht an den Server übermittelt wurde. Wenn Sie entweder die MQTT-Servicequalitätsstufe 'höchstens einmal' oder das HTTP-Äquivalent zum Zustellen von Ereignisnachrichten verwenden, muss das Gerät oder die Anwendung Wiederholungslogik implementieren, damit die Zustellung garantiert ist.

Weitere Informationen zum MQTT-Protokoll und den Servicequalitätsstufen für {{site.data.keyword.iot_short_notm}} finden Sie in [MQTT-Messaging](../reference/mqtt/index.html).

Weitere Informationen zum Verwalten von Gateway-Geräten mithilfe von APIs finden Sie in [HTTP-REST-APIs für Gateway-Geräte](../gateways/gw_api.html).
