---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-28"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}

The {{site.data.keyword.iotmapinsights_full}} is a service on {{site.data.keyword.Bluemix_notm}} that you can use to get fast access to static road network data and dynamic event data. {{site.data.keyword.iotmapinsights_short}} also provides geospatial tools for road networks, which you can use to integrate geospatial capabilities with your applications.
{:shortdesc}

The {{site.data.keyword.iotmapinsights_short}} service provides the following features:

- Static map data
- Dynamic event data
- Geospatial tools

The {{site.data.keyword.iotmapinsights_short}} service collects and uses [OpenStreetMap](http://www.openstreetmap.org/){: new_window} road network data that is stored in the service memory cache for processing.

Data from OpenStreetMap is made available under the Open Data Common Open Database License (ODbL) by the OpenStreetMap Foundation (OSMF). For more information, see [OpenStreetMap Copyright and License](http://www.openstreetmap.org/copyright){: new_window}.

## Static map data
{: #static_map_data_query}

One of the key features of the product is the ability to retrieve detailed road information for use with your applications. Use the Link Query REST API interface to query for static map road attribute data by link ID. Use the [map matching function](#map_matching) function of  {{site.data.keyword.iotmapinsights_short}} to identify the required link ID parameter.

The data that is returned includes the following information about the requested link ID:

- Road type
- Road length
- An array of detailed shape points
- Information about adjacent nodes and adjacent links

By querying detail road link information, your application can traverse a road link network by intelligently using the adjacent link information that is returned.

## Dynamic event data
{: #dynamic_event_data}

In addition to the static map data, the real world condition of roads by necessity includes dynamic events such as traffic congestion and road works. Use {{site.data.keyword.iotmapinsights_short}} to create, manage, and incorporate traffic events with [affected link searches](#link_search) for route planning purposes.

### Injecting and deleting events
{: #inject_event}

Use the {{site.data.keyword.iotmapinsights_short}} service event injection REST API to dynamically inject and remove traffic events in the form of map object models that are placed on specific road links. Each event includes basic attributes such as GPS coordinates, start time, event type, event duration, and the affected length of the road.

Use the event deletion REST API interface to remove events from the map when they are obsolete.

### Event query
{: #query_event}

Use the event query REST API to get detailed information about all dynamic events in a certain geographic area. You can query by area with a longitude and a latitude range, and you can include event attributes to narrow the number of target events that are returned.

## Geospatial tools
{: #geospatial_tools}

Enhance your application with the map matching and route search functions that are provided by the {{site.data.keyword.iotmapinsights_short}} geospatial tools.

### Map matching
{: #map_matching}

Use the map matching REST API interface with your application to map actual device GPS coordinates to [OpenStreetMap](http://www.openstreetmap.org/){: new_window} road network data to increase the location accuracy for inaccurate GPS data. You can also receive information about road attributes based on location. The map matching REST API enables your application to fit raw GPS data point to a matched point on the road link.

The map matching REST API interface receives one point of longitude and latitude GPS coordinate data and returns a map-matched point. The map-matched point is analyzed by considering historical data for each car within a specific time period to find the most probable point in real time. For points that do not have historical location data, the map matching interface returns the nearest point on the road link from the requested GPS point.

### Route search
{: #route_search}

One of the basic features of an application with geospatial functions is the ability to find the shortest path between two points.  

The route search REST API interface of the {{site.data.keyword.iotmapinsights_short}} service calculates the shortest path between start and end-point GPS coordinates. The received coordinates are matched to the nearest link of the map by using the map-matching function, and the shortest path between these map-matched points is calculated.

### Affected link search
{: #link_search}

When an event occurs on a road, it might affect various road links. You can use REST APIs to search for affected links and to also find road links where cars might reach the event. The search considers the topology of the road link network, not just the distance from cars to the event.
