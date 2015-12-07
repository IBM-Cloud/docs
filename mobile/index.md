# Creating mobile apps
{: #mobile}

With {{site.data.keyword.Bluemix_notm}} Mobile Services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications without relying on IT involvement. You can focus on building your mobile apps instead of the complexities of managing the back-end infrastructure.

<table><caption>Table 1. Bluemix Mobile Services boilerplate</caption><tr><td>
Each of the Bluemix Mobile Services can be used independently. You can also use them together to get the most benefit. To get started, use the Bluemix Mobile Services Boilerplate to create your app. This boilerplate:<ul><li>Creates a Node.js runtime with a template application. You can use this application to provide server-side functions, such as RESTful APIs and static files. You can read more about operating this application in the Developing Mobile Backend section. </li><li>
Provisions an instance of each of the Bluemix Mobile Services and binds the service to the  Node.js application. </li></ul>
</td><td> <img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> Bluemix Mobile Services Boilerplate </td></tr></table>

After you use the Bluemix Mobile Services Boilerplate to create your app, you can to either get HelloWorld samples for each of the services or start instrumenting your existing app to use Bluemix services.


## Services overview
{: #services-overview}
You can either use all of the Bluemix Mobile Services together by using Bluemix Mobile Services Boilerplate or you can use individual services from the Bluemix catalog. The following diagram outlines all the components of Bluemix Mobile Services.

![Bluemix mobile services architecture](images/bms_architecture.jpg)

<table>
<caption>Table 2. Bluemix and enterprise systems</caption>
<th>Bluemix</th>
<th>Enterprise systems</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js runtime icon"><b>Node.js</b> <br/> A Node.js runtime that hosts a template app is provided as part of the Bluemix Mobile Services boilerplate. You can use the template application to provide server-side functions, such as RESTful APIs and static files. <br/>For example, you might extend the Node.js application for custom logic processing or to connect with REST APIs in your company's existing infrastructure. Each app that you create on Bluemix has a unique app ID. Your mobile app uses this ID with the SDK to access the services that are associated with that application. The app ID is used by the platform as the context for common functions, such as metering and logging.
You can read more about operating this application in the "Developing Mobile Backend" section.</td>
<td valign="top"><b>Information providers</b> <br/>You can use a Node.js runtime that hosted on Bluemix to connect to any kind of information provider:
<ul>
<li>
Enterprise backend</li>
<li>Database </li>
<li>Another hosted 3rd party service</li></td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="Mobile Client Access service icon"> <b>Mobile Client Access</b><br/>Use the IBM Mobile Client Access for Bluemix service to protect Node.js and Java for Liberty applications that are hosted on Bluemix. By instrumenting your mobile app with the Mobile Client Access SDK, you can require users to log in to access to Node.js or Bluemix Mobile Services. In addition to security capabilities,  Mobile Client Access also gathers analytics data, so that you can monitor your mobile application performance and collect client logs and usage statistics. </td>
<td valign="top"><b>User identity providers</b> <br/>You can use the following identity providers: <ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Push Notifications service icon"> <b>Push Notifications</b><br/>IBM Push Notifications for Bluemix service provides a unified platform to send and manage mobile push notifications that are targeted to iOS and Android platforms. This service manages the mapping of your application users to their devices, device platform, and handles dispatching push notifications to the devices. With this service, you can send broadcasts, unicasts (based on userID, deviceID), and tags (or topics) based on push notifications to your mobile application users.</td>
<td valign="top"><b>Push service providers</b><ul><li>Apple Push Notifications Service</li><li>Google Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant service icon"><b>Cloudant NoSQLDB</b><br/> Cloudant is a NoSQL database as a service (DBaaS). It's built from the ground up to scale globally, run non-stop, and handle a wide variety of data types like JSON, full-text, and geospatial. </td>
<td>Cloudant.com</td>
</tr>
</table>
