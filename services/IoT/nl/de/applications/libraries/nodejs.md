---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Node.js für Anwendungsentwickler
{: #nodejs}

Letzte Aktualisierung: 29. Juli 2016
{: .last-updated}

Sie können die Clientbibliotheken und Beispiele in Node.js anpassen, um Anwendungen zu erstellen und anzupassen, die mit Ihrer Organisation in {{site.data.keyword.iot_full}} interagieren.
{:shortdesc}

Verwenden Sie die bereitgestellten Informationen und Beispiele, um mit der Entwicklung von Anwendungen mithilfe von Node.js zu beginnen.

## Node.js-Client und Ressourcen herunterladen
{: #nodejs_client_download}

Wechseln Sie für den Zugriff auf die Java-Clientbibliotheken für {{site.data.keyword.iot_short_notm}} und auf andere verfügbare Ressourcen in das Repository [iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs) in GitHub und folgen Sie den Installationsanweisungen.


Weitere Informationen finden Sie in den folgenden Ressourcen:
- [Anwendungsbeispiele](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples) in GitHub.
- [ibmiotf](https://www.npmjs.com/package/ibmiotf) in NPM.
- Abschnitt [Referenz](#reference_nodejs) dieses Dokuments.


## Konstruktor
{: #constructor}

Der Konstruktor erstellt die Anwendungsclientinstanz und akzeptiert eine JSON-Konfigurationsdatei, die folgende Eigenschaften enthält:

| Eigenschaft     |Beschreibung     |
|----------------|----------------|
|`org` |Die ID Ihrer Organisation. Dies ist ein erforderlicher Wert.|
|`id`  |Die eindeutige ID Ihrer Anwendung innerhalb Ihrer Organisation.|
|`auth-key`   |API-Schlüssel, mit dem Sie für Ihre Anwendung eine sichere Verbindung zu Watson IoT Platform herstellen.|
|`auth-token`   |API-Schlüsseltoken, mit dem Sie für Ihr Gerät eine sichere Verbindung zu Watson IoT Platform herstellen.|
|`type`  |Der Typ der Subskription. Geben Sie `shared` an, um die gemeinsam genutzte Subskription zu aktivieren.|


Für die Verwendung von Quickstart sind nur die ersten beiden Eigenschaften erforderlich.

```
  var Client = require("ibmiotf");
	var appClientConfig = {
		"org" : orgId,
		"id" : appId,
		"auth-key" : apiKey,
		"auth-token" : apiToken
	}

	var appClient = new Client.IotfApplication(appClientConfig);
```


### Konfigurationsdatei verwenden


Statt die JSON-Eigenschaften direkt zu übergeben, können Sie wie im folgenden Codebeispiel veranschaulicht auch eine Konfigurationsdatei verwenden:

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

Stellen Sie sicher, dass die JSON-Konfigurationsdatei folgendes Format aufweist:

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen
{: #connecting_to_iotp}

Übergeben Sie wie folgt die Anforderung *connect*, um eine Verbindung zu {{site.data.keyword.iot_short_notm}} herzustellen:

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Fügen Sie hier Ihren Code hinzu
	});
```

Nach dem erfolgreichen Herstellen einer Verbindung zum {{site.data.keyword.iot_short_notm}}-Service sendet der Anwendungsclient das Ereignis `connect`, sodass innerhalb dieser Callback-Funktion eine beliebige Logik implementiert werden kann.



Der Anwendungsclient versucht bei einem Verlust der Verbindung automatisch, die Verbindung wiederherzustellen. Wenn die Verbindungswiederholung erfolgreich ist, sendet der Client das Ereignis `reconnect`.



## Protokollierung
{: #logging}

Standardmäßig werden nur Protokollereignisse des Typs `warn` protokolliert. Wenn Sie eine höhere oder niedrigere Protokollebene einstellen möchten, verwenden Sie die Funktion `log.setLevel`. Folgende Protokollebenen werden unterstützt:
- trace
- debug
- info
- warn
- error

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//Protokollebene 'trace' einstellen
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Fügen Sie hier Ihren Code hinzu
	});
```

## Gemeinsam genutzte Subskriptionen
{: #shared_subscriptions}

Verwenden Sie die Funktion für die gemeinsame Subskription, um skalierbare Anwendungen zu erstellen, die die Nachrichtenlast gleichmäßig auf mehrere Instanzen der Anwendung aufteilen. Legen Sie zum Aktivieren des Lastausgleichs für das Feld `type` die Einstellung `shared` fest, wie im folgenden Beispiel gezeigt:

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // diese Verbindung als gemeinsam genutzte Verbindung festlegen
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//Protokollebene 'trace' einstellen
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Fügen Sie hier Ihren Code hinzu
	});
```

## Fehlerbehandlung
{: #handling_errors}

Wenn der Anwendungsclient einen Fehler feststellt, wird das Ereignis `error` generiert.

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//Protokollebene 'trace' einstellen
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Fügen Sie hier Ihren Code hinzu
	});
	appClient.on("error", function (err) {
		console.log("Error : "+err);
	});
```

## Geräteereignisse subskribieren
{: #subscribing_device_events}

Ereignisse sind der Mechanismus, über den Geräte Daten in der {{site.data.keyword.iot_short_notm}}-Instanz publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gerät an; dies bedeutet, dass ein Gerät nicht die Identität eines anderen Geräts annehmen kann.


Anwendungen subskribieren standardmäßig alle Ereignisse von allen verbundenen Geräten. Steuern Sie den Bereich der Subskription mithilfe der Parameter für den Gerätetyp, die Geräte-ID, das Ereignis und das Nachrichtenformat. Folgende Codebeispiele zeigen, wie der Bereich einer Subskription mithilfe dieser Parameter definiert werden kann:

### Alle Ereignisse von allen Geräten subskribieren


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### Alle Ereignisse von allen Geräten eines bestimmten Typs subskribieren

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### Bestimmtes Ereignis von allen Geräten subskribieren


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### Bestimmtes Ereignis von mindestens zwei unterschiedlichen Geräten subskribieren

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### Alle Ereignisse subskribieren, die im JSON-Format publiziert sind


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**Hinweis**: Ein einzelner Client kann mehrere Subskriptionen unterstützen.

### Ereignisse von Geräten verarbeiten


Zum Verarbeiten der Ereignisse, die über Ihre Subskriptionen empfangen werden, implementieren Sie eine Callback-Methode für Geräteereignisse. Der {{site.data.keyword.iot_short_notm}}-Anwendungsclient sendet das Ereignis `deviceEvent`. Diese Funktion weist folgende Eigenschaften auf:

- deviceType
- deviceId
- eventType
- format
- payload
- topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
	appClient.on("deviceEvent", function (deviceType, deviceId, eventType, format, payload) {

		console.log("Device Event from :: "+deviceType+" : "+deviceId+" of event "+eventType+" with payload : "+payload);

	});
```


## Gerätestatus subskribieren
{: #subscribing_device_status}

Wenn Sie den Gerätestatus subskribieren, werden standardmäßig Statusaktualisierungen für alle verbundenen Geräte empfangen. Steuern Sie den Bereich der Subskription mithilfe der Parameter für den Typ und die ID. Ein einzelner Client kann mehrere Subskriptionen unterstützen.

### Statusaktualisierungen aller Geräte subskribieren

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### Statusaktualisierungen aller Geräte eines bestimmten Typs subskribieren


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### Statusaktualisierungen für zwei unterschiedliche Geräte subskribieren

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### Statusaktualisierungen von Geräten verarbeiten

Zum Verarbeiten der Statusaktualisierungen, die von Ihren Subskriptionen empfangen werden, implementieren Sie eine Callback-Methode für den Gerätestatus. Der {{site.data.keyword.iot_short_notm}}-Anwendungsclient sendet das Ereignis `deviceStatus`. Diese Funktion weist folgende Eigenschaften auf:

-   deviceType
-   deviceId
-   payload
-   topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
	appClient.on("deviceStatus", function (deviceType, deviceId, payload, topic) {

		console.log("Device status from :: "+deviceType+" : "+deviceId+" with payload : "+payload);

	});
```


## Ereignisse von Geräten publizieren
{: #publishing_device_events}


Anwendungen können Ereignisse so publizieren, als stammten sie von einem Gerät. Die Funktion erfordert folgende Eigenschaften:

-   deviceType
-   deviceId
-   eventType
-   format
-   data


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50};
		myData = JSON.stringify(myData);
		appClient.publishDeviceEvent("myDeviceType","device01", "myEvent", "json", myData);

	});
```


## Befehle für Geräte publizieren
{: #publishing_commands_devices}

Anwendungen können Befehle an verbundene Geräte publizieren. Die Funktion erfordert folgende Eigenschaften:

-   deviceType
-   deviceId
-   eventType
-   format
-   data

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10};
		myData = JSON.stringify(myData);
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

	});
```


## Verbindung zum Client trennen
{: #disconnect_client}

Mithilfe des folgenden Beispiels wird die Verbindung zum Client getrennt und zusätzlich werden die Verbindungen freigegeben:

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## Referenz
{: #reference_nodejs}

In der folgenden Tabelle werden die Parameter beschrieben, die in den Funktionen verwendet werden, die in der vorliegenden Node.js-Dokumentation beschrieben sind:

|Parameter|Datentyp|Beschreibung|
|:---|:---|
|`deviceType`|Zeichenfolge|Der Gerätetyp. In der Regel ist 'deviceType' eine Zusammenfassung von Geräten, die eine bestimmte Aufgabe ausführen, beispielsweise 'Wetterballon'.|
|`deviceId`|Zeichenfolge|Die ID des Geräts. In der Regel ist 'deviceId' bei vorgegebenem Gerätetyp eine eindeutige Kennung des betreffenden Geräts, beispielsweise die Seriennummer oder MAC-Adresse.|
|`eventType`|Zeichenfolge|Eine Gruppe von bestimmten Ereignissen, beispielsweise 'Status', 'Warnung' und 'Daten'.|
|`format`|Zeichenfolge|Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.  |
|`data`|Wörterverzeichnis|Die Angaben für die Nachrichtennutzdaten. Die maximale Länge beträgt 131072 Byte.|
|`payload`|Zeichenfolge|Die Angaben für die Nachrichtennutzdaten. Die maximale Länge beträgt 131072 Byte.|
|`topic`|Zeichenfolge|Bei einer Publizierung als Gerät ist der Gerätetyp oder die Geräte-ID nicht in der Topic-Zeichenfolge (format_string) enthalten; diese Angaben werden aus der Client-ID übernommen.  Beispiel: `iot-2/evt/event_id/fmt/format_string`.  Wenn als Anwendung oder Gateway im Namen eines Geräts publiziert wird, muss das Topic den Gerätetyp (device_type) und die Geräte-ID (device_id) einschließen.  Beispiel: `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|
