---

copyright:
years: 2016, 2017
lastupdated: "2017-07-19"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Application interface scenario 1 (Beta)
{: #scenario}

******************************************************************************************************************************************
**Important:** Please note that the information management Beta is now closed as we work towards the delivery of an updated and generally available version of this functionality.

The device state functionality of this Beta is now generally available as part of the Data Management feature.  For more information, see [Introduction to data management](../GA_information_management/ga_im_device_twin.html). Please note that there are changes to the HTTP REST APIs and the configuration steps.

The device aggregation functionality of this Beta is not part of the current release but will be generally available soon in a future update.
******************************************************************************************************************************************

Use the following information to create a scenario in which two temperature sensors publish events to {{site.data.keyword.iot_short_notm}}. One sensor measures temperature in degrees Celsius. The other sensor measures temperature in degrees Fahrenheit. These readings are mapped to a single temperature reading that is in degrees Celsius. When a new temperature reading is published by these devices, the value of the property associated with the device state is changed.

## Pre-requisites

You must have a {{site.data.keyword.iot_short_notm}} organization instance and an API key or token for that organization. For more information about API keys and tokens, see [HTTP REST API for applications](../applications/api.html#authentication).

## About this task

In this scenario, two devices are configured.

One device is called *TemperatureSensor1*. This device publishes temperature events that are measured in degrees Celsius. The temperature event is published on the topic `iot-2/evt/tevt/fmt/json` and has the following example payload:
```
{
  “t” : 34.5
}
```

An application interface is also configured. This application interface represents the state for devices of this type in the following structure:
```
{
  “temperature” : <current temperature value in Celsius>
  }
```
This configuration means that you can configure your application to process the value that is associated with **temperature**, rather than configuring your application to process the value that is associated with **t** and to process the value that is associated with **temp** after converting that value to degrees Celsius.

![Mapping between temperature sensor devices and an application on {{site.data.keyword.iot_short_notm}}.](images/Information Management Device example.svg "Mapping between temperature sensor devices and an application on {{site.data.keyword.iot_short_notm}}")  

Use the following example scenario to set up your own interfaces environment.

## If needed, add a Device Type and a Device
{: #step14}

In this scenario, two device types and two device instances are assumed. Device instance *TemperatureSensor1* is associated with device type *EnvSensor1*. Device instance *TemperatureSensor2* is associated with device type *EnvSensor2*.

For information about using REST APIs to add a device type, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Configuration) documentation.

## Step 1: Create an event schema file
{: #step1}

For this scenario, create two event schema files to define the structure of each of the inbound temperature events.

**Important:** For structured [JSON ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://json-schema.org/){:new_window} event payloads, make sure that each level of nesting is properly wrapped in a `"properties"` entry. For example, if the payload is `{"d":{"t":<temp>}}` you might use:
```
 "properties" : {
    "d" : {
      "properties" : {
        "t" : {
          "description" : "Temperature in degrees Celsius",
          "type" : "number",
          "minimum" : -273.15,
          "default" : 0.0
        }
      },
      "required" : ["t"]
    }
  },
  "required" : ["d"]
```

The following example shows how to create a schema file that is called *tEventSchema.json*. This file defines the structure of an inbound event from a temperature sensor that measures temperature in degrees Celsius:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Celsius",
  "properties" : {
    "t" : {
      "description" : "temperature in degrees Celsius",
      "type" : "number",
      "minimum" : -273.15,
      "default" : 0.0
    }
  },
  "required" : ["t"]
}
  ```
**Tip:** Use the “required” parameter to mark one or more properties as required. Required properties must be included in a device message for Watson IoT Platform to update the device state with the device data. A message that does not include the required property is not processed.   

The schema file name *tEventSchema* is used when you create an event schema resource for your event type.

The following example shows how to create a schema file that is called *tempEventSchema.json*. This file defines the structure of an inbound event from a temperature sensor that measures temperature in degrees Fahrenheit:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Fahrenheit",
  "properties" : {
    "temp" : {
      "description" : "temperature in degrees Fahrenheit",
      "type" : "number",
      "minimum" : −459.67,
      "default" : 0.0
    }
  },
  "required" : ["temp"]
}
  ```
The schema file name *tempEventSchema* is used when you create an event schema resource for your event type.   

## Step 2: Create an event schema resource for your event type
{: #step2}

To create an event schema resource, use the following API:

```
POST /schemas
```

The following parameters are required:  

Parameter	|	Description  
------	|	-----  
name	|	Provide a name for the event schema that you are creating.  
schemaFile	|	Path to the local event schema JSON file.  



For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) documentation.

The following example shows how to use cURL to create the event schema resource *tEventSchema.json*:

```curl
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

The following example shows a response to the POST method:

```
{
  "name" : “tEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "contentType" : "application/octet-stream",
  "updated" : "2016-12-06T14:38:52Z",
  "schemaFileName" : "tEventSchema.json",
  "created" : "2016-12-06T14:38:52Z",
  "id" : "5846cd7c6522050001db0e0d",
  "refs" : {
      "content" : "/schemas/5846cd7c6522050001db0e0d/content"
  },
  "schemaType" : "json-schema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
The schema identifier *5846cd7c6522050001db0e0d* that is returned in response to the POST method is required when you add an event schema to your event type.

The following example shows how to use cURL to create the event schema resource *tempEventSchema.json*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

The following example shows a response to the POST method:

```
{
  "schemaType" : "json-schema",
  "schemaFileName" : "tempEventSchema.json",
  "updated" : "2016-12-06T14:44:51Z",
  "name" : "tempEventSchema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "created" : "2016-12-06T14:44:51Z",
  "id" : "5846cee36522050001db0e0e",
  "refs" : {
      "content" : "/schemas/5846cee36522050001db0e0e/content"
  },
  "contentType" : "application/octet-stream",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```
The schema identifier *5846cee36522050001db0e0e* that is returned in response to the POST method is required when you add an event schema to your event type.

## Step 3: Create an event type that references the event schema
{: #step3}

Each event type references the relevant event schema that was created in the previous example by using the schema identifier returned in the response to the POST method used to create the event schema resource.

To create an event type, use the following API:

```
POST /event/types
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
name	|	Provide a name for the event type that you are creating.
schemaId	|	The id created for the event schema resource.


For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Event_Types) documentation.


The following example shows how to use cURL to create an event type for a temperature event that is measured in degrees Celsius:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d”}'
```

The schema identifier *5846cd7c6522050001db0e0d* is used to add the event schema to the event type. This identifier was returned in response to the POST method that was used to create the event schema resource *tEventSchema.json*

The following example shows a response to the POST method:

```
{
  "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
    "schema" : "/schemas/5846cd7c6522050001db0e0d"
  },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

The event type identifier *5846d0fd6522050001db0e0f* that is returned in response to the POST method is used to add an event type to the physical interface.

The following example shows how to use cURL to create an event type for a temperature event that is measured in degrees Fahrenheit:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
The schema identifier *5846cee36522050001db0e0e* is used to add the event schema to the event type. This identifier was returned in response to the POST method that was used to create the event schema resource *tempEventSchema.json*

The following example shows a response to the POST method:

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : “tempEvent”,
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
The event type identifier *5846d2846522050001db0e10* that is returned in response to the POST method is used to add an event type to the physical interface.

## Step 4: Create a physical interface
{: #step7}

To create a physical interface, use the following API:

```
POST /physicalinterfaces
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
name	|	Provide a name for the physical interface that you are creating.


For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Physical_Interfaces) documentation.

In this scenario, we need two physical interfaces - one for each event type.

The following example shows how to use cURL to create the first physical interface:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

The following example shows a response to the POST method:

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
  },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

The physical interface identifier *5847d1df6522050001db0e1a* that is returned in the response is used in the URL of the POST method that is called to add a temperature event that is measured in degrees Celsius to the physical interface.

The following example shows how to use cURL to create the second physical interface:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

The following example shows a response to the POST method:

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1b/events"
  },
  "id" : "5847d1df6522050001db0e1b",
  "name" : "Env sensor physical interface 2",
  "created" : "2016-12-07T09:19:51Z",
  "updated" : "2016-12-07T09:19:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

The physical interface identifier *5847d1df6522050001db0e1b* that is returned in the response is used in the URL of the POST method that is called to add a temperature event that is measured in degrees Fahrenheit to the physical interface.   

## Step 5: Add the event type to the physical interface
{: #step8}

To add an event type to your physical interface, use the following API:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
eventId	|	Enter the event name from your device event payload.
eventTypeId	|	The id created for the event type.


For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Physical_Interfaces) documentation.

In this scenario, the following event types are added to the specified phyiscal interfaces:
- the Celsius temperature event *tevt* is added to the physical interface with identifier *5847d1df6522050001db0e1a* by using the *eventId* from the topic and the *eventTypeId* from the creation of the event schema resource.
- the Fahrenheit temperature event *tempevt* is added to the physical interface with identifier *5847d1df6522050001db0e1b* by using the *eventId* from the topic and the *eventTypeId* from the creation of the event schema resource.


The following example shows how to use cURL to add the temperature event *tevt* to the physical interface with the identifier *5847d1df6522050001db0e1a* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : “tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

The following example shows a response to the POST method:

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

The following example shows how to use cURL to add the temperature event *tempevt* to the physical interface with the identifier *5847d1df6522050001db0e1b*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

The following example shows a response to the POST method:

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : “tempevt"
}
```

## Step 6: Update the device type to connect the physical interface
{: #step9}

To update a device type, use the following API:

```
PUT /device/types/{typeId}
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
physicalInterfaceId	|	The id created for the physical interface.


For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) documentation.

In this scenario, device type *EnvSensor1* is updated to connect to physical interface *5847d1df6522050001db0e1a* and device type *EnvSensor2* is updated to connect to physical interface *5847d1df6522050001db0e1b*.

The following example shows how to use cURL to update device type *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a”}’
```

The following example shows a response to the POST method:

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1a",
  "updatedDateTime" : "2016-12-07T09:49:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor1/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor1/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1a"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
The device identifier *EnvSensor1* is required when you add your physical interface and your application interface.

The following example shows how to use cURL to update device type *EnvSensor2*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b”}’
```

The following example shows a response to the POST method:

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1b",
  "updatedDateTime" : "2016-12-07T09:59:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor2/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor2/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1b"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
The device identifier *EnvSensor2* is required when you add your physical interface and your application interface.



## Step 7: Create an application interface schema file
{: #step4}

The following example shows how to create an application interface schema file that is called *envSensor.json*.

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "type" : "object",
    "title" : "Environment Sensor Schema",
    "description" : "Schema to represent a canonical environment sensor device",
    "properties" : {
        "temperature" : {
            "description" : "temperature in degrees Celsius",
            "type" : "number",
            "minimum" : -273.15,
            "default" : 0.0
        }
    },
    "required" : ["temperature"]
}
```

## Step 8: Create an application interface schema resource
{: #step5}

To create an application interface schema resource, use the following API:

```
POST /schemas
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
name	|	Provide a name for the application interface schema that you are creating.
schemaFile	|	Path to the local application interface schema JSON file.


For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) documentation.

The following example shows how to use cURL to create the application interface schema:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

The following example shows a response to the POST method:

```
{
  "created" : "2016-12-06T16:51:14Z",
  "name" : "temperatureEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "updated" : "2016-12-06T16:51:14Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "schemaType" : "json-schema",
  "contentType" : "application/octet-stream",
  "schemaFileName" : "envSensor.json",
  "refs" : {
    "content" : "/schemas/5846ec826522050001db0e11/content"
  },
  "id" : "5846ec826522050001db0e11"
}
```
Use the schema identifier *5846ec826522050001db0e11* that is returned in the response to the POST method to add the application interface schema to the application interface.

## Step 9: Create an application interface that references an application interface schema
{: #step6}

To create an application interface, use the following API:

```
POST /applicationinterfaces
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
name	|	Provide a name for the application interface that you are creating.
schemaId	|	The id created for the application interface schema resource.


For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces) documentation.

In this scenario, use the schema identifier *5846ec826522050001db0e11* that was returned in the previous response to add the application interface schema to the application interface.

The following example shows how to use cURL to create an application interface:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

The following example shows a response to the POST method:

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "schemaId" : "5846ec826522050001db0e11",
  "created" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846ed076522050001db0e12",
  "updated" : "2016-12-06T16:53:27Z",
  "name" : "environment sensor interface"
}
```
In this scenario, use the application interface identifier *5846ed076522050001db0e12* that is returned in the response to the POST method to add your application interface to your device type. You also use this identifier to map an inbound device event to a property that is defined by the application interface.

## Step 10: Add the application interface to a device type
{: #step10}

To add an application interface to a device type, use the following API:

```
POST /device/types/{typeId}/applicationinterfaces
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
id	|	The id created for the application interface.
name	|	The name of the device type.
schemaId	|	The id created for the application interface resource.
refs/schema	|	The path to the application interface resource. Typically: /schemas/*schemaId*


For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) documentation.

In this scenario, the application interface is associated with device type *EnvSensor1* and device type *EnvSensor2*.

The following example shows how to use cURL to add the application interface *5846ed076522050001db0e12* which references application schema identifier *5846ec826522050001db0e11* to the device type *EnvSensor1*:

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
        }'
```

The following example shows a response to the POST method:

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

The following example shows how to use cURL to add the application interface *5846ed076522050001db0e12* associated with application schema identifier *5846ec826522050001db0e11* to the device type *EnvSensor2*:

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
        }'
```


The following example shows a response to the POST method:

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

## Step 11: Define mappings to map properties in the inbound event to properties in the application interface
{: #step11}

To map events, use the following API:

```
POST /device/types/{typeId}/mappings
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
applicationInterfaceId	|	The id created for the application interface.
propertyMappings	|	A valid JSON structure that maps properties defined for the application interface with the properties of the device event payload. See the following examples.


For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) documentation.

In this scenario, we define mappings for device type *EnvSensor1* to map the **t** property in the inbound event *tevt* to the **temperature** property on the application interface. We also define mappings for device type *EnvSensor2* to map the **temp** property in the inbound event *tempevt* to the **temperature** property on the application interface.

The following example shows how to use cURL to add a mapping to device type *EnvSensor1*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tevt" : {
                  "temperature" : "$event.t"
              }
            }
          }'
```

**Important:** For structured [JSON ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://json-schema.org/){:new_window} event payloads make sure that the $event.*property* entry correctly matches the JSON structure of your properties. For example, if the payload is `{"d":{"t":<temp>}}` use `$event.d.t`

Specify the application interface identifier *5846ed076522050001db0e12* that is returned in the response to the POST method used to create the application interface and the device type *EnvSensor1*.

The following example shows a response to the POST method:

```
{
  "propertyMappings" : {
      "tevt" : {
       "temperature" : "$event.t"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```
The following example shows how to use cURL to add a mapping to device type *EnvSensor2*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
              }
            }
          }'
```

Specify the application interface identifier *5846ed076522050001db0e12* that is returned in the response to the POST method used to create the application interface and the device type *EnvSensor2*.
A conversion is applied to change the value from a measurement in degrees Fahrenheit to a measurement in degrees Celsius.


The following example shows a response to the POST method:

```
{
  "propertyMappings" : {
    "tempevt" : {
      "temperature" : "($event.temp - 32) / 1.8"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```

## Step 12: Deploy the configuration
{: #step15}

Deploy the configuration that is related to device state update for each device type. This configuration includes your schemas, event types, physical interfaces, application interfaces, and mappings.

To deploy your device type configuration, use the following API:

```
PATCH /device/types/{typeId}
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
typeId	|	The device type ID

For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) documentation.

In this scenario, we need to deploy configuration for two device types.

The following example shows how to use cURL to deploy your configuration for device type *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy-configuration"
          }'
```

The following example shows a response to the PATCH method:

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor1' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor1"]
  },
 "failures": []
}
```

The following example shows how to use cURL to deploy your configuration for device type *EnvSensor2*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

The following example shows a response to the PATCH method:

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor2' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor2"]
  },
 "failures": []
}
```

## Step 13: Publish an inbound device event
{: #step12}

Publish a temperature event from *TemperatureSensor1* on topic `iot-2/evt/tevt/fmt/json` and a temperature event from *TemperatureSensor2* on topic `iot-2/evt/tempevt/fmt/json`.

For information about publishing an inbound event from a device, see [MQTT connectivity for applications](../applications/mqtt.html#publishing_device_events).


## Step 14: Check that the state of the device is changed
{: #step13}

To check the device state, use the following API:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```

The following parameters are required:  

Parameter	|	Description
------	|	-----
typeId	|	The device type ID
deviceId	|	The device ID.
applicationInterfaceId	|	The id created for the application interface.

For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) documentation.

The following example shows how to use cURL to retrieve the current state of *TemperatureSensor1* by referencing the identifier of the application interface that was created:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

The application interface identifier *5846ed076522050001db0e12* is used in the GET method. This identifier is returned in the response to the POST method that was used to create the application interface.
The following example shows a response to the GET method:
```
{
  "temperature":34.5
}
```
The following example shows how to use cURL to retrieve the current state of *TemperatureSensor2* by referencing the identifier of the application interface that was created:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

The application interface identifier *5846ed076522050001db0e12* is used in the GET method. This identifier is returned in the response to the POST method that was used to create the application interface.
The following example shows a response to the GET method:
```
{
  "temperature":22.5
}
```
Note that the temperature reading that is returned is in degrees Celsius and not in degrees Fahrenheit.

Your application can process this normalized data without requiring configuration to understand or convert the different temperature scales.


**Note:** To retrieve the latest deployed configuration, use the following API:

```
GET /device/types/<typeId>/deployedconfiguration
```
Use this API to retrieve the configuration that was deployed the last time that the PATCH deploy operation completed successfully. To retrieve the configuration for a resource that is changed but not deployed, use the regular GET method that is associated with the resource that you want to query.

For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) documentation.

The following example shows how to use cURL to retrieve the latest deployed configuration:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/deployedconfiguration \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```
The following example shows a response to the GET method:

```
{
    "schemas": [
        {
          "name" : “tEventSchema",
          "createdBy" : "a-8x7nmj-9iqt56kfil",
          "contentType" : "application/octet-stream",
          "updated" : "2016-12-06T14:38:52Z",
          "schemaFileName" : "tEventSchema.json",
          "created" : "2016-12-06T14:38:52Z",
          "id" : "5846cd7c6522050001db0e0d",
          "refs" : {
              "content" : "/schemas/5846cd7c6522050001db0e0d/content"
          },
          "schemaType" : "json-schema",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "content": "ew0KICAiJHNjaGVtYSI6ICJodHRwOi8vanNvbi1zY2hlbWEub3JnL2RyYWZ0LTA0L3NjaGVtYSMiLA0KICAidHlwZSIgOiAib2JqZWN0IiwNCiAgInRpdGxlIiA6ICJFbnZTZW5zb3IxIHRFdmVudCBTY2hlbWEiLA0KICAiZGVzY3JpcHRpb24iIDog4oCcZGVmaW5lcyB0aGUgc3RydWN0dXJlIG9mIGEgdGVtcGVyYXR1cmUgZXZlbnQgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgInByb3BlcnRpZXMiIDogew0KICAgICJ0IiA6IHsNCiAgICAgICJkZXNjcmlwdGlvbiIgOiAidGVtcGVyYXR1cmUgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgICAgICJ0eXBlIiA6ICJudW1iZXIiLA0KICAgICAgIm1pbmltdW0iIDogLTI3My4xNSwNCiAgICAgICJkZWZhdWx0IiA6IDAuMA0KICAgIH0NCiAgfSwNCiAgInJlcXVpcmVkIiA6IFsidCJdDQp9"
        }
    ],
    "eventTypes": [
        {
          "updated" : "2016-12-06T14:53:49Z",
          "schemaId" : "5846cd7c6522050001db0e0d",
          "refs" : {
            "schema" : "/schemas/5846cd7c6522050001db0e0d"
          },
          "name" : "tEvent",
          "created" : "2016-12-06T14:53:49Z",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "id" : "5846d0fd6522050001db0e0f",
          "createdBy" : "a-8x7nmj-9iqt56kfil"
        },
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
          "schemaId" : "5846cee36522050001db0e0e",
          "created" : "2016-12-06T15:00:20Z",
          "id" : "5846d2846522050001db0e10",
          "updated" : "2016-12-06T15:00:20Z",
          "name" : “tempEvent”,
          "refs" : {
            "schema" : "/schemas/5846cee36522050001db0e0e"
          },
          "updatedBy" : "a-8x7nmj-9iqt56kfil"
        }
    ],
    "physicalInterface": {
          "events":[
            {
                  "eventTypeId" : "5846d0fd6522050001db0e0f",
                  "eventId" : "tevt"
            },
            {
                "eventTypeId" : "5846d2846522050001db0e10",
                "eventId" : “tempevt"
            }
          ],
        "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "refs" : {
            "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
          },
          "id" : "5847d1df6522050001db0e1a",
          "name" : "Env sensor physical interface 1",
          "created" : "2016-12-07T09:09:51Z",
          "updated" : "2016-12-07T09:09:51Z",
          "createdBy" : "a-8x7nmj-9iqt56kfil"
    },
    "applicationInterfaces": [
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11",
          "created" : "2016-12-06T16:53:27Z",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "id" : "5846ed076522050001db0e12",
          "updated" : "2016-12-06T16:53:27Z",
          "name" : "environment sensor interface"
        }
    ],
    "mappings": [
        {
          "propertyMappings" : {
            "tevt" : {
               "temperature" : "$event.t"
            },
            "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
            }
          },
          "applicationInterfaceId" : "5846ed076522050001db0e12"
        }
    ]
}
```
