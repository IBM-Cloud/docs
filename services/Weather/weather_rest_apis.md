---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Using the {{site.data.keyword.weather_short}} REST APIs
{: #rest_apis}

You can use the [REST APIs](https://twcservice.{APPDomain}/rest-api/){:new_window}
to retrieve weather data. You can test API operations and instantly view the results
to help you build your applications faster.
{: shortdesc}

From the reference documentation, click **List Operations** to view details of each operation.
When you specify parameters and click **Try it out!**, you might be asked to provide credentials.
You must provide the user name and password from your `VCAP_SERVICES` environment variables.
You can find this information by opening your application and clicking **Environment Variables** from the table of contents.

**Note:** Each region is independent. You cannot use service credentials
that are provisioned to you in one region to authenticate to a service in another region.
Failure to enter proper credentials results in an *Unauthorized* message in the response body.

With the REST APIs, you can retrieve weather data by supplying a geolocation as latitude and longitude coordinates.
You can use the following APIs.

|**API**                                  |**Description**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |Returns the hourly weather forecast for the next 48 hours for a geolocation depending on the format that you supply. You can supply a `geocode/{latitude}/{longitude}` or a `location/{locationId}`. The hourly forecast data can contain up to 48 hourly forecasts for each location. You must discard all previous hourly forecasts for a location when new data is received.|
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |Returns daily weather forecasts for 3, 5, 7, or 10 days for a geolocation depending on the format that you supply. The number of days to be retrieved is specified in the format as `3day`, `5day`, `7day`, or `10day`. You can supply a `geocode/{latitude}/{longitude}` or a `location/{locationId}`. Each daily forecast can contain a daytime forecast, a nighttime forecast, and a 24-hour forecast. These segments are separate objects in the JSON responses. Daytime forecast data of the daily forecast is no longer available after 3:00 PM local time. At 3:00 PM local time, your application must no longer display the day forecast.|
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|Returns daily weather forecasts in six-hour periods for 3, 5, 7, or 10 days for a geolocation depending on the format that you supply. The number of days to be retrieved is specified in the format as `3day`, `5day`, `7day`, or `10day`. You can supply a `geocode/{latitude}/{longitude}` or a `location/{locationId}`. Each daily forecast can contain a morning, afternoon, evening, and overnight forecast. These segments are separate objects in the JSON responses.|
|`GET /v1/{geocode or location ID}/observations.json`              |Returns the current weather conditions for a geolocation. You can supply a `geocode/{latitude}/{longitude}` or a `location/{locationId}`.  These recent observations are retained in the database up to 10 minutes on specific reporting stations and 24 hours of observations per station. The recent observations data is continuously updated and replaced with a first-in / first-out methodology (rotating data with newest observation and moving the oldest observations to the archive storage) based on date/time stamping of the observations.|
|`GET /v1/{geocode or location ID}/observations/timeseries.json`   |Returns both the current observations and up to 24 hours of past observations, from the current date and time, for a geolocation. You can supply a `geocode/{latitude}/{longitude}` or a `location/{locationId}`. Weather observations are gathered from physical devices deployed worldwide, and the current weather observations.|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |Returns weather watches, warnings, statements, and advisories that are issued by the National Weather Service (NWS), Environment Canada, and MeteoAlarm (Europe) and include the translation of the event description, country name, and alert headlines in 49 languages. You can supply a `geocode/{latitude}/{longitude}`, `country/{countrycode}`, `country/{countrycode}/state/{statecode}`/, or `country/{countrycode}/area/{areaid}`.|
|`GET /v1/alert/{detail_key}/details.json`                         |Returns weather watches, warnings, statements, and advisories that are issued by the National Weather Service (NWS), Environment Canada, and MeteoAlarm (Europe). The details include in-depth information about the alert that is issued by the government weather authority for the specified area and include the translation of the event description, country name, and alert headlines in 49 languages.|
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |Returns daily almanac information (US only) that is sourced from National Weather Service observations stations from a time period spanning 10 to 30 years or more. The information is gathered and provided by the National Climatic Data Center (NCDC). You can supply a `geocode/{latitude}/{longitude}`, or `location/{PostalLocationId}`.|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |Returns monthly almanac information (US only) that is sourced from National Weather Service observations stations from a time period spanning 10 to 30 years or more. The information is gathered and provided by the National Climatic Data Center (NCDC). You can supply a `geocode/{latitude}/{longitude}`, or `location/{PostalLocationId}`.|
|`GET /v3/location/{search or point}`                                  |Provides the ability to look up a location name or geocode (latitude and longitude) to retrieve a set of locations that match the request. The Location Service supports search by city name or postal code.|
*Table 1. {{site.data.keyword.weather_short}} API summary*

## Daily and intraday forecasts
{: #daily_intraday}
The daily forecast API can contain multiple days of daily forecasts for each location.
Each day of a forecast can contain up to three separate forecasts. For any
forecast day, the API can return day, night, and 24-hour forecasts.

The intraday forecast API can contain multiple days of daily forecasts for each location.
Each day of a forecast contains four separate six-hour forecasts for morning (7 AM to 1 PM),
afternoon (1 PM to 7 PM), evening (7 PM to 1 AM), and overnight (1 AM to 7 AM). The
intraday forecast is similar in structure to the daily forecast.

Each segment has a day part number, day of the week name, and day part name. For example,
the following example shows the data field order and data values for
`num`, `dow`, and the `daypart_name`, for a forecast that is generated
by the APIs on a Thursday morning:
* 1, Thursday, Morning
* 2, Thursday, Afternoon
* 3, Thursday, Evening
* 4, Thursday, Overnight
* 5, Friday, Morning
* 6, Friday, Afternoon
* 7, Friday, Evening
* 8, Friday, Overnight

## Current and time-series observations
{: #time_series}

The current conditions and time-series weather observations data provides information about temperature,
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

## Alert headlines and details
{: #alerts_levels}
The alert APIs return active weather alert headlines that are related to severe
thunderstorms, tornadoes, earthquakes, and floods.
These APIs also return non-weather alerts such as child abduction alerts and
law enforcement warnings.

**Note**: This API is available only for the United States, Canada, and Europe.

The Alert Headlines API provides a key value in the `detail_key` attribute
to access the alert details in the Alert Details API.
Query the Alert Headlines API to get the `detail_key` value, and then retrieve the
Alert Details API response with the `detail_key`.

**Note**: You must display the data source attribution for any alert data that is displayed in your application.

The attribution phrase must display the following information:

*Issued by <Office Name> - &lt;Office Admin District Code&gt;, &lt;Office Country Code&gt;, &lt;Source&gt;, &lt;Disclaimer&gt;*

For example:
* Issued by National Weather Service - Bismarck, US
* Issued by Central Institute for Meteorology and Geodynamics - Austria, EMETNET-Meteoalarm

## Almanac information
{: #almanac_details}
The Almanac API requires a location ID and location type (city or postal code)
or a latitude and longitude pair to retrieve the information for a specific location.

When you use `location` in the URL, the location must include a location ID
(postal code) with a location type and a
country code. When you use `geocode` in the URL, the search location must be a valid
latitude and longitude combination.

The Almanac API uses parameters to specify either daily or monthly data,
a specific date or date range of information, and the units of measure to return the data in.

The date parameters are `start` and `end`. The `start` parameter is a required parameter
but the `end` parameter is optional. When the parameters are used together, the combination returns a
range of data instead of a specific month or day of data.

The date format for retrieving Daily Almanac results is a four-digit numeric value that represents
the month and day for the data required, that is, MMDD. Any single digit
day **must** have a preceding zero, for example, 01.

The date format for retrieving Monthly Almanac results is month, that is, MM. Any single digit
month **must** have a preceding zero, for example, 01. Any other format results in
an API error and no data will be returned.

**Note**: If you don't provide the date value in the request, the system returns a
status of 404 (Bad Request). The API does not provide a default value.

## URL construction
{: #url_construction}

The REST APIs use a common URL structure and query parameters to request and filter weather data.
The URLs that are passed to the APIs are constructed as follows:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

For example:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**Attribute**     |**Description**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |The hosted URL path. For example, `https://twcservice.mybluemix.net:443/api/weather`.|
|`version`         |The current iteration. For example, `v1`.|
|`location`        |The geocode or location ID. The location group can be `geocode` or `location`. For example, `geocode/45.4214/75.6919` represents Ottawa, Canada. If you supply a geocode coordinate, the API returns data for the closest location available. Periods are used as decimal separators and commas are used to separate latitude and longitude values. If you supply a geocode, the actual latitude and longitude values that are used are returned in the metadata of the response.|
|`product group`   |The product. For example, `observations` or `forecast`. A product subgroup, for example, `historical`, is optional.|
|`date`            |The date type. For example, `daily` or `monthly`.|
|`format`          |The format. For example, `3day`, `5day`, `7day`, or `10day`.|
|`units`           |The optional units to return the response in. The API supports English (e), Metric (m), and UK-Hybrid (h) units of measure. If you supply the units of measure but don't supply a value, the API returns the data in the unit of measure that corresponds to the language code. The default or requested unit of measure is returned in the units parameter in the metadata of the response.|
|`language`        |The language to return the response in. The default is en-US. The default or requested translation language is returned in the language parameter in the metadata of the response.|
*Table 2. URL details*

**Note**: The REST APIs use the ISO 3166 standard for country codes. For more information, see the
[ISO Standard Online Browsing Platform](https://www.iso.org/obp/ui/#search/code/){:new_window}.
The APIs use the WGS84 geocode coordinate reference system. For more information, see
[Basic Geo Vocabulary](https://www.w3.org/2003/01/geo/){:new_window}.

## Icon codes and images
{: #icon_code_images}

When the {{site.data.keyword.weather_short}} REST APIs return an icon code in the response,
you can use the icon code to determine which icon image to display in your app.
There is a one to one relationship between the icon code in the API response and the file name of the icon image.
For example, if the API response contains an `icon_code` of 1, you can use the file name `01.png`
to display the matching icon image.

In your code, you can create a function that uses the `icon_code` to determine
the URL of the icon image. For example:

```
function getIconURL(code) {
    return "images/weathericons/icon" + code + ".png";
}
```

The following table contains icon codes, descriptions, and images that can be used
with the {{site.data.keyword.weather_short}} REST APIs. The table indicates whether an icon
is used in the Forecast or Observation APIs and whether the icon is available in Night or Daytime
forecast parts.

|**Code**|**Description**|**Image**|**API usage** |**Night or Daytime**|
|----|--------------------------|------------|------------|--------------------|
| 0  | Tornado                  | <img src="images/00.png " width="100" height="100" alt="Icon image."/>| Forecast                | Night and Day |
| 1  | Tropical Storm           | <img src="images/01.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 2  | Hurricane                | <img src="images/02.png " width="100" height="100" alt="Icon image."/>| Forecast                | Night and Day |
| 3  | Strong Storms            | <img src="images/03.png " width="100" height="100" alt="Icon image."/>| Forecast                | Night and Day |
| 4  | Thunder and Hail         | <img src="images/04.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 5  | Rain to Snow Showers     | <img src="images/05.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 6  | Rain / Sleet             | <img src="images/06.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 7  | Wintry Mix Snow / Sleet  | <img src="images/07.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 8  | Freezing Drizzle         | <img src="images/08.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 9  | Drizzle                  | <img src="images/09.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 10 | Freezing Rain            | <img src="images/10.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 11 | Light Rain               | <img src="images/11.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 12 | Rain                     | <img src="images/12.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 13 | Scattered Flurries       | <img src="images/13.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 14 | Light Snow               | <img src="images/14.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 15 | Blowing / Drifting Snow  | <img src="images/15.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 16 | Snow                     | <img src="images/16.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 17 | Hail                     | <img src="images/17.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 18 | Sleet                    | <img src="images/18.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 19 | Blowing Dust / Sandstorm | <img src="images/19.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 20 | Foggy                    | <img src="images/20.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 21 | Haze / Windy             | <img src="images/21.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 22 | Smoke / Windy            | <img src="images/22.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 23 | Breezy                   | <img src="images/23.png " width="100" height="100" alt="Icon image."/>| Forecast                | Night and Day |
| 24 | Blowing Spray / Windy    | <img src="images/24.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 25 | Frigid / Ice Crystals    | <img src="images/25.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 26 | Cloudy                   | <img src="images/26.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 27 | Mostly Cloudy            | <img src="images/27.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 28 | Mostly Cloudy            | <img src="images/28.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Day         |
| 29 | Partly Cloudy            | <img src="images/29.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night       |
| 30 | Partly Cloudy            | <img src="images/30.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Day         |
| 31 | Clear                    | <img src="images/31.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night       |
| 32 | Sunny                    | <img src="images/32.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Day         |
| 33 | Fair / Mostly Clear      | <img src="images/33.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night       |
| 34 | Fair / Mostly Sunny      | <img src="images/34.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Day         |
| 35 | Mixed Rain & Hail        | <img src="images/35.png " width="100" height="100" alt="Icon image."/>| Forecast                | Day         |
| 36 | Hot                      | <img src="images/36.png " width="100" height="100" alt="Icon image."/>| Forecast                | Day         |
| 37 | Isolated Thunderstorms   | <img src="images/37.png " width="100" height="100" alt="Icon image."/>| Forecast                | Day         |
| 38 | Thunderstorms            | <img src="images/38.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 39 | Scattered Showers        | <img src="images/39.png " width="100" height="100" alt="Icon image."/>| Forecast                | Day         |
| 40 | Heavy Rain               | <img src="images/40.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 41 | Scattered Snow Showers   | <img src="images/41.png " width="100" height="100" alt="Icon image."/>| Forecast                | Day         |
| 42 | Heavy Snow               | <img src="images/42.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
| 43 | Blizzard                 | <img src="images/43.png " width="100" height="100" alt="Icon image."/>| Forecast                | Night and Day |
| 44 | Not Available (N/A)      | <img src="images/44.png " width="100" height="100" alt="Icon image."/>| Forecast                | Night and Day |
| 45 | Scattered Showers        | <img src="images/45.png " width="100" height="100" alt="Icon image."/>| Forecast                | Night       |
| 46 | Scattered Snow Showers   | <img src="images/46.png " width="100" height="100" alt="Icon image."/>| Forecast                | Night       |
| 47 | Scattered Thunderstorms  | <img src="images/47.png " width="100" height="100" alt="Icon image."/>| Forecast and Observations | Night and Day |
*Table 3. Icon codes and images*

You can download this set of weather icons as [PNGs](https://twcdocs.mybluemix.net/download/weather_icons_200x200_png.zip){:new_window} 
or [SVGs](https://twcdocs.mybluemix.net/download/weather_icons_200x200_svg.zip){:new_window} and use them your app. 

You can also download the [set of icons](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} that the
[{{site.data.keyword.weather_short}} demo app](http://weather-company-data-demo.{APPDomain}){: new_window} uses.

## Units of measure
{: #units_measure}

When you use the REST APIs, you don't need to explicitly pass a unit of measure. The APIs default to the unit of measure that is associated with the language code in the URL. However, if you want to provide a unit of measure that is different from the default, you can pass in a unit of measure that overrides the default.

* For en-US or en, the default unit of measure code is English/Imperial. The unit code is `e`.
* For en-GB, the default unit of measure is Hybrid-UK. The unit code is `h`.
* For everything else, the default unit of measure is Metric. The unit code is `m`.

## Language translation
{: #language_translation}

The REST APIs translate the phrases and unit of measure. When you format a request URL, you must provide a valid language.
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
|`wx_phrase`         |A text description of the observed weather conditions at the reporting station.|
|`pressure_desc`     |A phrase that describes the change in the barometric pressure reading over the last hour.|
|`headline_text`     |The text of the headline of an event for the location.|
|`event_desc`        |A description of an event.|
|`cntry_name`        |The country name where an event occurred, given in mixed case letters.|
*Table 4. Translated response fields*

## Handling null or missing data fields in the API response
{: #handling_null_or_missing}

If a data field is null because the data is not available, the REST APIs either return the appropriate field tags with the word `null` or don't return the field at all.

## Handling errors
{: #handling_errors}

The following error codes are common to all APIs:

|**Error** |**Description**                                    |
|----------|---------------------------------------------------|
|400       |Bad request. The request was not understood by the server due to malformed syntax. This error code is implemented for all APIs. API rejects the request if any invalid parameters are supplied.|
|401       |Unauthorized. The request requires authentication.|
|403       |Forbidden. The server understood the request but is refusing to fulfill it.|
|404       |Not found. If a required parameter is not present in the API request, a MissingParameterException error with a 404 error code is returned.|
|500       |Internal server error. The server encountered an unexpected condition that prevented it from fulfilling the request.|
*Table 5. Error response code*

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