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


# Embedded C for device developers
{: #embedded_c}

You can use Embedded C to build and customize devices that interact with your organization on {{site.data.keyword.iot_full}}. Use the information and examples that are provided to start developing your devices by using Embedded C.
{:shortdesc}

## Downloading the Embedded C client and resources
{: #embeddedc_client_download}

To access the Embedded C client libraries and samples for {{site.data.keyword.iot_short_notm}}, go to the [iotf-embeddedc ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iotf-embeddedc){: new_window} repository in GitHub and complete the installation instructions.


## Dependencies
{: #dependencies}

|Dependency |Description|
|:---|:---|
|[Eclipse Paho Embedded C library ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git){: new_window} |Provides an MQTT C client library. For more information, see [MQTT Client Package -  C for embedded devices ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}.|


## Installation
{: #installation}

To install the {{site.data.keyword.iot_short_notm}} client library for Embedded C, complete the following instructions:

1. To install the latest version of the library, enter the following code on the command line:
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Copy the Paho library .tar file to the *lib* directory.
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. Extract the library file
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
The downloaded client has the following file structure:

```
 |-lib - contains all the dependent files
 |-samples - contains the helloWorld and sampleDevice samples
   |-sampleDevice.c - sample device implementation
   |-helloworld.c - quickstart application
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - Main client file
 |-iotfclient.h - Header file for the client
```

## Initializing the client library
{: #initialize_client_library}

After the client library is downloaded, it must be initialized and connected to the {{site.data.keyword.iot_short_notm}}. You can initialize the {{site.data.keyword.iot_short_notm}} client library for Embedded C by passing parameters or by using a configuration file.

### Passing parameters

The `initialize` function uses the following parameters to connect to the {{site.data.keyword.iot_short_notm}} service:

|Definition |Description |
|:---|:---|
|`client`|A pointer to the *iotfclient*.|
|`org`|Your organization ID.|
|`type` |The type of your device.|
|`id` |The device ID.|
|`auth-method` |The method of authentication to be used. The only value that is currently supported is `token`.|
|`auth-token`|An authentication token to securely connect your device to Watson IoT Platform.|


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

### Using a configuration file

You can also use a configuration file to initialize the Embedded C client library. The `initialize_configfile` function takes the configuration file path as a parameter.

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

The configuration file must use the following format:

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## Connecting to the service
{: #connecting_service}

After you initialize the {{site.data.keyword.iot_short_notm}} Embedded C client library, you can connect to the {{site.data.keyword.iot_short_notm}} by calling the `connectiotf` function.

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

## Handling commands
{: #handling_commands}

When the device client connects, it automatically subscribes to any command for this device. To process specific commands, you need to register a command callback function by calling the `setCommandHandler` function. The callback function has the following properties:

|Property |Description|
|:---|:---|
|`commandName`  |The name of the command that was invoked. |  
|`format`  |The format of the event. The format can be any string, for example JSON.|
|`payload`  |The data for the command payload. Maximum length is 131072 bytes. |


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
**Note:** The ``yield()`` function enables the device to receive commands from the Watson IoT Platform and keeps the connection alive. If the ``yield()`` function is not called within the time frame that is specified by the keepAlive interval, then any commands that are sent from the platform will not be received by the device. The value that is assigned to the ``yield()`` function specifies length of time (in milliseconds) that data can be read from the socket before control is returned to the application.

## Publishing events
{: #publishing_events}

Events can be published with the following properties:

|Property |Description|
|:---|:---|
|eventType  |The type of event that is published, for example status or  gps. |  
|eventFormat  |The format can be any string, for example `json`. |
|data  |The data for the payload. Maximum length is 131072 bytes. |
|QoS  |The Quality of Service level for the publish event. Supported values are `0`, `1`, `2`.|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## Disconnecting the client
{: #disconnect_client}

To disconnect the client and release the connections, run the following code snippet:

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

## Samples
{: #samples}

Sample device and application code are provided in [GitHub ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples){: new_window}.
