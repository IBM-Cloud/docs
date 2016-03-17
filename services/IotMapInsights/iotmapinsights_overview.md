---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}

The {{site.data.keyword.iotmapinsights_short}} service is based on road network data that is stored in memory cache and provides high- speed access to static road network data, dynamic event data and road network-based geospatial tools, which enables your application to integrate geospatial capabilities.
{:shortdesc}

## {{site.data.keyword.iotmapinsights_full}}
{: #iotmapinsights_concept}

### Static map data query
{: #static_map_data_query}

In order to access road link attribute data, the {{site.data.keyword.iotmapinsights_short}} service provides Link Query REST API interface. The interface receives link ID as parameter that might be identified by map matching function, and returns detail information of requested link, such as road type, length, detail shape points array, adjacent nodes, and adjacent links. By using queried detail link information, your application can traverse road link network by observing adjacent link information.

### Dynamic event data
{: #dynamic_event_data}

An event in the {{site.data.keyword.iotmapinsights_short}} service is the object model for traffic event that is dynamically placed on specific road link and has basic attribute of traffic event like GPS coordinate, time, type, duration of event, affected length and so on. You can dynamically inject and delete events.

### Event injection and deletion
{: #inject_event}

With event injection REST API interface, you can store event on map. In order to inject an event, you can post the event information to the interface with defined event type to classify events and its attributes in accordance with the intended use of your application. With event deletion REST API interface, you can remove events from map, so that outdated events can be managed adequately.

### Event query
{: #query_event}

With event query REST API interface, you can query events under specified conditions that are set as request parameters. For query condition, you can set area with longitude and latitude range and event attribute to narrow target events that are returned as response of request.

### Geospatial tools
{: #geospatial_tools}

As geospatial tools, the {{site.data.keyword.iotmapinsights_short}} service provides REST API interface for map matching and route search functions.

### Map matching
{: #map_matching}

If GPS data from devices is not accurate enough to use analysis or visualization, or if the attributes of road link network are required for your application, you can use Map Matching REST API interface to fit raw GPS data point to matched point on the road link. Map Matching REST API interface receives the one point of longitude and latitude GPS coordinate data and returns map matched point that is analyzed by considering historical data of each vehicle within specific time period in order to find most probable point in real time. For the point that does not have historical location data, the map matching interface return nearest point on road link from requested GPS point.

### Route search
{: #route_search}

Functions to search the shortest path between two points is likely to be required if you need to implement application with geospatial functions. Route search REST API interface of the {{site.data.keyword.iotmapinsights_short}} service calculates the shortest path between two GPS coordinates of the start point and the end point. The received coordinates are map that is matched to the nearest link of map by using map matching function and calculation is done for the shortest path between these map matched points.

### Affected link search
{: #link_search}

When an event occurs on a road, it might affect various road links. REST APIs to search affected links find road links where vehicles on the road link might reach the event. The search is executed considering the topology of the road link network, not just distance from vehicles to the event.

