{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with Insights for Twitter {: #insights_twitter_overview}

*Last updated: 13 May 2016*

Use {{site.data.keyword.twitterfull}} to incorporate Twitter content from the Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} or [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} streams into your {{site.data.keyword.Bluemix}} applications.
{:shortdesc}

To get started using {{site.data.keyword.twittershort}}, first create your Bluemix web application with a runtime like Liberty for Java, then add the {{site.data.keyword.twittershort}} service to your app. When the {{site.data.keyword.twittershort}} service is bound to your app, the service instance is provisioned with unique credentials. Your app uses these credentials with REST APIs to search and consume Twitter content.  Follow these steps to retrieve the credentials from VCAP_SERVICES and integrate the service instance with your app.

1. Navigate to your application overview page.
2. Go to the **Environment Variables** section. The `VCAP_SERVICES` information for each of your services is displayed.
3. Note the username and password values from the {{site.data.keyword.twittershort}} service. In order to test operations in the REST API reference documentation, you will need to enter these credentials. For example, your `VCAP_SERVICES` will look similar to the following snippet:

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

<!--
## Adding Insights for Twitter to your application {: #adding_twitter}

The following instructions guide you through the process of creating an application, binding the application to the {{site.data.keyword.twittershort}} service, and retrieving the service credentials to interact with REST API operations in the provided API reference documentation.

### Create an application
For demonstration purposes, you'll create an application using the Liberty for Java&trade;  runtime, but the general process described below can be applied to other runtimes. If you don't have an existing application, click **CREATE AN APP** in the dashboard. When asked to confirm the type of app, click **WEB**.

1. Open the **Catalog** menu.
2. From the **Runtimes** section, click **Liberty for Java**.
3. Click **Create**.
4. In the **App Name** field, specify the name of your app.
5. Click **Finish**. Wait for your application to provision.

### Add the Insights for Twitter service
Follow these steps to add the {{site.data.keyword.twittershort}} service to your app.

1. Open the **Catalog** menu.
2. From the **Data & Analytics** section, click the {{site.data.keyword.twittershort}} tile.
3. In the **App** field, select the name of your app.
4. Click **Create**.
5. When prompted, click **Restage** to restart your application.
-->

<!-- 
The following video demonstrates the use of API operations from our API reference documentation and cURL examples entered from the command line. 

[//]: # <iframe width="420" height="315" src="https://www.youtube.com/embed/LZKVn496XJc" frameborder="0" allowfullscreen></iframe>

[//]: # To watch the video in a larger format, go to: [https://youtu.be/LZKVn496XJc](https://youtu.be/LZKVn496XJc){: new.window}
-->

# rellinks
## samples
* [Interactive decahose search demo](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: Tutorial and source code for decahose search demo](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analyzing "American Sniper" box office data (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## api
* [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## compatible runtimes {:id="buildpacks"}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## general
* [What's new in {{site.data.keyword.Bluemix_notm}} Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Adding a service to your application](../reqnsi.html){: new_window}
* [End-to-end development](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Pricing Sheet](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

