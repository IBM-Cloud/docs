---

copyright:
years: 2016, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using interfaces to map device data (Beta)
{: #im_index}

Use the interface mapping feature of {{site.data.keyword.iot_full}} to organize and integrate incoming and outgoing device data.
{:shortdesc}

**Important:** The interface mapping feature is available at present as a Beta feature only. Prior to final release, Beta updates are likely to include changes that are incompatible with the current version. It is strongly recommended that Beta features are not used in production applications until final release. To receive additional information and provide feedback on this Beta, please [register for the IM Beta program ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050){: new_window} and let us know what you think.

## Overview
{: #overview}

You can use the interface mapping feature to develop interfaces for your applications. You might have different types, makes, or models of device or sensor that you want to connect to {{site.data.keyword.iot_short_notm}}, and these devices might publish data in differing formats. Use the interface mapping feature to normalize incoming data and to simplify your applications by decoupling them from the complexities of how your specific devices are connected.

For example, you might have two temperature sensors. One sensor measures temperature in degrees Celsius and one sensor measures temperature in degrees Fahrenheit.

![Mapping between temperature sensor devices and an application on {{site.data.keyword.iot_short_notm}}.](images/Information Management example.svg "Mapping between temperature sensor devices and an application on {{site.data.keyword.iot_short_notm}}")

Temperature sensor 1 publishes a temperature reading of `{ "t" : 34.5 }` to {{site.data.keyword.iot_short_notm}}. This is a temperature reading with a value in Celsius. Temperature sensor 2 publishes a temperature reading of `{ "temp" : 72.55 }` to {{site.data.keyword.iot_short_notm}}. This is a different type of temperature sensor that has a reading with a value in Fahrenheit. The temperature readings are published as separate events to {{site.data.keyword.iot_short_notm}}.

By using the interface mapping feature, you can normalize these readings into a consistent form for processing. You do not need to write your application to understand or convert different temperature scales. The application receives a single, normalized view and can connect to **temperature** instead of connecting to **t** and **temp**.

## Data flow between devices and applications
{: #mapping}

The following flow diagram shows how the different resources in the interface mapping feature are used:

![The flow between a device and an application on {{site.data.keyword.iot_short_notm}}.](images/Information Management flow.svg "The flow between a device and an application on {{site.data.keyword.iot_short_notm}}")

The following diagram illustrates how schemas are used in this flow:

![The flow between a device and an application on {{site.data.keyword.iot_short_notm}}.](images/Information Management schema.svg "The flow between a device and an application on {{site.data.keyword.iot_short_notm}}")

JSON schemas are used to define and validate the format of incoming events and [device state](#key_concepts). For more information about these schemas, see [Schemas](#resources).

## Key concepts
{: #key_concepts}

The interface mapping feature extends the current concept of [device type](#resources) by adding a physical interface resource and an application interface resource to better control the data that flows through {{site.data.keyword.iot_short_notm}}.

The following diagram illustrates the logical mapping between devices and applications on {{site.data.keyword.iot_short_notm}} by using [resources](#resources):

![The logical mapping between a device and an application on {{site.data.keyword.iot_short_notm}}.](images/im_mapping.svg "The logical mapping between a device and an application on {{site.data.keyword.iot_short_notm}}")

Interface mapping refers to the concept of a device state. The device state consists of a set of properties that are defined by the application interface. The most recent values of these properties are stored in {{site.data.keyword.iot_short_notm}}, and are made available to the application on request by using an HTTP API.

To process data from inbound events, and map properties in the inbound event to properties on the application interface, the following information must be configured:

- The structure of one or more inbound events. The event schema defines this information.  Each event schema defines the structure of one inbound event and is associated with one event type. The physical interface groups one or more event types.

    The structure and format of data that is contained within an inbound device event is defined by an event schema file that is in JSON schema format. You can upload the event schema file to {{site.data.keyword.iot_short_notm}} by using a POST method to create a named schema resource. For Beta, all inbound events must be in JSON format.

- The structure of the desired device state. The application interface schema defines this information.

    The device state is a representation of the data structure and data that your application is configured to receive as data from the device. The property values that are stored in the device state are updated in response to an inbound device event. The latest device state values are provided to an application on request by using an HTTP API.

- Information about how to map the inbound events to the preferred device state. Mappings define this information.

    To map the data that is contained in the properties of an inbound event to the appropriate properties on the application interface, you need to create a mapping. The mapping describes how to update the properties that are defined by a specific application interface in response to an inbound event from a device.


## Resources
{: #resources}

You can manage the resources that are illustrated in the previous diagrams by using REST APIs. For information about the REST APIs, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window} documentation.

Resource                        | Description       
------------- | ------------- | -------------  
Schemas                         | JSON schemas are used to define the structure of inbound events that are published to the {{site.data.keyword.iot_short_notm}} from devices, and the desired device state. For more information about JSON Schema, see [JSON Schema ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://json-schema.org/){: new_window}. In interface mapping, two JSON schemas are referenced - event schemas and application interface schemas. Event schemas are used to define the structure of the events that are published to {{site.data.keyword.iot_short_notm}} by a device. Application interface schemas are referenced by the application interface and are used to define the structure of the [device state](#key_concepts) that is stored on {{site.data.keyword.iot_short_notm}}.
Event type                         | You must create an event type within your organization so that {{site.data.keyword.iot_short_notm}} can process the data that is contained within a specific event. All event types must reference an event schema. For the beta, all inbound events must be in JSON format.   
Physical interface                         | The physical interface can be associated with one or more event types and defines which event types are associated with a device type.  
Device type                         | Every device that is connected to the Watson IoT Platform is associated with a device type. Device types are groups of devices that share characteristics or behaviors. In interface mapping, the device type is extended to include a physical interface for a device and an application interface that can be used to retrieve the device state. A device type can be configured with multiple application interfaces. For more information about device types, see the "Identifiers and device types" section in [Device Model](../reference/device_model.html#id_and_device_types).
Application interface                         | The application interface must reference an application interface schema. Within your application interface, you can define the structure of the data that is stored as the device state. The device state is a representation of the data structure and data that an application is configured to receive as data from the device. At least one application interface must be associated with a device type before any mappings can be defined.
Mappings                         | Mappings define how properties that are associated with inbound events are mapped to properties that are defined on a specific application interface. A mapping must specify the application interface identifier that it applies to, and that application interface must be associated with the device type that the mapping is being added to.


## High-level workflow
{: #workflow}



### About this task

Use the following steps to help you to configure the resources that you need to start mapping your device data by using interfaces.

For details about the API, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window} documentation.
For more detailed information about each of the steps, see the [Example scenario](#scenario) or use the links to go directly to a specific step within the example scenario.

### Configure your environment to start using interfaces to map device data

1.  If needed, add a Device Type and a Device

  1. Create a device type by using the REST API POST method with the following URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  Add a device if needed.  
For more information about adding a device type and a device, see [Connecting devices](../iotplatform_task.html#devices)

2. Create a Physical Interface

  1. [Create an event schema file](#step1). The event schema file is a local .JSON file that defines the structure and format of an inbound event.

  2. [Create an event schema resource for your event type](#step2) by using the REST API POST method with the following URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. [Create an event type that references the event schema](#step3) by using the REST API POST method with the following URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      Add the event type to your event schema by using the schema identifier that was returned in response to the POST method used to create the event schema resource.

  4. [Create a physical interface](#step7) by using the REST API POST method with the following URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. [Add the event type to the physical interface](#step8) by using the REST API POST method with the following URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       Add the event type to your physical interface by using the *eventId* from the topic and the event type identifier *eventTypeId* that was returned in response to the POST method used to create the event type.       

3. Add your physical interface to your device type       

      [Update the device type to connect the physical interface](#step9) by using the REST API PUT method with the following URI:
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. Create an Application Interface

  1. [Create an application interface schema file](#step4). An application interface schema file is a local .JSON file that defines the device state.

  2. [Create an application interface schema resource](#step5) by using the REST API POST method with the following URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. [Create an application interface that references an application interface schema](#step6) by using the REST API POST method with the following URI:
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        The application interface references the application interface schema by using the schema identifier that was returned in response to the POST method used to create the application interface schema resource.

  4. [Add the application interface to a device type](#step10) by using the REST API POST method with the following URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        Add your application interface to your device type by using the response to the POST method that was used to create the application interface.

5. Define the mappings for the device type

  [Define mappings to map properties in the inbound event to properties in the application interface](#step11) by using the REST API POST method with the following URI:       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. Deploy the configuration that is associated with your device type

  [Deploy the configuration](#step15) to {{site.data.keyword.iot_short_notm}} by using the REST API PATCH method with the following URI:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. Verify that mapped device events are published to the application interface

  1. [Publish an inbound device event](#step12).

  2. [Check that the state of the device is changed](#step13) by using the REST API GET method with the following URI:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## Example scenario
{: #scenario}

Use the following information to create a scenario in which two temperature sensors publish events to {{site.data.keyword.iot_short_notm}}. One sensor measures temperature in degrees Celsius. The other sensor measures temperature in degrees Fahrenheit. These readings are mapped to a single temperature reading that is in degrees Celsius. When a new temperature reading is published by these devices, the value of the property associated with the device state is changed.

### Pre-requisites

You must have a {{site.data.keyword.iot_short_notm}} organization instance and an API key or token for that organization. For more information about API keys and tokens, see [HTTP REST API for applications](../applications/api.html#authentication).

### About this scenario

In this scenario, two devices are configured.

One device is called *TemperatureSensor1*. This device publishes temperature events that are measured in degrees Celsius. The temperature event is published on the topic `iot-2/evt/tevt/fmt/json` and has the following example payload:
```
{
  "t" : 34.5
}
```

**Note:** The event identifier is *tevt*. This identifier is required when you add a temperature event of this type to the physical interface and when you define mappings to map a property associated with an inbound event of this type to a property in your application interface. In this scenario, the property defined in the application interface is called **temperature**.

The other device is called *TemperatureSensor2*. This device publishes temperature events that are measured in degrees Fahrenheit. The temperature event is published on the topic `iot-2/evt/tempevt/fmt/json` and has the following example payload:
```
{
  "temp" : 72.55
}
```

**Note:** The event identifier is *tempevt*. This identifier is required when you add a temperature event of this type to the physical interface and when you define mappings to map a property associated with an inbound event of this type to a property in your application interface. In this scenario, the property defined in the application interface is called **temperature**.

An application interface is also configured. This application interface represents the state for devices of this type in the following structure:
```
{
  "temperature" : <current temperature value in Celsius>
  }
```
This configuration means that you can configure your application to process the value that is associated with **temperature**, rather than configuring your application to process the value that is associated with **t** and to process the value that is associated with **temp** after converting that value to degrees Celsius.

## Steps

Use the following information to configure the example scenario by using interfaces.

### If needed, add a Device Type and a Device
{: #step14}

In this scenario, two device types and two device instances are assumed. Device instance *TemperatureSensor1* is associated with device type *EnvSensor1*. Device instance *TemperatureSensor2* is associated with device type *EnvSensor2*.

For information about using HTTP APIs to add a device type, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Type_Configuration){: new_window} documentation.

### Create an event schema file
{: #step1}

For this scenario, create two event schema files to define the structure of each of the inbound temperature events.

The following example shows how to create a schema file that is called *tEventSchema.json*. This file defines the structure of an inbound event from a temperature sensor that measures temperature in degrees Celsius:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Celsius",
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

The schema file name *tEventSchema* is used when you create an event schema resource for your event type.

The following example shows how to create a schema file that is called *tempEventSchema.json*. This file defines the structure of an inbound event from a temperature sensor that measures temperature in degrees Fahrenheit:

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Fahrenheit",
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

### Create an event schema resource for your event type
{: #step2}

To create an event schema resource, use the following API:

```
POST /schemas
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas){: new_window}  documentation.

The following example shows how to use cURL to create the event schema resource *tEventSchema.json*:

```
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
  "name" : "tEventSchema",
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

### Create an event type that references the event schema
{: #step3}

Each event type references the relevant event schema that was created in the previous example by using the schema identifier returned in the response to the POST method used to create the event schema resource.

To create an event type, use the following API:

```
POST /event/types
```

For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Event_Types){: new_window} documentation.


The following example shows how to use cURL to create an event type for a temperature event that is measured in degrees Celsius:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
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
  "name" : "tempEvent",
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
The event type identifier *5846d2846522050001db0e10* that is returned in response to the POST method is used to add an event type to the physical interface.

### Create a physical interface
{: #step7}

To create a physical interface, use the following API:

```
POST /physicalinterfaces
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Physical_Interfaces){: new_window} documentation.

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

### Add the event type to the physical interface
{: #step8}

To add an event type to your physical interface, use the following API:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Physical_Interfaces){: new_window} documentation.

In this scenario, the following event types are added to the specified phyiscal interfaces:
- the Celsius temperature event *tevt* is added to the physical interface with identifier *5847d1df6522050001db0e1a* by using the *eventId* from the topic and the *eventTypeId* from the creation of the event schema resource.
- the Fahrenheit temperature event *tempevt* is added to the physical interface with identifier *5847d1df6522050001db0e1b* by using the *eventId* from the topic and the *eventTypeId* from the creation of the event schema resource.


The following example shows how to use cURL to add the temperature event *tevt* to the physical interface with the identifier *5847d1df6522050001db0e1a* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
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
  "eventId" : "tempevt"
}
```

### Update the device type to connect the physical interface
{: #step9}

To update a device type, use the following API:

```
PUT /device/types/{typeId}
```

For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} documentation.

In this scenario, device type *EnvSensor1* is updated to connect to physical interface *5847d1df6522050001db0e1a* and device type *EnvSensor2* is updated to connect to physical interface *5847d1df6522050001db0e1b*.

The following example shows how to use cURL to update device type *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
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
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
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



### Create an application interface schema file
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

### Create an application interface schema resource
{: #step5}

To create an application interface schema resource, use the following API:

```
POST /schemas
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas){: new_window} documentation.

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

### Create an application interface that references an application interface schema
{: #step6}

To create an application interface, use the following API:

```
POST /applicationinterfaces
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces){: new_window} documentation.

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

### Add the application interface to a device type
{: #step10}

To add an application interface to a device type, use the following API:

```
POST /device/types/{typeId}/applicationinterfaces
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} documentation.

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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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

### Define mappings to map properties in the inbound event to properties in the application interface
{: #step11}

To map events, use the following API:

```
POST /device/types/{typeId}/mappings
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} documentation.

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

### Deploy the configuration
{: #step15}

Deploy configuration that is related to device state update for each device type. This configuration includes your schemas, event types, physical interfaces, application interfaces, and mappings.

To deploy your device type configuration, use the following API:

```
PATCH /device/types/{typeId}
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} documentation.

In this scenario, we need to deploy configuration for two device types.

The following example shows how to use cURL to deploy your configuration for device type *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
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

### Publish an inbound device event
{: #step12}

Publish a temperature event from *TemperatureSensor1* on topic `iot-2/evt/tevt/fmt/json` and a temperature event from *TemperatureSensor2* on topic `iot-2/evt/tempevt/fmt/json`.

For information about publishing an inbound event from a device, see [MQTT connectivity for applications](../applications/mqtt.html#publishing_device_events).


### Check that the state of the device is changed
{: #step13}

To check the device state, use the following API:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
For more details, see the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} documentation.

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
