---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Getting started with {{site.data.keyword.iotmapinsights_short}}
{: #iotdriverinsights_index}
*Last updated: 22 June 2016*
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} is a service on {{site.data.keyword.Bluemix}} that you can use to enable geospatial functions such as map matching and shortest path search for road networks across the globe with your applications.  
{:shortdesc}

The following features are available through the {{site.data.keyword.iotmapinsights_short}} REST API:

|Feature|Use to...|
|:---|:---|
|Highly accurate map matching|Match your GPS location to the actual mapped road network|
|Road geometry data retrieval|Retrieve the mapped road network to draw road shapes on a map|
|Dynamic shortest path search|Search for the shortest route that incorporate real-time events such as traffic|
|Real-time traffic event manipulation|Add real-time map-matched events, for example, traffic conditions to improve route planning results|

## Before you begin
{: #byb}

1. When you add an instance of the service from the [{{site.data.keyword.Bluemix_notm}} catalog](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}, ensure that it is not bound to an app, and that you make a note of the automatically generated tenant ID, user name, and password values. You need these values later to access the service through the   {{site.data.keyword.iotmapinsights_short}} API.

2. Familiarize yourself with [OpenStreetMap](http://www.openstreetmap.org/){: new_window}.  

 The {{site.data.keyword.iotmapinsights_short}} service uses the road network data, in WGS84 coordinates, which is extracted from [OpenStreetMap](http://www.openstreetmap.org/){: new_window}. Only the roads that a car can travel on are used for analysis.  

 The following map regions are supported:

|Region|Map ID|
|:---|:---|
|Europe|map_id=1|
|Africa|map_id=2|
|Asia|map_id=3|
|Australia Oceania|map_id=4|
|North America|map_id=5|
|Central America|map_id=6|
|South America|map_id=7|

## Map matching
{: #map_matching}
To map raw GPS coordinates to map-matched coordinates, complete the following steps:

1. Prepare a set of raw GPS coordinates to be analyzed.
2. Send the raw GPS coordinates by using the `mapMatching` API command. Optionally set a heading angle of each position in degrees to specify the direction of the travel.
 - Request: Raw GPS data
 - Response: Map-matched GPS data, Link ID
3. Optional: Get the road type data by using the `getLinkInformation` API command. You can retrieve the matched road shape data as a series of coordinates with the `getLinkInformation` REST API.
 - Request: Link ID
 - Response: Road type

## Route searching
{: #route_searching}

Find the shortest route path information between the specified origin and destination coordinates by using the following steps:

1. Determine a start and end position for the shortest path.
2. Send the start and end coordinates with the `routeSearch` REST API.
Optionally, set a heading angle for each position, in degrees, to specify the direction of travel.
 - Request: Origin and destination coordinates
 - Response: Map-matched shortest route

Use the returned link shape data to draw the shape of the found path on a map.

## Adding traffic events
{: #traffic_events}

To add traffic event information to the {{site.data.keyword.iotmapinsights_short}} service, complete the following steps:

1. Choose the type and position of the traffic event that you want to create.
2. Inject the event by using the `createEvent` API command.
Send the traffic event information to the {{site.data.keyword.iotmapinsights_short}} service.
 - Request: Event information
 - Response: Event ID
3. Find events by using the `queryEvent` REST API command.
Search for traffic events that are within a specific rectangular area, and optionally for a specific traffic event type.
 - Request: Area information.
 - Response: Event information.  
4. Optional: Remove a traffic event that is no longer valid by using the `deleteEvent` API  command.
5. Optional: Retrieve an area on the road that is affected by a traffic event by using the `getAffectedLinksInformation` API command.

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Tutorial Part1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Tutorial Part2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive Starter Application](https://iot-automotive-starter.mybluemix.net){:new_window}

## API Reference
{: #api}

* [API docs](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## Related Links
{: #general}

* [Getting started with {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Getting started with {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [dW Answers on IBM developerWorks](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy; OpenStreetMap contributors](http://www.openstreetmap.org/copyright){:new_window}
* [Open Data Commons Open Database License (ODbL)](http://opendatacommons.org/licenses/odbl/){:new_window}
