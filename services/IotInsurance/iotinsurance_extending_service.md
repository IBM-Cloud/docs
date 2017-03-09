---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Extending the service with APIs
{: #iot4i_extending_service}
{{site.data.keyword.iotinsurance_full}} provides APIs to customize and extend your {{site.data.keyword.iotinsurance_short}} solution.
{:shortdesc}

{{site.data.keyword.iotinsurance_short}} comes with built-in support for Wink water leak sensors. By using the provided APIs, you can customize the {{site.data.keyword.iotinsurance_short}} solution to support new device types and vendors. {{site.data.keyword.iotinsurance_short}} relies on cloud-to-cloud communication to get sensor data from devices. By creating new transformation micro-services, you can customize {{site.data.keyword.iotinsurance_short}} to read the sensor data from new devices, pass it to the rest of the system through the {{site.data.keyword.iot_short_notm}} service, and then take actions as appropriate.

For a full set of example code, see the [API examples GitHub repository ![External link icon](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){: new_window}.

For complete information about the APIs, see the [API documentation ![External link icon](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){: new_window}.
