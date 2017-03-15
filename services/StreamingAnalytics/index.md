---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-09"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


#Getting started with {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} is powered by {{site.data.keyword.streamsshort}}, an advanced analytic platform that you can use to ingest, analyze, and correlate information as it arrives from different types of data sources in real time. When you create an instance of the {{site.data.keyword.streaminganalyticsshort}} service, you get your own instance of {{site.data.keyword.streamsshort}} running in the {{site.data.keyword.Bluemix_short}} cloud, ready to run your {{site.data.keyword.streamsshort}} applications.
{:shortdesc}

You can deploy your applications to a {{site.data.keyword.streaminganalyticsshort}} instance that is running in the {{site.data.keyword.Bluemix_short}} cloud.

You can get started with {{site.data.keyword.streaminganalyticsshort}} right away by running the [starter applications](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}. If you want to go further with your own applications, you need an {{site.data.keyword.streamsshort}} development environment and you must get your SPL cloud-ready.

To get started with {{site.data.keyword.streaminganalyticsshort}}, use one of the following methods to submit the application bundle (.sab file) that is associated with your SPL or Java™ application:
* Use the {{site.data.keyword.streaminganalyticsshort}} console.
* Develop a {{site.data.keyword.Bluemix_short}} application and add the {{site.data.keyword.streamsshort}} application to it. Control it by using the [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220). Verify that your SPL or Java application runs properly in your development environment.

**Note:** You must compile your applications in Red Hat Enterprise Linux (RHEL) 6.5 or an equivalent CentOS version, using Intel processors.

You can now use {{site.data.keyword.streaminganalyticsshort}} with other {{site.data.keyword.Bluemix_short}} services, including {{site.data.keyword.cloudant}} and {{site.data.keyword.messagehub}}. See the [Tutorials to integrate with other {{site.data.keyword.Bluemix_short}} services](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} for examples to get you up and running.

To develop an {{site.data.keyword.streamsshort}} application you must have an {{site.data.keyword.streamsshort}} development environment. If you don’t have an {{site.data.keyword.streamsshort}} environment, you can download the {{site.data.keyword.streamsshort}} Quick Start Edition, free-of-charge on the [{{site.data.keyword.streamsshort}} product page.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

If you are not familiar with {{site.data.keyword.streamsshort}} application development, there are resources to help you learn. For more information, see [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

If you already have an SPL application that you run on premise, you must [get your application ready for the cloud.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

# Related Links
{: #rellinks notoc}

## Tutorials and Samples
{: #samples notoc}
* [Introduction to {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} SDK for Node.js™ Starter Application](http://bit.ly/1iR1bzu){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} Liberty for Java™ Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [Getting your SPL application ready for the cloud](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Bluemix {{site.data.keyword.streaminganalyticsshort}} Development Guide](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [More tutorials](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## API Reference
{: #api notoc}
* [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} metrics using the {{site.data.keyword.streamsshort}} REST API](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## Compatible Runtimes
{: #buildpacks notoc}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Related Links
{: #general notoc}
* [{{site.data.keyword.streamsshort}} documentation](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}} Quick Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
