---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# MQTT-Konnektivität für Gateways
{: #mqtt}

MQTT ist das primäre Protokoll, das Geräte und Anwendungen für die Kommunikation mit {{site.data.keyword.iot_full}} verwenden. Es werden Clientbibliotheken, Informationen und Beispiele bereitgestellt, die Sie dabei unterstützen, MQTT-Clients als Gateways zu verwenden, um für Ihre Geräte eine Verbindung zu {{site.data.keyword.iot_short_notm}} herzustellen.
{:shortdesc}

## Clientverbindungen
{: #client_connections}

Informationen zur Clientsicherheit und dazu, wie MQTT-Clients als Gateways verbunden werden, finden Sie in [Anwendungen, Geräte und Gateways mit {{site.data.keyword.iot_short_notm}} verbinden](../reference/security/connect_devices_apps_gw.html).

## MQTT-Authentifizierung
{: #authentication}
{{site.data.keyword.iot_short_notm}} verwendet für Gateways und Geräte die tokenbasierte MQTT-Authentifizierung.

Zum Aktivieren der MQTT-Authentifizierung übergeben Sie beim Herstellen der MQTT-Verbindung einen Benutzernamen und ein Kennwort.

### Benutzername
{: #username}

Der Benutzername ist für alle Gateways gleich: `use-token-auth`. Dieser Wert bewirkt, dass {{site.data.keyword.iot_short_notm}} das Authentifizierungstoken des Gateways verwendet, das als Kennwort angegeben ist.

### Kennwort
{: #password}

Das Kennwort eines Gateways ist das eindeutige Authentifizierungstoken, das generiert wurde, als das Gateway in {{site.data.keyword.iot_short_notm}} registriert wurde.

## Ereignisse publizieren
{: #pub_events}

Ein Gateway kann Ereignisse von sich aus und im Namen eines beliebigen anderen Geräts publizieren, das über das Gateway verbunden ist. Zum Publizieren von Ereignissen verwenden Sie das folgende Topic und ersetzen Sie `Typ-ID` und `Geräte-ID` auf der Basis der beabsichtigten Herkunft des Ereignisses durch die entsprechenden Werte:

<pre class="pre">iot-2/type/<var class="keyword varname">Typ-ID</var>/id/<var class="keyword varname">Geräte-ID</var>/evt/<var class="keyword varname">Ereignis-ID</var>/fmt/<var class="keyword varname">Format_Zeichenfolge</var></pre>
{: codeblock}


**Beispiel**


|    |'Typ-ID'|'Geräte-ID'|
|:---|:---|:---|
|Gateway 1 |mygateway |gateway1 |
|Gerät 1 |mydevice |device1 |

-   Gateway 1 kann eigene Statusereignisse publizieren:
      
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   Gateway 1 kann Statusereignisse im Namen von Gerät 1 publizieren:
      
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**Wichtig:** Der Umfang der Nachrichtennutzdaten ist auf maximal 131072 Byte begrenzt. Nachrichten, die größer sind als dieser Wert, werden abgelehnt.

### Aufbewahrte Nachrichten
{{site.data.keyword.iot_short_notm}}-Organisationen sind nicht dazu berechtigt, aufbewahrte MQTT-Nachrichten zu publizieren. Wenn ein Gateway eine aufbewahrte Nachricht sendet, überschreibt der {{site.data.keyword.iot_short_notm}}-Service das Flag für aufbewahrte Nachricht, sofern es auf 'true' gesetzt ist, und verarbeitet die Nachricht so, als wäre das Flag auf 'false' gesetzt.

## Befehle subskribieren
{: #subscribing_cmds}

Ein Gateway kann Befehle subskribieren, die an das Gateway selbst gerichtet sind, sowie an jedes Gerät in der Organisation einschließlich anderer Gateways. Zum Subskribieren von Befehlen verwenden Sie das folgende Topic und ersetzen Sie die Werte für `Typ-ID` und `Geräte-ID` entsprechend:

<pre class="pre">iot-2/type/<var class="keyword varname">Typ-ID</var>/id/<var class="keyword varname">Geräte-ID</var>/cmd/<var class="keyword varname">Befehls-ID</var>/fmt/<var class="keyword varname">Format_Zeichenfolge</var></pre>
{: codeblock}

Das MQTT-Platzhalterzeichen `+` kann als `Typ-ID`, `Geräte-ID`, `Befehls-ID` und `formatString` (Format_Zeichenfolge) verwendet werden, um mehrere Befehlsquellen zu subskribieren.

**Beispiel:**

|Gerät |`Typ-ID`|`Geräte-ID`|
|:---|:---|
|Gateway 1| mygateway   | gateway1   |
|Gerät 1 | mydevice    | device1    |


-   Gateway 1 kann Befehle subskribieren, die an das Gateway gerichtet sind:
  
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   Gateway 1 kann Befehle subskribieren, die an Gerät 1 gesendet wurden:
      
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   Gateway 1 kann beliebige Befehle subskribieren, die an Geräte des Typs `mydevice` gesendet werden:
       
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**Wichtig:** Persistente MQTT-Sitzungen, die als `cleansession=false` angegeben sind, suchen nicht nach Geräten, die Verbindungen zu Gateways herstellen. Wenn ein Gerät eine Verbindung zu Gateway A und anschließend eine Verbindung zu Gateway B herstellt, empfängt es keine Nachrichten, die für dieses Gerät an Gateway A publiziert wurden, während die Verbindung unterbrochen war. Ein Gateway ist Eigner des MQTT-Clients und der Subskription, aber nicht der Geräte, die mit diesem Gateway verbunden sind.

## Automatische Registrierung für das Gateway
{: #auto-reg}

Gateway-Geräte können Geräte, die mit ihnen verbunden sind, automatisch registrieren. Wenn ein Gateway eine Nachricht publiziert oder ein Topic im Namen eines nicht registrierten Geräts subskribiert, wird dieses Gerät automatisch registriert.

Registrierungsanforderungen von Gateway-Geräten sind auf eine Anzahl von 128 gleichzeitig anstehenden Anforderungen gedrosselt. Der Versuch, eine Verbindung für viele neue Geräte herzustellen, führt möglicherweise zu einer Verzögerung bei der Registrierung von Geräten über das Gateway.

**Warnung**

Wenn das Gateway ein Gerät nicht automatisch registrieren kann, versucht es für einen kurzen Zeitraum nicht mehr, dieses Gerät erneut zu registrieren. Während dieser Zeit werden Nachrichten oder Subskriptionen des fehlgeschlagenen Geräts gelöscht.

## Gateway-Benachrichtigungen
{: #notification}

Wenn beim Prüfen des Topics 'publish' oder 'subscribe' oder während der automatischen Registrierung Fehler auftreten, wird eine Benachrichtigung an das Gateway-Gerät gesendet. Ein Gateway kann diese Benachrichtigungen durch Subskribieren des folgenden Topics empfangen, wobei `Typ-ID` und `Geräte-ID` durch entsprechende Werte ersetzt werden:

```
iot-2/type/**Typ-ID**/id/**Geräte-ID**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">Typ-ID</var>/id/<var class="keyword varname">Geräte-ID</var>/notify</pre>
{: codeblock}

Für Nachrichten, die für das Topic 'notify' empfangen werden, wird das folgende Format verwendet:

```   
{
   "Request": "<Anforderungstyp>",
   "Time": "<Zeitmarke>",
   "Topic": "<Topic>",
   "Type": "<Gerätetyp>",
   "Id": "<Geräte-ID>",
   "Client": "<Client-ID>",
   "RC": "<Rückgabecode>",
   "Message": "<Nachricht>"
}
```
Dabei gilt:
-   `Anforderungstyp`-Werte sind entweder `publish` oder `subscribe`
-   `Zeitmarke` ist die Zeit im Format ISO 8601
-   `Topic` ist das Anforderungstopic des Gateways
-   `Gerätetyp` ist der Gerätetyp des Topics
-   `Geräte-ID` ist die Geräte-ID des Topics
-   `Client-ID` ist die Client-ID der Anforderung
-   `Rückgabecode` ist der Rückgabecode
-   `Nachricht` ist die Fehlernachricht

Ein Gateway kann folgende Benachrichtigungen empfangen:

-   Topic entspricht nicht den zulässigen Topic-Regeln.
-   Gerätetyp ist ungültig.
-   Geräte-ID ist ungültig.
-   Maximale Anzahl Geräte pro Gateway wurde erreicht.
-   Maximale Anzahl Geräte pro Organisation wurde erreicht.
-   Geräte konnte aufgrund interner Fehler nicht erstellt werden.

## Verwaltete Gateways
{: #managed_gateways}

Die Unterstützung für das Lebenszyklusmanagement von Geräten ist optional. Das Gerätemanagementprotokoll, das von {{site.data.keyword.iot_short_notm}} verwendet wird, verwendet dieselbe MQTT-Verbindung, die das Gateway für Ereignisse und die Befehlssteuerung verwendet.

### Servicequalitätsstufen und bereinigte Sitzung
{: #quality_service}

Verwaltete Gateways können Nachrichten publizieren, deren Servicequalitätsstufe (QoS) '0' oder '1' ist.

Nachrichten, für die 'QoS=0' gilt, können verworfen werden; sie bleiben nach dem Neustart des Nachrichtenservers nicht bestehen. Nachrichten, für die 'QoS=1' gilt, können in die Warteschlange gestellt werden; sie bleiben nach dem Neustart des Nachrichtenservers bestehen. Durch die für eine Subskription geltende Permanenz ist festgelegt, ob eine Anforderung in die Warteschlange gestellt wird. Durch den Parameter `cleansession` der Verbindung, die die Subskription vorgenommen hat, wird die Permanenz der Subskription festgelegt.  

{{site.data.keyword.iot_short_notm}} publiziert Anforderungen, die die Servicequalitätsstufe '1' aufweisen, um das Einreihen von Nachrichten in die Warteschlange zu unterstützen. Um Nachrichten in die Warteschlange einzureihen, die gesendet werden, während ein verwaltetes Gateway nicht verbunden ist, konfigurieren Sie das Gerät mithilfe der Einstellung 'false' für den Parameter `cleansession` so, dass keine bereinigten Sitzungen verwendet werden.

**Warnung**

Wenn Ihr verwaltetes Gateway eine permanente Subskription verwendet, werden Gerätemanagementbefehle, die an das Gateway gesendet werden, während dies offline ist, als fehlgeschlagene Operationen berichtet, wenn das Gateway nicht vor dem Überschreiten des Zeitlimitwerts für die Anforderung erneut eine Verbindung zum Service herstellt. Wenn das Gateway die Verbindung wiederherstellt, werden diese Anforderungen vom Gateway verarbeitet. Die Permanenz von Subskriptionen wird durch den Parameter `cleansession=false` angegeben.

Das Gateway ist Eigner der MQTT-Sitzung; dabei ist unerheblich, welche Geräte hinter dem Gateway stehen. Wenn ein Gerät über ein Gateway eine Subskriptionsanforderung übergibt, navigiert die Anforderung ungeachtet der Einstellung für die Option `cleansession=false` nicht zu anderen Gateways.

### Topics
{: #topics}

Ein verwaltetes Gerät muss folgende Topics subskribieren, um Anforderungen und Antworten von {{site.data.keyword.iot_short_notm}} handhaben zu können:

-   Das verwaltete Gateway subskribiert Gerätemanagementantworten von:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">Typ-ID</var>/id/<var class="keyword varname">Geräte-ID</var>/response/+</pre>
{: codeblock}
-   Das verwaltete Gateway subskribiert Gerätemanagementanforderungen von:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">Geräte-ID</var>/id/<var class="keyword varname">Geräte-ID</var>/+</pre>
{: codeblock}

Ein verwaltetes Gateway publiziert folgende Antworten und Anforderungen:

- Gerätemanagementantworten werden publiziert in:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">Typ-ID</var>/id/<var class="keyword varname">Geräte-ID</var>/response/</pre>
{: codeblock}
- Gerätemanagementanforderungen werden publiziert in:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">Typ-ID</var>/id/<var class="keyword varname">Geräte-ID</var>/</pre>
{: codeblock}

Das Gateway kann Gerätemanagementprotokollnachrichten für sich selbst und im Namen anderer verbundener Geräte verarbeiten, indem die entsprechenden Werte für **Typ-ID** und **Geräte-ID** verwendet werden.

### Nachrichtenformat
{: #msg_format}

Alle Nachrichten werden im Format JSON gesendet.

**Anforderungen**

Anforderungen werden wie im folgenden Codebeispiel gezeigt formatiert:

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` umfasst alle Daten, die für die Anforderung relevant sind.
-   `reqId` ist eine Kennung der Anforderung und muss in eine Antwort kopiert werden. Wenn keine Antwort erforderlich ist, wird das Feld nicht verwendet.

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
-   `rc` ist ein Ergebniscode der ursprünglichen Anforderung.
-   `message` ist ein optionales Element mit einer Textbeschreibung des Antwortcodes.
-   `d` ist ein optionales Datenelement, das die Antwort begleitet.
-   `reqId` ist die Anforderungs-ID der ursprünglichen Anforderung. Die Anforderungs-ID wird verwendet, um Antworten mit Anforderungen zu korrelieren, und das Gerät muss sicherstellen, dass alle Anforderungs-IDs eindeutig sind. Antworten auf {{site.data.keyword.iot_short_notm}}-Anforderungen müssen den richtigen Wert für `reqId` enthalten.
