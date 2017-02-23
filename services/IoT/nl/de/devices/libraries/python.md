---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Python für Geräteentwickler
{: #python}

Verwenden Sie Python, um Gerätecode zu erstellen und zu entwickeln, der in {{site.data.keyword.iot_full}} mit Ihrer Organisation interagiert. Der Python-Client für {{site.data.keyword.iot_short_notm}} stellt eine API bereit, die eine einfache Interaktion mit {{site.data.keyword.iot_short_notm}}-Funktionen ermöglicht, indem die zugrunde liegenden Protokolle wie MQTT und HTTP herausgezogen werden.
{:shortdesc}

Verwenden Sie die bereitgestellten Informationen und Beispiele, um mit der Entwicklung Ihrer Geräte mithilfe von Python zu beginnen.

## Python-Client und Ressourcen herunterladen
{: #python_client_download}

Wechseln Sie für den Zugriff auf den Python-Client für {{site.data.keyword.iot_short_notm}} und auf andere verfügbare Ressourcen in GitHub in das Repository [iot-python](https://github.com/ibm-watson-iot/iot-python) und folgenden Sie den Installationsanweisungen.

## Konstruktor
{: #constructor}

Das Optionsverzeichnis erstellt Definitionen, die für die Interaktion mit dem {{site.data.keyword.iot_short_notm}}-Modul verwendet werden. Der Konstruktor erstellt die Clientinstanz und akzeptiert ein Optionsverzeichnis, das folgende Definitionen enthält:

|Definition|Beschreibung |
|:---|:---|
|`orgId`|Die ID Ihrer Organisation.|
|`type`|Der Typ des Geräts. Der Gerätetyp ist eine Gruppierung von Geräten, die eine bestimmte Aufgabe ausführen, beispielsweise 'Wetterballon'.|
|`id`|Eine eindeutige ID zur Angabe eines Geräts. In der Regel ist die Geräte-ID bei vorgegebenem Gerätetyp eine eindeutige Kennung des betreffenden Geräts, beispielsweise die Seriennummer oder MAC-Adresse.|
|`auth-method`|Die Methode der Authentifizierung. Die einzige Methode, die unterstützt ist, lautet `apikey`.|
|`auth-token`|API-Schlüsseltoken, das ebenfalls erforderlich ist, wenn Sie `apikey` als Wert für 'auth-method' festlegen.|
|`clean-session`|Der Wert 'true' oder 'false', der nur erforderlich ist, wenn Sie die Anwendung im Modus der permanenten Subskription verbinden möchten. Für `clean-session` ist standardmäßig der Wert 'true' festgelegt.|

Steht kein Optionsverzeichnis zur Verfügung, wird der Client als nicht registriertes Gerät mit dem Quickstart-Service von {{site.data.keyword.iot_short_notm}} verbunden.

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Konfigurationsdatei verwenden

Statt ein Optionsverzeichnis direkt zu definieren, können Sie ein Optionsverzeichnis wie im folgenden Codebeispiel gezeigt auch separat in einer Konfigurationsdatei definieren:

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

Die Konfigurationsdatei, die das Optionsverzeichnis enthält, muss folgendes Format aufweisen:

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token
clean-session=true/false
```

## Ereignisse publizieren
{: #publishing_events}

Ereignisse sind der Mechanismus, über den Geräte Daten in {{site.data.keyword.iot_short_notm}} publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gerät an; dies bedeutet, dass ein Gerät nicht die Identität eines anderen Geräts annehmen kann.

Ereignisse können mit einer beliebigen der drei durch das MQTT-Protokoll definierten Servicequalitätsstufen (QoS) publiziert werden.  Standardmäßig werden Ereignisse mit der Servicequalitätsstufe `0` publiziert.

### Ereignis mithilfe der standardmäßigen Servicequalität publizieren

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### Servicequalitätsstufe für ein Ereignis erhöhen

Sie können die [Servicequalitätsstufe](../../reference/mqtt/index.html#qos-levels) für zu publizierende Ereignisse erhöhen. Ereignisse, die eine höhere Servicequalitätsstufe als `0` aufweisen, benötigen für die Publizierung möglicherweise mehr Zeit, da zusätzliche Empfangsbestätigungsinformationen enthalten sind.

**Hinweis:** Der Modus für den Quickstart-Ablauf unterstützt nur Servicequalitätsstufe `0`.

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## Befehle verarbeiten
{: #handling_commands}

Wenn der Geräteclient eine Verbindung herstellt, subskribiert er automatisch alle für dieses Gerät geltenden Befehle. Zum Verarbeiten bestimmter Befehle müssen Sie eine Callback-Methode für Befehle registrieren. Die Nachrichten werden als Instanz der Befehlsklasse zurückgegeben, die folgende Eigenschaften enthält:

|Eigenschaft|Datentyp|Beschreibung|
|:---|:---|
|`command`|Zeichenfolge|Gibt den Befehl an.|
|`format`|Zeichenfolge|Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.|
|`data`|Wörterverzeichnis|Die Angaben für die Nutzdaten. Die maximale Länge beträgt 131072 Byte.|
|`timestamp`|Datum und Uhrzeit|Das Datum und die Uhrzeit des Ereignisses.|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## Unterstützung für das Format angepasster Nachrichten
{: #custom_message_format}

Als Nachrichtenformat wird standardmäßig `json` festgelegt; dies bedeutet, dass die Bibliothek das Verschlüsseln und Entschlüsseln der Python-Wörterverzeichnisobjekte im Format JSON unterstützt. Wenn als Nachrichtenformat `json-iotf` festgelegt ist, wird die Nachricht in Übereinstimmung mit der JSON-Nutzdatenspezifikation von {{site.data.keyword.iot_short_notm}} verschlüsselt. Informationen zum Hinzufügen von Unterstützung für Ihre eigenen angepassten Nachrichtenformate finden Sie in GitHub im [Beispiel für das Format angepasster Nachrichten](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat).

Wenn Sie ein angepasstes Encodermodul erstellen, müssen Sie es wie im folgenden Beispiel dargestellt im Geräteclient registrieren:

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
Wenn ein Ereignis in einem unbekannten Format gesendet wird oder wenn ein Ereignis das Format nicht erkennt, gibt die Gerätebibliothek die Bedingung `MissingMessageDecoderException` zurück.
