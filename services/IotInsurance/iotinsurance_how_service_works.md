---

copyright:
  years: 2016
lastupdated: "2016-10-26"

---


{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# How the service works
{{site.data.keyword.iotinsurance_full}} creates a flow to collect, manage, and analyze data from connected policy holders.
{:shortdesc}

The insurance provider creates an instance of {{site.data.keyword.iotinsurance_short}} within the {{site.data.keyword.Bluemix_notm}} organization. Customers of the insurer have sensors in their homes which are connected to the sensor provider's cloud. From their mobile devices, customers authorize the {{site.data.keyword.iotinsurance_short}} service to receive sensor data. The {{site.data.keyword.iotinsurance_short}} Transformer connects to the sensor provider's cloud and pulls data for each user and sends it to the {{site.data.keyword.iot_short_notm}} server. If the sensor shows that the parameters that are specified in the insurer's shields are met in the customer's home, notifications are sent to the insurer's dashboard and to the customer's device.

A connected sensor detects an event, such as a water leak, and sends that information to a smart home vendor, such as Wink.  {{site.data.keyword.iotinsurance_short}} detects the signal by using its connection with the smart home vendor's cloud and creates an alert payload. The payload is sent through MQTT to the {{site.data.keyword.iotinsurance_short}} shield engine for processing. The shield engine analyzes whether the payload matches criteria that are defined by the shield rules. If it does, the shield engine emits a hazard payload through MQTT to the {{site.data.keyword.iotinsurance_short}} action engine. The action engine performs actions that are defined by the shield for that type of hazard, for example, sending a text message to the homeowner.

{{site.data.keyword.iotinsurance_short}} relies on {{site.data.keyword.iot_full}} to pass alert and hazard payloads between its components. A complete working system requires users, shields, and associations between users and shields.

![{{site.data.keyword.iotinsurance_short}} Process. This diagram is described in the main body of the topic.](images/IoT4I_process.svg "{{site.data.keyword.iotinsurance_short}} process")

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}
* [Sample mobile app code on GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API Reference
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API Examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Related Links
{: #general}
* [{{site.data.keyword.iot_full}} documentation](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
