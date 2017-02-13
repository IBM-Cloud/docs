---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-19"

---

# Creating mobile apps from the {{site.data.keyword.mobilefirst_notm}} Services Starter boilerplate
{: #try_mobile}

You can use each of the {{site.data.keyword.Bluemix}} Mobile services independently. You can also use them together, with the {{site.data.keyword.mobilefirstbp}} Starter boilerplate, to get the most benefit.

To get started, use the {{site.data.keyword.mobilefirstbp}} Starter to create your app. The boilerplate enables you to complete the following actions:

* Create a Node.js runtime with a template application. You can use this application to provide server-side functions, such as RESTful APIs and static files. <!-- You can read more about operating this application in the Developing Mobile Backend section.-->
* Provision an instance of each of the {{site.data.keyword.Bluemix_notm}} Mobile services and bind the service to the Node.js application.

<!--
<img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> {{site.data.keyword.mobilefirstbp}} Starter boilerplate
-->

After you use the {{site.data.keyword.mobilefirstbp}} Starter boilerplate to create your app, you can either get Hello Bluemix samples for each of the services or start instrumenting your existing app to use {{site.data.keyword.Bluemix_notm}} services.


## Services overview
{: #services-overview}
You can either use all of the {{site.data.keyword.Bluemix_notm}} Mobile services together by using {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter boilerplate or you can use individual services from the {{site.data.keyword.Bluemix_notm}} catalog. The following diagram outlines the components of {{site.data.keyword.Bluemix_notm}} Mobile services.

![{{site.data.keyword.Bluemix_notm}} mobile services architecture](images/bms_architecture.jpg)

Figure 1: {{site.data.keyword.Bluemix_notm}} Mobile services architecture

<table summary="This table describes {{site.data.keyword.Bluemix_notm}} Mobile services">
<caption>Table 1. {{site.data.keyword.Bluemix_notm}} and enterprise systems</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>Enterprise systems</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js runtime icon"><b>Node.js</b> <br/> A Node.js runtime that hosts a template app is provided as part of the {{site.data.keyword.mobilefirstbp}} Starter boilerplate. You can use the template application to provide server-side functions, such as RESTful APIs and static files. <br/>For example, you might extend the Node.js application for custom logic processing or to connect with REST APIs in your company's existing infrastructure. Each app that you create on {{site.data.keyword.Bluemix_notm}} has a unique app ID. Your mobile app uses this ID with the SDK to access the services that are associated with that application. The app ID is used by the platform as the context for common functions, such as metering and logging.
<!--You can read more about operating this application in the "Developing Mobile Backend" section.--></td>
<td valign="top"><b>Information providers</b> <br/>You can use a Node.js runtime that is hosted on {{site.data.keyword.Bluemix_notm}} to connect to any kind of information provider:
<ul>
	<li>Enterprise backend</li>
	<li>Database </li>
	<li>Another hosted 3rd party service</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/authentication_icon.png" alt="{{site.data.keyword.amashort}} service icon"> <b>{{site.data.keyword.amashort}}</b><br/>Use the {{site.data.keyword.amafull}}  service to protect Node.js and Java for Liberty applications that are hosted on {{site.data.keyword.Bluemix_notm}}. By instrumenting your mobile app with the {{site.data.keyword.amashort}} SDK, you can require users to log in to access to Node.js or {{site.data.keyword.Bluemix_notm}} Mobile services. <!-- In addition to security capabilities, {{site.data.keyword.amashort}} also gathers analytics data, so that you can monitor your mobile application performance and collect client logs and usage statistics.--> </td>
<td valign="top"><b>User identity providers</b> <br/>You can use the following identity providers: <ul><li>Facebook</li><li>Google</li><li> Custom </li></ul></td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} service icon"> <b>{{site.data.keyword.mobilepushshort}}</b><br/>The {{site.data.keyword.mobilepushfull}} service provides a unified platform to send and manage push notifications targeted to Mobile (iOS & Android) platforms, and Web browser applications. This service manages the mapping of your application users to their devices, device platform, and browsers, and handles dispatching push notifications to subscribers. With this service, you can send broadcasts, unicasts (based on userID, deviceID), and tags (or topics) based on push notifications to your customers.</td>
<td valign="top"><b>Push service providers</b><ul><li>Apple Push Notifications Service</li><li>Firebase Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant service icon"><b>Cloudant NoSQLDB</b><br/> Cloudant is a NoSQL database as a service (DBaaS). It's built from the ground up to scale globally, run non-stop, and handle a wide variety of data types like JSON, full-text, and geospatial. </td>
<td>Cloudant.com</td>
</tr>
</table>
