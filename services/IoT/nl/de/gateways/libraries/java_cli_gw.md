---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-30"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#In {{site.data.keyword.iot_short_notm}} Gateways unter Verwendung von Java entwickeln
{: #java_cli_gw}

Wenn von Ihren Geräten keine direkte Verbindung zu Ihrer Organisation in {{site.data.keyword.iot_full}} herstellt werden kann, können Sie Gateways unter Verwendung von Java™ erstellen und anpassen. Es werden eine Java-Clientbibliothek für {{site.data.keyword.iot_short_notm}} sowie Dokumentation und Beispiele bereitgestellt, die Sie bei den ersten Schritten der Gateway-Entwicklung unterstützen.
{:shortdesc}

## Java-Client und Ressourcen herunterladen
{: #java_client_download}

Wechseln Sie für den Zugriff auf die Java-Clientbibliotheken und Beispiele für {{site.data.keyword.iot_short_notm}} in GitHub in das Repository [iot-java](https://github.com/ibm-watson-iot/iot-java) und folgen Sie den Installationsanweisungen.

## Konstruktor
{: #constructor}

Der Konstruktur erstellt die Gateway-Clientinstanz und akzeptiert das Objekt `Properties`, das die folgenden Definitionen enthält:

|Definition |Beschreibung |
|:----|:----|
|`org`|Erforderlicher Wert, für den die ID Ihrer Organisation eingestellt werden muss. Wenn Sie einen Quickstart-Ablauf verwenden, geben Sie `quickstart` an.|
|`domain`|Die URL des Nachrichtenendpunkts (optional). Wenn Sie keinen Wert für eine Domäne angeben, wird die Standardeinstellung `internetofthings.ibmcloud.com` verwendet, d. h. der {{site.data.keyword.iot_short_notm}}-Produktionsserver.|
|`type`|Erforderlicher Wert, der den Typ des Gateways angibt.|
|`id` |Erforderlicher Wert, der die eindeutige ID des Gateways angibt.|
|`auth-method`|Die zu verwendende Authentifizierungsmethode. Die einzige Methode, die unterstützt ist, lautet `token`.|
|`auth-token`|Ein API-Schlüsselauthentifizierungstoken zum Herstellen einer sicheren Verbindung zwischen Ihrem Gateway und {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Der Wert 'true' oder 'false', der nur erforderlich ist, wenn Sie das Gateway im Modus für permanente Subskription verbinden möchten. Für `clean-session` ist standardmäßig der Wert 'true' festgelegt.|
|`WebSocket`|Der Wert 'true' oder 'false', der nur erforderlich ist, wenn Sie das Gateway über Web-Sockets verbinden möchten.|
|`Port`|Die Nummer des Ports, zu dem eine Verbindung hergestellt werden soll. Geben Sie entweder 8883 oder 443 an. Wenn Sie keine Portnummer angeben, stellt der Client standardmäßig eine Verbindung zu {{site.data.keyword.iot_short_notm}} über den Port Nummer 8883 her.|
|`MaxInflightMessages`|Legt die maximale Anzahl der gerade ausgeführten Nachrichten für die Verbindung fest. Der Standardwert ist 100.|
|`Automatic-Reconnect`|Der Wert 'true' oder 'false', der erforderlich ist, wenn Sie das Gateway automatisch erneut mit {{site.data.keyword.iot_short_notm}} verbinden möchten, während es sich im nicht verbundenen Status befindet. Der Standardwert ist 'false'.|
|`Disconnected-Buffer-Size`|Die maximale Anzahl Nachrichten, die im Speicher gespeichert werden kann, während die Verbindung zum Client getrennt ist. Der Standardwert ist '5000'.|

**Hinweis:** Um das Gateway im Modus für permanente Subskription zu verbinden, legen Sie für `clean-session` die Einstellung `false` fest. Weitere Informationen zur bereinigten Sitzung (clean session) finden Sie im Abschnitt 'Subskriptionspuffer und bereinigte Sitzung' der [MQTT-Dokumentation](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

Das `Properties`-Objekt erstellt Definitionen, die für die Interaktion mit dem {{site.data.keyword.iot_short_notm}}-Modul verwendet werden.

Das folgende Codebeispiel zeigt, wie eine Gateway-Clientinstanz erstellt wird:

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### Konfigurationsdatei verwenden

Anstelle der direkten Verwendung eines Objekts `Properties` zum Erstellen einer Gateway-Instanz können Sie eine Konfigurationsdatei verwenden, die die Name/Wert-Paare für die Eigenschaften des Gateways enthält. Verwenden Sie das folgende Codeformat, um das Objekt `Properties` für das Gateway mithilfe einer Konfigurationsdatei zu erstellen:

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

Der Inhalt der Konfigurationsdatei muss folgendes Format aufweisen:

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen
{: #connecting_to_iotp}

Verwenden Sie zum Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} die Funktion `connect()`. Die Funktion `connect()` enthält einen optionalen booleschen Parameter mit der Bezeichnung `autoRetry`, mit dem festgelegt wird, ob die Bibliothek beim Auftreten eines Verbindungsfehlers 'MqttException' (MQTT-Ausnahmebedingung) versucht, die Verbindung erneut herzustellen. Für `autoRetry` ist standardmäßig der Wert 'true' festgelegt. Wenn die Verbindung mit 'MqttSecurityException' fehlschlägt, da falsche Details für die Geräteregistrierung übergeben wurden, versucht die Bibliothek nicht, die Verbindung erneut herzustellen, auch wenn für `autoRetry` die Einstellung 'true' festgelegt ist.

Zum Festlegen des Keepalive-Intervalls für MQTT können Sie vor dem Aufrufen der Funktion `connect()` optional die Methode `setKeepAliveInterval(int)` verwenden. Der Wert für `setKeepAliveInterval(int)` wird in Sekunden gemessen und definiert die maximale Länge des Zeitintervalls zwischen Nachrichten, die gesendet oder empfangen werden. Wenn ein Wert für `setKeepAliveInterval(int)` angegeben wird, kann der Client erkennen, dass der Server nicht mehr verfügbar ist, ohne das Ende des TCP/IP-Zeitlimitintervalls abzuwarten. Der Client stellt sicher, dass während jedes Keepalive-Zeitintervalls mindestens eine Nachricht im Netz unterwegs ist. Wenn während des Zeitlimitintervalls null datenbezogene Nachrichten empfangen werden, sendet der Client eine kurze Pingnachricht (`ping`), die der Server bestätigt. Für `setKeepAliveInterval(int)` wird als Wert standardmäßig '60 Sekunden' eingestellt. Um die Keepalive-Verarbeitungsfunktion auf dem  Client zu inaktivieren, legen Sie für `setKeepAliveInterval(int)` den Wert '0' fest.

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

Zum Steuern der Anzahl von Wiederholungen, die beim Auftreten eines Verbindungsfehlers erfolgen sollen, verwenden Sie die überladene Funktion 'connect(int numberOfTimesToRetry)'.

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

Sobald der Gateway-Client die Verbindung zu {{site.data.keyword.iot_short_notm}} erfolgreich hergestellt hat, kann das Gateway Ereignisse publizieren sowie Befehle für sich selbst und im Namen der Geräte subskribieren, die an das Gateway angeschlossen sind.

## Geräte registrieren, die sich hinter dem Gateway befinden
{: #register_device_gateway}

Sie können Geräte, die sich hinter dem mit Ihrer {{site.data.keyword.iot_short_notm}}-Instanz verbundenen Gateway befinden, entweder automatisch registrieren oder durch das Entwickeln von Code mithilfe der API.

### Automatische Geräteregistrierung
Sie können Ihre Geräte in {{site.data.keyword.iot_short_notm}} automatisch registrieren, sobald das Gateway für die mit ihm verbundenen Geräte Ereignisse publiziert oder Befehle subskribiert.

### Geräteregistrierung mithilfe der API
Sie können auch die {{site.data.keyword.iot_short_notm}}-API verwenden, um Geräte zu registrieren, die sich hinter einem Gateway für Ihre {{site.data.keyword.iot_short_notm}}-Instanz befinden.

Um die Entwicklungsarbeit mit der {{site.data.keyword.iot_short_notm}}-API zu vereinfachen, starten Sie eine API-Clientinstanz durch Aufrufen der Methode 'api()', wie im folgenden Codebeispiel gezeigt:

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
Sobald die Handle des API-Clients empfangen wurde, können Sie mit dem Registrieren von Geräten für ein Gateway beginnen, wie im folgenden Codebeispiel gezeigt:

```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

Beim Registrieren eines Geräts, das sich hinter einem Gateway befindet, wird das betreffende Gerät mithilfe der Attributwerte für `gwDeviceId` und `gwDeviceType` dem Gateway zugeordnet.

## Ereignisse publizieren
{: #publish_events}

Ereignisse sind der Mechanismus, mit dem Gateways und Geräte Daten in {{site.data.keyword.iot_short_notm}} publizieren. Das Gateway oder Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu. Ein Gateway kann Ereignisse von sich aus und im Namen eines beliebigen anderen Geräts publizieren, das über das Gateway verbunden ist.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gateway an. Dies bedeutet, dass ein Gateway nicht die Identität eines anderen Geräts annehmen kann.

Ereignisse können mit einer beliebigen der drei durch das MQTT-Protokoll definierten [Servicequalitätsstufen (Qos)](../../reference/mqtt/index.html#qos-levels) publiziert werden.  Standardmäßig werden Ereignisse mit der Servicequalitätsstufe '0' (Qos=0) publiziert.

### Code zum Publizieren von Gateway-Ereignissen auf der standardmäßigen Servicequalitätsstufe

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### Code zum Erhöhen der standardmäßigen Servicequalitätsstufe für ein Ereignis

Sie können die [Servicequalitätsstufen](../../reference/mqtt/index.html#qos-levels) für zu publizierende Gateway-Ereignisse erhöhen. Die Publizierung von Ereignissen, deren Servicequalitätsstufe größer als Null ist, beansprucht möglicherweise mehr Zeit, da zusätzliche Empfangsbestätigungsinformationen enthalten sind.


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### Code zum Publizieren von Ereignissen in angepassten Formaten

Ereignisse können in verschiedenen Formaten publiziert werden, beispielsweise JSON, Zeichenfolgeformat, binäres Format und weitere. Die Bibliothek publiziert Ereignisse standardmäßig im JSON-Format; Sie können die Daten jedoch in anderen Formaten angeben, falls Sie dies vorziehen. Verwenden Sie beispielsweise das folgende Code-Snippet, um Daten im Zeichenfolgeformat zu publizieren.

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**Hinweis:** Im oben stehenden Codebeispiel müssen die Nutzdaten des Ereignisses das Zeichenfolgeformat aufweisen.

XML-Daten können in das Zeichenfolgeformat konvertiert und publiziert werden, wie im folgenden Codebeispiel gezeigt:

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

Verwenden Sie ähnlich dazu die im folgenden Beispiel gezeigte Bytefeldgruppe, um Ereignisse im Binärformat zu publizieren:

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### Code zum Publizieren der Ereignisse von Geräten
{: #publishing_events_devices}

Ein Gateway kann Ereignisse im Namen eines beliebigen Geräts publizieren, das über das Gateway verbunden ist, indem die zugehörigen Typ-ID- und Geräte-ID-Werte des ursprünglichen Ereignisses übergeben werden, wie im folgenden Beispiel gezeigt:

```java

gwClient.connect()

//Zu publizierendes Ereignis generieren
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

// Ereignis im Namen des Geräts publizieren
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

Verwenden Sie die überladene Methode `publishDeviceEvent()`, um das Geräteereignis auf einer bevorzugten Servicequalitätsstufe zu publizieren. Weitere Informationen zur verwendeten Topic-Struktur finden Sie in [MQTT-Konnektivität für Gateways](../mqtt.html).

### Code zum Publizieren von Geräteereignissen mit angepasstem Format

Ähnlich wie Gateway-Ereignisse können auch Geräteereignisse in verschiedenen Formaten publiziert werden. Die Bibliothek publiziert Geräteereignisse standardmäßig im JSON-Format. Sie können die Daten jedoch in anderen Formaten angeben, falls Sie dies vorziehen. Verwenden Sie beispielsweise das folgende Code-Snippet, um Daten im Zeichenfolgeformat zu publizieren:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**Hinweis:** Die Nutzdaten des Ereignisses müssen das Zeichenfolgeformat aufweisen.

XML-Daten können in das Zeichenfolgeformat konvertiert und publiziert werden, wie im folgenden Beispiel gezeigt:

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

In ähnlicher Weise können Sie Geräteereignisse im Binärformat publizieren, indem Sie die Bytefeldgruppe verwenden, wie im folgenden Beispiel gezeigt:
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## Befehle verarbeiten
{: #handling_commands}

Das Gateway kann Befehle subskribieren, die an das Gateway selbst gerichtet sind, sowie an jedes verbundene Gerät, das sich hinter einem Gateway befindet. Der Gateway-Client subskribiert beim Herstellen einer Verbindung automatisch alle Befehle für das betreffende Gateway. Verwenden Sie zum Subskribieren der Befehle für die Geräte, die über das Gateway verbunden sind, die überladene Methode `subscribeToDeviceCommands()`, wie im folgenden Beispiel gezeigt:

```java
gwClient.connect()

// Befehle im Namen des Geräts subskribieren
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Zum Verarbeiten bestimmter Befehle müssen Sie eine Callback-Methode `Command` registrieren. Die Nachrichten werden als Instanz der Klasse `Command` (Befehl) zurückgegeben und enthalten die folgenden Eigenschaften:


| Eigenschaft     |Datentyp     | Beschreibung|
|----------------|----------------|---------------
|`deviceType`|Zeichenfolge| Der Gerätetyp, für den der Befehl empfangen wird.|
|`deviceId`|Zeichenfolge| Die Geräte-ID, für die der Befehl empfangen wird (dies kann entweder das Gateway sein oder ein Gerät, das über das Gateway verbunden ist).|
|`data`|Objekt| Die Nutzdaten des Befehls.|
|`format`|Zeichenfolge| Das Format der Nutzdaten des Befehls (dies kann eine beliebige Zeichenfolge wie 'JSON', 'binary', 'text' usw. sein).|
|`command`|Zeichenfolge|Der Name des Befehls.|
|`timestamp`|org.joda.time.DateTime|Der Zeitpunkt (Datum und Uhrzeit), an dem der Befehl gesendet wird.|

Das folgende Codebeispiel zeigt, wie die Callback-Methode `Command` implementiert werden kann:

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// Eine Warteschlange, die die Befehle enthält und verarbeitet
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
  	        Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // Code zum Verarbeiten des Befehls
  	    }
  	}

  	/**
	 * Wenn ein Gateway ein Topic von einem Gerät subskribiert oder Daten im Namen eines Geräts sendet, für
	 * das das Gateway keine Verbindungsberechtigung besitzt, wird die Nachricht oder die Subskription ignoriert.
	 * Dieses Verhalten unterscheidet sich vom Verhalten der Anwendung, die die Verbindung beenden würde.
	 * Das Gateway wird über das Topic der Benachrichtigung informiert:
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
Ist die Callback-Methode `Command` zum Gateway-Client hinzugefügt, wird stets die Methode `processCommand()` aufgerufen, wenn ein Befehl publiziert wird, der die Subskriptionsbedingungen enthält.

Das folgende Codebeispiel zeigt, wie die Callback-Methode `Command` in der Gateway-Clientinstanz hinzugefügt werden kann.

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to a device that is connected to the gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Für die Steuerung der Befehlssubskription sind überladene Methoden verfügbar.

### Geräte auflisten, die über ein Gateway verbunden sind
{: #list_devices_gw}


Um alle Geräte abzurufen, die über das angegebene Gateway (typeId, deviceId) mit {{site.data.keyword.iot_short_notm}} verbunden sind, rufen Sie die Methode `getDevicesConnectedThroughGateway()` auf.

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## Beispiele
{: #samples}

Die bereitgestellten Beispiele bieten Unterstützung beim Verbinden von Gateways und Geräten, die sich hinter Gateways befinden, mit Ihrer {{site.data.keyword.iot_short_notm}}-Instanz. Die Beispiele verwenden die {{site.data.keyword.iot_short_notm}}-Java-Clientbibliothek und sind in [Gateway-Beispiele - GitHub-Repository](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples) enthalten.

## Anleitungen
{: #recipes}

| Anleitung     | Beschreibung|
|----------------|----------------
|[Gerät als Gateway mit {{site.data.keyword.iot_short_notm}} verbinden](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/)| Ein GitHub-Projekt mit detaillierten Anweisungen, die beschreiben, wie ein Raspberry Pi-Gateway und Arduino Uno-Geräte hinter dem Gateway mit {{site.data.keyword.iot_short_notm}} verbunden werden.
|[Raspberry Pi als verwaltetes Gateway in {{site.data.keyword.iot_short_notm}} ](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/)|Eine Erweiterung der vorherigen Gateway-Anleitung, die beschreibt, wie Ihr Raspberry Pi-Gateway als verwaltetes Gerät in {{site.data.keyword.iot_short_notm}} verbunden wird und wie Gerätemanagementoperationen ausgeführt werden.
