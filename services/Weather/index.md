---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with {{site.data.keyword.weather_short}}
{: #insights_weather_overview}

Use {{site.data.keyword.weatherfull}} to incorporate weather data from
The Weather Company (TWC) into your {{site.data.keyword.Bluemix}} applications.
{:shortdesc}

**Attention:** Currently, the {{site.data.keyword.weather_short}} service **may not** be purchased
or used in the following countries or regions: Afghanistan, Armenia, Azerbaijan,
Bahrain, Bangladesh, Bhutan, Brunei, Cambodia, China, Cyprus, Georgia,
Indonesia, Iran, Iraq, Japan, Jordan, Kazakhstan, Kuwait, Kyrgyzstan, Laos,
Lebanon, Malaysia, Maldives, Mongolia, Myanmar, Nepal, Oman, Pakistan, Philippines,
Qatar, Russia, Saudi Arabia, Singapore, South Korea, Sri Lanka, Syria,
Tajikistan, Timor-Leste, Turkey, Turkmenistan, United Arab Emirates,
Uzbekistan, Vietnam, Yemen. This list is updated when additional information is available.

If you have an existing application that uses the
[Insights for Weather service](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window},
your app will continue to work without any modifications for 90 days after the introduction of
{{site.data.keyword.weather_short}}. To take advantage of the newly added APIs
and the improved pricing model, you can migrate your application to the new service.

Before you begin, create a {{site.data.keyword.Bluemix_notm}} web app in the dashboard
with a runtime such as Liberty for Java. Wait for your app to provision,
and then add the {{site.data.keyword.weather_short}} service to your app.

When you bind your app to {{site.data.keyword.weather_short}}, you are provisioning a
service instance with unique credentials. Your app uses these credentials with
the [REST APIs](https://twcservice.{APPDomain}/rest-api/){:new_window} to retrieve weather data.

Follow these steps to retrieve the service credentials from `VCAP_SERVICES`
and integrate the service instance with your app.

1. Navigate to your application overview page.
2. Go to the **Environment Variables** section. The `VCAP_SERVICES` information for each of your services is displayed.
3. Note the user name and password values from the {{site.data.keyword.weather_short}} service.
To try the [REST APIs](https://twcservice.{APPDomain}/rest-api/){:new_window},
you must enter these credentials when you are prompted to log in.
Your `VCAP_SERVICES` looks similar to the following example:

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**Note:** Each region is independent. You cannot use service credentials
that are provisioned to you in one region to authenticate to a service in another region.
Failure to enter proper credentials results in an *Unauthorized* message in the response body.

# rellinks
{: #rellinks}
## samples
{: #samples}
* [{{site.data.keyword.weather_short}} demo app](http://weather-company-data-demo.{APPDomain}){: new_window}
* [{{site.data.keyword.weather_short}} Deep Dive video](https://youtu.be/pZHXIibziUo){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [{{site.data.keyword.Bluemix_notm}} + Weather sample app](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Bare Metal, NYC Taxi Data, and Insights for Weather (YouTube tutorial)](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

## api
{: #api}
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## compatible runtimes
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## general
{: #general}
* [Adding a service to your application](/docs/services/reqnsi.html){: new_window}
* [End-to-end development](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Pricing Sheet](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}