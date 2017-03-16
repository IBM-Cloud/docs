---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-09"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Service administration dashboard
{: #service-dashboard}


You can see the status of your {{site.data.keyword.geospatialshort_Geospatial}} service instance and stop or restart it from the service administration dashboard. You can get to the service administration dashboard by clicking the {{site.data.keyword.geospatialshort_Geospatial}} tile on your {{site.data.keyword.geospatialshort_Geospatial}} dashboard. If you are using the sample application and your service instance hits the event limit and stops, you can restart the service. Stopping the service removes the event limit. It continues to receive events until you stop the service. The service administration dashboard also displays the status of your service instance and statistics.
{:shortdesc}

##{{site.data.keyword.geospatialshort_Geospatial}} Region Checks

{{site.data.keyword.geospatialshort_Geospatial}} monitors devices on-the-move from the Internet of Things. Each monitored device sends device messages containing a unique identifier along with its current position, comprising latitude and longitude. The device position is checked against the coordinates of each defined geographical region. The service then produces events when devices enter, exit, or are "hanging out" in a specific region.

A Region Check is used as unit to measure usage of the {{site.data.keyword.geospatialfull}}. For each device message, one region check is performed if entry, exit, or both entry and exit detection is specified for the region. For each device message, one region check is performed if hangout detection is specified for the region. If no regions are defined, for each device message, one region check is counted as if there is 1 region. This means that if you have 100 regions defined checking, entry, exit, and hangout, a single device message would produce 200 region checks.
