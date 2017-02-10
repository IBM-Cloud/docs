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

# About
{: #about}

You can perform real-time analysis on data in motion as part of your {{site.data.keyword.Bluemix_short}} applications by using {{site.data.keyword.streaminganalyticsfull}}. 
{:shortdesc}

{{site.data.keyword.streaminganalyticsshort}} is powered by {{site.data.keyword.streamsshort}}, an advanced analytic platform that you can use to ingest, analyze, and correlate information as it arrives from different types of data sources in real time. When you create an instance of the {{site.data.keyword.streaminganalyticsshort}} service, you get your own instance of {{site.data.keyword.streamsshort}} running in the {{site.data.keyword.Bluemix_short}} cloud, ready to run your {{site.data.keyword.streamsshort}} applications.

New to {{site.data.keyword.streaminganalyticsshort}}? Get a [quick introduction to the service](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}. If you want to go further with your own applications, you need an {{site.data.keyword.streamsshort}} development environment and you must get your SPL cloud-ready.

The {{site.data.keyword.streaminganalyticsshort}} service provides the following capabilities that enable you to deploy, analyze, and monitor your data in the cloud:

**Interactive and programmatic use of the service:**

You can use the service interactively through the [{{site.data.keyword.streaminganalyticsshort}} console](/docs/services/StreamingAnalytics/c_streams_console.html), or programatically through the [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}.

**Deployment and monitoring of SPL and Java applications:**

{{site.data.keyword.streamsfull}} Processing Language (SPL) is a programming language that is used to create streams processing applications. You can write {{site.data.keyword.streamsshort}} applications in SPL or in Java. [Deploy and monitor these applications](/docs/services/StreamingAnalytics/t_deploytocloud.html) using {{site.data.keyword.streaminganalyticsshort}}. 

**Compatibility with {{site.data.keyword.streamsshort}} operators:**

The {{site.data.keyword.streamsshort}} operators in the [{{site.data.keyword.streamsshort}} Processing Language (SPL) standard toolkit should all be compatible](/docs/services/StreamingAnalytics/c_beta_adapters.html) with {{site.data.keyword.streaminganalyticsshort}}.

## {{site.data.keyword.streaminganalyticsfull}} responsibilities

### Client responsibilities

Client is responsible for:

* Following IBM’s initial configuring of the {{site.data.keyword.streamsshort}}, monitoring, configuring and managing the {{site.data.keyword.streamsshort}} jobs running in their instance. Client has flexibility to start and stop the instance and start and stop jobskeywordnning on the instance.
* Developing, as necessary or required, programs and applications on the service to analyze data and obtain insights from it. Client is also responsible for the quality and performance of such programs or applications developed. Programs may be developed in SPL, Java, or other supported languages by using the {{site.data.keyword.streamsshort}} Topology feature. They must be compiled using either {{site.data.keyword.streamsshort}} Developer Edition or {{site.data.keyword.streamsshort}} Quick Start Edition with the same operating system as used for {{site.data.keyword.streaminganalyticsshort}}. 
* Checking the following link periodically to be informed about a scheduled non-disruptive or disruptive downtime - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* Backing up all data, metadata, configuration files and environment parameters as per business requirements so as to ensure continuity.
* Restoring data, metadata, configuration files and environment parameters from any backup to ensure continuity, in an eventuality of failure of any type including but not limited to data center or pod failure, server failure or hard disk failure or software failures.

### IBM Responsibilities

As part of {{site.data.keyword.streaminganalyticsfull}}, IBM will:

* Provide and manage servers, storage and networking infrastructure for the Customer instance. 
* Provide an initial configuration of the {{site.data.keyword.streamsshort}} on the number of nodes selected.
* Provide and manage infrastructure for Internet facing and internal firewall for protection and isolation. 
* Monitor and manage the following components on {{site.data.keyword.streaminganalyticsfull}}:
	* Network components
	* Servers and their local storage
	* Infrastructure Operating Systems
	* {{site.data.keyword.streamsshort}} management services
	* {{site.data.keyword.streamsshort}} instances 
* Provide maintenance patches, including appropriate security patches for the infrastructure operating systems and {{site.data.keyword.streamsshort}}.
* Perform regular maintenance that should not require any system downtime (“non-disruptive” maintenance) and maintenance that may require some system downtime and restarting (“disruptive” maintenance”), will be performed at the scheduled times published at [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window} 
* Any changes to the scheduled maintenance times will be posted with appropriate notice. 
