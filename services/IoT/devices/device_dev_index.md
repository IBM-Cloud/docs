---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Developing devices on {{site.data.keyword.iot_short_notm}}
{: #device_dev_index}

A device is anything that has a connection to the internet and has data to send to or receive from the cloud. You can use devices to send event information such as sensor readings to the cloud, and to accept commands from applications in the cloud.

Devices publish data to the {{site.data.keyword.iot_short_notm}} by using events. The device controls the content of the event and assigns a name for each event that is sent. When an event is received by the {{site.data.keyword.iot_short_notm}} from a device, the credentials of the connection on which the event was received are used to determine from which device the event was sent. This architecture prevents a device from impersonating another device.

For more information about key concepts, including devices, see [About Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts).


## Connecting your device to {{site.data.keyword.iot_short_notm}}
{: #device_connect}
You can connect your device to {{site.data.keyword.iot_short_notm}} by using HTTP or MQTT protocols. Use HTTP if you want a configure request-response scenario, such as when someone makes a purchase and receives an acknowledgement. Use MQTT if you want to configure an event scenario, such as when someone rings a doorbell and causes an alert to be triggered in a mobile device.

A device must be registered with an organization before it can connect to the {{site.data.keyword.iot_full}}. To connect securely to {{site.data.keyword.iot_short_notm}}, you must register for a Bluemix account and create your own {{site.data.keyword.iot_short_notm}} organisation. You can then register your device by using this organisation's ID. Registered devices identify themselves to the {{site.data.keyword.iot_short_notm}} with a unique device identifier, for example the MAC address, and an authentication token that is accepted for that device only. Once you have connected securely, use Bluemix to build your own applications. Try using Node-RED to wire your applications together.

If you want to connect your device without registering it, for example to run a proof of concept, you can do so by using the special organization ID `QuickStart`. `QuickStart` is a public sandbox instance of {{site.data.keyword.iot_short_notm}} that runs in the cloud. If you do not need to connect securely, you can use `QuickStart` to test your device connectivity and experiment with {{site.data.keyword.iot_short_notm}}. When you have finished experimenting, reconnect your device securely to your own specific organization ID instance by using TLS and your authentication token.

For more information about connecting your device to the {{site.data.keyword.iot_short_notm}} by using the HTTP protocol, see [HTTP REST API for devices](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html).
For more information about connecting your device to the {{site.data.keyword.iot_short_notm}} by using the MQTT protocol, see [MQTT connectivity for devices](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html).

## Getting started with developing devices
{: #get_started}
If you have a device that is already enabled for {{site.data.keyword.iot_short_notm}}, you can simply start using it.

If your device is not already enabled, check out the recipes that are available on [developerWorks](https://developer.ibm.com/recipes/). Browse the existing recipes to see if there's a recipe for your device, and use the recipe to help you to start developing. You can even publish your own recipes if you want to.

If you cannot find a recipe for your particular device, then IBM provide a number of programming guides and APIs that you can use to get started. These guides contain client libraries, samples and information that can help you to build and develop code for integrating and connecting your devices and applications to {{site.data.keyword.iot_short_notm}}. The following programming guides are currently available:

- Java
- Node.js
- Embedded C
- ARM mBed C++
- Python
- C#
- Node-RED

For more information and links to the programming guides that are available, see [Client libraries for {{site.data.keyword.iot_short_notm}} development](../iot_platform_client_lib.html).

If you cannot find a suitable {{site.data.keyword.iot_short_notm}} programming guide, you can write your own program and use MQTT or HTTP protocol to connect your device to the {{site.data.keyword.iot_short_notm}}.

MQTT is an open standard managed by the OASIS standards organization and international recognized by ISO. For more information, see [OASIS Message Queuing Telemetry Transport ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt){: new_window}.

A wide variety of MQTT client libraries are available for many different systems, including the following environments:
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

For more information about MQTT, see [MQTT messaging](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3).
