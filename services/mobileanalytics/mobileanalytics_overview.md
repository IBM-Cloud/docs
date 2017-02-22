---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# About {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}

{: shortdesc}
The {{site.data.keyword.mobileanalytics_full}} service provides key application usage and performance insights for mobile application developers and application owners. By using {{site.data.keyword.mobileanalytics_short}} application owners and developers can understand what is happening on the user side, and they can use this insight to build better applications that are hyper-relevant to users and that stand out in the veritable sea of mobile applications. 

{: #overview}  
The service includes the {{site.data.keyword.mobileanalytics_short}} Console where developers and application owners can monitor mobile application performance, see usage statistics, and search device logs.  {{site.data.keyword.mobileanalytics_short}}  provides client SDKs for iOS 8+ (Swift only) and Android 4+.

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

With the {{site.data.keyword.mobileanalytics_short}} service you can:
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>Gain immediate insight</dt>
		<dd>See performance and usage metrics in real time.</dd>
	<dt>Implement in minutes</dt>
		<dd>Create a service instance in {{site.data.keyword.Bluemix}}, add the SDK to your project, paste two lines of code into your application and you are ready to collect dozens of pre-defined metrics.</dd>
	<dt>Collect any data you want</dt>
		<dd>Instrument apps with custom events, discover how users are interacting with your app, track purchases, and monitor app activity.  
</dd>
<dt>See metrics for all of your applications at-a-glance</dt>
	<dd>The {{site.data.keyword.mobileanalytics_short}} console offers <!-- both --> ready-made <!--and custom--> charts, without the need to write queries.</dd>
<dt>Focus on what is important to you</dt>
	<dd>Filter metrics by time, adapter, application, application version, OS, OS version, or device model.</dd>
<dt>Rapidly discover issues</dt>
	<dd>Monitor crash status. Set alert triggers on critical metrics and route alerts to any REST endpoint. </dd>
<dt>Troubleshoot to root cause</dt>
	<dd>Use custom logging in your application and automatically upload the logs and search them from the console. Drill down on crash events to see stack traces. </dd>
</dl>
 

## Using metrics and events
{: #usingmetrics}

With **pre-defined metrics** you can answer questions like:

* How many new users do I have?  
* How many people are actively using my application?  
* How frequently are people using my application? 
* What time of day are people using my application?  
* What device models do my users prefer? 
* When should I deprecate support for legacy operating systems? 
* Which applications are experiencing performance issues?  

By adding your own **custom events** you can answer questions like: 

* What features are used most and least?  
* Where are users entering and leaving my app?  
* What activities are users viewing most?  
* Are users completing workflows in the app (for example, conversion funnels)?   

Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics service on demand. Developers and administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that is gathered by the client SDK.

## Data visualization
{: data-visualization notoc}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. <!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.--> In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. 

## {{site.data.keyword.mobileanalytics_short}} frequently asked questions 
{: #faq}

<dl>
	<dt>What is {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} is a service that provides real time and historical insight into how your mobile applicaitons are performing and being used. Using {{site.data.keyword.mobileanalytics_short}}, application developers and application owners can make data driven decisions by monitoring trends in active users, sessions, mobile platforms, and application crashes. You can also set alerts on selected metrics that, once triggered, sends messages to any REST endpoint, including a push service or your internal messaging services.</dd>
	<dt>What can I do with {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}?</dt>
		<dd>As a Mobile Application Product Manager, you can see how many people use your application (user metrics) and when they are using it (session metrics). This information is presented as a time series and updated in real time so you can see the effect of changes you make to your application. You can filter to see specific application versions or operating systems to make deprecation and prioritization decisions. </dd>
		<dd>As a Mobile Application Marketer, you can use user and session metrics to monitor engagement, manage churn, and evaluate the effectiveness of mobile application marketing efforts by observing changes over time and correlating to your event dates.</dd>
		<dd>As a Mobile Application Developer, you can use crash metrics to discover and resolve mobile application performance issues before they frustrate users and damage the reputation of the application. You can monitor both crash count and crash rate from the analytics console, and you can prioritize crashes affecting the most users. You can set alerts to send notifications or take automated actions when crashes exceed a given threshold, and you can troubleshoot by drilling down on crash instances to see device logs and application stack traces.</dd>
	<dt>Do I need data analyst skills to use Mobile Analytics?</dt>
		<dd>No, {{site.data.keyword.mobileanalytics_short}} offers a ready-to-use analytics console for business stakeholders and application developers. No query skills are required.</dd>
	<dt>Can I perform custom queries on my analytics data?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} does not allow custom queries, but there is consideration for this feature for the future.</dd>
	<dt>How do I connect my application to {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>[Download our open-source SDK for iOS or Android](install-client-sdk.html), or use the {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/) for other platforms. </dd>
	<dt>In what Bluemix regions is {{site.data.keyword.mobileanalytics_short}} available?</dt>
		<dd>Currently, Mobile Analytics is available in the United States - South and the United Kingdom. Availability in other regions is planned, but the timeframe is not yet determined.</dd>
	<dt>How much does this service cost?</dt>
		<dd>The first 100 million events that are collected each month are free, and thereafter, events cost $1 per million events.</dd>
	<dt>What is an event?</dt>
		<dd>Currently reported events include application session start, application session end (including application crash), alert notifications, and log entries.</dd>
	<dt>How can I estimate how much the service will cost per month?</dt>
		<dd>Because pricing depends on the number of events that are sent to the service per client account, estimating pricing means estimating events.  
<p>
The price you are charged is the sum of events from all applications that you have connected to {{site.data.keyword.mobileanalytics_short}}. For a given application, the number of events depends on the degree of instrumentation that you have implemented within the application, the number of users, and how active the users are.   
</p>
<p>
Use this formula to estimate usage:
events per month per app = (users per day)(sessions per user per day)(days per month)(events per session)
</p>
<p>
Events per session can vary widely from 2 to several hundred, depending on what network calls, custom analytics, log captures, and alert definitions the developer has configured into the application.
</p>
	<dt>How long is my analytics data kept?</dt>
		<dd>Data is kept for at least 30 days.</dd>
	<dt>How long does it take for data to display in the {{site.data.keyword.mobileanalytics_short}} console?</dt>
		<dd>Data in the {{site.data.keyword.mobileanalytics_short}} console is near-real-time, meaning that the data displays within seconds of the actual events.</dd>
	<dt>What is the difference between {{site.data.keyword.mobileanalytics_full}} and the mobile analytics found in MobileFirst Platform Foundation?</dt>
		<dd>User and session are very similar in these two consoles, but analytics that come with MobileFirst Platform Foundation contains additional metrics and settings that allow clients to manage their own analytics cluster on-premises. Also, the MobileFirst Platform Foundation analytics console breaks out metrics for adapters and adapter procedures, whereas in the {{site.data.keyword.mobileanalytics_short}} service, these metrics are integrated into network request charts and tables.</dd>
	<dt>I am using MobileFirst Platform Foundation on premises to develop my apps, but I don't want to host my own analytics cluster. Can I use {{site.data.keyword.mobileanalytics_full}} instead?</dt>
		<dd>Yes. You have a couple of options: If you are using MobileFirst Platform Foundation 7.x or 8.0 and your apps are instrumented with MobileFirst Platform SDKs, you can configure your MobileFirst server to report analtyics data to {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}. Read the [Configuring Mobile Analytics and Mobile Foundation Bluemix services ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/){: new_window} blog post for details. Alternatively, you can instrument your apps using the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} SDK and report directly to the {{site.data.keyword.mobileanalytics_short}} service.</dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# Related Links
{: #rellinks notoc}

## SDK
{: #sdk notoc}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window} 
* [iOS SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}

