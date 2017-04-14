---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Getting started with {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} is powered by {{site.data.keyword.streamsshort}}, an advanced analytic platform that you can use to ingest, analyze, and correlate information as it arrives from different types of data sources in real time. When you create an instance of the {{site.data.keyword.streaminganalyticsshort}} service, you get your own instance of {{site.data.keyword.streamsshort}} running in the {{site.data.keyword.Bluemix_short}} cloud, ready to run your {{site.data.keyword.streamsshort}} applications.
{:shortdesc}

Get started with {{site.data.keyword.streaminganalyticsshort}} right away by running the [starter applications](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}.

To get started with {{site.data.keyword.streaminganalyticsshort}}, use one of the following methods to submit the application bundle (.sab file) that is associated with your SPL, Java™, Python or Scala Streams application:
* Use the **Submit Job** button in the {{site.data.keyword.streaminganalyticsshort}} console.
* Develop a {{site.data.keyword.Bluemix_short}} application and add the {{site.data.keyword.streamsshort}} application to it. Control it by using the [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220).


Use {{site.data.keyword.streaminganalyticsshort}} with other {{site.data.keyword.Bluemix_short}} services, including {{site.data.keyword.cloudant}} and {{site.data.keyword.messagehub}}. See the [Tutorials to integrate with other {{site.data.keyword.Bluemix_short}} services](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} for examples to get you up and running.

If you want to go further with your own applications, you can get a {{site.data.keyword.streamsshort}} development environment and you must get your application cloud-ready. If you don’t have an {{site.data.keyword.streamsshort}} environment, you can download the {{site.data.keyword.streamsshort}} Quick Start Edition, free-of-charge on the [{{site.data.keyword.streamsshort}} product page.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

If you are not familiar with {{site.data.keyword.streamsshort}} application development, there are resources to help you learn. For more information, see [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

If you already have an SPL application that you run on premise, you must [get your application ready for the cloud.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

**Note:** You must compile your applications in Red Hat Enterprise Linux (RHEL) 6.5 or an equivalent CentOS version, using Intel processors.

## {{site.data.keyword.streamsshort}} Python apps for {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted_py notoc}

You can now create Streams apps in a Python environment, such as IBM Data Science Experience (DSX), and submit these apps to the {{site.data.keyword.streaminganalyticsshort}} instance to be deployed in the Bluemix cloud. You no longer need to install {{site.data.keyword.streamsshort}} locally to compile and deploy a Streams Python app.

Get started by creating sample Streams Python apps using Jupyter notebooks in DSX, and submit these apps to the service instance directly from DSX. For more information, see [Developing Streams Python apps in DSX](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx).

{{site.data.keyword.streaminganalyticsshort}} also supports the deployment of Streams apps from your local Python environment. You must use the [{{site.data.keyword.streamsshort}} Python Application API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), which is included in the streamsx package, to develop your Streams Python apps locally and submit them to the service instance. To get started, follow the steps in the [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) tutorial.
