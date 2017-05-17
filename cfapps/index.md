---



copyright:

  years: 2015，2017

lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Creating Cloud Foundry apps

With {{site.data.keyword.Bluemix}}, you can create your app in the {{site.data.keyword.Bluemix_notm}} user interface. After it's created, you can decide to continue to use the UI, use the cf command line interface, or use {{site.data.keyword.jazzhub_title}} to develop, track, plan, and deploy your app.
{:shortdesc}

When you create an app in {{site.data.keyword.Bluemix_notm}}, you begin with a starter. A *starter* is a template that includes predefined services and application code that is configured with a particular buildpack. There are two types of starters: boilerplates and runtimes.

A *boilerplate* is a container for an application and its associated runtime environment and predefined services for a particular domain. For example, the Mobile Cloud boilerplate includes a Node.js runtime, as well as the Mobile Data, Mobile Application Security, and Push services. It also includes an SDK and sample applications to get started developing mobile apps that access these services.

A *runtime* is the set of resources that is used to run an application. {{site.data.keyword.Bluemix_notm}} provides runtime environments as containers for different types of applications. The runtime environments are integrated as buildpacks into {{site.data.keyword.Bluemix_notm}}, are automatically configured for use, and require little to no maintenance.

To get started creating your application, take the following steps:
  1. Go to the Dashboard in the {{site.data.keyword.Bluemix_notm}} user interface.
  2. Click **CREATE AN APP**.
  3. Click **WEB** and follow the guided experience to choose a starter, specify a name, and select how you want to code.
  4. When you are finished with the guided experience, click **VIEW APP OVERVIEW**. The Overview for your app is displayed on the Dashboard.
  5. You can add a service to your app by clicking **ADD A SERVICE OR API** on the app Overview in the {{site.data.keyword.Bluemix_notm}} user interface. Browse and select services from the catalog, or, scroll to the end of the catalog and click **{{site.data.keyword.Bluemix_notm}} Experimental Services** to browse experimental services. Or, you can use the cf command line interface. See Options for working with apps.
  6. On the app's Overview page, scroll to the "Continuous delivery" card and click **Enable**. Your app's source will be saved in a repo in Git Repos and Issue Tracking, which is hosted on Bluemix. An open toolchain that uses that repo and a delivery pipeline to develop and deploy your app is also created. For more information about the Continuous Delivery service, see <https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started>Getting started with Continuous Delivery</a>.

**Note:** If a service that you bind to an app crashes, the app might stop running or have errors. {{site.data.keyword.Bluemix_notm}} does not automatically restart the app to recover from these problems. Consider coding your app to identify and recover from outages, exceptions, and connection failures. See the Apps are not automatically restarted troubleshooting topic for more information.

## Options for working with apps

After your app is created, you have a few options for continuing to add services to your app and to build and deploy your app:

<dl><dt>cf command line interface</dt>
<dd>Use the cf command line interface to update your application, create a service instance, or bind the service to your application. You can also use the cloud-cli command line interface to create, update, and delete service offerings.</dd>
<dt>{{site.data.keyword.Bluemix_notm}} user interface</dt>
<dd>Use the {{site.data.keyword.Bluemix_notm}} user interface to build your application, including picking which services and runtimes to combine to solve your business problem.</dd>
<dt>{{site.data.keyword.contdelivery_full}}</dt>
<dd>Use {{site.data.keyword.contdelivery_short}} to automate builds, unit tests, deployments, and more. Edit and push code through the rich web based IDE. Create toolchains to enable tool integrations that support your development, deployment, and operation tasks. The Continuous Delivery service includes Delivery Pipeline, Eclipse Orion Web IDE, and Git Repos and Issue Tracking. For more information, see <https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started>Getting started with Continuous Delivery</a>
</dd>
</dl>

## Tips

Use the following tips while developing your web apps:

<dl><dt>Persistence</dt>
<dd>Do not specify any local storage for your applications. Each instance of your application, even if only one instance is running, can be restarted or moved to a different virtual machine at any time, typically for load balancing. Anything stored in local storage is erased when the application is moved or deleted. Use one of the {{site.data.keyword.Bluemix_notm}} data store services for persistence.</dd>
<dt>Resource limits</dt>
<dd>Be aware of limits on the quantities of resources that a trial account can use. The limits are as follows:
<table style="width:100%">
<caption>Table 1. {{site.data.keyword.Bluemix_notm}} resource limits for a trial account</caption>
  <th>Resource type</th>	<th>Quantity limit</th>
<tr><td>Number of services that are used across all apps</td> <td>10</td>
<tr><td>Memory used across all apps</td> <td>	2 G</td>
<tr><td>Number of routes</td> <td>500</td>
</table>
</dd></dl>
