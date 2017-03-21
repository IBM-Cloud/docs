---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# IoT for Automotive APIs
{: #iotautomotive_apis}


# REST APIs
{: #api}

Several APIs are available for connecting your vehicle and device data to {{site.data.keyword.iot4auto_full}} and for developing features and capabilities to build a powerful automotive solution that meets your requirements.

By using the available REST API commands, you can customize your {{site.data.keyword.iot4auto_short}} service instance in the following ways:

- Inject specific events into the system
- Store the normalized car probe data from a vehicle in the preferred analytics data store
- Retrieve the events of interest in real time together with the geographic location of the vehicle

## Vehicle Data Hub API
{: #vdh_api}

Use the [{{site.data.keyword.iot4auto_short}} API docs: Vehicle Data Hub ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/IoT4Auto_VDH_APIdoc){:new_window} to retrieve and manage large volumes of automotive data, including map context and driver behavior data. API commands are available to fetch vehicle location, movement, vehicle health, and analytic insights.


## Asset API
{: #asset_api}

Use the [{{site.data.keyword.iot4auto_short}} API docs: Asset ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/IoT4Auto_Asset_APIdoc){:new_window} to create and manage master asset data, for example, system data that relates to vehicles, rules, drivers, vendors, and event types.

## Contextual Map service API
{: #context_map_api}

Use the [Contextual Map service API ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/IoTContextMapping_APIdoc){:new_window} to enable your automotive applications to use geospatial map matching and shortest path search.

## Driver Behavior service API
{: #driver_behavior_api}

Use the [Driver Behavior service API ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window} to analyze the driver and vehicle data and produce insights and patterns about driving behavior. You can also use the Driver Behavior APIs to analyze the geographical movement and route patterns of driving trips and produce trajectory patterns.

## REST API commands
{: #rest_api_commands}

|Goal |API command |Description |
|:---|:---|:---|
|Inject events|`sendEvent`|Sends the traffic or other events to the platform.|
|Send car probe data|`sendCarProbe`|Sends the position-based sensor data from the vehicle and retrieves the affected events for the vehicle by the result of real-time analysis.|
|Create vehicle data|`createVehicle`|Create a record of the vehicle as an asset. This information is used for authentication, inventory, and other uses.|
|Get car probe data|`getCarProbe`|Gets the latest car probe data of the vehicle that was sent by the `sendCarProbe` API command.|
|Get map events|`getEvent` |Gets the events on the map that were sent by the `sendEvent` API command.|
|Get vehicle asset data|`getVehicle`| Gets the vehicle data as an asset from the `createVehicle` API command.|

*Table 1. {{site.data.keyword.iot4auto_short}} REST API commands*

More information about the available API commands is available from each of the API location links.
