---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# How the service works
{{site.data.keyword.iotinsurance_full}} creates a flow to collect, manage, and analyze data from connected policy holders.
{:shortdesc}

The insurance provider creates an instance of {{site.data.keyword.iotinsurance_short}} within the {{site.data.keyword.Bluemix_notm}} organization. Customers of the insurer have sensors in their homes which are connected to the sensor provider's cloud. From their mobile devices, customers authorize the {{site.data.keyword.iotinsurance_short}} service to receive sensor data. The {{site.data.keyword.iotinsurance_short}} Transformer connects to the sensor provider's cloud and pulls data for each user and sends it to the {{site.data.keyword.iot_short_notm}} server. If the sensor shows that the parameters that are specified in the insurer's shields are met in the customer's home, notifications are sent to the insurer's dashboard and to the customer's device.

A connected sensor detects an event, such as a water leak, and sends that information to a smart home vendor, such as Wink.  {{site.data.keyword.iotinsurance_short}} detects the signal by using its connection with the smart home vendor's cloud and creates an alert payload. The payload is sent through MQTT to the {{site.data.keyword.iotinsurance_short}} shield engine for processing. The shield engine analyzes whether the payload matches criteria that are defined by the shield rules. If it does, the shield engine emits a hazard payload through MQTT to the {{site.data.keyword.iotinsurance_short}} action engine. The action engine performs actions that are defined by the shield for that type of hazard, for example, sending a text message to the homeowner.

{{site.data.keyword.iotinsurance_short}} relies on {{site.data.keyword.iot_full}} to pass alert and hazard payloads between its components. A complete working system requires users, shields, and associations between users and shields.

![{{site.data.keyword.iotinsurance_short}} Process. This diagram is described in the main body of the topic.](images/IoT4I_process.svg "{{site.data.keyword.iotinsurance_short}} process")
