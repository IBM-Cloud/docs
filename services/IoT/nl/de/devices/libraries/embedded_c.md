---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Embedded C für Geräteentwickler
{: #embedded_c}

Verwenden Sie Embedded C, um Geräte zu erstellen und anzupassen, die in {{site.data.keyword.iot_full}} mit Ihrer Organisation interagieren. Verwenden Sie die bereitgestellten Informationen und Beispiele, um mit der Entwicklung Ihrer Geräte mithilfe von Embedded C zu beginnen.
{:shortdesc}

## Embedded C-Client und Ressourcen herunterladen
{: #embeddedc_client_download}

Wechseln Sie für den Zugriff auf die Embedded C-Clientbibliotheken und Beispiele für {{site.data.keyword.iot_short_notm}} in GitHub in das Repository [iotf-embeddedc ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-messaging/iotf-embeddedc){: new_window} und folgen Sie den Installationsanweisungen.


## Abhängigkeiten
{: #dependencies}

|Abhängigkeit |Beschreibung|
|:---|:---|
|[Bibliothek für Eclipse Paho Embedded C ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git){: new_window} |Stellt eine MQTT-C-Clientbibliothek bereit. Weitere Informationen finden Sie in [MQTT Client Package -  C for embedded devices ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}.|


## Installation
{: #installation}

Führen Sie folgende Anweisungen aus, um die {{site.data.keyword.iot_short_notm}}-Clientbibliothek für Embedded C zu installieren:

1. Zum Installieren der neuesten Bibliotheksversion geben Sie in der Befehlszeile folgenden Code ein:
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Kopieren Sie die TAR-Datei (.tar) der Paho-Bibliothek in das Verzeichnis *lib*.
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. Extrahieren Sie die Bibliotheksdatei.
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
Der heruntergeladene Client hat folgende Dateistruktur:

```
 |-lib - enthält alle abhängigen Dateien
 |-samples - enthält die Beispiele 'helloWorld' und 'sampleDevice'
   |-sampleDevice.c - Implementierung eines Beispielgeräts
   |-helloworld.c - Quickstart-Anwendung
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - Haupt-Clientdatei
 |-iotfclient.h - Headerdatei für den Client
```

## Clientbibliothek initialisieren
{: #initialize_client_library}

Nachdem die Clientbibliothek heruntergeladen wurde, muss sie initialisiert und mit {{site.data.keyword.iot_short_notm}} verbunden werden. Sie können die {{site.data.keyword.iot_short_notm}}-Clientbibliothek für Embedded C initialisieren, indem Sie Parameter übergeben oder eine Konfigurationsdatei verwenden.

### Parameter übergeben

Die Funktion `initialize` verwendet folgende Parameter, um eine Verbindung zum {{site.data.keyword.iot_short_notm}}-Service herzustellen:

|Definition |Beschreibung |
|:---|:---|
|`client`|Ein Verweis auf *iotfclient*.|
|`org`|Die ID Ihrer Organisation.|
|`type` |Der Typ Ihres Geräts.|
|`id` |Die Geräte-ID.|
|`auth-method` |Die zu verwendende Authentifizierungsmethode. Der einzige Wert, der aktuell unterstützt ist, lautet `token`.|
|`auth-token`|Ein Authentifizierungstoken zum Herstellen einer sicheren Verbindung zwischen Ihrem Gerät und Watson IoT Platform.|


```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"org","type","id","auth-method","auth-token");
	....
```

### Konfigurationsdatei verwenden

Sie können auch eine Konfigurationsdatei verwenden, um die Embedded C-Clientbibliothek zu initialisieren. Die Funktion `initialize_configfile` verwendet den Pfad der Konfigurationsdatei als Parameter.

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

Die Konfigurationsdatei muss folgendes Format verwenden:

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## Herstellen der Verbindung zum Service
{: #connecting_service}

Nach dem Initialisieren der Embedded C-Clientbibliothekt von {{site.data.keyword.iot_short_notm}} können Sie eine Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen, indem Sie die Funktion `connectiotf` aufrufen.

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	char *configFilePath = "./device.cfg";

	rc = initialize_configfile(&client, configFilePath);

	if(rc != SUCCESS){
		printf("initialize failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}

	rc = connectiotf(&client);

	if(rc != SUCCESS){
		printf("Connection failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}
	....
```

## Befehle verarbeiten
{: #handling_commands}

Wenn der Geräteclient eine Verbindung herstellt, subskribiert er automatisch alle für dieses Gerät geltenden Befehle. Zum Verarbeiten bestimmter Befehle müssen Sie eine Callback-Funktion für Befehle registrieren, indem Sie die Funktion `setCommandHandler` aufrufen. Die Callback-Funktion weist folgende Eigenschaften auf:

|Eigenschaft |Beschreibung|
|:---|:---|
|`commandName`  |Der Name des aufgerufenen Befehls. |  
|`format`  |Das Format des Ereignisses. Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel 'JSON'.|
|`payload`  |Die Angaben für die Nutzdaten des Befehls. Die maximale Länge beträgt 131072 Byte. |


```
	#include "iotfclient.h"

	void myCallback (char* commandName, char* format, void* payload)
	{
	printf("The command received :: %s\n", commandName);
	printf("format : %s\n", format);
	printf("Payload is : %s\n", (char *)payload);
	}
	...
	...
	char *filePath = "./device.cfg";
	rc = connectiotfConfig(filePath);
	setCommandHandler(myCallback);

	yield(1000);
	....

```
**Hinweis:** Die Funktion `yield()` ermöglicht es dem Gerät, Befehle von Watson IoT Platform zu empfangen und die Verbindung aufrecht zu erhalten. Wenn die Funktion `yield()` nicht innerhalb des durch das Keepalive-Intervall vorgegebenen Zeitrahmens aufgerufen wird, werden von Watson IoT Platform gesendete Befehle nicht vom Gerät empfangen. Der der Funktion `yield()` zugeordnete Wert gibt die Länge der Zeit (in Millisekunden) an, während der Daten aus dem Socket gelesen werden können, bevor die Steuerung an die Anwendung zurückgegeben wird.

## Ereignisse publizieren
{: #publishing_events}

Ereignisse können mit folgenden Eigenschaften publiziert werden:

|Eigenschaft |Beschreibung|
|:---|:---|
|eventType  |Der Typ des zu publizierenden Ereignisses, beispielsweise 'status' oder 'gps'. |  
|eventFormat  |Das Format kann eine beliebige Zeichenfolge sein, zum Beispiel `json`. |
|data  |Die Angaben für die Nutzdaten. Die maximale Länge beträgt 131072 Byte. |
|QoS  |Die Servicequalitätsstufe für das zu publizierende Ereignis. Unterstützte Werte sind `0`, `1`, `2`.|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## Verbindung zum Client trennen
{: #disconnect_client}

Zum Trennen der Verbindung zum Client und zum Freigeben der Verbindungen führen Sie das folgende Code-Snippet aus:

```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", payload , QOS0);
	...
	rc = disconnect();
	....
```

## Beispiele
{: #samples}

Beispielcode für Geräte und Anwendungen wird in [GitHub ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples){: new_window} bereitgestellt.
