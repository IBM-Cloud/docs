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


# Python für Anwendungsentwickler
{: #python}


Verwenden Sie Python, um Anwendungen zu erstellen und zu entwickeln, die in {{site.data.keyword.iot_full}} mit Ihrer Organisation interagieren. Der Python-Client für {{site.data.keyword.iot_short_notm}} stellt eine API bereit, die eine einfache Interaktion mit {{site.data.keyword.iot_short_notm}}-Funktionen ermöglicht, indem die zugrunde liegenden Protokolle wie MQTT und HTTP herausgezogen werden.

{:shortdesc}

Verwenden Sie die bereitgestellten Informationen und Beispiele, um mit der Entwicklung von Anwendungen mithilfe von Python zu beginnen.

## Python-Client und Ressourcen herunterladen
{: #python_client_download}

Wechseln Sie für den Zugriff auf den Python-Client für {{site.data.keyword.iot_short_notm}} und auf andere verfügbare Ressourcen in das Repository [iot-python ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-messaging/iot-python){: new_window} in GitHub und folgenden Sie den Installationsanweisungen.

## Konstruktor
{: #constructor}

Das Optionsverzeichnis erstellt Definitionen, die für die Interaktion mit dem {{site.data.keyword.iot_short_notm}}-Modul verwendet werden. Der Konstruktor erstellt die Clientinstanz und akzeptiert ein Optionsverzeichnis, das folgende Definitionen enthält:

|Definition|Beschreibung |
|:-----|:-----|
|`orgId`|Die ID Ihrer Organisation.|
|`appId`|Die eindeutige ID einer Anwendung in Ihrer Organisation.|
|`auth-method`|Die Methode der Authentifizierung. Die einzige Methode, die unterstützt ist, lautet `apikey`.|
|`auth-key`|Optionaler API-Schlüssel, den Sie angeben müssen, wenn `apikey` als Wert für 'auth-method' festgelegt ist.|
|`auth-token`|API-Schlüsseltoken, das ebenfalls erforderlich ist, wenn Sie `apikey` als Wert für 'auth-method' festlegen.|
|`clean-session`|Der Wert 'true' oder 'false', der nur erforderlich ist, wenn Sie die Anwendung im Modus der permanenten Subskription verbinden möchten. Für `clean-session` ist standardmäßig der Wert 'true' festgelegt.|


Steht kein Optionsverzeichnis zur Verfügung, wird der Client als nicht registriertes Gerät mit dem Quickstart-Service von {{site.data.keyword.iot_short_notm}} verbunden.

```python

import ibmiotf.application
try:
  options = {
    "org": organization,
    "id": appId,
    "auth-method": authMethod,
    "auth-key": authKey,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Konfigurationsdatei verwenden


Wenn Sie kein Optionsverzeichnis verwenden, müssen Sie eine Konfigurationsdatei einschließen, die ein Optionsverzeichnis im folgenden Codeformat enthält:

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
Die Anwendungskonfigurationsdatei muss das folgende Format aufweisen:

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## API-Aufrufe
{: #api_calls}

Jede Methode im API-Client antwortet mit einer der beiden folgenden Möglichkeiten:

- Bei Erfolg mit einer gültigen JSON- oder booleschen Antwort
- Bei Nichterfolg mit der Ausnahmebedingung 'IoTFCReSTException'

Damit weitere Informationen dazu zur Verfügung stehen, warum ein API-Aufruf fehlgeschlagen ist oder um festzustellen, ob die Aktion teilweise erfolgreich ist, kann eine Anwendung die Eigenschaften einer Ausnahmeantwort parsen. Die Ausnahmeantwort 'IoTFCReSTException' enthält folgende Eigenschaften:

|Eigenschaft|Beschreibung|
|:---|:---|
|`httpcode`|Der HTTP-Statuscode.|
|`message`|Ausnahmebedingungsnachricht, die die Ursache für das Fehlschlagen enthält.|
|`response`|Das JSON-Element, das die Teilantwort enthält. Falls ein solches nicht vorhanden ist, wird für diesen Wert null eingestellt.|

## Geräteereignisse subskribieren
{: #subscribe_device_events}

Ereignisse sind der Mechanismus, über den Geräte Daten in der {{site.data.keyword.iot_short_notm}}-Instanz publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gerät an; dies bedeutet, dass es für ein Gerät unmöglich ist, die Identität eines anderen Geräts anzunehmen.

Anwendungen subskribieren standardmäßig alle Ereignisse von allen verbundenen Geräten. Steuern Sie den Bereich der Subskription mithilfe der Parameter 'deviceType', 'deviceId', 'event' und 'msgFormat'. Ein einzelner Client kann mehrere Subskriptionen unterstützen. Folgende Codebeispiele zeigen, wie der Bereich einer Subskription mithilfe der Parameter 'deviceType', 'deviceId', 'event' und 'msgFormat' definiert werden kann:


### Alle Ereignisse von allen Geräten subskribieren


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### Alle Ereignisse von allen Geräten eines bestimmten Typs subskribieren


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### Bestimmtes Ereignis von allen Geräten subskribieren


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### Bestimmtes Ereignis von mindestens zwei unterschiedlichen Geräten subskribieren

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### Alle Ereignisse subskribieren, die im JSON-Format publiziert sind

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## Ereignisse von Geräten verarbeiten
{: #handling_events_devices}

Zum Verarbeiten der Ereignisse, die über Ihre Subskriptionen empfangen werden, müssen Sie eine Callback-Methode für Ereignisse registrieren. Die Nachrichten werden als Instanz der Ereignisklasse zurückgegeben:

|Eigenschaft|Datentyp|Beschreibung|
|:---|:---|
|`event.device`|Zeichenfolge|Gibt das Gerät unter allen Gerätetypen der Organisation eindeutig an.|
|`event.deviceType`|Zeichenfolge|Gibt den Gerätetyp an. In der Regel ist 'deviceType' eine Zusammenfassung von Geräten, die eine bestimmte Aufgabe ausführen, beispielsweise 'Wetterballon'.|
|`event.deviceId`|Zeichenfolge|Stellt die ID des Geräts dar. In der Regel ist 'deviceId' bei vorgegebenem Gerätetyp eine eindeutige Kennung des betreffenden Geräts, beispielsweise die Seriennummer oder MAC-Adresse.|
|`event.event`|Zeichenfolge|In der Regel zum Gruppieren bestimmter Ereignisse verwendet, beispielsweise 'Status', 'Warnung' und 'Daten'.
|`event.format`|Zeichenfolge|Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.
|`event.data`|Wörterverzeichnis|Die Angaben für die Nachrichtennutzdaten. Die maximale Länge beträgt 131072 Byte.
|`event.timestamp`|Datum und Uhrzeit|Datum und Uhrzeit des Ereignisses.|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  def myEventCallback(event):
      str = "%s event '%s' received from device [%s]: %s"
      print(str % (event.format, event.event, event.device, json.dumps(event.data)))

...
client.connect()
client.deviceEventCallback = myEventCallback
client.subscribeToDeviceEvents()
```


## Gerätestatus subskribieren
{: #subscribe_device_status}


Wenn Sie den Gerätestatus subskribieren, werden standardmäßig Statusaktualisierungen für alle verbundenen Geräte empfangen. Steuern Sie den Bereich der Subskription mithilfe der Parameter für den Typ und die ID. Ein einzelner Client kann mehrere Subskriptionen unterstützen.

### Statusaktualisierungen aller Geräte subskribieren


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### Statusaktualisierungen aller Geräte eines bestimmten Typs subskribieren


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### Statusaktualisierungen für zwei unterschiedliche Geräte subskribieren


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## Statusaktualisierungen von Geräten verarbeiten
{: #handling_device_updates}

Statusereignisse

Zum Verarbeiten der Statusaktualisierungen, die über Ihre Subskriptionen empfangen werden, müssen Sie eine Callback-Methode für Ereignisse registrieren. Die Nachrichten werden als Instanz der Statusklasse zurückgegeben.

Es gibt zwei Typen von Statusereignissen, `Connect`-Ereignisse und `Disconnect`-Ereignisse. Alle Statusereignisse enthalten folgende Eigenschaften:

|Eigenschaft|Datentyp|
|:---|:---|
|`status.clientAddr`|Zeichenfolge|
|`status.protocol`|Zeichenfolge|
|`status.clientId`|Zeichenfolge|
|`status.user`|Zeichenfolge|
|`status.time`|Datum und Uhrzeit|
|`status.action`|Zeichenfolge|
|`status.connectTime`|Datum und Uhrzeit|
|`status.port`|Ganze Zahl|


Mit der Eigenschaft `status.action` wird festgelegt, ob ein Statusereignis den Typ `Connect` oder `Disconnect` aufweist.

`Disconnect`-Statusereignisse enthalten zusätzlich folgende Eigenschaften:

|Eigenschaft|Datentyp|
|:---|:---|
|`status.writeMsg`|Ganze Zahl|
|`status.readMsg`|Ganze Zahl|
|`status.reason`|Zeichenfolge|
|`status.readBytes`|Ganze Zahl|
|`status.writeBytes`|Ganze Zahl|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

def myStatusCallback(status):

  if status.action == "Disconnect":
    str = "%s - device %s - %s (%s)"
    print(str % (status.time.isoformat(), status.device, status.action, status.reason))
    else:
      print("%s - %s - %s" % (status.time.isoformat(), status.device, status.action))
  ...
client.connect()
client.deviceStatusCallback = myStatusCallback
client.subscribeToDeviceStstus()
```


## Ereignisse von Geräten publizieren
{: #publishing_device_events}

Anwendungen können Ereignisse so publizieren, als stammten sie von einem Gerät.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## Befehle für Geräte publizieren
{: #publishing_commands_devices}


Anwendungen können Befehle an verbundene Geräte publizieren.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", commandData)
```


## Organisationsdetails
{: #org_details}

Anwendungen können mithilfe der Methode `getOrganizationDetails()` Details zur Konfiguration der Organisation abrufen.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

Der Abschnitt zur Organisationskonfiguration in der [{{site.data.keyword.iot_short_notm}}-API ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} enthält Informationen zum Anforderungs-/Antwortmodell und zu den HTTP-Statuscodes.


## Massenoperationen für Geräte
{: #bulk_device_ops}

Ihre Anwendungen können mithilfe von Massenoperationen mehrere Geräte gleichzeitig abrufen, hinzufügen oder entfernen.

Der Abschnitt zu den Massenoperationen in der [{{site.data.keyword.iot_short_notm}}-API ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/){: new_window} enthält Informationen zu der Liste der Abfrageparameter, zum Anforderungs-/Antwortmodell und zu HTTP-Statuscodes.


### Geräteinformationen abrufen

Massendaten zu Geräten können mithilfe der Methode `getAllDevices()` abgerufen werden. Mit dieser Methode werden Informationen zu allen in der Organisation registrierten Geräten abgerufen. Jede Anforderung kann maximal 512 KB enthalten.

Die Antwort enthält Parameter, die für die Anwendung erforderlich sind. Verwenden Sie die Wörterverzeichnisergebnisse aus der Antwort, um die zurückgegebene Gruppe von Geräten abzurufen. Andere Parameter in der Antwort sind erforderlich, um weitere Aufrufe vorzunehmen; beispielsweise kann das Element `_bookmark` verwendet werden, um durch Ergebnisse zu blättern. Übergeben Sie die erste Anforderung, ohne ein Lesezeichen anzugeben, und verwenden Sie das in der Antwort zurückgegebene Lesezeichen anschließend in der Anforderung für die nächste Seite. Wiederholen Sie diesen Vorgang, bis das Ende der Ergebnismenge erreicht ist. Dies wird dadurch angegeben, dass kein Lesezeichen vorhanden ist. Für die übrigen Parameter müssen alle Anforderungen dieselben Werte verwenden, andernfalls sind die Ergebnisse nicht definiert.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### Mehrere Geräte hinzufügen


Mit der Methode `addMultipleDevices()` können Sie Ihrer {{site.data.keyword.iot_short_notm}}-Organisation mindestens ein Gerät hinzufügen. Eine Anforderung darf nicht größer als 512 KB sein. Die Antwort enthält die Authentifizierungstokens, die für das jeweilige Gerät generiert wurden. Stellen Sie sicher, dass Sie eine Kopie der Authentifizierungstokens machen; wenn die Authentifizierungstokens verloren gehen, können sie nicht mehr abgerufen werden.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
  deviceList = client.api.addMultipleDevices(listOfDevicesToAdd)
except IoTFCReSTException as e:
  print("ERROR [" + e.httpcode + "] " + e.message)
```

### Mehrere Geräte löschen


Mit der Methode `deleteMultipleDevices()` können Sie mehrere Geräte aus einer {{site.data.keyword.iot_short_notm}}-Organisation löschen. Eine Anforderung darf nicht größer als 512 KB sein.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToDelete = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
      deviceList = client.api.deleteMultipleDevices(listOfDevicesToDelete)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Gerätetypenoperationen
{: #device_type_ops}

Die Gerätetypen, die Sie in Ihrer Organisation erstellen, können zum Erstellen von Vorlagen für das Hinzufügen von Geräten verwendet werden. Durch Verwenden der Funktionen der {{site.data.keyword.iot_short_notm}}-API können Ihre Anwendungen Gerätetypen in Ihrer Organisation auflisten, erstellen, löschen, anzeigen oder aktualisieren.

Der Abschnitt 'Gerätetypen' der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-API ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} enthält Informationen zu Abfrageparametern, zum Anforderungs-/Antwortmodell und zu HTTP-Statuscodes. 


### Alle Gerätetypen abrufen

Mithilfe der Methode `getAllDeviceTypes()` können Sie alle Gerätetypen abrufen, die in Ihrer {{site.data.keyword.iot_short_notm}}-Organisation vorhanden sind.
Verwenden Sie die Wörterverzeichnisergebnisse aus der Antwort, um die zurückgegebene Gruppe von Geräten abzurufen. Andere Parameter in der Antwort sind erforderlich, um weitere Aufrufe vorzunehmen; beispielsweise kann das Element `_bookmark` verwendet werden, um durch Ergebnisse zu blättern. Übergeben Sie die erste Anforderung, ohne ein Lesezeichen anzugeben, und verwenden Sie das in der Antwort zurückgegebene Lesezeichen anschließend in der Anforderung für die nächste Seite. Wiederholen Sie diesen Prozess, bis das Ende der Ergebnismenge erreicht ist. Dies wird dadurch gekennzeichnet, dass kein Lesezeichen vorhanden ist. Für die übrigen Parameter müssen alle Anforderungen dieselben Werte verwenden, andernfalls sind die Ergebnisse nicht definiert.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

 listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
   options = {'_limit' : 2}
   deviceTypeList = client.api.getAllDeviceTypes(options)
except IoTFCReSTException as e:
   print("ERROR [" + e.httpcode + "] " + e.message)

```

### Gerätetyp hinzufügen

Mit der Methode `addDeviceType()` können Sie in Ihrer {{site.data.keyword.iot_short_notm}}-Instanz einen Gerätetyp registrieren. In den einzelnen Anforderungen müssen Sie zunächst die Gerätedaten und die Metadatenelemente des Geräts definieren, die auf alle Geräte dieses Typs angewendet werden sollen. Das Element mit den Gerätedaten besteht aus mehreren Variablen, die Seriennummer, Hersteller, Modell, Klasse, Beschreibung, Firmware- und Hardwareversionen und den beschreibenden Standort umfassen. Das Metadatenelement besteht aus angepassten Variablen und Werten, die vom Benutzer definiert werden können.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2"
  }

try:
      deviceType = client.api.addDeviceType(deviceType = "myDeviceType", description = "My first device type", deviceInfo = info, metadata = meta)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Gerätetyp löschen


Mit der Methode `deleteDeviceType()` können Sie in Ihrer {{site.data.keyword.iot_short_notm}}-Organisation einen Gerätetyp löschen.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Informationen zu bestimmten Gerätetypen abrufen


Mit der Methode `getDeviceType()` können Sie Informationen zu einem bestimmten Gerätetyp abrufen. Die Typ-ID (`typeId`) des Gerätetyps, den Sie abrufen wollen, muss als Parameter angegeben werden.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### Gerätetyp aktualisieren


Mit der Methode `updateDeviceType()` können Sie die Eigenschaften eines Gerätetyps ändern. Wenn Sie die Methode `updateDeviceType()` verwenden, geben Sie zuerst die Typ-ID (`typeId`) des Gerätetyps an, der aktualisiert werden soll, und geben Sie anschließend folgende Elemente an:

- `description`
- `deviceInfo`
- `metadata`

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2",
      "customField3": "customValue3"
  }

try:
      updatedDeviceTypeInfo = client.api.updateDeviceType("myDeviceType", "New description", deviceInfo, metadata)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Geräteoperationen
{: #device_ops}

Die in der API verfügbaren Geräteoperationen umfassen das Auflisten, Hinzufügen, Entfernen, Anzeigen, Aktualisieren, Anzeigen von Standorten und Anzeigen von Gerätemanagementinformationen zu Geräten in einer {{site.data.keyword.iot_short_notm}}-Organisation.

Der Abschnitt über Geräte in der [{{site.data.keyword.iot_short_notm}}-API ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} enthält Informationen zu den Abfrageparametern, zum Anforderungs-/Antwortmodell und zu den HTTP-Statuscodes.


### Geräte eines bestimmten Gerätetyps abrufen

Mit der Methode `retrieveDevices()` können Sie alle Geräte eines bestimmten in einer Organisation vorhandenen Gerätetyps in einer {{site.data.keyword.iot_short_notm}}-Instanz wie im folgenden Beispiel gezeigt abrufen:


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

Verwenden Sie die Wörterverzeichnisergebnisse aus der Antwort, um die zurückgegebene Gruppe von Geräten abzurufen. Andere Parameter in der Antwort sind erforderlich, um weitere Aufrufe vorzunehmen; beispielsweise kann das Element *_bookmark* verwendet werden, um durch Ergebnisse zu blättern. Übergeben Sie die erste Anforderung, ohne ein Lesezeichen anzugeben, und verwenden Sie das in der Antwort zurückgegebene Lesezeichen anschließend in der Anforderung für die nächste Seite. Wiederholen Sie diesen Vorgang, bis das Ende der Ergebnismenge erreicht ist. Dies wird dadurch angegeben, dass kein Lesezeichen vorhanden ist. Für die übrigen Parameter müssen alle Anforderungen dieselben Werte verwenden, andernfalls sind die Ergebnisse nicht definiert.

Zum Übergeben von *_bookmark* oder einer beliebigen anderen Bedingung muss die überladene Methode verwendet werden. Die überladene Methode akzeptiert Parameter im Format eines Wörterbuchverzeichnisses, wie im folgenden Beispiel gezeigt:

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

Im vorherigen Codebeispiel wird die Antwort auf der Basis der Geräte-ID sortiert und anschließend wird das Lesezeichen verwendet, um durch die Ergebnisse zu blättern.

### Gerät hinzufügen


Verwenden Sie zum Hinzufügen eines Geräts zu einer {{site.data.keyword.iot_short_notm}}-Organisation die Methode `registerDevice()`. Mit der Methode `registerDevice()` wird Ihrer {{site.data.keyword.iot_short_notm}}-Organisation ein einzelnes Gerät hinzugefügt. Beim Hinzufügen eines Geräts können Sie folgende Parameter angeben:

|Parameter|Anforderung|Beschreibung
|:---|:---|
|`deviceTypeId`|Optional|Ordnet dem Gerät einen Gerätetyp zu. Wenn zwischen den Variablen, die durch den Gerätetyp definiert sind, und den Variablen, die durch die Variable `deviceInfo` definiert sind, ein Konflikt besteht, haben die gerätespezifischen Variablen Vorrang.|
|`deviceId`|Obligatorisch||
|`authToken`|Optional|Falls nicht angegeben, wird ein Authentifizierungstoken generiert und in die Antwort eingeschlossen.|
|`deviceInfo`|Optional|Enthält einige Variablen, zu denen Seriennummer, Hersteller, Modell, Geräteklasse, Beschreibung, beschreibender Standort sowie Firmware- und Hardwareversionen gehören.|
|`metadata`|Optional|Zeichenfolgepaare aus angepassten Feldern und Werten, wie in [Beispielcode zum Hinzufügen eines Gerätetyps](#sample_device_type) dargestellt.|
|`location`|Optional|Enthält die Variablen 'longitude', 'latitude', 'elevation', 'accuracy' und 'measuredDateTime'.|

In der [API-Dokumentation ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices){: new_window} finden Sie weitere Informationen zu diesen Parametern und zum Antwortformat sowie den Codes.

Wenn Sie die Methode `registerDevice()` verwenden, müssen Sie den obligatorischen Parameter 'deviceID' und die optionalen Parameter definieren, die für Ihr Gerät erforderlich sind, und Sie müssen die Methode anschließend mithilfe der von Ihnen ausgewählten Parameter aufrufen.

### Beispielcode zum Hinzufügen eines Gerätetyps
{: #sample_device_type}

Fügen Sie nach dem Konstruktorcode in einer Python-Scriptdatei (.py) folgenden Code hinzu. Das Beispiel veranschaulicht eine Methode zum Hinzufügen eines Gerätetyps, bei der die Parameter 'deviceId', 'authToken', 'metadata', 'deviceInfo' und 'location' definiert werden.

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### Gerät löschen

Mit der Methode `deleteDevice()` können Sie in der {{site.data.keyword.iot_short_notm}}-Organisation ein Gerät aus einer Organisation entfernen. Wenn Sie ein Gerät mithilfe der Methode `deleteDevice()` löschen, müssen Sie die Parameter 'deviceTypeId' und 'deviceId' angeben.

Das folgende Codebeispiel zeigt das für diese Methode erforderliche Format:

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### Gerät abrufen

Mit der Methode `getDevice()` können Sie in {{site.data.keyword.iot_short_notm}} ein Gerät aus einer Organisation abrufen. Wenn Sie Gerätedetails mithilfe der Methode `getDevice()` abrufen, müssen Sie die Parameter 'deviceTypeId' und 'deviceId' angeben.

Das folgende Codebeispiel veranschaulicht das Format, das für diese Methode erforderlich ist.

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### Alle Geräte abrufen

Mit der Methode `getAllDevices()` können Sie in {{site.data.keyword.iot_short_notm}} alle Geräte einer Organisation abrufen.

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### Gerät aktualisieren

Zum Ändern mindestens einer Eigenschaft eines Geräts verwenden Sie die Methode `updateDevice()`.

Sie können in den Parametern 'deviceInfo' oder 'metadata' beliebige Eigenschaften aktualisieren. Zum Aktualisieren einer Geräteeigenschaft definieren Sie vor dem Aufrufen der Methode `updateDevice()` den Parameter 'deviceInfo'. Der Statusparameter muss '`alert`: True' enthalten. Die Eigenschaft 'alert' steuert, ob ein Gerät in der {{site.data.keyword.iot_short_notm}}-Benutzerschnittstelle Fehlercodes anzeigt, und für sie muss standardmäßig '`enabled`: True' eingestellt sein, wie im folgenden Codebeispiel dargestellt:

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### Beispielcode zum Aktualisieren von Eigenschaften für 'deviceInfo'

Das folgende Codebeispiel gibt ein bestimmtes Gerät an und aktualisiert anschließend einige Eigenschaften des Parameters 'deviceInfo'.

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### Positionsinformationen abrufen


Mit der Methode `getDeviceLocation()` können Sie die Positionsinformationen eines Geräts abrufen. Zum Abrufen der Positionsdaten sind die Parameter 'deviceTypeId' und 'deviceId' erforderlich.

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

Die Antwort auf diese Methode enthält die Eigenschaften 'longitude', 'latitude', 'elevation', 'accuracy', 'measuredTimeStamp' und 'updatedTimeStamp'.

### Positionsinformationen aktualisieren


Mit der Methode `updateDeviceLocation()` können Sie die Positionsinformationen für ein Gerät ändern. Wie beim Aktualisieren der Geräteeigenschaften muss zusammen mit den Änderungen, die Sie anwenden möchten, der Parameter 'deviceLocation' definiert werden. Das folgende Codebeispiel veranschaulicht die Standortdaten für ein bestimmtes Gerät:

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

Wenn kein Datum angegeben ist, werden das aktuelle Datum und die zugehörige Zeit verwendet.


### Managementinformationen abrufen


Mit der Methode `getDeviceManagementInformation()` können Sie die Gerätemanagementinformationen zu einem Gerät abrufen. Die Antwort enthält Datum und Uhrzeit der letzten Aktivität, die Einstellungen für den ruhenden Status (true/false), Unterstützung für Geräte- und Firmwareaktionen sowie Firmwaredaten. In der entsprechenden API-Dokumentation finden Sie eine umfassende Liste des Antwortinhalts.

Mit dem folgenden Codebeispiel werden die Gerätemanagementinformationen für ein Gerät zurückgegeben, dessen Geräte-ID (deviceId) den Wert '00aabbccde03' aufweist und dessen Gerätetypen-ID (deviceTypeId) auf 'iotsample-arduino' eingestellt ist:

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## Gerätediagnoseoperationen
{: #device_diag_ops}

Mit den Gerätediagnoseinformationen können Sie folgende Tasks für die Fehlerbehebung und das Protokollmanagement implementieren:
- Protokolle löschen
- Alle oder bestimmte Protokolle für ein Gerät abrufen
- Protokollinformationen hinzufügen
- Protokolle löschen
- Fehlercodes löschen
- Fehlercodes zu einem Gerät abrufen
- Fehlercodes hinzufügen

In der [{{site.data.keyword.iot_short_notm}}-API-Dokumentation ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} finden Sie weitere Informationen zu Anforderungs-/Antwortmodellen, Antwortcodes und Abfrageparametern.

### Diagnoseprotokolle abrufen


Mit der Methode `getAllDiagnosticLogs()` können Sie alle Diagnoseprotokolle für ein bestimmtes Gerät abrufen. Für die Methode `getAllDiagnosticLogs()` sind die Parameter 'deviceTypeId' und 'deviceId' erforderlich.

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

Das Antwortmodell für diese Methode enthält die Eigenschaften 'Protokoll-ID', 'Nachricht', 'Schweregrad', 'Daten' und 'Zeitmarke'.

### Diagnoseprotokolle für ein Gerät löschen


Mit der Methode `clearAllDiagnosticLogs()` können Sie alle Diagnoseprotokolle für ein bestimmtes Gerät löschen. Die erforderlichen Parameter sind 'deviceTypeId' und 'deviceId'. Seien Sie sorgfältig beim Löschen von Protokolldateien, da diese nach dem Löschen nicht mehr wiederhergestellt werden können.

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### Diagnoseprotokoll hinzufügen


Mit der Methode `addDiagnosticLog()` können Sie dem Diagnoseprotokoll des Geräts einen Eintrag hinzufügen. Das Protokoll kann beim Hinzufügen des neuen Eintrags bereinigt werden. Wird kein Datum angegeben, so werden dem Eintrag das aktuelle Datum und die zugehörige Uhrzeit hinzugefügt. Um diese Methode zu verwenden, müssen Sie mithilfe der folgenden Variablen den Parameter 'logs' definieren:


|Variable|Anforderung|Beschreibung|
|:---|:---|:---|
|`message`|Obligatorisch|Enthält die Diagnosenachricht, die hinzugefügt werden soll.|
|`severity`|Optional|Entspricht dem Schweregrad des Diagnoseprotokolls und kann die Einstellung '0' (Informationsnachricht), '1' (Warnung) oder '2' (Fehler) aufweisen.|
|`data`|Optional|Enthält Diagnosedaten.|
|`timestamp`|Optional|Enthält das Datum und die Uhrzeit des Protokolleintrags im Format ISO8601; erfolgt keine Angabe, werden das aktuelle Datum und die zugehörige Uhrzeit verwendet.|


Die übrigen in der Methode erforderlichen Parameter sind die für das Gerät geltenden Werte für 'deviceTypeId' und 'deviceId'.

Das folgende Codebeispiel enthält ein Beispiel für die Methode `addDiagnosticLog()`:

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### Bestimmtes Diagnoseprotokoll abrufen


Mit der Methode `getDiagnosticLog()` können Sie auf der Basis der Protokoll-ID ein bestimmtes Diagnoseprotokoll für ein angegebenes Gerät abrufen. Die erforderlichen Parameter für diese Methode lauten 'deviceTypeId', 'deviceId' und 'logId'.

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Diagnoseprotokoll löschen


Mit der Methode `deleteDiagnosticLog()` können Sie ein bestimmtes Diagnoseprotokoll löschen. Um das Diagnoseprotokoll anzugeben, müssen die Parameter 'deviceTypeId', 'deviceId' und 'logID' angegeben werden.

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Fehlercodes zu einem Gerät abrufen


Mit der Methode `getAllDiagnosticErrorCodes()` können Sie alle Diagnosefehlercodes abrufen, die einem bestimmten Gerät zugeordnet sind.

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### Diagnosefehlercodes löschen


Mit der Methode `clearAllErrorCodes()` können Sie die Liste der Fehlercodes löschen, die dem Gerät zugeordnet sind. Die Liste wird durch einen einzigen Fehlercode mit dem Wert 'null' ersetzt.

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### Einzelnen Diagnosefehlercode hinzufügen


Mit der Methode `addErrorCode()` können Sie der Liste der Fehlercodes, die dem Gerät zugeordnet sind, einen Fehlercode hinzufügen. Die Liste kann beim Hinzufügen des neuen Eintrags bereinigt werden. Die erforderlichen Parameter für die Methode lauten 'deviceTypeId', 'deviceId' und 'errorCode'. Der Parameter 'errorCode' enthält folgende Variablen:

- errorCode: Diese Variable ist obligatorisch und muss als ganze Zahl festgelegt werden. Mit dieser Variablen wird die Nummer des zu erstellenden Fehlercodes festgelegt.
- timestamp: Diese Variable ist optional und enthält das Datum und die Uhrzeit des Protokolleintrags im Format ISO8601. Wenn diese Variable nicht enthalten ist, wird sie zusammen mit dem aktuellen Datum und der zugehörigen Uhrzeit automatisch hinzugefügt.

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## Problembestimmung bei Verbindungsproblemen
{: #connection_problem_determination}

Mit der Methode `getDeviceConnectionLogs()` können Sie Verbindungsprotokollereignisse aufzulisten. Verbindungsprotokollereignisse sind bei der Diagnose von Konnektivitätsproblemen bei der Verbindung zwischen dem Gerät und dem {{site.data.keyword.iot_short_notm}}-Service hilfreich. In den Einträgen werden erfolgreiche Verbindungen, nicht erfolgreiche Verbindungsversuche, absichtliche Verbindungstrennungsereignisse und vom Server initiierte Verbindungstrennungsereignisse aufgezeichnet.

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

Die Antwort enthält eine Liste mit Protokolleinträgen, die Protokollnachrichten und Zeitmarken enthalten.
