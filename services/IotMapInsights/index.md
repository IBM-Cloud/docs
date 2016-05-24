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
*Last updated: 24 May 2016*

{{site.data.keyword.iotmapinsights_full}} makes it easy for developers to enable their applications to use geospatial functions such as map matching and shortest path search based on the road networks across the globe.
{:shortdesc}

You can use the following functions through the {{site.data.keyword.iotmapinsights_short}} REST API:

- Highly accurate map matching that use the road network geometry.
- Manipulation of real-time events on a map, such as traffic.
- Dynamic shortest path search (route search) considering real-time events, such as traffic.
- Retrieval of the road geometry data that can be used for drawing road shapes on a map.

The {{site.data.keyword.iotmapinsights_short}} service uses the road network data, in WGS84 coordinates, that is extracted from OpenStreetMap. Only the roads that a vehicle can travel on are used for analysis.

Supported map regions are:

- Europe (map_id=1)
- Africa (map_id=2)
- Asia (map_id=3)
- Australia Oceania (map_id=4)
- North America (map_id=5)
- Central America (map_id=6)
- South America (map_id=7)


Follow these steps to use the analytics functions of the {{site.data.keyword.iotmapinsights_short}} service.

## Using {{site.data.keyword.iotmapinsights_short}} for map matching

1. Prepare a set of raw GPS coordinates data to be analyzed.
2. Send the raw GPS coordinates data in time-series order to the {{site.data.keyword.iotmapinsights_short}} service by using the `mapMatching` REST API. Optionally, set a heading angle of each position in degrees (North is 0, clockwise angle) to specify the direction of the travel.
3. Receive the map-matched coordinates and road link information in response to the `mapMatching` REST API call.
4. Optionally, retrieve the road shape data of the map matched road link by using the `getLinkInformation` REST API. Call the `getLinkInformation` REST API with a link ID to get a series of coordinates that consists of a road shape.

## Using {{site.data.keyword.iotmapinsights_short}} for route searching

1. Determine a start and end position for which you want to get a shortest path.
2. Send the start and end coordinates to the {{site.data.keyword.iotmapinsights_short}} service by using the `routeSearch` REST API. Optionally, set a heading angle of each position in degrees (North is 0, clockwise angle) to specify the direction of travel.
3. Receive a list of road links in response to the `routeSearch` REST API call. You can draw the shape of the found path on a map by using the shape data that is included in the result data.

## Using {{site.data.keyword.iotmapinsights_short}} for traffic event manipulation

1. Determine a type and position of a traffic event that you want to create.
2. Send the traffic event information to the {{site.data.keyword.iotmapinsights_short}} service by using the `createEvent` REST API.
3. Receive an event ID of the created traffic event in response to the `createEvent` REST API call.
4. Search the traffic events within a specific rectangular area, and optionally with a specific traffic event type, by using the `queryEvent` REST API.

- Optionally, remove a traffic event that is no longer valid using the `deleteEvent` REST API.
- Optionally, retrieve an area on the road that is affected by a traffic event by using the `getAffectedLinksInformation` REST API.


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
