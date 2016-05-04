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

*Last updated: 06 April 2016*

Use {{site.data.keyword.weatherfull}} to incorporate weather data from
The Weather Company (TWC) into your {{site.data.keyword.Bluemix}} applications.
{:shortdesc}

The following instructions guide you through the process of creating an application,
binding the application to the Insights for Weather service, and retrieving the
service credentials to interact with the [REST APIs](https://twcservice.{APPDomain}/rest-api/).

### Create an application
{: #create_an_app}

For demonstration purposes, you create an application by using the Liberty for Java
runtime, but the following general process can be applied to other runtimes.

1. If you don't have an existing application, in the dashboard, click **CREATE APP**.
2. When you are asked to choose your app template, click **WEB**.
3. When you are asked to choose a starter, click **Liberty for Java**.
4. Click **Continue**.
5. In the **App Name** field, enter the name of your app.
6. Click **Finish**. Wait for your application to provision.

### Add the Insights for Weather service
{: #add_insights_for_weather_service}

Follow these steps to add the Insights for Weather service to your app.
1. Open the **Catalog** menu.
2. From the **Data & Analytics** section, click the **Insights for Weather** tile.
3. In the **App** drop-down list, select your app.
4. Click **USE**.
5. When prompted, click **Restage** to restart your application.

### Retrieve Insights for Weather credentials
{: #retrieve_weather_credentials}

When you bind your application to Insights for Weather, you are provisioning a
service instance with unique credentials. These credentials are stored in your
application's `VCAP_SERVICES` and are essential to support the interaction between services.

1. Navigate to your application overview page.
2. Go to the **Environment Variables** section. The `VCAP_SERVICES` information for each of your services is displayed.
3. Note the username and password values from the Insights for Weather service.
To try the [REST APIs](https://twcservice.{APPDomain}/rest-api/){:new_window},
you must enter these credentials when you are prompted to login.
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

# rellinks
## samples
* [Insights for Weather demo](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## api
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## compatible runtimes {:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## general
* [About Insights for Weather](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [Adding a service to your application](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [End-to-end development](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Pricing Sheet](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}