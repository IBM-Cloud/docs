---

copyright:
years: 2016, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Use data from The Weather Company with your devices
{: #weathercompany}

The Weather Company integration lets you combine weather data with your existing {{site.data.keyword.iot_short_notm}} devices.
{:shortdesc}

Weather data from The Weather Company appears in the device details view if an update location request has been made by using the API, or if the device has already set its location by using a device management message.

**Important:** Only managed devices can set their own locations. All unmanaged devices must have their locations set manually by using the API. For more information on setting a device location, see [Update Location requests](../../devices/device_mgmt/index.html#update-location).

## REST APIs for The Weather Company
To access the REST API for The Weather Company, see the
Device Location Weather section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} documentation.

## Viewing weather data

To view the weather data retrieved for a device location:
1. Click the device in the **Devices** pane.
2. In the detailed device view scroll down to the **Extensions** section.  
The following weather data is listed:
 - Current weather.
 - Current temperature.
 - Predicted maximum and minimum temperature.
 - Relative humidity.
 - Pressure.
 - Visibility.
 - Wind speed.
 - Wind direction.
 - Latitude.
 - Longitude.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
