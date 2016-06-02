---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with Insights for Weather
{: #insights_weather_overview}

*Last updated: 19 May 2016*

Use {{site.data.keyword.weatherfull}} to incorporate weather data from
The Weather Company (TWC) into your {{site.data.keyword.Bluemix}} applications.
{:shortdesc}

**Note:** The Insights for Weather service is not currently available in Japan.
 
Before you begin, create a {{site.data.keyword.Bluemix_notm}} web app in the dashboard 
with a runtime such as Liberty for Java. Wait for your app to provision, 
and then add the Insights for Weather service to your app.

When you bind your app to Insights for Weather, you are provisioning a
service instance with unique credentials. Your app uses these credentials with 
the [REST APIs](https://twcservice.{APPDomain}/rest-api/){:new_window} to retrieve weather data.

Follow these steps to retrieve the credentials from `VCAP_SERVICES` and integrate the service instance with your app.

1. Navigate to your application overview page.
2. Go to the **Environment Variables** section. The `VCAP_SERVICES` information for each of your services is displayed.
3. Note the user name and password values from the Insights for Weather service.
To try the [REST APIs](https://twcservice.{APPDomain}/rest-api/){:new_window},
you must enter these credentials when you are prompted to log in.
Your `VCAP_SERVICES` looks similar to the following example:

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

**Note:** Each region is independent. You cannot use service credentials
that are provisioned to you in one region to authenticate to a service in another region.
Failure to enter proper credentials results in an "Unauthorized" message in the response body. 

# rellinks
{: #rellinks}
## samples
{: #samples}
* [Insights for Weather demo](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

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
* [Adding a service to your application](../reqnsi.html){: new_window}
* [End-to-end development](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Pricing Sheet](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}