---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# About Insights for Weather
{: #about_weather}

*Last updated: 19 May 2016*

Use {{site.data.keyword.weatherfull}} to incorporate weather data from
The Weather Company (TWC) into your {{site.data.keyword.Bluemix}} applications.
{:shortdesc}

You can add weather observations and forecasts to your {{site.data.keyword.Bluemix_notm}} application and display the weather data
for an area that is specified by a geolocation by using the [Insights for Weather REST APIs](https://twcservice.{APPDomain}/rest-api/){:new_window}.
The Weather Company is the most comprehensive provider of historical and forecast
weather data. Data for all forms of weather, including precipitation, barometric pressure,
wind, and thunderstorms, is captured.

You can use the REST APIs to retrieve the following information:

* An hourly weather forecast for the next 24 hours that starts from the current time for a specified geolocation.
* A daily weather forecast for the next 10 days that includes forecasts for the daytime and nighttime segments for a specified geolocation. This forecast includes the forecast narrative text string of up to 256 characters with appropriate units of measure for the location and in the language requested.
* The current observed weather data for a specified geolocation. This weather data includes temperature, precipitation, wind direction and speed, humidity, barometric pressure, dew point, visibility, and ultraviolet (UV) radiation.
* The observed weather data for a specified geolocation and a specified time range. This data is sourced from physical observation stations. This API returns weather observations for current conditions and past observations up to and including the previous 24 hours.

For more information about The Weather Company's weather phrases and icons, see [Icon Code, Phrases and Images](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}.
You can also [download a set of icons](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} to use in your app.

## Pricing model
{: #pricing_models}

The pricing model is based on daily calls to the Insights for Weather APIs that
are charged to the client monthly. You can test the weather data in your applications
for any geographic area, forecast type, or time series observations with only a
restriction on number of calls. The Free, Base, and Premium plans can be purchased
without a contract. These plans allow your app to make 500, 5,000, or 50,000 API calls per day respectively.

Multiple Premium plans can also be purchased for each service instance that is
deployed during the billing period. If your app uses more than 50,000 calls per
day or over 1,000 calls per minute, you need a contract with IBM for ongoing provision of services.

When your app reaches the limit of API calls that it is allowed to make based on
the plan that you selected, the next API call that is made will not succeed
until your app is allowed to request more API calls.

For example, if you are using the Base plan, your app can make 500 API calls in a
minute even though it exceeds the limit of the plan, but the next API call won't
be allowed until 5 minutes later. Therefore, a user might notice a delay in the
refresh of weather data in your app. You must ensure that you develop your app
to handle these limits and not request bursts of API calls. Instead, you can
monitor the API call usage of your app. You can verify whether your app reaches the
limit of its plan by checking the number of items that are returned by the API call.

## Feedback and support
{: #feedback_support}

If you have technical questions about creating an app with Insights for Weather,
post your question on [Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window}
and tag your question with **bluemix** and **weather**.

If you experience any issues with this service, use the [IBM developerWorks Answers forum](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}.
Include the **insights-weather** and **bluemix** tags to allow IBM to support you better.

For information about troubleshooting problems with Bluemix, see [Troubleshooting](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
For details about searching for information and asking questions through forums, and about contacting support, see [Getting customer support](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.