---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# About {{site.data.keyword.weather_short}}
{: #about_weather}

*Last updated: 01 July 2016*
{: .last-updated}

Use {{site.data.keyword.weatherfull}} to incorporate weather data from
The Weather Company (TWC) into your {{site.data.keyword.Bluemix}} applications.
{:shortdesc}

You can add weather observations and forecasts to your {{site.data.keyword.Bluemix_notm}}
application and display the weather data for an area that is specified by a
geolocation by using the [REST APIs](https://twcservice.{APPDomain}/rest-api/){:new_window}.
The Weather Company is the most comprehensive provider of historical and forecast
weather data. Data for all forms of weather, including precipitation, barometric pressure,
wind, and thunderstorms, is captured.

You can use the REST APIs to retrieve the following information:

* An hourly weather forecast for the next 48 hours that starts from the current time for a specified geolocation.
* A daily forecast for each of the next 3, 5, 7, or 10 days starting from the current day that includes forecasts for the daytime and nighttime segments for a specified geolocation. This forecast includes the forecast narrative text string of up to 256 characters with appropriate units of measure for the location and in the language requested.
* A daily forecast for each of the next 3, 5, 7, or 10 days starting from the current day, which breaks each daily forecast into morning, afternoon, evening, and overnight segments.
* The current observed weather data for a specified geolocation. This weather data includes temperature, precipitation, wind direction and speed, humidity, barometric pressure, dew point, visibility, and ultraviolet (UV) radiation.
* The observed weather data for a specified geolocation up to and including the previous 24 hours. This data is sourced from physical observation stations.
* Government-issued weather alerts, including weather watches, warnings, statements, and advisories issued by the National Weather Service (US), Environment Canada, and MeteoAlarm (Europe).
* Almanac services that provide historical daily or monthly weather data sourced from National Weather Service observations stations from a time period spanning 10 to 30 years or more.
* Location mapping services that provide the ability to look up a location name or geocode (latitude and longitude) to retrieve a set of locations that match your request.

You can [download a set of icons](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} to use in your app.

## Pricing model
{: #pricing_models}

The pricing model is based on the number of calls per minute to the REST
APIs. The client is charged monthly. The Free and Base plans allow you
to make a maximum of 10 API calls per minute. The Standard and Premium plans
allow you to make 150 and 375 API calls per minute respectively. Each plan has
a maximum number of API calls allowed.

You can test the weather data in your applications
for any geographic area, forecast type, or time series observations with only a
restriction on number of calls. The Free, Base, Standard, and Premium plans can be purchased
without a contract. The Free plan allows your app to make 10,000 calls. The
remaining plans allow your app to make 150,000, 2 million,
or 5 million API calls per month respectively.

Multiple paid plans can also be purchased for each service instance that is
deployed during the billing period. If your app uses more than 10,000 calls,
you need a contract with IBM for ongoing provision of services.

When your app reaches the limit of API calls per minute that it is allowed to
make based on the plan that you selected, the next API call that is made will
not succeed until your app is allowed to request more API calls.

For example, if you are using the Standard plan, your app *can* make 500 API calls
in a minute even though it exceeds the limit of the plan (150 calls per minute),
but the next API call won't be allowed until 5 minutes later. Therefore, a
user might notice a delay in the refresh of weather data in your app.
You must ensure that you develop your app to handle these limits and not request
bursts of API calls. Instead, you can monitor the API call usage of your app.
You can verify whether your app reaches the limit of its plan by checking the
number of items that are returned by the API call.

When your app reaches the limit of API calls per month that it is allowed to make
based on the plan that you selected, the next API calls are charged at an overage
rate of $1.70 per 10,000 API calls.

## Feedback and support
{: #feedback_support}

If you have technical questions about creating an app with {{site.data.keyword.weather_short}},
post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window}
and tag your question with **ibm-bluemix** and **weather**.

If you experience any issues with this service, use the [IBM developerWorks Answers forum](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}.
Include the **bluemix** and **weather** tags to allow IBM to support you better.

If you have questions about migrating your app from Insights for Weather to {{site.data.keyword.weather_short}}, 
contact us at [IBM developerWorks](http://www.ibm.com/developerworks){:new_window}.

For information about troubleshooting problems with Bluemix, see [Troubleshooting](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
For details about searching for information and asking questions through forums, and about contacting support, see [Getting customer support](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.