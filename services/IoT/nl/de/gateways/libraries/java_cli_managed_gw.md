---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-12-06"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Entwickeln verwalteter Gateways unter Verwendung von Java
{: #java_cli_managed_gw}

Gateways spielen eine wichtige Rolle bei der Verwaltung der mit ihnen verbundenen Geräte. Viele Basisgeräte verfügen nicht über Gerätemanagementfunktionen und müssen daher von einem Gateway verwaltet werden. Ein verwaltetes Gateway ist in {{site.data.keyword.iot_full}} ein Gateway, das die mit ihm verbundenen Geräte verwalten kann und Gerätemanagementfunktionen wie Firmware-, Positions- und Diagnoseaktualisierungen bereitstellt.
{:shortdesc}

Bei Verwendung der {{site.data.keyword.iot_short}} Java™-Clientbibliothek und der bereitgestellten Funktionen können Sie Java-Code entwickeln, der Ihr Gateway zu einem verwalteten Gateway macht. Darüber hinaus werden hilfreiche Beispiele zum Entwickeln von Java-Code bereitgestellt, um ein Gateway mit dem Gerätemanagementservice zu verbinden und Gerätemanagementoperationen auszuführen.

## Gerätemanagementservice
{: #dm_service}

Der Gerätemanagementservice (Device Management, DM) von {{site.data.keyword.iot_short}} stellt Gerätemanagementfunktionen bereit, die Gateways das Verwalten der mit ihnen verbundenen Geräte ermöglichen.

Ein verwaltetes Gateway führt einen Gerätemanagementagenten aus, der als Proxy für alle Geräte ausgeführt wird, die über das Gateway eine Verbindung zu {{site.data.keyword.iot_short}} herstellen.

### Gerätemanagementagent

Geräte, die indirekt über ein Gateway die Verbindung zu {{site.data.keyword.iot_short}} herstellen, können verschiedene Verbindungsprotokolle verwenden, sofern diese von dem Gateway-Gerät unterstützt werden.

Die Instanz `ManagedGateway` ist ein Gerätemanagementagent, der eine Liste der Methoden zum Durchführen einer oder mehrerer Gerätemanagementaktionen bereitstellt (z. B. das Teilnehmen an Gerätemanagementaktivitäten, das Aktualisieren von Fehlercodes, Protokollen und Position sowie Firmware- oder Geräteaktionen).

Der Gerätemanagementagent in dem Gateway konvertiert und verarbeitet das Verbindungsprotokoll der Geräte, die Verbindungen herstellen, und stellt damit sicher, dass das Gerät von {{site.data.keyword.iot_short}} verwaltet werden kann. Durch den Gerätemanagementagenten wird das Gateway mehr als nur ein transparenter Tunnel zwischen dem angeschlossenen Gerät und {{site.data.keyword.iot_short}}. Wenn ein mit einem Gateway verbundenes Gerät beispielsweise nicht in der Lage ist, Firmware herunterzuladen, kann der Gerätemanagementagent im Gateway die folgenden Aktionen ausführen:
- Anforderung zum Herunterladen von Firmware für ein Gerät abfangen
- Firmware für das Gerät herunterladen
- Firmware des Gerät im Gateway speichern

Wenn das Gerät später ein Upgrade anfordert, kann der Gerätemanagementagent im Gateway die Firmware mit einer Push-Operation an das Gerät übermitteln und das Update durchführen.

## Erstellen des Gerätemodells
{: #create_device_model}

In {{site.data.keyword.iot_short}} beschreibt das Gerätemodell die Metadaten und die Managementmerkmale für Geräte und Gateways. Die Gerätedatenbank ist die Masterquelle für Geräte- und Gateway-Informationen. Anwendungen und verwaltete Geräte können Positionsaktualisierungen, Fortschrittsaktualisierungen für Firmware-Upgrades und andere Aktualisierungstypen senden. Sobald Aktualisierungen von {{site.data.keyword.iot_short}} empfangen werden, wird die Gerätedatenbank aktualisiert, um die Informationen für verbundene Anwendungen verfügbar zu machen.

In {{site.data.keyword.iot_short}}-Java-Clientbibliothek wird das Gerätemodell durch die Java-Classe `DeviceData` dargestellt.

Erstellen Sie die folgenden Objekte, um die Klasse `DeviceData` zu erstellen: 

- `DeviceInfo` (optional)
- `DeviceLocation` (optional; nur erforderlich, wenn das Gerät über die Position benachrichtigt werden möchte, die von der Anwendung durch die {{site.data.keyword.iot_short}}-API festgelegt wird)
- `DeviceFirmware` (optional)
- `DeviceMetadata` (optional)

Weitere Informationen finden Sie in [Gerätemodell](../../reference/device_model.html).

### DeviceInfo

Das folgende Code-Snippet mit Beispieldaten zeigt, wie die Objekte `DeviceInfo` und `DeviceMetadata` erstellt werden:

```java
DeviceInfo deviceInfo = new DeviceInfo.Builder().
                           serialNumber("10087").
                           manufacturer("IBM").
                           model("7865").
                           deviceClass("A").
                           description("My RasPi Device").
                           fwVersion("1.0.0").
                           hwVersion("1.0").
                           descriptiveLocation("EGL C").
                           build();

/**
  * Erstellen Sie ein DeviceMetadata-Objekt
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);

```

Das folgende Code-Snippet zeigt, wie die Klasse `DeviceData` unter Verwendung der im vorherigen Beispiel erstellten Objekte `DeviceInfo` und `DeviceMetadata` erstellt wird:

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();
```

Jedes Gateway und jedes angeschlossene Gerät muss über eine eigene Klassendefinition `DeviceData` verfügen, die das jeweilige Gerät in {{site.data.keyword.iot_short}} darstellt. Für Gateways wird die Klasse `DeviceData` beim Erstellen der Instanz `ManagedGateway` an die Bibliothek übergeben. Für angeschlossene Geräte wird die Klasse `DeviceData` als Teil des Objekts `sendDeviceManageRequest()` an die Bibliothek übergeben.

## Konstruktoren für verwaltete Gateways
{: #construct_managed_gateway}

`ManagedGateway` ist eine Java-Klasse, die ein Gateway als verwaltetes Gateway mit {{site.data.keyword.iot_short}} verbindet, das mindestens eine Gerätemanagementoperation entweder für sich selbst oder für die angeschlossenen Geräte ausführen kann. Eine Instanz von `ManagedGateway` kann auch verwendet werden, um normale Gateway-Operationen auszuführen (z. B. Publizieren von Gateway- oder Geräteereignissen und Empfangen von Anwendungsbefehlen). Die Instanz `ManagedGateway` ist ein Gerätemanagementagent.

In der Klasse `ManagedGateway` unterstützen die beiden Konstruktoren (Konstruktor 1 und Konstruktor 2) unterschiedliche Benutzermuster.

### Konstruktor 1

Konstruktor 1 erstellt eine Instanz `ManagedGateway`, indem eine Klasse `DeviceData` akzeptiert wird, die alle folgenden Eigenschaften enthält:

| Eigenschaft     |Beschreibung     |
|----------------|----------------|
|`Organization-ID` |Die ID Ihrer Organisation.|
|`Gateway-Type` |Der Typ Ihres Gateway-Geräts.|
|`Gateway-ID` |Die ID des Gateway-Geräts.|
|`Authentication-Method`|Die Methode der Authentifizierung. Die einzige Methode, die unterstützt wird, lautet "token".|
|`Authentication-Token`|Das API-Schlüsseltoken.|
|`auth-key`   |Optionaler API-Schlüssel, den Sie angeben müssen, wenn `apikey` als Wert für 'auth-method' festgelegt ist.|
|`auth-token`   |API-Schlüsseltoken, das ebenfalls erforderlich ist, wenn Sie `apikey` als Wert für 'auth-method' festlegen. |
|`clean-session`|Der Wert 'true' oder 'false', der nur erforderlich ist, wenn Sie das Gateway im Modus für permanente Subskription verbinden möchten. Die Standardeinstellung für `clean-session` lautet `true`.|
|`Port`|Die Nummer des Ports, zu dem eine Verbindung hergestellt werden soll. Geben Sie entweder 8883 oder 443 an. Wenn Sie keine Portnummer angeben, stellt der Client standardmäßig eine Verbindung zu {{site.data.keyword.iot_short_notm}} über den Port Nummer 8883 her.|
|`WebSocket`|Der Wert 'true' oder 'false', der nur erforderlich ist, wenn Sie das Gateway über Web-Sockets verbinden möchten.|
|`MaxInflightMessages`  |Legt die maximale Anzahl der gerade ausgeführten Nachrichten für die Verbindung fest. Der Standardwert ist 100.|
|`Automatic-Reconnect`  |Der Wert 'true' oder 'false', der erforderlich ist, wenn Sie das Gerät automatisch erneut mit {{site.data.keyword.iot_short_notm}} verbinden möchten, während es sich im nicht verbundenen Status befindet. Der Standardwert ist 'false'.|
|`Disconnected-Buffer-Size`|Die maximale Anzahl Nachrichten, die im Speicher gespeichert werden kann, während die Verbindung zum Client getrennt ist. Der Standardwert ist '5000'.|

**Hinweis:** Um das Gateway im Modus für permanente Subskription zu verbinden, legen Sie für `clean-session` die Einstellung `false` fest. Weitere Informationen zur Eigenschaft `clean-session` finden Sie im Abschnitt 'Subskriptionspuffer und bereinigte Sitzung' der [MQTT-Dokumentation](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

Der folgende Code umreisst, wie Sie eine Instanz `ManagedGateway` erstellen können:

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### Konstruktor 2

Konstruktor 2 erstellt eine Instanz `ManagedGateway`, indem ein Objekt `DeviceData` und die MQTT-Clientinstanz akzeptiert wird. Konstruktor 2 setzt außerdem voraus, dass das Ojekt `DeviceData` in der Instanz den Gerätetyp und die Geräte-ID enthält, wie im folgenden Codebeispiel dargestellt:

```java
// Code zum Erstellen einer synchronen oder asynchronen MQTT-Clientinstanz von mqttClient.
.....

// Code zum Erstellen des Objekts 'DeviceData'
DeviceData deviceData = new DeviceData.Builder().
                         typeId("Gateway-Type").
                         deviceId("Gateway-ID").
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();

....
ManagedGateway ManagedGateway = new ManagedGateway(mqttClient, deviceData);

```

**Hinweis:** Verwenden Sie zum Entwickeln von Code für angepasste Geräte den Konstruktor 2, da dieser Konstruktor eine verwaltete Gateway-Instanz unter Verwendung der vorhandenen verbundenen MQTT-Clientinstanz erstellt, damit Gerätemanagementoperationen genutzt werden können. Verwenden Sie für alle Gerätefunktionen die Java-Clientbibliothek.

## Gerätemanagementanforderungen von einem Gateway
{: #dm_requests}

### Senden einer Managementanforderung von einem Gateway

Um das Gateway anzuweisen, an Gerätemanagementaktivitäten mitzuwirken, rufen Sie die Methode `sendGatewayManageRequest()` auf, die im folgenden Codebeispiel dargestellt wird:

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
Die Managementanforderung initiiert intern eine Verbindungsanforderung, wenn für das Gerät noch keine Verbindung zu {{site.data.keyword.iot_short}} besteht.

Die Methode `sendGatewayManageRequest()` akzeptiert die folgenden Parameter:

| Parameter     |Beschreibung     |
|----------------|----------------|
|`lifetime`|Gibt den Zeitraum in Sekunden an, in dem das Gateway eine weitere Anforderung des Typs 'Gerät verwalten' senden muss, um nicht als 'ruhend' klassifiziert und damit zu einem nicht verwalteten Gerät zu werden. Wenn das Feld `lifetime` nicht angegeben oder auf '0' gesetzt wird, wird das verwaltete Gateway nicht als 'ruhend' klassifiziert. Der für das Feld `lifetime` unterstützte Mindestwert lautet '3600' Sekunden (eine Stunde).|
|`supportFirmwareActions`|Ein Wert 'true' oder 'false', der festlegt, ob das Gateway Firmwareaktionen unterstützt. Das Gateway muss außerdem einen Firmwarehandler zum Abwickeln der Firmwareanforderungen hinzufügen.|
|`supportDeviceActions`|Ein Wert 'true' oder 'false', der festlegt, ob das Gateway Geräteaktionen unterstützt. Das Gateway muss außerdem einen Geräteaktionshandler hinzufügen, der Warmstartanforderungen und Anforderungen zum Zurücksetzen auf die Werkseinstellungen abwickelt.|


Die Instanz `ManagedGateway` ist ein Gerätemanagementagent, der eine Liste der Methoden zum Durchführen einer oder mehrerer Gerätemanagementaktionen bereitstellt (z. B. das Teilnehmen an Gerätemanagementaktivitäten, das Aktualisieren von Fehlercodes, Protokollen und Position sowie Firmware- oder Geräteaktionen).

### Senden einer Managementanforderung von angeschlossenen Geräten

Um Geräten, die hinter einem Gateway verbunden sind, die Teilnahme an Gerätemanagementaktivitäten zu ermöglichen, rufen Sie die Methode `sendDeviceManageRequest()` auf.

Die Methode `sendDeviceManageRequest()` akzeptiert die Details der angeschlossenen Geräte sowie die Parameter `lifetime`, `supportFirmwareActions` und `supportDeviceActions`. Ein Gateway kann außerdem die überladene Methode `sendDeviceManageRequest()` verwenden, um das Objekt `DeviceData` für das angeschlossene Gerät zu definieren.

#### Beispiel für das Senden einer Managementanforderung von angeschlossenen Geräten

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### Senden einer Managementbeendigungsanforderung von einem Gateway

Wenn ein Gateway nicht länger verwaltet werden muss, rufen Sie zum Stoppen der Gerätemanagementaktivitäten im Gateway die Methode `sendGatewayUnmanageRequet()` auf. Sobald `sendGatewayUnmanageRequet()` aufgerufen wird, sendet {{site.data.keyword.iot_short}} keine weiteren neuen Gerätemanagementanforderungen für das Gateway und alle Gerätemanagementanforderungen von dem Gateway werden abgelehnt (mit Ausnahme von **Manage**-Anforderungen). Anforderungen von Geräten hinter dem Gateway werden nicht abgelehnt.

#### Beispiel für das Senden einer Managementbeendigungsanforderung von einem Gateway

```java
managedGateway.sendGatewayUnmanageRequet();
```

### Senden einer Managementbeendigungsanforderung von angeschlossenen Geräten

Wenn ein Gerät, das sich hinter einem Gateway befindet, nicht länger verwaltet werden muss, kann das Gateway die Methode `sendDeviceUnmanageRequet()` aufrufen, um das Gerät aus einem verwalteten Status in einen nicht verwalteten Status zu versetzen. Sobald `sendDeviceUnmanageRequet()` aufgerufen wird, sendet {{site.data.keyword.iot_short}} keine weiteren neuen Gerätemanagementanforderungen für das Gerät und alle Gerätemanagementanforderungen von dem Gateway für die angeschlossenen Geräte werden abgelehnt (mit Ausnahme von **Manage**-Anforderungen).

#### Beispiel für das Senden einer Managementbeendigungsanforderung von angeschlossenen Geräten

```java
managedGateway.sendDeviceUnmanageRequet();
```

## Positionsaktualisierungen
{: #location_updates}

### Senden von Gateway-Positionsaktualisierungen

Für Gateways, die ihre Position bestimmen können, kann ausgewählt werden, dass {{site.data.keyword.iot_short}} über Positionsänderungen benachrichtigt wird. Das Gateway kann eine der überladenen Methoden `updateLocation()` aufrufen, um die Position des Geräts zu aktualisieren.

```java
    // Position mit Längengrad, Breitengrad und Höhenangabe aktualisieren.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### Senden von Positionsaktualisierungen für angeschlossene Geräte

Das Gateway kann die entsprechende Methode `updateDeviceLocation()` für Geräte aufrufen, um die Position der angeschlossenen Geräte zu aktualisieren. Die überladene Methode kann verwendet werden, um die Methode `measuredDateTime` anzugeben.  

```java
// Position des angeschlossenen Geräts mit Längengrad, Breitengrad und Höhe aktualisieren.
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
Weitere Informationen zu Positionsaktualisierungen finden Sie in [Gerätemanagementanforderungen](../../devices/device_mgmt/index.html#/update-location#update-location).

## Behandlung von Fehlercodes
{: #errors}

### Erstellen und Löschen von Gateway-Fehlercodes

Für ein Gateway kann ausgewählt werden, dass {{site.data.keyword.iot_short}} über Änderungen des Gateway-Fehlerstatus benachrichtigt wird. Das Gateway kann die Methode `addErrorCode()` aufrufen, um den aktuellen Fehlercode in {{site.data.keyword.iot_short}} hinzuzufügen.

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

Fehlercodes für ein Gateway können aus {{site.data.keyword.iot_short}} gelöscht werden, indem die Methode `clearErrorCodes()` wie folgt aufgerufen wird:

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### Erstellen und Löschen von Fehlercodes für angeschlossene Geräte

Ein Gateway kann auch die entsprechende Gerätemethode aufrufen, um Fehlercodes für die angeschlossenen Geräte hinzuzufügen oder zu löschen: 

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### Erstellen und Löschen von Gateway-Protokollnachrichten

Für ein Gateway kann ausgewählt werden, dass {{site.data.keyword.iot_short}} durch Hinzufügen eines neuen Protokolleintrags über Änderungen benachrichtigt wird. Ein Protokolleintrag enthält die folgenden Elemente:

- Nachrichtenzeichenfolge
- Zeitmarke
- Schweregrad
- (Optional) Binäre Diagnosedaten mit Base64-Codierung

Gateways können die Methode `addGatewayLog()` aufrufen, um Protokollnachrichten zu senden, wie im folgenden Beispiel gezeigt:

```java
// Beispiel für ein Protokollereignis
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

Zum Löschen von Protokollnachrichten aus {{site.data.keyword.iot_short}} kann die Methode `clearLogs()` aufgerufen werden:

```java
rc = managedGateway.clearGatewayLogs();
```

### Erstellen und Löschen von Protokollen für angeschlossene Geräte

In ähnlicher Weise kann das Gateway die entsprechende Gerätemethode zum Erstellen oder Löschen der Protokolle für die angeschlossenen Geräte aufrufen, wie im folgenden Codebeispiel gezeigt:

```java

// Beispiel für ein Protokollereignis:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

Um die Protokolle für angeschlossene Geräte zu löschen, rufen Sie die Methode `clearDeviceLogs()` auf und geben Sie die Details des angeschlossenen Geräts an, wie im folgenden Codebeispiel gezeigt:

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

Die Operationen zur Gerätediagnose sollen Informationen zu Gateway- oder Gerätefehlern bereitstellen. Sie stellen keine Diagnoseinformationen für die Verbindung eines Geräts mit {{site.data.keyword.iot_short}} bereit.

Weitere Informationen zu Diagnoseoperation finden Sie in [Gerätemanagementanforderungen](../../devices/device_mgmt/index.html#/update-location#update-location).

## Firmware-Updates und -Aktionen
{: #firmware}

Der Prozess für das Firmware-Update ist in zwei separate Aktionen aufgeteilt: 

- Herunterladen der Firmware
- Aktualisieren der Firmware

Das Gateway muss die folgenden Aktivitäten ausführen, um eigene Firmwareaktionen und Firmwareaktionen für die angeschlossenen Geräte zu unterstützen: 

1. Optional: Ein Objekt `DeviceFirmware` erstellen
2. Den Server über die Unterstützung der Firmwarekation informieren
3. Den Handler für Firmwareaktionen erstellen
4. Den Handler in `ManagedGateway` hinzufügen

### Schritt 1: Objekt `DeviceFirmware` erstellen

Zum Ausführen von Firmwareaktionen kann ein Gateway optional ein Objekt `DeviceFirmware` für den eigenen Bedarf und für die angeschlossenen Geräte erstellen und dieses Objekt zu dem Objekt `DeviceData` hinzufügen, wie im folgenden Beispiel gezeigt:

```java
DeviceFirmware firmware = new DeviceFirmware.Builder().
			version("Firmware.version").
			name("Firmware.name").
			url("Firmware.url").
			verifier("Firmware.verifier").
			state(FirmwareState.IDLE).				
			build();

DeviceData deviceData = new DeviceData.Builder().
			deviceInfo(deviceInfo).
			deviceFirmware(firmware).
			metadata(metadata).
			build();

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
managedGateway.connect();
```

Das erstellte Objekt `DeviceData` für die angeschlossenen Geräte kann beim Senden der Managementanforderung an die Bibliothek übergeben werden, wie im folgenden Codebeispiel gezeigt:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

Das Objekt `DeviceFirmware` stellt die aktuelle Firmware des Gateways oder des angeschlossenen Geräts dar und wird zum Berichten des Status für die Aktionen 'Firmware-Download' und 'Firmware-Update' an {{site.data.keyword.iot_short}} verwendet. Wenn das Objekt `DeviceFirmware` nicht vom Gateway erstellt wird, erstellt die Bibliothek ein leeres Objekt und berichtet den Status an {{site.data.keyword.iot_short}}.

### Schritt 2: Den Server über die Firmwareaktionsunterstützung informieren

Für das Gateway oder die angeschlossenen Geräte muss das Aktionsflag für Firmware auf 'true' eingestellt werden, damit der Server die Firmwareanforderung aufruft. Diese Änderung kann durch Übergeben des Werts 'true' für den Parameter `supportFirmwareActions` in der Managementanforderung vorgenommen werden.

Das Gateway kann die folgende Methode aufrufen, um den Server über die Firmwareunterstützung zu informieren:
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

Auf ähnliche Weise kann das Gateway die entsprechende Gerätemethode aufrufen, um über die Firmwareunterstützung von angeschlossenen Geräten zu informieren:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

Wenn der Gerätemanagementserver über die Unterstützung informiert ist, leitet der Server die Firmwareaktionen (für das Gateway oder für die dahinter liegenden Geräte) anschließend an das Gateway weiter.

### Schritt 3: Den Handler für Firmwareaktionen erstellen

Zum Unterstützen der Firmwareaktion muss das Gateway einen Handler erstellen und zu `managedGateway` hinzufügen. Der Handler muss eine `DeviceFirmwareHandler`-Klasse erweitern und die folgenden Methoden implementieren:

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**Hinweis**: Für das Gateway und die angeschlossenen Geräte darf nur ein einziger Handler zur Bibliothek hinzugefügt werden, an den die Download- oder Aktualisierungsanforderungen für Firmware umgeleitet werden. Bei der Implementierung muss ein Thread erstellt werden oder ein Thread-Pool, der mehrere Firmwareanforderungen gleichzeitig verarbeitet. 

Eine Beispielimplementierung für einen Thread-Pool-Handler finden Sie in [Gateway-Beispiele - GitHub-Repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Beispielimplementierung von `downloadFirmware`

Durch die Implementierung muss Logik hinzugefügt werden, um die Firmware herunterzuladen und den Status des Downloads mithilfe eines Objekts `DeviceFirmware` zu berichten. Wenn die Downloadoperation für die Firmware erfolgreich ist, sollte der Status der Firmware auf 'DOWNLOADED' und die Eigenschaft `UpdateStatus` auf 'SUCCESS' festgelegt werden.

Wenn während des Firmware-Downloads ein Fehler auftritt, muss der Status auf 'IDLE' und die Eigenschaft `updateStatus` auf einen der folgenden Fehlerstatuswerte festgelegt werden:

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

Das folgende Codebeispiel zeigt eine Beispielimplementierung für den Firmware-Downlaod:

**Wichtig:** In dem bereitgestellten Codebeispiel fehlt der Abschnitt für den Thread-Pool. Eine vollständige Beispielimplementierung für den Firmware-Handler finden Sie in [IBM Java-Gatewaybeispiel - GitHub-Repository ](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

```java
public void downloadFirmware(DeviceFirmware deviceFirmware) {
	boolean success = false;
    URL firmwareURL = null;
    URLConnection urlConnection = null;

	try {
		firmwareURL = new URL(deviceFirmware.getUrl());
        urlConnection = firmwareURL.openConnection();
        if(deviceFirmware.getName() != null) {
			downloadedFirmwareName = deviceFirmware.getName();
        } else {
			// Die Zeitmarke als Name verwenden
			downloadedFirmwareName = "firmware_" +new Date().getTime()+".deb";
		}

		File file = new File(downloadedFirmwareName);
		BufferedInputStream bis = new BufferedInputStream(urlConnection.getInputStream());
		BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(file.getName()));

		int data = bis.read();
        if(data != -1) {
			bos.write(data);
            byte[] block = new byte[1024];
            while (true) {
				int len = bis.read(block, 0, block.length);
                if(len != -1) {
					bos.write(block, 0, len);
                } else {
					break;
                }
			}
            bos.close();
            bis.close();
            success = true;
        } else {
			//Da keine Daten zum Lesen vorliegen, legen Sie einen Fehler fest
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
        }
	} catch(MalformedURLException me) {
		// Ungültige URL, legen Sie als Status etwas fest, dass dies widerspiegelt
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
    } catch (IOException e) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.CONNECTION_LOST);
    } catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }

    if(success == true) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
        deviceFirmware.setState(FirmwareState.DOWNLOADED);
    } else {
		deviceFirmware.setState(FirmwareState.IDLE);
    }
}
```

Ein verwaltetes Gateway kann die Integrität des heruntergeladenen Firmware-Image mithilfe der Verifizierung prüfen und den Status zurück an {{site.data.keyword.iot_short}} berichten. Die Verifizierung kann in den folgenden Phasen vom Gateway festgelegt werden:

- Beim Start während der Erstellung des Objekts 'DeviceFirmware'
- Beim Übermitteln einer Anforderung 'downloadFirmware' durch eine Anwendung

#### Beispiel

```java
private boolean verifyFirmware(File file, String verifier) throws IOException {
	FileInputStream fis = null;
    String md5 = null;
    try {
		fis = new FileInputStream(file);
        md5 = org.apache.commons.codec.digest.DigestUtils.md5Hex(fis);
        System.out.println("Downloaded Firmware MD5 sum:: "+ md5);
    } catch (FileNotFoundException e) {
		e.printStackTrace();
    } catch (IOException e) {
		e.printStackTrace();
    } finally {
		fis.close();
    }
    if(verifier.equals(md5)) {
		System.out.println("Firmware verification successful");
		return true;
	}
	System.out.println("Download firmware checksum verification failed."
			+ "Expected "+verifier + " found "+md5);
    return false;
}
```

Sie finden den vollständigen Code im Gatewaymanagementbeispiel [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Beispielimplementierung von `updateFirmware`

Durch die Implementierung muss ein separater Thread erstellt und Logik hinzugefügt werden, um die heruntergeladene Firmware zu installieren und den Status der Aktualisierung mithilfe des Objekts `DeviceFirmware` zu berichten. Wenn die Updateoperation für die Firmware erfolgreich ist, muss der Status auf 'IDLE' und die Eigenschaft `updateStatus` auf 'SUCCESS' festgelegt werden.

Wenn während eines Firmware-Updates ein Fehler auftritt muss der Wert `updateStatus` auf einen der folgenden Fehlerstatuswerte festgelegt werden:

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

Das folgende Codebeispiel zeigt, wie ein Firmware-Update für ein Raspberry Pi-Gerät implementiert werden kann:

```java
public void updateFirmware(DeviceFirmware deviceFirmware) {
	try {
		ProcessBuilder pkgInstaller = null;
        Process p = null;
        pkgInstaller = new ProcessBuilder("sudo", "dpkg", "-i", downloadedFirmwareName);
        boolean success = false;
        try {
			p = pkgInstaller.start();
            boolean status = waitForCompletion(p, 5);
            if(status == false) {
				p.destroy();
                deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
                return;
            }
            System.out.println("Firmware Update command "+status);
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
            deviceFirmware.setState(FirmwareState.IDLE);
        } catch (IOException e) {
			e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        } catch (InterruptedException e) {
			e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        }
	} catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }
}
```

Sie finden den vollständigen Code im Beispiel `GatewayFirmwareHandlerSample` in [Gateway-Beispiele - GitHub-Repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Schritt 4: Den Handler in `ManagedGateway` hinzufügen

Wenn ein Handler erstellt wurde, muss er zur Instanz `ManagedGateway` hinzugefügt werden, damit die Java-Clientbibliothek die entsprechende Methode aufruft, wenn eine Firmwareaktionsanforderung von {{site.data.keyword.iot_short}} vorliegt.

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

Weitere Informationen zu Firmwareaktionen finden Sie in [Gerätemanagementanforderungen](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions).

## Geräteaktionen
{: #dev_actions}

{{site.data.keyword.iot_short}} unterstützt die folgenden Geräteaktionen:

- Neu starten
- Zurücksetzen auf Werkseinstellungen

Das Gateway muss die folgenden Aktivitäten ausführen, um eigene Geräteaktionen und Geräteaktionen für die angeschlossenen Geräte hinter dem Gateway zu unterstützen:

1. Den Server über die Unterstützung der Geräteaktionen informieren
2. Den Handler für Geräteaktionen erstellen
3. Den Handler in `ManagedGateway` hinzufügen

### Schritt 1: Den Server über die Unterstützung der Geräteaktionen informieren

Vor dem Ausführen einer Neustartaktion oder einer Aktion zum Zurücksetzen auf Werkseinstellungen für ein Gateway und die angeschlossenen Geräte muss das Gateway zunächst {{site.data.keyword.iot_short}} über die Unterstützung informieren. DieseMaßnahme Aktion kann durch Übergeben des Werts 'true' für den Parameter `supportDeviceActions` beim Senden der Anforderung **Manage** erfolgen.

Ein Gateway kann die folgende Methode aufrufen, um den Server über die Unterstützung der Geräteaktion zu informieren. 

```java
// Der letzte Parameter gibt die Unterstützung der Geräteaktion an
managedGateway.sendGatewayManageRequest(3600, true, true);
```

Ein Gateway kann die entsprechende Gerätemethode aufrufen, um über die Unterstützung der Geräteaktion von angeschlossenen Geräten zu informieren:

```java
// Der letzte Parameter gibt die Unterstützung der Geräteaktion an
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

Wenn der Gerätemanagerserver über die Unterstützung informiert ist, leitet der Server die Geräteaktionsanforderungen an das Gerät weiter.

### Schritt 2: Den Handler für Geräteaktionen erstellen

Zum Unterstützen der Geräteaktion muss das Gateway einen Handler erstellen und ihn zur Instanz `managedGateway` hinzufügen. Der Handler muss eine `DeviceActionHandler`-Klasse erweitern und die Implementierung der folgenden Methoden bereitstellen:

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**Hinweis:** Für das Gateway und die angeschlossenen Geräte darf nur ein einziger Handler zur Bibliothek hinzugefügt werden, an den die Geräteaktionsanforderungen umgeleitet werden. Bei der Implementierung muss ein Thread erstellt werden oder ein Thread-Pool, der mehrere Geräteaktionsanforderungen gleichzeitig verarbeitet. Eine Beispielimplementierung mit einem Thread-Pool finden Sie in [IoT-Gateway-Beispiele - GitHub-Repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java).

### Beispielimplementierung von `handleReboot`

Durch die Implementierung muss ein separater Thread erstellt und Logik hinzugefügt werden, um das Gateway und das angeschlossene Gerät neu zu starten und den Status des Neustarts mithilfe eines Objekts `DeviceAction` zu berichten. Nachdem die Anforderung empfangen wurde, muss das Gateway zunächst den Server über die Unterstützung oder den Fehler informieren, bevor der Neustart durchgeführt wird. Wenn das Beispiel keinen Neustart für das Gerät durchführen kann oder beim Neustart ein anderer Fehler auftritt, kann das Gateway den Status in einer optionalen Nachricht aktualisieren. Das folgende Codebeispiel stellt eine Beispielimplementierung für den Neustart eines Raspberry Pi-Geräts bereit:

```java
public void handleReboot(DeviceAction action) {
	ProcessBuilder processBuilder = null;
    Process p = null;
    processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
    boolean status = false;
    try {
		p = processBuilder.start();
        // Warten Sie ca. 2 Minuten, bevor Sie es aufgeben
        status = waitForCompletion(p, 2);
    } catch (IOException e) {
		action.setMessage(e.getMessage());
    } catch (InterruptedException e) {
		action.setMessage(e.getMessage());
    }
    if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

Die vollständige Beispielimplementierung eines Handlers, der einen Thread-Pool verwendet, finden Sie in [IoT-Gateway-Beispiele - GitHub-Repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java).


### Beispielimplementierung von `handleFactoryReset`

Durch die Implementierung muss ein separater Thread erstellt und Logik hinzugefügt werden, um das Gateway und das angeschlossene Gerät auf die Werkseinstellungen zurückzusetzen und den Status der Zurücksetzung mithilfe des Objekts 'DeviceAction' zu berichten. Nachdem die Anforderung empfangen wurde, muss das Gateway zunächst den Server über die Unterstützung oder den Fehler informieren, bevor das Zurücksetzen durchgeführt wird. Der allgemeine Ablauf der Implementierung für das Zurücksetzen wird im folgenden Codebeispiel gezeigt: 

```java
public void handleFactoryReset(DeviceAction action) {
	try {
		// Code für die Ausführung von 'Zurücksetzen auf Werkseinstellungen'
    } catch (IOException e) {
		action.setMessage(e.getMessage());
    }
    if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

### Schritt 3: Den Handler in `ManagedGateway` hinzufügen

Wenn ein Handler erstellt wurde, muss er zur Instanz `ManagedGateway` hinzugefügt werden, damit die Java-Clientbibliothek die entsprechende Methode aufruft, wenn eine Geräteaktionsanforderung von {{site.data.keyword.iot_short}} für das Gateway oder für angeschlossene Geräte vorliegt.

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

Weitere Informationen zu Geräteaktionen finden Sie in [Gerätemanagementanforderungen](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot).

## Empfangsbereitschaft für Geräteattributänderungen
{: #listen_device_attributes}

Durch die Java-Clientbibliothek werden die entsprechenden Objekte jedes Mal aktualisiert, wenn eine Aktualisierungsanforderung von {{site.data.keyword.iot_short}} vorliegt. Diese Aktualisierungsanforderungen werden von der Anwendung entweder direkt oder indirekt durch ein Firmware-Update über die {{site.data.keyword.iot_short}}-REST-API initiiert. Neben der Aktualisierung dieser Attribute stellt die Bibliothek einen Mechanismus bereit, mit dem das Gateway benachrichtigt werden kann, sobald ein Geräteattribut aktualisiert wird.

Mit diesem Operationstyp können die Attribute für Position, Metadaten, Geräteinformationen und Firmware des Gateways oder der angeschlossenen Geräte aktualisiert werden.

Um über Attributänderungen benachrichtigt zu werden, muss das Gateway eine Änderungslistener für Eigenschaften zu den Objekten hinzufügen, die von Interesse sind, wie im folgenden Codebeispiel gezeigt: 

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

Das Gateway muss außerdem die Methode `propertyChange()` an der Position implementieren, an der die Benachrichtigung empfangen wird, wie in der folgenden Beispielimplementierung gezeigt:

```java
public void propertyChange(PropertyChangeEvent evt) {
	if(evt.getNewValue() == null) {
		return;
	}
	Object value = (Object) evt.getNewValue();
		switch(evt.getPropertyName()) {
		case "metadata":
            DeviceMetadata metadata = (DeviceMetadata) value;
            System.out.println("Received an updated metadata -- "+ metadata);
            break;

			case "location":
            DeviceLocation location = (DeviceLocation) value;
            System.out.println("Received an updated location -- "+ location);
            break;

			case "deviceInfo":
            DeviceInfo info = (DeviceInfo) value;
            System.out.println("Received an updated device info -- "+ info);
            break;

			case "mgmt.firmware":
            DeviceFirmware firmware = (DeviceFirmware) value;
            System.out.println("Received an updated device firmware -- "+ firmware);
            break;
    }
}
```

Weitere Informationen zum Aktualisieren der Geräteattribute finden Sie in [Gerätemanagementanforderungen](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes).

## Beispiele
{: #samples}

Die bereitgestellten Beispiele bieten Unterstützung beim Verbinden von Gateways und Geräten, die sich hinter Gateways befinden, mit Ihrer {{site.data.keyword.iot_short_notm}}-Instanz. Die Beispiele verwenden die {{site.data.keyword.iot_short_notm}}-Java-Clientbibliothek und sind in [Gateway-Beispiele - GitHub-Repository](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples) enthalten.

## Anleitungen
{: #recipes}

Eine Anleitung zum Verbinden eines Rasberry Pi-Geräts als verwaltetes Gateway mit {{site.data.keyword.iot_short_notm}} und zum Verwalten der angeschlossenen Geräte finden Sie in [Raspberry Pi als verwaltetes Gateway in {{site.data.keyword.iot_short_notm}} ](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/).

In dieser Anleitung wird die Verwendung des Gerätemanagementprotokolls von {{site.data.keyword.iot_short_notm}} zum Verwalten eines Arduino Uno-Geräts über ein Raspberry Pi-Gerät erläutert, das als Gateway fungiert, und die Ausführung von Gerätemanagementoperationen wie das Neustarten des Geräts oder das Hinzufügen einer Programmskizze.
