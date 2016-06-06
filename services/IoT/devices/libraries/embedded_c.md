---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Embedded C for device developers
{: #embedded_c}

For more information about Embedded C, see [iotf-embeddedc](https://github.com/ibm-messaging/iotf-embeddedc) in GitHub.

## Dependencies
{: #dependencies}

Eclipse [Paho Embedded C library](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git), which provides an MQTT C client library. For more information, see [MQTT Client Package -  C for embedded devices](http://www.eclipse.org/paho/clients/c/embedded/).


## Installation
{: #installation}

To install the {{site.data.keyword.iot_full}} client library for Embedded C, complete the following instructions:

1. To install the latest version of the library, enter the following code on the command line:
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Copy the Paho library .tar file that you downloaded in the previous step to the *lib* directory.
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. Extract the library file
``  cd lib
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

After downloading the client library, it must be initialized and connected to the {{site.data.keyword.iot_short_notm}}. There are 2 ways to initialize the {{site.data.keyword.iot_short_notm}} client library for Embedded C:

### Passing as parameters

The 'initialize' function uses the following details to connect to the {{site.data.keyword.iot_short_notm}} service:

-   client - Pointer to the *iotfclient*
-   org - Your organization ID
-   type - The type of your device
-   id - The device ID
-   authmethod - Method of authentication (the only value currently supported is "token")
-   authtoken - API key token (required if auth-method is "token")

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"orgid","type","id","token","authtoken");
	....
```

### Using a configuration file

You can also use a configuration file to initialize the Embedded C client library. The function 'initialize\_configfile' takes the configuration file path as a parameter.

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

After initializing the {{site.data.keyword.iot_short_notm}} Embedded C client library, you can connect to the {{site.data.keyword.iot_short_notm}} by calling the 'connectiotf' function.

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

When the device client connects, it automatically subscribes to any command for this device. To process specific commands you need to register a command callback function by calling the function 'setCommandHandler'. The commands are returned as:

- commandName - name of the command invoked
- format - e.g json, xml
- payload

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
**Note:** The 'yield' function must be called periodically to receive commands.

## Publishing events
{: #publishing_events}

Events can be published by using:

- eventType - Type of event to be published e.g status, gps
- eventFormat - Format of the event e.g json
- data - Payload of the event
- QoS - qos for the publish event. Supported values : QOS0, QOS1, QOS2

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

To disconnect the client and release the connections, run the following code snippet.

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

Sample device and application code are provided in [GitHub](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples).
