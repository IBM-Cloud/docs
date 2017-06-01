---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Using the Weather package
{: #openwhisk_catalog_weather}

The `/whisk.system/weather` package offers a convenient way to call the Weather Company Data for IBM Bluemix API.

The package includes the following action.

| Entity | Type | Parameters | Description |
| --- | --- | --- | --- |
| `/whisk.system/weather` | package | username, password | Services from the Weather Company Data for IBM Bluemix API  |
| `/whisk.system/weather/forecast` | action | latitude, longitude, timePeriod | forecast for specified time period|

Creating a package binding with the `username` and `password` values is suggested. This way, you don't need to specify the credentials every time you invoke the actions in the package.

## Setting up the Weather package in Bluemix

If you're using OpenWhisk from Bluemix, OpenWhisk automatically creates package bindings for your Bluemix Weather service instances.

1. Create a Weather Company Data service instance in your Bluemix [dashboard](http://console.ng.Bluemix.net).
  
  Be sure to remember the name of the service instance and the Bluemix organization and space you're in.
  
2. Refresh the packages in your namespace. The refresh automatically creates a package binding for the Weather Company Data service instance that you created.
  
  ```
  wsk package refresh
  ```
  {: pre}
  
  
  ```
  created bindings:
  Bluemix_Weather_Company_Data_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Weather Bluemix_Weather_Company_Data_Credentials-1 private
  ```
  
 
## Setting up a Weather package outside Bluemix

If you're not using OpenWhisk in Bluemix or if you want to set up your Weather Company Data service outside of Bluemix, you must manually create a package binding for your WWeather Company Data service. You need the Weather Company Data service user name, and password.

- Create a package binding that is configured for your Watson Translator service.

  ```
  wsk package bind /whisk.system/weather myWeather -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## Getting a weather forecast for a location
{: #openwhisk_catalog_weather_forecast}

The `/whisk.system/weather/forecast` action returns a weather forecast for a location by calling an API from The Weather Company. The parameters are as follows:

- `username`: Username for The Weather Company Data for IBM Bluemix that is entitled to invoke the forecast API.
- `password`: Password for The Weather Company Data for IBM Bluemix that is entitled to invoke the forecast API.
- `latitude`: The latitude coordinate of the location.
- `longitude`: The longitude coordinate of the location.
- `timePeriod`: Time period for the forecast. Valid options are:
  - `10day` - (default) Returns a daily 10-day forecast
  - `48hour` - Returns an hourly 2-day forecast
  - `current` - Returns the current weather conditions
  - `timeseries` - Returns both the current observations and up to 24 hours of past observations, from the current date and time.


- The following is an example of creating a package binding and then getting a 10-day forecast.1. Create a package binding with your API key.
  
  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}

- Invoke the `forecast` action in your package binding to get the weather forecast.
  
  ```
  wsk action invoke myWeather/forecast --result \
  --param latitude 43.7 \
  --param longitude -79.4
  ```
  {: pre}
  ```json
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  
