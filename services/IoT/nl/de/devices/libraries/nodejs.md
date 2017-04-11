---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Node.js für Geräteentwickler
{: #nodejs}

Sie können die Clientbibliotheken und Beispiele in Node.js anpassen, um Gerätecode zu erstellen und zu entwickeln, der mit Ihrer Organisation in {{site.data.keyword.iot_full}} interagiert.
{:shortdesc}

Verwenden Sie die bereitgestellten Informationen und Beispiele, um mit der Entwicklung Ihrer Geräte mithilfe von Node.js zu beginnen.

## Node.js-Client und Ressourcen herunterladen
{: #node.js_client_downloads}

Wechseln Sie für den Zugriff auf die Node.js-Clientbibliotheken für {{site.data.keyword.iot_short_notm}} und auf andere verfügbare Ressourcen in das Repository [iot-nodejs ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} in GitHub und folgen Sie den Installationsanweisungen.


Weitere Informationen finden Sie in den folgenden Ressourcen:

- [Beispiele für Geräte ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window} in Github
- Das Repository [ibmiotf ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.npmjs.com/package/ibmiotf){: new_window} in NPM

## Konstruktor
{: #constructor}

Der Konstruktur erstellt die Geräteclientinstanz. Es wird eine Konfigurations-JSON akzeptiert, die die folgende Definitionen enthält:

|Definition |Beschreibung |
|:---|:---|
|`org` |Die ID Ihrer Organisation.|
|`type`  |Der Typ Ihres Geräts. In der Regel ist 'deviceType' eine Zusammenfassung von Geräten, die eine bestimmte Aufgabe ausführen, beispielsweise 'Wetterballon'.|
|`id`  |Die ID Ihres Geräts. In der Regel ist 'deviceId' bei vorgegebenem Gerätetyp eine eindeutige Kennung des betreffenden Geräts, beispielsweise die Seriennummer oder MAC-Adresse.|
|`auth-method`   |Die zu verwendende Authentifizierungsmethode. Der einzige Wert, der aktuell unterstützt ist, lautet `token`.|
|`auth-token`   |Ein Authentifizierungstoken zum Herstellen einer sicheren Verbindung zwischen Ihrem Gerät und Watson IoT Platform. Dieses Feld ist erforderlich, wenn für `auth-method` der Wert `token` eingestellt ist.|

**Hinweis:** Wenn Sie den Quickstart-Service verwenden möchten, müssen Sie nur die ersten drei Eigenschaften übergeben.

```
    var iotf = require("ibmiotf");
    var config = {
		"org" : "organization",
		"id" : "deviceId",
		"type" : "deviceType",
		"auth-method" : "token",
		"auth-token" : "authToken"
    };


    var deviceClient = new iotf.IotfDevice(config);
```

### Konfigurationsdatei verwenden

Statt die Konfiguration direkt zu übergeben, können Sie wie im folgenden Beispiel gezeigt eine JSON-Konfigurationsdatei verwenden, um die erforderlichen Konfigurationseigenschaften anzugeben:


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
Die Konfigurationsdatei `device.json` muss folgendes Format aufweisen:

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen
{: #connecting_to_iotp}

Sie können eine Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen, indem Sie die Funktion `connect` aufrufen.

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//Als Protokollebene 'debug' festlegen. Standardmäßig ist dies 'warn'
	deviceClient.log.setLevel('debug');

	deviceClient.connect();

	deviceClient.on('connect', function(){
		var i=0;
		console.log("connected");
		setInterval(function function_name () {
			i++;
			deviceClient.publish('myevt', 'json', '{"value":'+i+'}', 2);
		},2000);
	});

```

Nach dem erfolgreichen Herstellen einer Verbindung zum {{site.data.keyword.iot_short_notm}}-Service sendet der Geräteclient ein `connect`-Ereignis. Dieser Prozess bedeutet, dass sämtliche Gerätelogik innerhalb dieser Callback-Funktion implementiert werden kann.

Der Geräteclient versucht bei einem Verlust der Verbindung automatisch, die Verbindung wiederherzustellen. Wenn die Verbindungswiederholung erfolgreich ist, sendet der Client das Ereignis `reconnect`.

## Protokollierung
{: #logging}

Standardmäßig werden nur Protokollereignisse des Typs *warn* protokolliert. Wenn Sie eine höhere oder niedrigere Protokollebene einstellen möchten, verwenden Sie die Funktion 'log.setLevel'. Folgende Protokollebenen werden unterstützt:
- trace
- debug
- info
- warn
- error

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//Als Protokollebene 'debug' festlegen. Standardmäßig ist dies 'warn'
	deviceClient.log.setLevel('debug');

```


## Ereignisse publizieren
{: #publishing_events}

Ereignisse sind der Mechanismus, über den Geräte Daten in {{site.data.keyword.iot_short_notm}} publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gerät an; dies bedeutet, dass ein Gerät nicht die Identität eines anderen Geräts annehmen kann.

Sie können die Servicequalitätsstufe für zu publizierende Ereignisse erhöhen. Ereignisse, die eine höhere Servicequalitätsstufe als `0` aufweisen, benötigen für die Publizierung möglicherweise mehr Zeit, da zusätzliche Empfangsbestätigungsinformationen enthalten sind.

**Hinweis:** Der Modus für den Quickstart-Ablauf unterstützt nur Servicequalitätsstufe `0`.


Ereignisse können mit folgenden Eigenschaften publiziert werden:

|Eigenschaft |Beschreibung|
|:---|:---|
|`eventType`  | Der Typ des zu publizierenden Ereignisses, beispielsweise 'status' oder 'GPS'. |  
|`eventFormat`  |Das Format des Ereignisses, zum Beispiel 'JSON'. |
|`data`  | Die Nutzdaten des Ereignisses, bei denen es sich um eine Pufferzeichenfolge handeln muss. |
|`QoS`  | Die MQTT-Servicequalität für das zu publizierende Ereignis. Unterstützt sind die Werte '0', '1' und '2'.|


```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //Ereignis mit standardmäßiger Servicequalität publizieren
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //Ereignis mit benutzerdefinierter Servicequalität publizieren
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## Befehle verarbeiten
{: #handling_commands}

Wenn der Geräteclient eine Verbindung herstellt, subskribiert er automatisch alle für dieses Gerät geltenden Befehle. Zum Verarbeiten bestimmter Befehle müssen Sie eine Callback-Funktion für Befehle registrieren. Der Geräteclient ruft die Callback-Funktion für Befehle auf, wenn ein Befehl empfangen wird. Die Callback-Funktion weist folgende Eigenschaften auf:

|Eigenschaft |Beschreibung|
|:---|:---|
|`commandName`  | Zeichenfolge, die den Namen des aufgerufenen Befehls angibt. |  
|`format`  | Zeichenfolge, die das Format des Ereignisses (beispielsweise JSON) angibt. |
|`payload`  | Zeichenfolge, die das Datum der Nutzdaten für den Befehl angibt.  |
|`topic`  | Bei einer Publizierung als Gerät ist der Gerätetyp oder die Geräte-ID nicht in der Topic-Zeichenfolge (format_string) enthalten; diese Angaben werden aus der Client-ID übernommen.  Beispiel: `iot-2/evt/event_id/fmt/format_string`.  Wenn als Anwendung oder Gateway im Namen eines Geräts publiziert wird, muss das Topic den Gerätetyp (device_type) und die Geräte-ID (device_id) einschließen.  Beispiel: `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|


```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//Ereignis mit standardmäßiger Servicequalität publizieren
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("command", function (commandName,format,payload,topic) {
		if(commandName === "blink") {
			console.log(blink);
			//Für diesen Befehl auszuführende Funktion
			blink(payload);
		} else {
			console.log("Command not supported.. " + commandName);
		}
	});

```

## Fehlerbehandlung
{: #handling_errors}

Wenn der Geräteclient einen Fehler feststellt, sendet er das Ereignis *error*.

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//Ereignis mit standardmäßiger Servicequalität publizieren
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## Verbindung zum Client trennen
{: #disconnecting_client}

Das folgende Beispiel zeigt, wie Sie die Verbindung zum Client trennen und freigeben können:

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//Ereignis mit standardmäßiger Servicequalität publizieren
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//öÖEreignis mit benutzerdefinierter Servicequalität publizieren
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//Verbindung zum Client trennen
		client.disconnect();
	});

	....
```
