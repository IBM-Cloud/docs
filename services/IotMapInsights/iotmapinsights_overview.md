---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}

The service provides high-speed access to static road network data, dynamic event data, and road network-based geospatial tools that you can use to integrate geospatial capabilities with your application.
{:shortdesc}

The {{site.data.keyword.iotmapinsights_short}} service provides you with the following main feature sets:

- Static map data
- Dynamic event data
- Geospatial tools

The {{site.data.keyword.iotmapinsights_short}} service collects and uses  [OpenStreetMap](http://www.openstreetmap.org/){:new_window} road network data that is stored in the service memory cache for processing.

## Static map data
{: #static_map_data_query}

One of the key features of the product is the ability to pull in detailed road information for use by your application. Use the Link Query REST API interface to query for static map road attribute data by link ID. The required link ID parameter can be identified by a [map matching function](#map_matching).

The returned data includes detailed information for each requested link ID such as road type, road length, a detail shape points array, information about adjacent nodes and adjacent links.

By using queried detail link information, your application can traverse a road link network by intelligently using the returned adjacent link information.

## Dynamic event data
{: #dynamic_event_data}

In addition to the static map data, the real world condition of roads by necessity includes dynamic events such as traffic congestion and road works. Use {{site.data.keyword.iotmapinsights_short}} to create and manage traffic events, and incorporate them with [affected link searches](#link_search) for route planning purposes.

### Event injection and deletion
{: #inject_event}

Use the {{site.data.keyword.iotmapinsights_short}} service event injection REST API to dynamically inject and remove traffic events in the form of map object models that are placed on specific road links. Each event includes basic attributes such as GPS coordinates, start time, event type, event duration, and affected length of road.

Use the event deletion REST API interface to remove events from the map when they are no longer in effect.

### Event query
{: #query_event}

Use the event query REST API to get detailed information about all dynamic events in a certain geographic area. You can query by area with a longitude and a latitude range, and include event attributes to narrow the number of target events that are returned.

## Geospatial tools
{: #geospatial_tools}

Enhance your application with the {{site.data.keyword.iotmapinsights_short}} geospatial tools that include map matching and route search functions.

### Map matching
{: #map_matching}

Use the map matching REST API interface with your application to map actual device GPS coordinates to [OpenStreetMap](http://www.openstreetmap.org/){:new_window} road network data to increase the location accuracy for inaccurate GPS data. You can also receive information about road attributes based on location. The map matching REST API enables your application to fit raw GPS data point to a matched point on the road link.

The map matching REST API interface receives one point of longitude and latitude GPS coordinate data and returns a map-matched point. This point is analyzed by considering historical data for each car within a specific time period to find the most probable point in real time. For point that do not have historical location data, the map matching interface returns the nearest point on the road link from the requested GPS point.

### Route search
{: #route_search}

One of the basic features of an application with geospatial functions is the ability to find the shortest path between two points.  

The route search REST API interface of the {{site.data.keyword.iotmapinsights_short}} service calculates the shortest path between start and end-point GPS coordinates. The received coordinates are matched to the nearest link of the map by using the map-matching function, and the shortest path between these map-matched points is calculated.

### Affected link search
{: #link_search}

When an event occurs on a road, it might affect various road links. You can use REST APIs to search affected links and to find road links where cars might reach the event. The search considers the topology of the road link network, not just the distance from cars to the event.
