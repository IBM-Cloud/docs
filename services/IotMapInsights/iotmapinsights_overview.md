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

The {{site.data.keyword.iotmapinsights_short}} service is based on road network data that is stored in memory cache. The service provides high-speed access to static road network data, dynamic event data, and road network-based geospatial tools, which enables your application to integrate geospatial capabilities.
{:shortdesc}

## Static map data query
{: #static_map_data_query}

To access road link attribute data, the {{site.data.keyword.iotmapinsights_short}} service provides a Link Query REST API interface. The interface receives a link ID as a parameter that can be identified by a map matching function, and returns detailed information for the requested link, such as road type, length, detail shape points array, adjacent nodes, and adjacent links. By using queried detail link information, your application can traverse a road link network by observing adjacent link information.

## Dynamic event data
{: #dynamic_event_data}

An event in the {{site.data.keyword.iotmapinsights_short}} service is an object model for a traffic event that is dynamically placed on a specific road link. The event has basic attributes of a traffic event, such as GPS coordinates, time, type, duration of event, and affected length. You can dynamically inject and delete events.

## Event injection and deletion
{: #inject_event}

With the event injection REST API interface, you can store an event on a map. To inject an event, you can post the event information to the interface with a defined event type to classify events and its attributes in accordance with the intended use of your application. With the event deletion REST API interface, you can remove events from the map so that outdated events can be managed.

## Event query
{: #query_event}

With the event query REST API interface, you can query events under specified conditions that are set as request parameters. For a query condition, you can set the area with a longitude and a latitude range, and event attributes to narrow target events that are returned as a response of the request.

## Geospatial tools
{: #geospatial_tools}

For geospatial tools, the {{site.data.keyword.iotmapinsights_short}} service provides a REST API interface for map matching and route search functions.

## Map matching
{: #map_matching}

If GPS data from devices is not accurate enough to use analysis or visualization, or if the attributes of the road link network are required for your application, you can use the map matching REST API interface. The map matching REST API enables your app to fit raw GPS data point to a matched point on the road link. The map matching REST API interface receives one point of longitude and latitude GPS coordinate data and returns a map-matched point. This point is analyzed by considering historical data for each vehicle within a specific time period to find the most probable point in real time. For point that do not have historical location data, the map matching interface returns the nearest point on the road link from the requested GPS point.

## Route search
{: #route_search}

If you need to implement an application with geospatial functions, you'll need to search the shortest path between two points.  The route search REST API interface of the {{site.data.keyword.iotmapinsights_short}} service calculates the shortest path between start point and end point GPS coordinates. The received coordinates are matched to the nearest link of the map by using the map-matching function, and the shortest path between these map-matched points is calculated.

## Affected link search
{: #link_search}

When an event occurs on a road, it might affect various road links. You can use REST APIs to search affected links and to find road links where vehicles might reach the event. The search takes into consideration the topology of the road link network, not just the distance from vehicles to the event.

