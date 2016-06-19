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
{: #gettingstartedtemplate}
*Last updated: 19 June 2016*
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} makes it easy for you to enable geospatial functions such as map matching and shortest path search for road networks across the globe with your applications.  
{:shortdesc}

The following features are available through the {{site.data.keyword.iotmapinsights_short}} REST API:

- Highly accurate map matching.  
Match your GPS location to the actual mapped road network.
- Road geometry data retrieval.  
Retrieve the mapped road network to draw road shapes on a map.
- Dynamic shortest path search.  
Use for route searches that incorporate real-time events such as traffic.
- Real-time traffic event manipulation.  
Add real-time map-matched events such as traffic conditions for use with route planning.

The following tasks outline the required steps to implement these functions in your application with the {{site.data.keyword.iotmapinsights_short}} API after you create and deploy it as an unbound service instance. Use these steps as guidance when you develop your application.

## Before you begin
- Get the automatically generated *Tenant ID*, *Username*, and *Password* that are required to access the {{site.data.keyword.iotmapinsights_short}} API.

 1. From the {{site.data.keyword.Bluemix_notm}} dashboard, click the {{site.data.keyword.iotmapinsights_short}} tile.
 2. Select the **Manage** view of your service instance.
 3. Make a note of the *Tenant ID*, *Username*, and *Password* that are listed for your Tenant ID.
- Familiarize yourself with OpenStreetMap.  
 The {{site.data.keyword.iotmapinsights_short}} service uses the road network data, in WGS84 coordinates, that is extracted from  [OpenStreetMap](http://www.openstreetmap.org/){:new_window}. Only the roads that a car can travel on are used for analysis.  
 Supported map regions are:
 - Europe (map_id=1)
 - Africa (map_id=2)
 - Asia (map_id=3)
 - Australia Oceania (map_id=4)
 - North America (map_id=5)
 - Central America (map_id=6)
 - South America (map_id=7)

## Using {{site.data.keyword.iotmapinsights_short}} for map matching
Map raw GPS coordinates to map-matched coordinates.

1. Prepare a set of raw GPS coordinates data to be analyzed.
2. Send the raw GPS coordinates with the `mapMatching` API.  
 Optionally, set a heading angle of each position in degrees to specify the direction of the travel.
 - Request: Raw GPS data
 - Response: Map-matched GPS data, Link ID
3. Optional: Get road type data with the `getLinkInformation` API.  
Retrieve the matched road shape data as a series of coordinates with the `getLinkInformation` REST API.
 - Request: Link ID
 - Response: Road type

## Using {{site.data.keyword.iotmapinsights_short}} for route searching
Find the shortest route path information between the specified origin and destination coordinates.

1. Determine a start and end position for which you want the shortest path.
2. Send the start and end coordinates with the `routeSearch` REST API.
Optionally, set a heading angle for each position in degrees to specify the direction of travel.
 - Request: Origin and destination coordinates.
 - Response: Map-matched shortest route.  

Use the returned link shape data to draw the shape of the found path on a map.

## Using {{site.data.keyword.iotmapinsights_short}} for traffic event manipulation
Inject new event information into the {{site.data.keyword.iotmapinsights_short}} service.

1. Decide a type and position of a traffic event that you want to create.
2. Inject the event with the `createEvent` API.  
Send the traffic event information to the {{site.data.keyword.iotmapinsights_short}} service.
 - Request: Event information.
 - Response: Event ID.  
3. Find events with the `queryEvent` REST API.  
Search the traffic events within a specific rectangular area, and optionally with a specific traffic event type.
 - Request: Area information.
 - Response: Event information.  
4. Optional: Remove a traffic event that is no longer valid with the `deleteEvent` API.
5. Optional: Retrieve an area on the road that is affected by a traffic event with the `getAffectedLinksInformation` API.


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

