---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Deploying {{site.data.keyword.streamsshort}} applications to the cloud
{: #t_deploytocloud}

You can deploy your {{site.data.keyword.streamsshort}} applications to a {{site.data.keyword.streaminganalyticsshort}} instance that is running in the {{site.data.keyword.Bluemix_short}} cloud.
{:shortdesc}

{{site.data.keyword.streamsshort}} applications are written in {{site.data.keyword.streamsshort}} Processing Language (SPL) in an {{site.data.keyword.streamsshort}} environment. {{site.data.keyword.streamsshort}} also supports several Java™ development kits that you can use to develop your applications. For more information about the Java support in {{site.data.keyword.streamsshort}}, see [Supported Java development kits for application development](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}. 
{{site.data.keyword.streaminganalyticsshort}} doesn't include an {{site.data.keyword.streamsshort}} development environment in the cloud, but you can deploy the applications that you develop locally to the cloud.

Before you begin, disable the pop-up blocker of your browser to display the Streaming Analytics console.

To deploy your {{site.data.keyword.streamsshort}} applications to the cloud:

1. Set up an {{site.data.keyword.streamsshort}} environment to develop and test your application. 

	If you don’t have an {{site.data.keyword.streamsshort}} environment, you can download the {{site.data.keyword.streamsshort}} Quick Start Edition, free-of-charge. Go to the [IBM Streams product page](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window} and click **Download the native software installation**.

2. Develop your SPL or Java application in your {{site.data.keyword.streamsshort}} environment by using Streams Studio or the command-line tools.
3. Verify that your SPL or Java application runs properly in your development environment.
4. Submit the application bundle (.sab file) that is associated with your SPL or Java application to your service instance in the cloud by using one of these methods:
	* Use the {{site.data.keyword.streaminganalyticsshort}} console to submit the application bundle.
    * Develop a {{site.data.keyword.Bluemix_short}} application and add the {{site.data.keyword.streamsshort}} application to it. Control it by using the {{site.data.keyword.streaminganalyticsshort}} REST API.

Your application is now deployed in the cloud. You can monitor your application using the {{site.data.keyword.streaminganalyticsshort}} service. You can also submit more than one SPL or Java application (.sab files) to your service instance. As many as you want.
