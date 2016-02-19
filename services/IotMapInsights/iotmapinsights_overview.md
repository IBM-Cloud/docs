{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}

{{site.data.keyword.iotmapinsights_short}} service is based on road network data stored in memory cache and provides high speed access to static road network data, dynamic event data and road network based geospatial tools, which enables your application to integrate geospatial capabilities.
{:shortdesc}

## {{site.data.keyword.iotmapinsights_full}}
{: #iotmapinsights_concept}

### Static map data query
{: #static_map_data_query}
In order to access road link attribute data, {{site.data.keyword.iotmapinsights_short}} provide Link Query REST API interface. The interface receives link ID as parameter that could be identified by map matching function below, and returns detail information of requested link like road type, length, detail shape points array and next nodes, links. By using queried detail link information, your application can traverse link to link by observing next link information.
 
### Dynamic event data
{: #dynamic_event_data}
Event in {{site.data.keyword.iotmapinsights_short}} is the object model for traffic event which is placed on specific road link and has basic attribute of traffic event like GPS coordinate, time, type, duration of event, affected length and so on.

### Inject event 
{: #inject_event}
Inject Event interface allows you to store event on map. In order to inject an event, you can post the event information to the interface with define event type for classify events and its attributes in accordance with the intended use of your application.

### Query event
{: #query_event}
Query Event interface allows you to query events under specified conditions that are set as request parameters. For query condition, you can set area with longitude and latitude range and event attribute to narrow target events that are returned as response of request.

### Geospatial tools
{: #geospatial_tools}
As geospatial tools, {{site.data.keyword.iotmapinsights_short}} provide REST API interface for map matching, route search, and link search functions.

### Map matching
{: #map_matching}
If GPS data from devices is not enough accurate to analyze or visualize and also the attributes of road link attribute is required for your application, you can use Map Matching REST API interface to fit raw GPS data point to matched point on the road link.
Map Matching interface receives the one point of longitude and latitude GPS coordinate data and return map matched point that is analyzed by taking into account the each vehicles specific period of history data in order to find most probable point in real time.
For the point which does not have history of location data, the map matching interface return nearest point on road link from requested GPS point.

### Route search
{: #route_search}
Searching shortest path between two points is likely to be needed if you need to implement application with geospatial functions. Route search interface of Map Insight provide the function to calculate specific GPS coordinates. The request coordinates are map matched to nearest link of map using map matching function and calculate the shortest path between these map matched points. 

### Link search
{: #link_search}
To find all links that are reachable from specific point, you can use Link Search interface. The interface returns all links in consideration of regulated traffic direction. In order to use this interface you can specify GPS coordinate of start point of search with heading information as search direction and search range.
