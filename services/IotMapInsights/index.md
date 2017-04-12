---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Getting started with Context Mapping
{: #iotdriverinsights_index}

{{site.data.keyword.iotmapinsights_full}} is a service on {{site.data.keyword.Bluemix}} that you can use to enable geospatial functions, such as map matching and shortest path search for global road networks, in your applications. Use the powerful capabilities of {{site.data.keyword.iotmapinsights_short}} to build smart automotive solutions.
{:shortdesc}

## Features
{: #features}

The following features are available by using the {{site.data.keyword.iotmapinsights_short}} REST API:

|Feature|Use to...|
|:---|:---|
|Highly accurate map matching|Match your GPS location to the actual mapped road network|
|Road geometry data retrieval|Retrieve the mapped road network to draw road shapes on a map|
|Dynamic shortest path search|Search for the shortest route that incorporates real-time events, such as traffic|
|Real-time traffic event manipulation|Add real-time map-matched events, such as traffic conditions, to improve route planning results|

## Before you begin
{: #byb}

1. When you add an instance of the service from the [{{site.data.keyword.Bluemix_notm}} catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}, ensure that it is not bound to an app and that you make a note of the automatically generated tenant ID, user name, and password values. You need these values later to access the service by using the   {{site.data.keyword.iotmapinsights_short}} API.

2. Familiarize yourself with [OpenStreetMap ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.openstreetmap.org/){: new_window}.  

 The {{site.data.keyword.iotmapinsights_short}} service uses the road network data, in WGS84 coordinates, which is extracted from [OpenStreetMap ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.openstreetmap.org/){: new_window}. Only the roads that a car can travel on are used for analysis.  

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
2. Send the raw GPS coordinates by using the `mapMatching` API command. Optionally, set a heading angle of each position in degrees to specify the direction of the travel.
 - Request: Raw GPS data
 - Response: Map-matched GPS data, Link ID
3. Optional: Get the road type data by using the `getLinkInformation` API command. You can retrieve the matched road shape data as a series of coordinates by using the `getLinkInformation` REST API.
 - Request: Link ID
 - Response: Road type

## Route searching
{: #route_searching}

Find the shortest route path information between the specified origin and destination coordinates by using the following steps:

1. Determine a start and end position for the shortest path.
2. Send the start and end coordinates by using the `routeSearch` REST API.
Optionally, set a heading angle for each position in degrees to specify the direction of travel.
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
Search for traffic events that are within a specific rectangular area and optionally, for a specific traffic event type.
 - Request: Area information.
 - Response: Event information.  
4. Optional: Remove a traffic event that is no longer valid by using the `deleteEvent` API  command.
5. Optional: Retrieve an area on the road that is affected by a traffic event by using the `getAffectedLinksInformation` API command.

## Starter experience
{: #starter_exp}
Experience the capabilities of {{site.data.keyword.iotmapinsights_short}} and other {{site.data.keyword.iot4auto_short}} services. Visit the [{{site.data.keyword.iot4auto_short}} Starter Experience ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://iot-for-automotive-starter-experience.mybluemix.net){:new_window} page to play an interactive demo and try out some starter apps that provide examples of how you can use several {{site.data.keyword.iot4auto_short}} services on {{site.data.keyword.Bluemix_notm}} to build automotive solutions.

## Service availability and updates
{: #service_up}
To find out about the status and any upcoming planned service maintenance updates for the {{site.data.keyword.iotmapinsights_short}} API services on {{site.data.keyword.Bluemix_notm}}, go to the [IBM Watson IoT Service Health Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://status.internetofthings.ibmcloud.com).
