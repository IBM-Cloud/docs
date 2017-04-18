---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-27"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Verwendung des Shield-Toolkits
{: #iot4i_shield_toolkit}
Shields werden zum Schutz von Eigentum und Benutzern verwendet, indem Gefahren erkannt und die entsprechenden automatisierten Maßnahmen erzeugt werden. Sie können die Shields aus der {{site.data.keyword.iotinsurance_short}}-Shields-Bibliothek verwenden oder ändern bzw. mithilfe der folgenden Anweisungen und Beispiele eigene Shields erstellen und implementieren.
{:shortdesc}

## Informationen zu Shields.
Bei einem Shield handelt es sich um eine Reihe von Regeln und definierten Aktionen, die durch bestimmte Bedingungen in der Eingabe ausgelöst werden können, die von einem Sensor empfangen wird. Sie können beispielsweise ein Shield mit einer Regel erstellen, die besagt, dass eine Textnachricht gesendet werden soll, falls der Sensor einen Wasserleitungsschaden ermittelt.

## Shields aus der {{site.data.keyword.iotinsurance_short}}-Shields-Bibliothek verwenden

In der [{{site.data.keyword.iotinsurance_short}}-Shields-Bibliothek ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window} finden Sie ein breites Spektrum an vordefinierten Shields. In der Readme-Datei auf der Site finden Sie Anweisungen zum Herunterladen der Shields sowie zu deren Verwendung.

## Erstellung eines eigenen Shields
Bei diesem Beispiel sehen Sie, wie Sie Ihre Umgebung einrichten, ein Shield definieren, einen Benutzer erstellen und anschließend das Shield dem Benutzer zuordnen können.  Optional können Sie auch Hochstufungen und simulierte Gefahren erzeugen.  

In den folgenden Abschnitten sehen Sie Codebeispiele für die Erstellung eines einfachen Shields für Wasserleitungsschäden. Im [GitHub-Repository iot4i-api-examples-nodejs](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/) ist eine ganze Reihe von Beispielcode verfügbar.

### Voraussetzungen
Stellen Sie zunächst sicher, dass folgende Voraussetzungen erfüllt sind:

- [Node.js](https://nodejs.org/en/) ist auf Ihrem Computer installiert.  
- Eine Node.js-fähige Laufzeitumgebung wie z. B. Eclipse ist vorhanden.
- Git-Software und Zugriff auf das [GitHub-Quellcode-Repository für die API-Beispiele ist vorhanden](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   Alternativ können Sie das [Archiv mit den Quellcodedateien herunterladen](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Vorbereiteter Quellcode.  
  Führen Sie die folgenden Schritte aus, um den Quellcode vorzubereiten:
  1. Klonen Sie das [GitHub-Quellcode-Repository](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) oder laden Sie es auf Ihren Computer herunter.
  2. Installieren Sie die Open-Source-Voraussetzungen des Projekts, indem Sie über eine Befehlszeile in den Ordner wechseln, der die geklonten Quellcodedateien enthält, und dort den Befehl `npm install` ausführen.

### Eigene Umgebung einrichten
{: #environment}
Für die Konfiguration Ihrer Umgebung zum Senden von REST-API-Aufrufen müssen Sie die URL für die API in der Datei config.js konfigurieren. Die Aggregator-URL kann in diesem Kontext ignoriert werden.

```
var config = module.exports = {
  api: "https//iot4insurance-api-<uniqueid>.mybluemix.net",
  aggregator: "https//iot4i-aggregator-<uniqueid>.mybluemix.net",
  credentials : {
    user: "Admin",
    pass: "<password from IoT4I service credentials>"
  }
};
```

### Shield-Definition erstellen
{: #create_shield_def}

Methode: POST  
API: /shield  
https://iot4i-docs-api.mybluemix.net/dist/#!/shield/addShield

Erstellen Sie in der Datei createShield.js eine Shield-Definition.  Das folgende Beispiel stellt ein einfaches Shield dar, das einen Wasserleitungsschaden erkennt.

```
var shield = {
  "UUID": "26",
  "name": "demoShield",
  "type": "Environmental Measurements",
  "description": "Detect water leaks",
  "image": "shieldWater",
  "canBeDisabled": false,
  "hazardDetectionOnCloud": true,
  "jsCodeMethod": "demoShield",
  "actions": [
     "pushios"
  ],
  "potentialClaimAmount": "10",
  "shieldParameters": []
};

```

Dabei gilt Folgendes:
- **UUID** - Dies ist die Universal Unique Identifier (UUID) des Shields.
- **actions** - Eine Liste mit Aktionen, die bei der Erzeugung einer Gefahr ausgelöst werden. In diesem Beispiel werden Informationen zu der Gefahr mithilfe einer iOS-Push-Benachrichtigung an die Benutzer-App gesendet.

### Shield-Code erstellen
{: #create_shield_code}
Erstellen Sie in der Datei shieldCode.js einen Shield-Code, um festzulegen, wie die Shield-Engine Nutzdaten verarbeitet.

Im folgenden Beispiel sehen Sie einen Shield-Code, der für die Verarbeitung von Nutzdaten zu einem Wasserleitungssschaden für das Shield verwendet werden kann, das in den vorherigen Beispielen gezeigt wurde.

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

Jeder Shield-Code enthält Ressourcen, die in den resource/shield.js-Anweisungen definiert sind. Jede der folgenden Ressourcen beinhaltet ein Beispiel, das mit in den vorherigen Beispielen angezeigtem Shield, angezeigten Nutzdaten und angezeigtem Benutzer verwendet werden kann.

  - Shield-Name  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - Shield-Verzögerung - Die Verzögerung zwischen den Gefahren in Millisekunden.  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - Shield-UUID (Universal Unique Identifier))  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - Eingabebedingung - Die Bedingung und die Attribute, die für die Shield-Engine zur Nutzdatenverarbeitung erforderlich sind. In dem Beispiel besteht die Bedingung darin, dass die Nutzdaten das Attribut **liquid_detected** enthalten müssen.  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - Der Kern des Shields, durch den ein Algorithmus berechnet und ausgeführt wird, um festzustellen, ob eine Gefahr vorliegt. Im folgenden Beispiel lautet das einzige erforderliche Attribut **liquid_detected**; Safelets können jedoch für die Definition komplexer Algorithmen verwendet werden.  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - Nachricht - Die Nachricht, die an den Benutzer gesendet wird, falls die Gefahr verarbeitet wird.
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - Shield-Ausführung - Die Funktion, die für die direkte Ausführung des Shields verwendet wird; dabei muss nicht gewartet werden, bis die Shield-Engine alle relevanten Shields automatisch ausführt.  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - Shield registrieren - Eine vordefinierte Funktion, die im Shield-Code aufgerufen werden muss, um das Shield in der Shield-Engine zu registrieren. Der Wert **undefined** in dem Beispiel stellt die Vorbearbeitungsfunktion dar, die jedoch in diesem bestimmten Beispiel nicht erforderlich ist. Bei einigen Shields kann die Vorbearbeitungsfunktion zur Neuanordnung der Daten in den Nutzdaten verwendet werden. Beispiel: Werden gemessene Temperaturwerte in Fahrenheit gemeldet und sind für das Safelet jedoch Celsius erforderlich, kann die Vorbearbeitungsfunktion zur Konvertierung der Temperaturwerte in den erforderlichen Wert verwendet werden.  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### Benutzer erstellen
{: #create_user}

Methode: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/user/addUser

Erstellen Sie in der Datei createUser.js einen Benutzer. Im folgenden Beispiel sehen Sie, wie ein einzelner Benutzer erstellt wird.

```
var user = {
  "username": "user1",
  "fullname": "John Doe",
  "firstname": "John",
  "lastname": "Doe",
  "password": "user1234",
  "accessLevel": "100",
  "address": "42 Wallaby Way, Sydney",
  "email": "user@example.com",
  "deviceID": "user1",
  "deviceType": "wink",
  "type": "wink"
};

```

Dabei gilt Folgendes:
- **username** - Der eindeutige Schlüssel für den Benutzer, der für die Ermittlung der dem Benutzer zugeordneten Entitäten verwendet wird, z. B. Geräte, Shields und Hochstufungen.
- **password** - Es wird nur der Hashwert des Kennworts in der Datenbank gespeichert.
- **DeviceId** - Die ID, die für die Registrierung des Benutzers in {{site.data.keyword.iot_full}} verwendet wird. Der Wert ist mit dem Benutzernamen identisch.
- **accessLevel** - Der Wert definiert die API-Endpunkte, auf die der Benutzer zugreifen kann:
  - 100 - Mobile App
  - 10 - Dashboard
  - 1 - Systemadministrator

### Shield-Zuordnung erstellen
{: #create_shield_assoc}

Methode: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/shieldassociation/addShieldAssociation

Erstellen Sie in der Datei createUserShieldAssociation.js eine Shield-Zuordnung, bei der das Shield mit dem Benutzer verknüpft wird.

Im folgenden Beispiel sehen Sie eine Shield-Zuordnung für das Shield und den Benutzer, die in den vorherigen Abschnitten erstellt wurden.

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### Simulierte Gefahr einrichten
{: #create_sim_hazard}

Methode: POST  
API: /sendPayloadToMQTT  
https://iot4i-docs-api.mybluemix.net/dist/#!/global/sendPayloadToMQTT

Sie können Nutzdaten für eine simulierte Gefahr erstellen, um Ihre Shields zu testen.

Im folgenden Beispiel sehen Sie, wie Nutzdaten erstellt werden, durch die das Shield aktiviert wird, das im vorherigen Beispiel erstellt wurde, und durch die ein Alert an den zugeordneten Benutzer gesendet wird.

```
var parameters {
  "payload": {
    "sensor_pod_id": "190107",
    "name": "Sensor",
    "manufacturer_device_model": "leakSMART",
    "device_manufacturer": "leaksmart",
    "model_name": "leakSMART Sensor",
    "upc_code": "waxman_sensor",
    "hub_id": "379652",
    "lat_lng": [null, null],
    "location": "",
    "status": "online",
    "liquid_detected": true,
    "usr": "user1",
    "activation": "2016-06-20T12:05:02.776Z"
  },
  "outputtype": "evt",
  "devicetype": "wink",
  "deviceid": "wink",
  "type": "wink"
};

```


### Hochstufung erstellen
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}} kann mithilfe der mobilen App Hochstufungen an den Hausbesitzer senden. Mithilfe der Datei createPromotion.js können Sie Hochstufungen erstellen.

Im folgenden Beispiel sehen Sie, wie eine Hochstufung für einen autorisierten Klempner erstellt wird.

```
var promotion = {
  "title": "Promotion 9",
  "description": "Contact one of our authorized plumbers to install your water leak detection solution.",
  "buttonTitle": "Call Now",
  "type": "1",
  "phone": "+015555555555",
  "username": "user1",  
};

```

Optional können Sie Ihre mobile App bereitstellen und [die Anweisungen im GitHub-Repository ioti-mobile](https://github.com/ibm-watson-iot/ioti-mobile) zur Herstellung einer Verbindung als Benutzer, den Sie im vorherigen Abschnitt erstellt haben, verwenden.
