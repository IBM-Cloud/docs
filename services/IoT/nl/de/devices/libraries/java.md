---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java für Geräteentwickler 
{: #java}

Letzte Aktualisierung: 2. August 2016
{: .last-updated}


Verwenden Sie Java, um Geräte zu erstellen und anzupassen, die in {{site.data.keyword.iot_full}} mit Ihrer Organisation interagieren. Verwenden Sie die bereitgestellten Informationen und Beispiele, um mit der Entwicklung Ihrer Geräte mithilfe von Java zu beginnen.
{:shortdesc}

## Java-Client und Ressourcen herunterladen 
{: #java_client_download}

Wechseln Sie für den Zugriff auf die Java-Clientbibliotheken und Beispiele für {{site.data.keyword.iot_short_notm}} in GitHub in das Repository [iot-java](https://github.com/ibm-watson-iot/iot-java) und folgen Sie den Installationsanweisungen. 


## Konstruktor 
{: #constructor}

Der Konstruktor erstellt die Clientinstanz und akzeptiert ein properties-Objekt, das folgende Definitionen enthält: 

|Definition |Beschreibung  |
|:---|:---|
|`org` |Die ID Ihrer Organisation. Dieses Feld ist erforderlich. Wenn Sie einen Quickstart-Ablauf verwenden, geben Sie `quickstart` an. |
|`type`  |Der Typ Ihres Geräts. Dieses Feld ist erforderlich. |
|`id`  |Die ID Ihres Geräts. Dieses Feld ist erforderlich. |
|`auth-method`   |Die zu verwendende Authentifizierungsmethode. Der einzige Wert, der aktuell unterstützt ist, lautet `token`. |
|`auth-token`   |Ein Authentifizierungstoken zum Herstellen einer sicheren Verbindung zwischen Ihrem Gerät und Watson IoT Platform. |
|`clean-session`|Der Wert 'true' oder 'false', der nur erforderlich ist, wenn Sie die Anwendung im Modus der permanenten Subskription verbinden möchten. Die Standardeinstellung für `clean-session` lautet `true`. |

**Hinweis:** Um das Gerät im Modus der permanenten Subskription zu verbinden, legen Sie für `clean-session` die Einstellung `false` fest. Weitere Informationen zur bereinigten Sitzung (clean session) finden Sie im Abschnitt 'Subskriptionspuffer und bereinigte Sitzung' der [MQTT-Dokumentation](../../reference/mqtt/index.html#subscription-buffers-and-clean-session). 

Das properties-Objekt erstellt Definitionen, die für die Interaktion mit dem {{site.data.keyword.iot_short_notm}}-Modul verwendet werden. 

Der folgende Code zeigt ein Gerät, das im Quickstart-Modus Ereignisse publiziert. 

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Stellen Sie gerätespezifische Daten mithilfe der Klasse 'Properties' bereit
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Instanziieren Sie die Klasse durch Übergeben der Eigenschaftendatei
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Stellen Sie eine Verbindung her zu {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generieren Sie ein JSON-Objekt des zu publizierenden Ereignisses
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Quickstart-Ablauf lässt nur Folgendes zu: QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

Das folgende Codebeispiel zeigt, wie Geräte Ereignisse in einem registrierten Ablauf publizieren können. 


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Geben Sie die gerätespezifischen Daten sowie 'Auth-key' und 'token' mithilfe der Klasse 'Properties' an
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instanziieren Sie die Klasse durch Übergeben der Eigenschaftendatei
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Stellen Sie eine Verbindung her zu {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generieren Sie ein JSON-Objekt des zu publizierenden Ereignisses
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registrierter Ablauf lässt Servicequalitätsstufen '0', '1' und '2' zu
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### Konfigurationsdatei verwenden 

Statt ein properties-Objekt direkt zu verwenden, können Sie eine Konfigurationsdatei verwenden, die die Name/Wert-Paare für die Eigenschaften enthält. Wenn Sie eine Konfigurationsdatei verwenden, die ein properties-Objekt enthält, müssen Sie das folgende Codeformat verwenden: 

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Geben Sie die gerätespezifischen Daten sowie 'Auth-key' und 'token' mithilfe der Klasse 'Properties' an
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Instanziieren Sie die Klasse durch Übergeben der Eigenschaftendatei
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Stellen Sie eine Verbindung her zu {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generieren Sie ein JSON-Objekt des zu publizierenden Ereignisses
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registrierter Ablauf lässt Servicequalitätsstufen '0', '1' und '2' zu
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

Der Inhalt der Konfigurationsdatei muss folgendes Format aufweisen: 

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen 
{: #connecting_to_iotp}

Stellen Sie eine Verbindung zu {{site.data.keyword.iot_short_notm}} her, indem Sie die Verbindungsfunktion aufrufen. Die Verbindungsfunktion verlangt den optionalen booleschen Parameter `autoRetry`, dessen Einstellung standardmäßig `true` lautet. Der Parameter `autoRetry` lässt für die Bibliothek zu, die Verbindung zu wiederholen, wenn der Fehler 'MqttException' auftritt. Beachten Sie, dass die Bibliothek keinen erneuten Verbindungsaufbau versucht, wenn MqttSecurityException-Fehler auftreten, weil für die Geräteregistrierung falsche Details verwendet wurden, auch wenn für den Parameter `autoRetry` die Einstellung `true` festgelegt ist. 

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

Nach dem erfolgreichen Herstellen einer Verbindung zum {{site.data.keyword.iot_short_notm}}-Service kann der Geräteclient Operationen wie beispielsweise das Publizieren von Ereignissen und das Subskribieren von Gerätebefehlen von einer Anwendung aus ausführen. 


## Ereignisse publizieren 
{: #publishing_events}

Ereignisse sind der Mechanismus, über den Geräte Daten in {{site.data.keyword.iot_short_notm}} publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu. 

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gerät an; dies bedeutet, dass ein Gerät nicht die Identität eines anderen Geräts annehmen kann. 

Ereignisse können mit einer beliebigen der drei durch das MQTT-Protokoll definierten [Servicequalitätsstufen (Qos)](../../reference/mqtt/index.html#qos-levels) publiziert werden. Standardmäßig werden Ereignisse mit der Servicequalitätsstufe '0' (Qos=0) publiziert. 

### Ereignisse mit der standardmäßigen Servicequalitätsstufe publizieren 

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### Servicequalitätsstufe für ein Ereignis erhöhen 

Sie können die [Servicequalitätsstufen](../../reference/mqtt/index.html#qos-levels) für zu publizierende Ereignisse erhöhen. Ereignisse, die eine höhere Servicequalitätsstufe als null aufweisen, benötigen für die Publizierung möglicherweise mehr Zeit, da zusätzliche Empfangsbestätigungsinformationen enthalten sind. 

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registrierter Ablauf lässt Servicequalitätsstufen '0', '1' und '2' zu
myClient.publishEvent("status", event, 2);
```

### Ereignisse mithilfe von HTTP publizieren 

Zusätzlich zu MQTT können Geräte Ereignisse in {{site.data.keyword.iot_short_notm}} mithilfe von HTTP und mithilfe der folgenden Schritte publizieren: 

* Erstellen Sie mithilfe der Eigenschaftendatei eine Geräteclientinstanz (DeviceClient). 
* Erstellen Sie ein Ereignis, das publiziert werden muss. 
* Geben Sie den Ereignisnamen an und publizieren Sie das Ereignis mithilfe der Methode `publishEventOverHTTP()`, wie im folgenden Code gezeigt: 

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

Sie finden den vollständigen Code im Gerätebeispiel [HttpDeviceEventPublish]. 

Je nach den Einstellungen in der Eigenschaftendatei wird das Ereignis mit der Methode `publishEventOverHTTP()` entweder im Quickstart-Modus oder im Modus des registrierten Ablaufs publiziert. Wenn `quickstart` die in der Eigenschaftendatei angegebene Organisations-ID ist, publiziert die Methode `publishEventOverHTTP()` das Ereignis an den Quickstart-Service des Gerätebeispiels und publiziert das Ereignis im einfachen HTTP-Format. Wenn in der Eigenschaftendatei eine gültige registrierte Organisation verwendet wird, publiziert die Methode das Ereignis immer in HTTPS, bei dem es sich um HTTP over SSL handelt, damit die gesamte Kommunikation geschützt ist. 

Das HTTP-Protokoll bietet die Zustellung 'höchstens einmal', die der Servicequalitätsstufe 'höchstens einmal' (QoS 0) des MQTT-Protokolls ähnelt. Wenn Sie die Zustellungsart 'höchstens einmal' zum Publizieren von Ereignissen verwenden, muss die Anwendung die Wiederholungslogik implementieren, falls ein Fehler auftritt. 

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Befehle verarbeiten 
{: #handling_commands}

Wenn der Geräteclient eine Verbindung herstellt, subskribiert er automatisch alle für dieses Geräte geltenden Befehle. Zum Verarbeiten bestimmter Befehle müssen Sie eine Callback-Methode für Befehle registrieren.
Die Nachrichten werden als Instanz der Befehlsklasse zurückgegeben, die folgende Eigenschaften aufweist: 

| Eigenschaft      |Datentyp      | Beschreibung |
|----------------|----------------|
|`payload` |java.lang.String| Die Angaben für die Nachrichtennutzdaten. |
|`format`  |java.lang.String| Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'. |
|`command`   |java.lang.String|Gibt den Befehl an. |
|`timestamp`   |org.joda.time.DateTime|Das Datum und die Uhrzeit des Ereignisses. |


``` sourceCode
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implementieren Sie die Klasse 'CommandCallback', um anzugeben, wie der Befehl verarbeitet werden soll
class MyNewCommandCallback implements CommandCallback, Runnable {

    // Eine Warteschlange, die die Befehle für eine reibungslose Verarbeitung von MQTT-Nachrichten enthält & handhabt
    private BlockingQueue<Befehl> queue = new LinkedBlockingQueue<Befehl>();

    /**
    * Diese Methode wird von der Bibliothek stets aufgerufen, wenn ein Befehl vorhanden ist, der mit den Subskriptionskriterien übereinstimmt
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
    public void run() {
        while(true) {
            Command cmd = null;
            try {
                //In diesem Beispiel wird nur der Befehl gezeigt
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Geben Sie die gerätespezifischen Daten sowie 'Auth-key' und 'token' mithilfe der Klasse 'Properties' an
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instanziieren Sie die Klasse durch Übergeben der Eigenschaftendatei
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Übergeben Sie das oben implementierte Element 'CommandCallback' als Argument an diesen Geräteclient
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Stellen Sie eine Verbindung her zu {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## Beispiele 
{: #samples}

Im [GitHub-Repository](https://github.com/ibm-messaging/iot-device-samples/tree/master/java) finden Sie eine Liste der mit der {{site.data.keyword.iot_short_notm}}-Java-Client-Bibliothek entwickelten Beispiele für Geräte und das Gerätemanagement. 
