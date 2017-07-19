---

copyright:
years: 2016, 2017
lastupdated: "2017-07-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Step-by-step guide: A detailed example about how to work with devices through a common interface
{: #scenario}

Use the following information to create a scenario in which two temperature sensors publish events to {{site.data.keyword.iot_full}}. One sensor measures temperature in degrees Celsius. The other sensor measures temperature in degrees Fahrenheit. These readings are mapped to a single temperature reading that is in degrees Celsius. When a new temperature reading is published by these devices, the value of the property associated with the device state is changed.
{: shortdesc}

## Pre-requisites

You must have a {{site.data.keyword.iot_short_notm}} organization instance and an API key or token for that organization.

## About this task

In this scenario, two devices are configured.

One device is called *TemperatureSensor1*. This device publishes temperature events that are measured in degrees Celsius. The temperature event is published on the topic `iot-2/evt/tevt/fmt/json` and has the following example payload:
```
{
  "t" : 34.5
}
```

**Note:** The event identifier is *tevt*. This identifier is required when you add a temperature event of this type to the physical interface and when you define mappings to map a property associated with an inbound event of this type to a property in your logical interface. In this scenario, the property defined in the logical interface is called **temperature**.

The other device is called *TemperatureSensor2*. This device publishes temperature events that are measured in degrees Fahrenheit. The temperature event is published on the topic `iot-2/evt/tempevt/fmt/json` and has the following example payload:
```
{
  "temp" : 72.55
}
```

**Note:** The event identifier is *tempevt*. This identifier is required when you add a temperature event of this type to the physical interface and when you define mappings to map a property associated with an inbound event of this type to a property in your logical interface. In this scenario, the property defined in the logical interface is called **temperature**.
