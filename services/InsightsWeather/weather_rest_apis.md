---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:note:.deprecated} 

# Using the Insights for Weather REST APIs
{: #rest_apis}

You can use the [REST APIs](https://twcservice.{APPDomain}/rest-api-deprecated/){:new_window} 
to retrieve weather data. You can test API operations and instantly view the results to help you build your applications faster.
{:shortdesc}

**This service is deprecated:** All instances of this service are deprecated. 
The revised service is available in Bluemix as Weather Company Data for IBM Bluemix.  
Current apps that use the Insights for Weather APIs will continue to work without 
any modifications for 90 days after the Weather Company data service is released on July 1 2016.
To take advantage of the newly added APIs and the improved pricing model, 
it is in your best interest to migrate to one of the new plans.
{:deprecated}

From the reference documentation, click **List Operations** to view details of each operation.
When you specify parameters and click **Try it out!**, you might be asked to provide credentials.
You must provide the user name and password from your `VCAP_SERVICES` environment variables.
You can find this information by opening your application and clicking **Environment Variables** from the table of contents.

**Note:** Each region is independent. You cannot use service credentials
that are provisioned to you in one region to authenticate to a service in another region.
Failure to enter proper credentials results in an "Unauthorized" message in the response body.

With the Insights for Weather APIs, you can retrieve weather data by supplying a geolocation as latitude and longitude coordinates.
You can use the following APIs.

|**API**                                  |**Description**              |
|-----------------------------------------|-----------------------------|
|`GET /v2/forecast/daily/10day`           |Returns weather forecasts for the current day and the next nine days for a geolocation. Each daily forecast can contain a daytime forecast and a nighttime forecast. These segments are separate objects in the JSON responses. Daytime forecast data of the daily forecast are no longer available after 3:00 PM local time. At 3:00 pm local time, your application must no longer display the day forecast.|
|`GET /v2/forecast/hourly/24hour`         |Returns an hourly forecast for the current day and the next 24 hours for a geolocation. The hourly forecast data can contain up to 24 hourly forecasts for each location. You must discard all previous hourly forecasts for a location when new data is received|
|`GET /v2/observations/current`           |Returns the current weather conditions for a geolocation. These recent observations are retained in the database up to 10 minutes on specific reporting stations and 24 hours of observations per station. The recent observations data is continuously updated and replaced with a first-in / first-out methodology (rotating data with newest observation and moving the oldest observations to the archive storage) based on date/time stamping of the observations.|
|`GET /v2/observations/timeseries/24hour` |Returns both the current observations and up to 24 hours of past observations, from the current date and time, for a geolocation. Weather observations are gathered from physical devices deployed worldwide, and the current weather observations.|
*Table 1. Insights for Weather API summary*

## Time-series observations
{: #time_series}

The time-series weather observations data provides information about temperature,
precipitation, wind, barometric pressure, visibility, ultraviolet (UV) radiation,
and other related observation elements, including observation station,
observation date/time, weather icon codes and phrases. The difference between
time-series observations and current observations is the time period
of the observation, which results in one or more observation data sets.

The current conditions are the most recent observations for the location that is
requested with no time parameter. One data set is returned. The time-series
observations include past observations that occurred up to and including the
last 24 hours for the location requested.

Recent observations are retained in the primary database up to 48 hours (2 days)
on specific reporting stations. The recent observations data is continuously
updated and replaced with a first-in/first-out methodology (rotating data with
newest observation and moving the oldest observations to the archive storage)
based on date/time stamping of the observations. The amount of data that is
retained and available from any station can be more than 24 individual
observation reports. The number of observations is
determined by the type of observation it is.

## URL construction
{: #url_construction}

The Insights for Weather APIs use a common URL structure and query parameters to request and filter weather data.
The URLs that are passed to the Insights for Weather APIs are constructed as follows:

```
https://twcservice.mybluemix.net/api/weather/v2/<product group>/&format={format type}&geocode={latitude,longitude}&language={language code}&units={units code}

```

|**Attribute**     |**Description**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |The hosted URL path (for example, `https://twcservice.mybluemix.net:443/api/weather`)|
|`version`         |The current iteration (for example, "v2")|
|`product group`   |The product (for example, "observations" or "forecast")|
|`geocode`         |The optional latitude and longitude, for example, "45.4214,75.6919" represents Ottawa, Canada. If you supply a geocode coordinate, the API returns data for the closest location available. Periods are used as decimal separators and commas are used to separate latitude and longitude values. If you supply a geocode, the actual latitude and longitude values that are used are returned in the metadata of the response.|
|`language`        |The language to return the response in. The default is en-US. The default or requested translation language is returned in the language parameter in the metadata of the response.|
|`units`           |The optional units to return the response in. The API supports English (e), Metric (m), and UK-Hybrid (h) units of measure. If you supply the units of measure but don't supply a value, the API returns the data in the unit of measure that corresponds to the language code. The default or requested unit of measure is returned in the units parameter in the metadata of the response.|
*Table 2. URL details*

## Units of measure
{: #units_measure}

When you use the Insights for Weather APIs, you don't need to explicitly pass a unit of measure. The Insights for Weather APIs default to the unit of measure that is associated with the language code in the URL. However, if you want to provide a unit of measure that is different from the default, you can pass in a unit of measure that overrides the default.

* For en-US or en, the default unit of measure code is English/Imperial. The unit code is "e".
* For en-GB, the default unit of measure is Hybrid-UK. The unit code is "h".
* For everything else, the default unit of measure is Metric. The unit code is "m".

## Language translation
{: #language_translation}

The Insights for Weather APIs translate the phrases and unit of measure. When you format a request URL, you must provide a valid language.
The following fields are translated:

|**Field**           |**Description**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |The narrative forecast for the 24-hour period|
|`dow`               |Day of week|
|`wind_phrase`       |The phrase that describes the wind direction and speed for a 12-hour daypart|
|`wdir_cardinal`     |Daytime average wind direction in cardinal notation|
|`daypart_name`      |The name of a 12-hour daypart not including day names in the first 48 hours|
|`temp_phrase`       |The short phrase that contains the forecasted high or low temperature for 12-hour forecast period|
|`shortcast`         |An abbreviated sensible weather portion of narrative forecast|
|`long_daypart_name` |The named time frame for the valid weather forecast in an expanded format. The named time frame can be either for 12-hour periods or 24-hour periods.|
|`golf_category`     |The golf index category that is expressed as a phrase for the weather conditions for playing golf|
|`phrase_nnchar`     |Daytime sensible weather phrase|
|`lunar_phrase`      |Three-character short code for lunar phases|
|`uv_desc`           |The UV index description, which complements the UV index value by providing an associated level of risk of skin damage due to exposure|
|`sky_cover`         | Descriptive sky cover that is based on percentage of cloud cover|
|`ptend_desc`        | Descriptive text of pressure tendency over the past 3 hours|
*Table 3. Translated response fields*

## Handling null or missing data fields in the API response
{: #handling_null_or_missing}

If a data field is null because the data is not available, the Insights for Weather APIs either return the appropriate field tags with the word "null" or don't return the field at all.

## Handling errors
{: #handling_errors}

The following error codes are common to all APIs:

|**Error** |**Description**                                    |
|----------|---------------------------------------------------|
|400       |Bad request. The request was not understood by the server due to malformed syntax. This error code is implemented for all APIs. API rejects the request if any invalid parameters are supplied.|
|401       |Unauthorized. The request requires authentication.|
|403       |Forbidden. The server understood the request but is refusing to fulfill it.|
|404       |Not found. If a required parameter is not present in the API request, a MissingParameterException error with a 404 error code is returned.|
|405       |Method Not Allowed. For example, sending a POST instead of a GET.|
|406       |Not Acceptable. For example, not accepting gzip compressed responses.|
|408       |Request Timeout. Client did not produce request within time server was willing to wait.|
|500       |Internal server error. The server encountered an unexpected condition that prevented it from fulfilling the request.|
|502-504   |Service Unavailable or Gateway issue. These error codes are returned if the service is temporarily unavailable.|
*Table 4. Error response code*

The response on error is always the same. Multiple error codes can be returned in one response.
For example, a JSON error response might be returned as follows:

```
{
  metadata: {
    transaction_id: "1411496413365:-1880721071"
  },
  success: false,
  errors: [
    {
      error: {
        code: "NDF-0001",
        message: "There was no data found for your product query."
      }
    }
}
```