---

copyright:
  years: 2015,2016

---

{:new_window: target=\_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:note: .deprecated}

**This service is being merged with {{site.data.keyword.iot_full}}:**  Existing instances are being merged with the corresponding {{site.data.keyword.iot_short_notm}} organizations which now contains the Real-Time Insights analytics and dashboard features. You can also access your instances from the {{site.data.keyword.iotrtinsights_short}} dashboard until 1 September 2016. For more information, see the [IBM Watson IoT Platform blog](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} on IBM developerWorks and [Analyzing IoT Data](https://new-console.{DomainName}/docs/services/IoT/analytics.html){: new_window} in the {{site.data.keyword.iot_short_notm}} documentation.  
{: deprecated}

# Nested message schemas
Last updated: 1 August 2016
{: .last-updated}

{{site.data.keyword.iotrtinsights_short}} supports nested JSON message payloads that meet the {{site.data.keyword.iot_short}} specification.   
{: shortdesc}

## Supported nested message payload format
Nested data points can be used when creating rules, dashboards, and templates.

**Note:** Real-Time Insights does not support Custom JSON payloads. More information about the {{site.data.keyword.iot_short}} message payload specification is in the [{{site.data.keyword.iot_short}} documentation](https://docs.internetofthings.ibmcloud.com/messaging/payload.html).

The following examples illustrate supported nested message formats:
- Simple data  
```
{
    "d":
    {"msg": "Hello World"}  
}
```
{: codeblock}

- Complex data
```
{
    "d": {  
      "host": "IBM700-R9E683D",  
      "mem": 54.9,  
      "network":
      {  
        "up": 1.22,  
        "down": 0.55  
      },  
      "cpu": 1.3,  
    }  
}
```  
{: codeblock}

**Important:** Nested JSON messages must contain the d element, which is where you include all data for the event that is transmitted in the message.
- The element is required for your message to meet the {{site.data.keyword.iot_short}} message specification.
- The element must always be a JSON object and not an array.
- If you want to send no data, ensure that the d element is used and that it contains an empty object.
