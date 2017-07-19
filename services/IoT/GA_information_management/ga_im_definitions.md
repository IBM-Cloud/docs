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


# Understanding data management
{: #definitions_resources}
You might have a number of different devices that you want to connect to {{site.data.keyword.iot_full}}, and these devices might publish data in different formats. By using the data management feature, you can normalize and transform the data output from your devices into a single logical view that can be easily consumed by your applications. By using a single logical view, you remove the need to code your applications to understand the different data formats that are output by each device. 
{: shortdesc}

## Overview

Use the data management feature to create shared abstractions of devices (device twins), to improve reuse and maintenance and to manage the complexities of an IoT ecosystem while keeping the application insulated from data change. 

Applications can access the current state of a device on request by using an HTTP API, or by subscribing to a topic string. The state consists of a set of state properties that are defined by a logical interface. If the state of a device changes as a result of an event being published to {{site.data.keyword.iot_short_notm}}, the values of these properties are updated and stored in {{site.data.keyword.iot_short_notm}}.

By using the data management feature, you can achieve the following benefits:
- Map state properties to event message data
- Define the data structure that you prefer
- Define more than one representation or view of the device state
- Subscribe to device states or query them at any time through an HTTP API

Some common use cases for implementing the data management feature include:
- Providing your application developers consistent interfaces to access event-driven device data in a REST-like manner
- Normalizing data from devices of different makes or models that publish data in different formats
- Modifying and converting data formats to fit your application model

## Example: Mapping heterogeneous temperature sensors to a logical interface
{: #device-type-example}
To start using the data management feature, you need to define a number of resources which are described in the following sections. 

The following example shows how these resources can fit together to enable applications to access homogeneous temperature state data in one format, regardless of the device event message payload format. TemperatureSensor1 publishes a Celsius temperature reading of `{ "t" : 34.5 }` to {{site.data.keyword.iot_short_notm}}. TemperatureSensor2 publishes a Fahrenheit temperature reading of `{ "temp" : 72.55 }`. Each temperature sensor is associated with its own [device type](../reference/device_model.html#id_and_device_types). The temperature readings are published as separate events.
