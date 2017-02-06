---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Developing gateways on {{site.data.keyword.iot_short_notm}}
{: #gw_dev_index}

If your devices cannot directly connect to the internet, you can build a gateway device to retrieve and send data to applications in your {{site.data.keyword.iot_full}} organization. Client libraries, samples, and information are provided to help you to connect device gateways to your {{site.data.keyword.iot_short_notm}} organization and applications.
{:shortdesc}

## Connection protocols
Gateways connect to {{site.data.keyword.iot_short_notm}} by using the MQTT messaging protocol. Connecting gateways to {{site.data.keyword.iot_short_notm}} by using HTTP messaging is not supported. Only devices can connect by using HTTP messaging.

## Client libraries
Client libraries for developing gateways that can connect to {{site.data.keyword.iot_short_notm}} are available in the following languages:

|Client library |Link to library and further documentation
|:---|:---
|C++| https://github.com/ibm-watson-iot/iot-cpp
|C#| https://github.com/ibm-watson-iot/iot-csharp
|Embedded C| https://github.com/ibm-watson-iot/iot-embeddedc
|Java™|https://github.com/ibm-watson-iot/iot-java
|mBed C++|https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/
|Node.js|https://github.com/ibm-watson-iot/iot-nodejs
|Node-RED|https://github.com/ibm-watson-iot/iot-nodered
|Python|https://github.com/ibm-watson-iot/iot-python

For more information and links to the client libraries that are available, see also [Client libraries for {{site.data.keyword.iot_short_notm}} development](../iot_platform_client_lib.html).
