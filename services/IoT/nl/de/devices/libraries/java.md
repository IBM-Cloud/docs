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

# Java für Geräteentwickler
{: #java}

Sie können mithilfe von Java™ Geräte erstellen und anpassen, die in {{site.data.keyword.iot_full}} mit Ihrer Organisation interagieren. Es werden eine Java-Clientbibliothek für {{site.data.keyword.iot_short_notm}}, Dokumentation und Beispiele bereitgestellt, die Sie bei den ersten Schritten der Geräteentwicklung unterstützen.
{:shortdesc}

## Java-Client und Ressourcen herunterladen
{: #java_client_download}

Wechseln Sie für den Zugriff auf die Java-Clientbibliotheken und Beispiele für {{site.data.keyword.iot_short_notm}} in das Repository [iot-java ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-java){: new_window} in GitHub und folgen Sie den Installationsanweisungen.

## Konstruktor
{: #constructor}

Der Konstruktor erstellt die Clientinstanz und akzeptiert das `Properties`-Objekt, das folgende Definitionen enthält:

|Definition |Beschreibung |
|:----|:----|
|`org` |Erforderlicher Wert, für den die ID Ihrer Organisation eingestellt werden muss. Wenn Sie einen Quickstart-Ablauf verwenden, geben Sie `quickstart` an.|
|`type`  |Erforderlicher Wert, der den Typ des Geräts angibt.|
|`id`  |Erforderlicher Wert, der die eindeutige ID des Geräts angibt.|
|`auth-method`  |Die zu verwendende Authentifizierungsmethode. Die einzige Methode, die unterstützt ist, lautet `token`.|
|`auth-token`   |Ein Authentifizierungstoken zum Herstellen einer sicheren Verbindung zwischen Ihrem Gerät und {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Der Wert 'true' oder 'false', der nur erforderlich ist, wenn Sie die Anwendung im Modus der permanenten Subskription verbinden möchten. Für `clean-session` ist standardmäßig der Wert 'true' festgelegt.|
|`Port`|Die Nummer des Ports, zu dem eine Verbindung hergestellt werden soll. Geben Sie entweder 8883 oder 443 an. Wenn Sie keine Portnummer angeben, stellt der Client standardmäßig eine Verbindung zu {{site.data.keyword.iot_short_notm}} über den Port Nummer 8883 her.|
|`MaxInflightMessages`  |Legt die maximale Anzahl der gerade ausgeführten Nachrichten für die Verbindung fest. Der Standardwert ist 100.|
|`Automatic-Reconnect`  |Der Wert 'true' oder 'false', der erforderlich ist, wenn Sie das Gerät automatisch erneut mit {{site.data.keyword.iot_short_notm}} verbinden möchten, während es sich im nicht verbundenen Status befindet. Der Standardwert ist 'false'.|
|`Disconnected-Buffer-Size`|Die maximale Anzahl Nachrichten, die im Speicher gespeichert werden kann, während die Verbindung zum Client getrennt ist. Der Standardwert ist '5000'.|
|`WebSocket`|Der Wert 'true' oder 'false', der erforderlich ist, wenn Sie WebSocket-Verbindungen mit {{site.data.keyword.iot_short_notm}} verwenden möchten. Der Standardwert ist 'false'.|

**Hinweis:** Um das Gerät im Modus der permanenten Subskription zu verbinden, legen Sie für `clean-session` die Einstellung `false` fest. Weitere Informationen zur bereinigten Sitzung (clean session) finden Sie im Abschnitt 'Subskriptionspuffer und bereinigte Sitzung' der [MQTT-Dokumentation](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

Das `Properties`-Objekt erstellt Definitionen, die für die Interaktion mit dem {{site.data.keyword.iot_short_notm}}-Modul verwendet werden.

Das folgende Codebeispiel zeigt, wie Geräte Ereignisse im Quickstart-Modus publizieren können.

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

Statt ein `Properties`-Objekt direkt zu verwenden, können Sie eine Konfigurationsdatei verwenden, die die Name/Wert-Paare für die Eigenschaften enthält. Wenn Sie eine Konfigurationsdatei verwenden, die das `Properties`-Objekt enthält, müssen Sie das folgende Codeformat verwenden:

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


Verwenden Sie zum Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} die Funktion `connect()`. Die Funktion `connect()` enthält einen optionalen booleschen Parameter mit der Bezeichnung `autoRetry`, mit dem festgelegt wird, ob die Bibliothek bei Auftreten des Verbindungsfehlers 'MqttException' versucht, die Verbindung erneut herzustellen. Für `autoRetry` ist standardmäßig der Wert 'true' festgelegt. Wenn die Verbindung mit 'MqttSecurityException' fehlschlägt, da falsche Details für die Geräteregistrierung übergeben wurden, versucht die Bibliothek nicht, die Verbindung erneut herzustellen, auch wenn für `autoRetry` die Einstellung 'true' festgelegt ist.

Zum Festlegen des Keepalive-Intervalls für MQTT können Sie vor dem Aufrufen der Funktion `connect()` optional die Methode `setKeepAliveInterval(int)` verwenden. Der Wert für `setKeepAliveInterval(int)` wird in Sekunden gemessen und definiert die maximale Länge des Zeitintervalls zwischen Nachrichten, die gesendet oder empfangen werden. Wird dies verwendet, kann der Client erkennen, dass der Server nicht mehr verfügbar ist, ohne dass gewartet werden muss, bis das Ende des TCP/IP-Zeitlimitintervalls erreicht ist. Der Client stellt sicher, dass während jedes Keepalive-Intervalls mindestens eine Nachricht im Netz unterwegs ist. Wenn während des Zeitlimitintervalls null datenbezogene Nachrichten empfangen werden, sendet der Client eine kurze Pingnachricht (`ping`), die der Server bestätigt. Für `setKeepAliveInterval(int)` wird als Wert standardmäßig '60 Sekunden' eingestellt. Um auf dem Client die Keepalive-Verarbeitungsfunktion zu inaktivieren, legen Sie für `setKeepAliveInterval(int)` den Wert '0' fest.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

Zum Steuern der Anzahl von Wiederholungen, die bei Auftreten eines Verbindungsfehlers erfolgen sollen, verwenden Sie die überladene Funktion 'connect(int numberOfTimesToRetry)'.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

Nachdem Ihre Geräte erfolgreich eine Verbindung zu {{site.data.keyword.iot_short_notm}} hergestellt haben, können sie Ereignisse publizieren und Gerätebefehle einer Anwendung subskribieren.


## Ereignisse publizieren
{: #publishing_events}

Ereignisse sind der Mechanismus, über den Geräte Daten in {{site.data.keyword.iot_short_notm}} publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gerät an; dies bedeutet, dass ein Gerät nicht die Identität eines anderen Geräts annehmen kann.

Ereignisse können mit einer beliebigen der drei durch das MQTT-Protokoll definierten [Servicequalitätsstufen (Qos)](../../reference/mqtt/index.html#qos-levels) publiziert werden.  Standardmäßig werden Ereignisse mit der Servicequalitätsstufe '0' (Qos=0) publiziert.

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

Sie können die [Servicequalitätsstufen](../../reference/mqtt/index.html#qos-levels) für zu publizierende Ereignisse erhöhen. Ereignisse mit einer höheren Servicequalitätsstufe als null benötigen für die Publizierung möglicherweise mehr Zeit, da zusätzliche Empfangsbestätigungsinformationen enthalten sind.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registrierter Ablauf lässt Servicequalitätsstufen '0', '1' und '2' zu
myClient.publishEvent("status", event, 2);
```

### Ereignisse in angepassten Formaten publizieren

Ereignisse können in verschiedenen Formaten publiziert werden, beispielsweise JSON, Zeichenfolgeformat, binäres Format und weitere. Die Bibliothek publiziert Ereignisse standardmäßig im JSON-Format; Sie können die Daten jedoch in anderen Formaten angeben, falls Sie dies vorziehen. Verwenden Sie das folgende Codesnippet, wenn Sie Daten beispielsweise im Zeichenfolgeformat publizieren möchten.

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**Hinweis:** Im oben stehenden Codebeispiel müssen die Nutzdaten des Ereignisses das Zeichenfolgeformat aufweisen.

Alle XML-Daten können in das Zeichenfolgeformat konvertiert und wie folgt publiziert werden:

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

Verwenden Sie ähnlich dazu die im folgenden Beispiel gezeigte Bytefeldgruppe, um Ereignisse im Binärformat zu publizieren:

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Ereignisse mithilfe von HTTP publizieren
{: #publishing_events_http}


Zusätzlich zur Verwendung von MQTT können Sie Ihre Geräte auch so konfigurieren, dass Ereignisse in {{site.data.keyword.iot_short_notm}} über HTTP publiziert werden. In den folgenden Schritten wird die Abfolge für das Publizieren von Ereignissen über HTTP beschrieben:

1. Erstellen Sie mithilfe der Eigenschaftendatei eine Geräteclientinstanz (`DeviceClient`).
2. Erstellen Sie ein Ereignis, das publiziert werden soll.
3. Geben Sie den Ereignisnamen an und publizieren Sie das Ereignis anschließend mithilfe der Methode `publishEventOverHTTP()`, wie im folgenden Codebeispiel gezeigt:

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

Zum Lesen des gesamten Codes zeigen Sie das Gerätebeispiel [HttpDeviceEventPublish] an.

Je nach den Einstellungen in der Eigenschaftendatei wird das Ereignis mit der Methode `publishEventOverHTTP()` entweder im Quickstart-Modus oder im Modus des registrierten Ablaufs publiziert. Wenn als Organisations-ID in der Eigenschaftendatei `quickstart` festgelegt ist, publiziert die Methode `publishEventOverHTTP()` das Ereignis an den Quickstart-Service des Gerätebeispiels und publiziert das Ereignis im einfachen HTTP-Format. Wenn in der Eigenschaftendatei eine gültige registrierte Organisation angegeben ist, werden Ereignisse sicher mithilfe von HTTPS publiziert.

Das HTTP-Protokoll bietet die Zustellung 'höchstens einmal', die der Servicequalitätsstufe 'höchstens einmal' (QoS 0) des MQTT-Protokolls ähnelt. Wenn Sie die Zustellungsart 'höchstens einmal' zum Publizieren von Ereignissen verwenden, muss die Anwendung bei jedem Fehler, der auftritt, Wiederholungslogik implementieren.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Befehle verarbeiten
{: #handling_commands}

Wenn der Geräteclient eine Verbindung herstellt, subskribiert er automatisch alle für dieses Geräte geltenden Befehle. Zum Verarbeiten bestimmter Befehle müssen Sie eine Callback-Methode für Befehle registrieren.
Die Nachrichten werden als Instanz der Klasse `Command` (Befehl) zurückgegeben, die folgende Eigenschaften enthält:

| Eigenschaft     |Datentyp     | Beschreibung|
|----------------|----------------|
|`payload` |java.lang.String| Die Angaben für die Nachrichtennutzdaten.|
|`format`  |java.lang.String| Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.|
|`command`   |java.lang.String|Gibt den Befehl an.|
|`timestamp`   |org.joda.time.DateTime|Das Datum und die Uhrzeit des Ereignisses.|


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

Eine Liste der mit der {{site.data.keyword.iot_short_notm}}-Java-Clientbibliothek entwickelten Beispiele für Geräte und für das Gerätemanagement finden Sie im [GitHub-Repository 'iot-device-samples' ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-messaging/iot-device-samples/tree/master/java){: new_window}.
