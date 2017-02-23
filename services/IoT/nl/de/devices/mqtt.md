---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# MQTT-Konnektivität für Geräte
{: #mqtt}

MQTT ist das primäre Protokoll, das Geräte und Anwendungen für die Kommunikation mit {{site.data.keyword.iot_full}} verwenden. Es werden Clientbibliotheken, Informationen und Beispiele bereitgestellt, die Sie dabei unterstützen, für Ihre Geräte eine Verbindung zu {{site.data.keyword.iot_short_notm}} herzustellen und die Geräte zu integrieren.
{:shortdesc}

## Clientverbindungen
{: #client_connections}

Informationen zur Clientsicherheit und zur Vorgehensweise beim Herstellen von Verbindungen zwischen MQTT-Clients und Geräten in {{site.data.keyword.iot_short_notm}} finden Sie in [Anwendungen, Geräte und Gateways mit {{site.data.keyword.iot_short_notm}} verbinden](../reference/security/connect_devices_apps_gw.html).


## Verbindung zwischen Geräten und dem Quickstart-Service herstellen
{: #connecting_devices}

Der Quickstart-Service ist die schnellste Servicestufe. Er bietet keine Empfangsbestätigung und unterstützt keine MQTT-Servicequalitätsstufen, die höher als null sind. Wenn Sie eine Verbindung zum Quickstart-Service herstellen, ist keine Authentifizierung oder Registrierung erforderlich und für `orgId` muss `quickstart` festgelegt werden.

Wenn Sie Gerätecode schreiben, der mit Quickstart verwendet werden soll, müssen Sie beachten, dass folgende Servicefunktionen von {{site.data.keyword.iot_short_notm}} im Quickstart-Modus nicht unterstützt werden:

-  Befehle subskribieren
-  Gerätemanagementprotokoll
-  Bereinigte oder permanente Sitzungen

**Wichtig: ** Nachrichten, die von Geräten mit einer Geschwindigkeit von mehr als eine Nachricht pro Sekunde gesendet werden, können verworfen werden.


## MQTT-Authentifizierung
{: #mqtt_authentication}

{{site.data.keyword.iot_short_notm}} verwendet für Gateways und Geräte die tokenbasierte MQTT-Authentifizierung.

Zum Aktivieren der MQTT-Authentifizierung übergeben Sie beim Herstellen der MQTT-Verbindung einen Benutzernamen und ein Kennwort.

### Benutzername

Der Benutzername ist für alle Geräte gleich: `use-token-auth`. Dieser Wert bewirkt, dass {{site.data.keyword.iot_short_notm}} das Authentifizierungstoken des Geräts verwendet, das als Kennwort angegeben ist.

### Kennwort

Das Kennwort eines Geräts ist das eindeutige Authentifizierungstoken, das generiert wurde, als das Gerät in {{site.data.keyword.iot_short_notm}} registriert wurde.

## Ereignisse publizieren
{: #publishing_events}

Geräte verwenden zum Publizieren in Ereignistopics folgendes Format:

<pre class="pre">iot-2/evt/<var class="keyword varname">Ereignis-ID</var>/fmt/<var class="keyword varname">Format_Zeichenfolge</var></pre>
{: codeblock}

Dabei gilt:

-  **Ereignis-ID** ist die ID des Ereignisses, beispielsweise `status`.  Die Ereignis-ID kann eine beliebige Zeichenfolge sein, die in MQTT gültig ist. Wenn keine Platzhalterzeichen verwendet werden, müssen Subskribentenanwendungen diese Zeichenfolge in ihrem Subskriptionstopic verwenden, um die Ereignisse zu empfangen, die in ihrem Topic publiziert werden.
-  **Format_Zeichenfolge** ist eine Zeichenfolge, die den Inhaltstyp der Nachrichtennutzdaten definiert, damit der Empfänger der Nachricht bestimmen kann, wie der Inhalt geparst werden muss. Zu den üblichen Werten für den Inhaltstyp gehören unter anderen 'json', 'xml', 'txt' und 'csv'. Der Wert kann eine beliebige Zeichenfolge sein, die in MQTT gültig ist.

**Wichtig:** Der Umfang der Nachrichtennutzdaten ist auf maximal 131072 Byte begrenzt. Nachrichten, die größer sind als dieser Wert, werden abgelehnt.

### Aufbewahrte Nachrichten
{{site.data.keyword.iot_short_notm}}-Organisationen sind nicht dazu berechtigt, aufbewahrte MQTT-Nachrichten zu publizieren. Wenn ein Gerät eine aufbewahrte Nachricht sendet, überschreibt der {{site.data.keyword.iot_short_notm}}-Service das Flag für aufbewahrte Nachricht, sofern es auf 'true' gesetzt ist, und verarbeitet die Nachricht so, als wäre das Flag auf 'false' gesetzt.


## Befehle subskribieren
{: #subscribing_to_commands}

Geräte verwenden zum Subskribieren von Befehlstopics folgendes Format:

<pre class="pre">iot-2/cmd/<var class="keyword varname">Befehls-ID</var>/fmt/<var class="keyword varname">Format_Zeichenfolge</var></pre>
{: codeblock}

Dabei gilt:
 - **Ereignis-ID** ist die ID des Befehls, zum Beispiel `update`. Die Befehls-ID kann eine beliebige Zeichenfolge sein, die im MQTT-Protokoll gültig ist.  Wenn keine Platzhalterzeichen verwendet werden, müssen Geräte diese Zeichenfolge in ihrem Subskriptionstopic verwenden, um Befehle zu empfangen, die in ihrem Topic publiziert werden.
 - **Format_Zeichenfolge** ist eine Zeichenfolge, die den Inhaltstyp der Befehlsnutzdaten definiert, damit der Empfänger des Befehls bestimmen kann, wie der Inhalt geparst werden muss. Zu den üblichen Werten für den Inhaltstyp gehören unter anderen 'json', 'xml', 'txt' und 'csv'. Der Wert kann eine beliebige Zeichenfolge sein, die in MQTT gültig ist.

Geräte können keine Ereignisse anderer Geräte subskribieren. Ein Gerät empfängt publizierte Befehle nur für das eigene Gerät.

## Verwaltete Geräte
{: #managed-devices}

Die Unterstützung für das Lebenszyklusmanagement von Geräten ist optional. Das Gerätemanagementprotokoll verwendet dieselbe MQTT-Verbindung, die Ihr Gerät bereits für Ereignisse und die Befehlssteuerung verwendet.

### Servicequalitätsstufen und bereinigte Sitzung

Verwaltete Geräte können Nachrichten publizieren, deren Servicequalitätsstufe (QoS) '0' oder '1' ist.

Nachrichten, für die 'QoS=0' gilt, können verworfen werden; sie bleiben nach dem Neustart des Nachrichtenservers nicht bestehen. Nachrichten, für die 'QoS=1' gilt, können in die Warteschlange gestellt werden; sie bleiben nach dem Neustart des Nachrichtenservers bestehen. Durch die für eine Subskription geltende Permanenz ist festgelegt, ob eine Anforderung in die Warteschlange gestellt wird. Durch den Parameter `cleansession` der Verbindung, die die Subskription vorgenommen hat, wird die Permanenz der Subskription festgelegt.  

{{site.data.keyword.iot_short_notm}} publiziert Anforderungen, die die Servicequalitätsstufe '1' aufweisen, um das Einreihen von Nachrichten in die Warteschlange zu unterstützen. Um Nachrichten in die Warteschlange einzureihen, die gesendet werden, während ein verwaltetes Gerät nicht verbunden ist, konfigurieren Sie das Gerät mithilfe der Einstellung 'false' für den Parameter `cleansession` so, dass keine bereinigten Sitzungen verwendet werden.

**Warnung:**
Wenn Ihr verwaltetes Gerät eine permanente Subskription verwendet, werden alle Befehle, die an Ihr Gerät gesendet werden, während dies offline ist, als fehlgeschlagene Operationen berichtet, wenn das Gerät nicht vor dem Überschreiten des Zeitlimitwerts für die Anforderung erneut eine Verbindung zum Service herstellt. Wenn das Gerät die Verbindung jedoch wiederherstellt, werden diese Anforderungen vom Gerät verarbeitet. Die Permanenz der Subskription wird durch den Parameter `cleansession=false` angegeben.

### Topics

Ein verwaltetes Gerät muss eines der folgenden Topics subskribieren, um Anforderungen und Antworten vom {{site.data.keyword.iot_short_notm}}-Service handhaben zu können:

```
iotdm-1/#
```


Ein verwaltetes Gerät publiziert in Topics, die für den ausgeführten Typ von Managementanforderung spezifisch sind:

- Das verwaltete Gerät publiziert Gerätemanagementantworten in `iotdevice-1/response`.
- Weitere Topics, in denen ein verwaltetes Gerät publizieren kann, finden Sie im [Gerätemanagementprotokoll](device_mgmt/index.html) und in den [Gerätemanagementanforderungen](device_mgmt/requests.html).



### Nachrichtenformat

Alle Nachrichten werden im Format JSON gesendet.

**Anforderungen**  
Anforderungen werden wie im folgenden Codebeispiel gezeigt formatiert:

<pre class="pre">{  "d": {...}, "<var class="keyword varname">Anforderungs-ID</var>": "b53eb43e-401c-453c-b8f5-94b73290c056" }</pre>
{: codeblock}

Dabei gilt:

 - **d** umfasst alle Daten, die für die Anforderung relevant sind.
 - **Anforderungs-ID** ist eine Kennung der Anforderung und muss in eine Antwort kopiert werden. Wenn keine Antwort erforderlich ist, können Sie das Feld *req-Id* übergehen.

**Antworten**  
Antworten werden wie im folgenden Codebeispiel gezeigt formatiert:
```
        {
            "rc": 0,
            "message": "success",
            "d": {...},
            "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
        }
```
Dabei gilt:  
 - **rc** ist ein Ergebniscode der ursprünglichen Anforderung.
 - **message** ist ein optionales Element mit einer Textbeschreibung des Antwortcodes.
 - **d** ist ein optionales Datenelement, das die Antwort begleitet.
 - **reqId** ist die Anforderungs-ID der ursprünglichen Anforderung, das zum Korrelieren von Antworten mit Anforderungen verwendet wird. Das Gerät muss sicherstellen, dass alle Anforderungs-IDs (reqId) eindeutig sind. Antworten auf {{site.data.keyword.iot_short_notm}} müssen den richtigen Wert für **reqId** enthalten.

Weitere Informationen zu besonderen Anforderungs- und Antwortnachrichten finden Sie im [Gerätemanagementprotokoll](device_mgmt/index.html) und in den [Gerätemanagementanforderungen](device_mgmt/requests.html).
