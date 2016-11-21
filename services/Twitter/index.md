---

copyright:
  years: 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Getting started with Insights for Twitter {: #insights_twitter_overview}

Use {{site.data.keyword.twitterfull}} to incorporate Twitter content from the Twitter [Decahose](http://support.gnip.com/gnip2.0/){: new_window} or [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} streams into your {{site.data.keyword.Bluemix}} applications.
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

# rellinks
{: #rellinks}
## samples
{: #samples}
* [Interactive decahose search demo](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: Tutorial and source code for decahose search demo](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analyzing "American Sniper" box office data (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## api
{: #api}
* [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## compatible runtimes
{: #buildpacks}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## general
{: #general}
* [What's new in {{site.data.keyword.Bluemix_notm}} Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Adding a service to your application](../reqnsi.html){: new_window}
* [End-to-end development](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Pricing Sheet](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

