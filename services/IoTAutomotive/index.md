---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.iot4auto_short}} (Experimental)
{: #getting_started_iotautomotive}

*Last updated: 29 June 2016*
{: .last-updated}

{{site.data.keyword.iot4auto_full}} is a {{site.data.keyword.Bluemix_notm}} service that you can use to retrieve, manage, and analyze big data from connected vehicles. The analytics of {{site.data.keyword.iot4auto_short}} provide powerful and actionable insights into driving behavior, vehicle location, and other automotive-related activities and events of interest.

{:shortdesc}

By using {{site.data.keyword.iot4auto_short}}, you can do the following tasks:

- Send car probe data and normalized data into the data store for analysis
- Inject events into the context map and retrieve the events that specific vehicles are affected by
- Identify new events from car probe data
- Retrieve information about connected vehicles
- Manage asset data for drivers, vehicles, event rules, event types, and vendors


The {{site.data.keyword.iot4auto_short}} service includes the following {{site.data.keyword.Bluemix_notm}} services, which are also separately available in the {{site.data.keyword.Bluemix_notm}} catalog:

|Service|Description|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html){:new_window}| A service that can analyze driver behavior and identify trajectory patterns of a journey from the car probe and context data that is retrieved from a connected vehicle.
|[Context Mapping](../IotMapInsights/index.html){:new_window}| A service that provides geospatial functions, such as map matching and shortest path search for road networks.

Before you begin integrating your automotive devices and applications with the service, ensure that you complete the following steps:

1. Review the [About {{site.data.keyword.iot4auto_short}}](iotautomotive_overview.html) topic to familiarize yourself with the features and analytics that are available and supported for the service.
2. When you add an instance of the service from the [{{site.data.keyword.Bluemix_notm}} catalog](https://console.ng.bluemix.net/catalog/labs/){:new_window}, ensure that it is not bound to an app, and that you make a note of the automatically generated tenant ID, user name, and password values. You need these values later to access the service through the {{site.data.keyword.iot4auto_short}} API.
3. Using the console on the dashboard, configure the ports, target host names, and other settings for your {{site.data.keyword.iot4auto_short}}. For more information, see [Administering](iotautomotive_admin.html).

You can integrate your automotive devices and applications with this service by using {{site.data.keyword.iot4auto_short}} REST API commands.

To get up and running quickly, complete the following steps:

1. Inject events by using the `sendEvent` API request command to send events to be analyzed.
  - Request: event data with position
2. Confirm that the event data is stored with Map Matching by using the `getEvent` API request command to retrieve the event.
  - Request: area data (longitude and latitude of the start or end points)
  - Response: event data with road link ID
3.  Send car probe data to be analyzed by using the `sendCarProbe` API request command.
  - Request: car probe data with position
4. Confirm that the car probe data is stored with Map Matching by using the `getCarProbe` API request command to retrieve the data.
  - Request: area data (longitude and latitude of the start or end points)
  - Response: car probe data with road link ID
5. Analyze the driver data. For more information, see [Driver Behavior](../IotDriverInsights/index.html){:new_window}.

# Related Links
{: #rellinks}

## API Reference
{: #api}
* [{{site.data.keyword.iot4auto_short}} API docs](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [Contextual Map service APIs](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [Driver Behavior service APIs]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## Related Links
{: #general}
* [Getting started with {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Getting started with {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Getting started with {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [dW Answers on IBM developerWorks](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
