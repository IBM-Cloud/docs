---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-17"

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
|C++|[https://github.com/ibm-watson-iot/iot-cpp](https://github.com/ibm-watson-iot/iot-cpp)
|C#|[https://github.com/ibm-watson-iot/iot-csharp](https://github.com/ibm-watson-iot/iot-csharp)
|Embedded C| [https://github.com/ibm-watson-iot/iot-embeddedc](https://github.com/ibm-watson-iot/iot-embeddedc)
|Java™|[https://github.com/ibm-watson-iot/iot-java](https://github.com/ibm-watson-iot/iot-java)
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/)
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs)
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered](https://github.com/ibm-watson-iot/iot-nodered)
|Python|[https://github.com/ibm-watson-iot/iot-python](https://github.com/ibm-watson-iot/iot-python)

For more information and links to the client libraries that are available, see also [Client libraries for {{site.data.keyword.iot_short_notm}} development](../iot_platform_client_lib.html).

## Edge Analytics
{: #eaa_community}

The {{site.data.keyword.iot_short_notm}} Edge Analytics feature enables you to run {{site.data.keyword.iot_short_notm}} Analytics on a gateway device. Use Edge Analytics to bring analytics to analyze and respond to data collected at the edge of the network. You can also send device data to {{site.data.keyword.iot_short_notm}} for additional analytic processing, dashboard visualization, as input to other analytics, or to be stored in a cloud-based historian repository.

You can download the Edge Analytics SDK from the [IBM Edge Analytics community page](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true). The SDK includes the SDK JAR file, javadoc, sample code, recipe links, and README files. In the community, you can also watch videos to get up and running with Edge Analytics, and you can use the community forum to ask questions.
