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


# mBed C++ für Geräteentwickler
{: #mbedcpp}

Verwenden Sie die [mBed C++-Clientbibliothek ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}, um ohne großen Aufwand eine Verbindung zwischen [mBed-Geräten ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.mbed.com/en/){: new_window}, wie beispielsweise [LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) oder [FRDM-K64F ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/platforms/FRDM-K64F/){: new_window}, und dem {{site.data.keyword.iot_full}}-Service herzustellen.
{:shortdesc}

Weitere Informationen finden Sie in [ibmiotf ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window} unter [developer.mbed.org ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/){: new_window}.

Die Bibliothek verwendet zwar C++, es wird jedoch vermieden, dynamische Speicherzuordnungen und STL-Funktionen zu verwenden, da die mBed-Geräte in manchen Fällen idiosynkratische Speichermodelle aufweisen, die Probleme bei der Portierbarkeit verursachen können. In jedem Fall ermöglicht die Bibliothek es Ihnen die Speicherbelegung so vorhersehbar wie möglich zu gestalten.

## Abhängigkeiten
{: #dependencies}

|Abhängigkeit |Beschreibung|
|:---|:---|
|[Eclipse Paho-MQTT-Bibliothek ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/teams/mqtt/code/MQTT/){: new_window}|Bietet eine MQTT-Clientbibliothek für mBed-Geräte. Weitere Informationen finden Sie in [Eingebettete MQTT-C/C++-Clientbibliotheken ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}|
|[Ethernet-Schnittstellenbibliothek ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/){: new_window}|Eine mBed-IP-Bibliothek über Ethernet.|

## Verwendung der Bibliothek
{: #library_use}

Verwenden Sie bei Verwendung der mBed C++-Clientbibliothek 'IBMIoTF' den [mBed-Compiler ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/compiler/){: new_window}, um Ihre Anwendungen zu erstellen. Der mBed-Compiler stellt eine schlanke C/C++-Online-IDE zur Verfügung, die für das Schreiben, Kompilieren und Herunterladen von Programmen konfiguriert wurde, die auf Ihrem mBed-Mikrocontroller ausgeführt werden sollen.

**Hinweis:** Für die Ausführung von mBed müssen Sie nichts installieren oder einrichten.

Informationen zur Vorgehensweise beim Herstellen einer Verbindung zwischen dem Mikrocontroller ARM mBed NXP LPC 1768 und {{site.data.keyword.iot_short_notm}} finden Sie in der Anleitung [mBed-C++-Clientbibliothek für IBM Watson IoT Platform ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/){: new_window}.

## Konstruktor
{: #constructor}

Der Konstruktor erstellt die Clientinstanz und akzeptiert folgende Parameter:

|Parameter |Beschreibung |
|:---|:---|
|`org` |Die ID Ihrer Organisation. Dieser Wert ist erforderlich. Wenn Sie einen Quickstart-Ablauf verwenden, geben Sie `quickstart` an.|
|`type`   |Der Typ Ihres Geräts. Dieses Feld ist erforderlich.|
|`id`   |Die ID Ihres Geräts. Dieses Feld ist erforderlich.|
|`auth-method`   |Die Authentifizierungsmethode; hier handelt es sich um ein optionales Feld, das nur für den registrierten Ablauf erforderlich ist. Der einzige Wert, der aktuell unterstützt ist, lautet `token`.|
|`auth-token`   |Ein Authentifizierungstoken zum Herstellen einer sicheren Verbindung zwischen Ihrem Gerät und Watson IoT Platform. Dies ist ein optionales Feld, das nur für einen registrierten Ablauf erforderlich ist.|

Diese Parameter erstellen Definitionen, die für die Interaktion mit dem {{site.data.keyword.iot_short_notm}}-Service verwendet werden.

Das folgende Codebeispiel zeigt, wie eine DeviceClient-Instanz mit dem Quickstart-Service von {{site.data.keyword.iot_short_notm}} interagieren kann:

```
  #include "DeviceClient.h"
  ....
  ....

  // Legen Sie {{site.data.keyword.iot_short_notm}}-Verbindungsparameter fest
  char organization[11] = "quickstart";     // Ist bei einer registrierten Verbindung durch Ihre 'Organisation' zu ersetzen
  char deviceType[8] = "LPC1768";           // Ist bei einer registrierten Verbindung durch Ihren Gerätetyp zu ersetzen
  char deviceId[3] = "01";                  // Ist bei einer registrierten Verbindung durch Ihre Geräte-ID zu ersetzen

  // Erstellen Sie 'DeviceClient'
  IoTF::DeviceClient client(organization, deviceType, deviceId);

  // Rufen Sie im Quickstart-Modus und falls die Geräte-ID nicht angegeben ist 'DeviceID(MAC Address)' ab
  if((strcmp(organization, QUICKSTART) == 0) && (strcmp("", deviceId) == 0))
  {
  	char tmpBuf[50];
  	client.getDeviceId(tmpBuf, sizeof(tmpBuf));
  }
  ....
```

Wie im vorangegangenen Codebeispiel gezeigt, verwendet 'DeviceClient' zum Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} die MAC-Adresse des Geräts, wenn die Geräte-ID nicht angegeben ist. Der Gerätecode kann die Methode `getDeviceId()` verwenden, um die Geräte-ID aus der DeviceClient-Instanz abzurufen.

Der folgende Codeblock zeigt, wie eine DeviceClient-Instanz erstellt wird, sodass sie mit der registrierten Organisation von {{site.data.keyword.iot_short_notm}} interagiert.

```
  #include "DeviceClient.h"
  ....
  ....

  // Legen Sie {{site.data.keyword.iot_short_notm}}-Verbindungsparameter fest
  char organization[11] = "hrcl78";
  char deviceType[8] = "LPC1768";
  char deviceId[3] = "LPC176801";
  char method[6] = "token";
  char token[9] = "password";

  // Erstellen Sie 'DeviceClient'
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);
  ....
```

## Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen
{: #connecting_to_iotp}

Das Gerät kann eine Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen, indem es die Verbindungsfunktion in der DeviceClient-Instanz aufruft.

```
  #include "DeviceClient.h"
  ....
  ....

  // Erstellen Sie 'DeviceClient'
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
Nach dem erfolgreichen Herstellen der Verbindung kann das Gerät in {{site.data.keyword.iot_short_notm}} Ereignisse publizieren und für Befehle empfangsbereit sein.

Das Gerät kann darüber hinaus den Status der Verbindung mithilfe der Methode `isConnected()` abfragen; dies wird im folgenden Beispiel gezeigt:

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## Ereignisse publizieren
{: #publishing_events}

Ereignisse sind der Mechanismus, über den Geräte Daten in {{site.data.keyword.iot_short_notm}} publizieren. Das Gerät steuert den Inhalt des Ereignisses und ordnet jedem Ereignis, das von ihm gesendet wird, einen Namen zu.

Wenn ein Ereignis von der {{site.data.keyword.iot_short_notm}}-Instanz empfangen wird, geben die Berechtigungsnachweise des empfangenen Ereignisses das sendende Gerät an; dies bedeutet, dass ein Gerät nicht die Identität eines anderen Geräts annehmen kann.

Ereignisse können mit einer beliebigen der drei durch das MQTT-Protokoll definierten [Servicequalitätsstufen (Qos)](../../reference/mqtt/index.html#qos-levels) publiziert werden. Standardmäßig werden Ereignisse mit der Servicequalitätsstufe (QoS) '0' publiziert.

### Ereignis mithilfe der standardmäßigen Servicequalität publizieren

Das folgende Beispiel zeigt, wie folgende Datenpunkte im JSON-Format in {{site.data.keyword.iot_short_notm}} publiziert werden:

- LPC1768, wie beispielsweise die X-, Y- und Z-Achse
- Joystickposition
- Aktuell gemessener Temperaturwert

```
	boolean status = client.connect();

	// Erstellen Sie einen Puffer, der das Ereignis enthalten soll
	char buf[250];

	// Erstellen Sie eine Ereignisnachricht mit den gewünschten Datenpunkten im JSON-Format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf);
	....
```
Das vollständige Beispiel finden Sie im [ IBMIoTClientLibrarySample ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}.

### Servicequalitätsstufe für ein Ereignis erhöhen

Sie können die [Servicequalitätsstufen](../../reference/mqtt/index.html#qos-levels) für zu publizierende Ereignisse erhöhen. Ereignisse, die eine höhere Servicequalitätsstufe als `0` aufweisen, benötigen für die Publizierung möglicherweise mehr Zeit, da zusätzliche Empfangsbestätigungsinformationen enthalten sind.

**Hinweis:** Der Modus für den Quickstart-Ablauf unterstützt nur Servicequalitätsstufe '0'.

```
	#include "MQTTClient.h"

	boolean status = client.connect();

	// Erstellen Sie einen Puffer, der das Ereignis enthalten soll
	char buf[250];

	// Erstellen Sie eine Ereignisnachricht mit den gewünschten Datenpunkten im JSON-Format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf, MQTT::QOS2);
	....
```

### Verarbeiten des Verbindungsunterbrechungsfehlers beim Publizieren von Ereignissen


Wenn die Methode `publishEvent()` den falschen Wert zurückgibt, können Sie den Status der Verbindung überprüfen und die Methode `reConnect()` aufrufen, falls die Verbindung verloren wurde.

```
	#include "MQTTClient.h"

	status = client.publishEvent("blink", buf, MQTT::QOS2);

	if(status == false) {
	    // Überprüfen Sie, ob die Verbindung verloren wurde und wiederholen Sie den Versuch
	    while(!client.isConnected())
	    {
	        client.reConnect();
	        wait(5.0);
	    }
	}
	....
```
Die Bibliothek speichert keine Ereignisse, die während der Verbindungsunterbrechung publiziert wurden, sodass das Gerät die Methode `publishEvent()` erneut aufrufen muss, um diese Ereignisse nach dem erneuten Verbindungsaufbau zu senden.


## Befehle verarbeiten
{: #handling_commands}

Wenn der Geräteclient eine Verbindung herstellt, subskribiert er automatisch alle für dieses Geräte geltenden Befehle. Zum Verarbeiten bestimmter Befehle müssen Sie eine Callback-Methode für Befehle registrieren.
Die Nachrichten werden als Instanz der Befehlsklasse zurückgegeben, die folgende Eigenschaften aufweist:

|Eigenschaft |Beschreibung|
|:---|:---|
|`command` | Der Name des aufgerufenen Befehls.|  
|`format`  |Das Format des Ereignisses. Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'. |
|`payload`  |Die Angaben für die Nutzdaten des Befehls. Die maximale Länge beträgt 131072 Byte. |


Mit dem folgenden Code wird eine Callback-Beispielfunktion für Befehle definiert, die den Befehl für das LED-Blinkintervall von der Anwendung verarbeitet und zur DeviceClient-Instanz hinzufügt.

```
    #include "DeviceClient.h"
    #include "Command.h"

    // Befehl verarbeiten und LED-Blinkintervall festlegen
    void processCommand(IoTF::Command &cmd)
    {
        if (strcmp(cmd.getCommand(), "blink") == 0)
    	{
    	    char *payload = cmd.getPayload();
    	    char* pos = strchr(payload, '}');
    	    if (pos != NULL) {
    	        *pos = '\0';
    	        char* ratepos = strstr(payload, "rate");
    	        if(ratepos == NULL)
    	            return;
    	        if ((pos = strchr(ratepos, ':')) != NULL)
    	        {
    	            int blink_rate = atoi(pos + 1);
    	            blink_interval = (blink_rate <= 0) ? 0 : (blink_rate > 50 ? 1 : 50/blink_rate);
    	        }
    	    }
    	} else {
            WARN("Unsupported command: %s\n", cmd.getCommand());
        }
    }

    client.setCommandCallback(processCommand);

    client.yield(1000);  // Für den MQTT-Client den Empfang von Nachrichten zulassen
    ....
```
Das vollständige Beispiel finden Sie im [ IBMIoTClientLibrarySample ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}.

**Hinweis:** Damit Befehle empfangen werden, muss in bestimmten Abständen die Funktion `client.yield()` aufgerufen werden.
Die Funktion `client.yield()` ermöglicht es dem Gerät, Befehle von Watson IoT Platform zu empfangen und die Verbindung aufrecht zu erhalten. Wenn die Funktion `client.yield()` nicht innerhalb des durch das Keepalive-Intervall vorgegebenen Zeitrahmens aufgerufen wird, werden von Watson IoT Platform gesendete Befehle nicht vom Gerät empfangen. Der der Funktion `client.yield()` zugeordnete Wert gibt die Länge der Zeit (in Millisekunden) an, während der Daten aus dem Socket gelesen werden können, bevor die Steuerung an die Anwendung zurückgegeben wird.

## Verbindung zum Client trennen
{: #disconnect_client}

Zum Trennen der Verbindung zum Client und zum Freigeben der Verbindungen führen Sie das folgende Code-Snippet aus:

```
	...
	client.disconnect();
	....
```
## Beispiele
{: #samples}

[IBMIoTClientLibrarySample ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/){: new_window} ist ein Codebeispiel, in dem gezeigt wird, wie die {{site.data.keyword.iot_short_notm}}-Clientbibliothek zum Herstellen einer Verbindung zwischen den Geräten 'mbed LPC1768' oder 'FRDM-K64F' und der Serviceinstanz verwendet werden kann.
