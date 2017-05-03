---

 

copyright:

  years: 2015, 2017

lastupdated: "2017-05-03" 

---


{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# What's new in {{site.data.keyword.Bluemix_notm}}

Stay up-to-date with the new features and services that are available in {{site.data.keyword.Bluemix}}, so that you get the most out of your {{site.data.keyword.Bluemix_notm}} experience. The updates are organized into these categories: [{{site.data.keyword.Bluemix_notm}} platform](index.html#platform_category), [{{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated](index.html#dedicatedandlocal), [Compute](index.html#compute_category), and [Services](index.html#services_category).
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}} platform
{: #platform_category}

### Identity and access management
New as of: 01 May 2017

With the latest updates and improvements, {{site.data.keyword.Bluemix_notm}} account owners or administrators can now use a new unified access control UI to take advantage of the following capabilities:
 * Manage users' fine-grained access to Kubernetes services and other services as they adopt the new access control features
 * Assign service policies and Cloud Foundry roles to users within their organizations

Additionally, {{site.data.keyword.Bluemix_notm}} platform users can create, delete, and list API keys associated with their user IDs. And platform users can use those API keys to authenticate when using APIs or CLIs.

Lastly, we’ve enhanced our unified user management capability to ensure that in a linked IaaS-PaaS account, users are managed in a unified way with no need to add users separately in the SoftLayer Customer Portal or the {{site.data.keyword.Bluemix_notm}} console.

For more information about the recent update, check out the [Introducing Identity & Access Management](https://www.ibm.com/blogs/bluemix/2017/05/introducing-identity-access-management/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") blog post.

### Navigation design changes for {{site.data.keyword.Bluemix_notm}} docs
New as of: 13 April 2017

With this navigation update, we think you'll understand how content is organized throughout our docs better, and will be able to find relevant content more efficiently. With fewer nested layers of content, you won't have to dig around to find the documentation you need to be successful with {{site.data.keyword.Bluemix_notm}}.

### {{site.data.keyword.Bluemix_notm}} Cloud Foundry upgrade to new Diego architecture
New as of: 03 February 2017

{{site.data.keyword.Bluemix_notm}} Cloud Foundry has been upgraded for all public environments making Diego the defaultdeployment target, so all new apps that are pushed are deployed to a Diego cell. For more information about this improvement of the Cloud Foundry platform for {{site.data.keyword.Bluemix_notm}}, see [{{site.data.keyword.Bluemix_notm}} Cloud Foundry: Diego is live](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-cloud-foundry-diego-live/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").


## {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated
{: #dedicatedandlocal}

### April updates for the administration console
{: #apriladminconsole}
New as of: 2 May 2017

With the latest updates and improvements from April, you can use the following new features:

 * Newly designed status app for {{site.data.keyword.Bluemix_notm}} Dedicated and Local environments. You can quickly search by component name or date of posting. You can also switch between the component status posts view and the notifications specific to your environment. See the [New {{site.data.keyword.Bluemix_notm}} Status Page](https://www.ibm.com/blogs/bluemix/2017/05/new-bluemix-status-page/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") blog post for more information.
 * Service usage data for select services from the Resource Usage tile. See [Service usage details](/docs/hybrid/index.html#servicesresourceusage) for more information about what services are supported and what you can expect from the new view.

### March updates for the administration console
{: #mar17adminconsole}
New as of: 31 March 2017

With the latest updates and improvements from March, you can use the following new features:

* A redesigned and improved System Status page is available to preview. The improvements include:
 * Viewing the status of multiple environments that are owned by the same {{site.data.keyword.Bluemix_notm}} account.
 * Displaying IaaS status and long-term events.
 * Event filtering by service or runtime.
 * Viewing the historical data of an event.
 
We welcome your comments and feedback on the redesigned status page. To preview and test the latest status improvements, access the new System Status page by using the following example URL and enter your domain details -- https://console._your-domain_/status/v2. Contact your customer support manager to send us your feedback. You can also request a conference call to discuss the details with a screen sharing session.   
* Usability improvements to the navigation on the landing page, and side navigation, that include maintenance updates and notification subscriptions.
* Performance improvements to speed up the Catalog Management page.

### February updates for the administration console
{: #feb17adminconsole}
New as of: 24 February 2017

With the latest updates and improvements from February, you can use the following new feature:

* Subscription-based threshold alerts can be set to notify you when organizations are approaching their allocated capacity. 

### January updates for the administration console
{: #jan17adminconsole}
New as of: 27 January 2017

With the latest updates and improvements from January, you can use the following new features:

* Improvements to the System Status page to display the current status for the specific services that you are using in    {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated environments. 
* You can display Diego Cell resource usage. The usage displayed includes CPU, Memory, and Disk resources. 
* When adding a user to your {{site.data.keyword.Bluemix_notm}} account, you can add the user to multiple organizations at the same time. If you use a Lightweight Directory Access Protocol (LDAP) directory, you can add a user or a group of users to multiple organizations. 
* You can add a user to your {{site.data.keyword.Bluemix_notm}} account even if you do not know their email address by using an LDAP directory.  

## Compute
{: #compute_category}

### Latest updates for buildpacks

Visit the following pages for a cumulative list of the latest updates:

* [Latest Updates to the SDK for Nodejs buildpack](/docs/runtimes/nodejs/updates.html#latest_updates)
* [Latest Updates to the Liberty buildpack](/docs/runtimes/liberty/updates.html#latest_updates)
* [Latest Updates to the ASP.NET Core buildpack](/docs/runtimes/dotnet/updates.html#latest_updates)
* [Latest updates to the IBM XPages for {{site.data.keyword.Bluemix_notm}} buildpack](/docs/starters/xpages/index.html#updates)

### New Liberty for Java buildpack v3.9
New as of: 27 April 2017

The Liberty buildpack v3.9 provides new monthly Liberty runtime version and contains other improvements. The default Liberty runtime version was updated to include the PI77770, PI77605, IFPI77438 and IFPI79275 iFixes. The monthly Liberty runtime version was updated to the  [2017.3.0.0](https://developer.ibm.com/wasdev/blog/2017/03/14/beta-websphere-liberty-tools-march-2017/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") release. Memory Calculation was moved from staging to the start process, allowing for easier heap memory changes with the restart of an application. The buildpack also provides updated versions of the Auto-Scaling service agent, and Extreme Scale Client. See the [latest updates](/docs/runtimes/liberty/updates.html) documentation for additional information.

### New Liberty for Java buildpack v3.8
New as of: 14 March 2017

The Liberty buildpack v3.8 provides new default and monthly Liberty runtime versions and contains other improvements. The default Liberty runtime version was updated to the [17.0.0.1](http://www-01.ibm.com/support/docview.wss?uid=swg24043339){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") release and to include the PI75512 iFix. The monthly Liberty runtime version was updated to the [2017.2.0.0](https://developer.ibm.com/wasdev/blog/2017/02/17/beta-websphere-liberty-tools-february-2017/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") release. The IBM JRE versions 8 and 7.1 were updated to SR4 FP1. In addition, the auto-configuration supports the Monitoring and Analytics service. Applications that are using the Free plan can no longer use the log capability. The auto-configuration support was also extended to work with [ibm-websphere-extreme-scale IBM Container](https://console.ng.bluemix.net/docs/images/docker_image_extreme_scale/ibm-websphere-extreme-scale_starter.html). The auto-configuration support for [Cloudant NoSQL Database](https://console.ng.bluemix.net/docs/services/Cloudant/index.html) provides the option of using the Cloudant Java Library instead of org.ektorp. The buildpack also provides updated versions of the Auto-Scaling service agent, Management Client Liberty Connector (RMU), and Application Management. For more information, see the [latest updates](https://console.ng.bluemix.net/docs/runtimes/liberty/updates.html) documentation.

## Services
{: #services_category}

### {{site.data.keyword.sparks}} updates: Apache Spark 2.1 is supported now
New as of: 21 April 2017

{{site.data.keyword.sparkl}} is introducing the support for Apache Spark 2.1 to create algorithms that harness insights from complex data. Apache Spark 2.1 will help significantly around structured streaming with added support for event time watermarks and Kafka 0.10. Apache Spark 2.1 also focused on increasing stability and usability in Spark SQL, SparkR and the MLlib modules. For more details on Spark 2.1, see [Spark Release 2.1.0](http://spark.apache.org/releases/spark-release-2-1-0.html).

We are happy to answer any questions related to {{site.data.keyword.sparkl}} or the newer version of Apache Spark 2.1 and are reachable at sparksrv@us.ibm.com. 

### {{site.data.keyword.macm_long}} is being deprecated
New as of: 18 April 2017

As of March 30th, 2017, {{site.data.keyword.macm_long}} service tile will be removed from the {{site.data.keyword.Bluemix_notm}} Catalog and you will no longer be able to provision new MACM instances. However, existing instances will continue to be supported. The End of Support Date is 30 March 2018. Please delete your {{site.data.keyword.macm_short}} (MACM) service instances before the End of Support Date. We encourage users to migrate to the IBM Watson Content Hub. Watson Content Hub is available on IBM Marketplace and provides users with a 30-day free trial. IBM Watson Content Hub provides similar functionality to MACM with added new capabilities such as asset management, cognitive tagging using IBM Watson services, and included content delivery network (CDN) to ensure an optimal experience for your customers. IBM offers service engagments to migrate content from MACM to Watson Content Hub.

### {{site.data.keyword.streaminganalyticsfull}} service updates: Develop Streams applications in your Python development environment
New as of: 13 April 2017

In the past, you had to install a local version of IBM Streams to develop Python applications. That’s no longer the case. Now you can develop applications with Python in your favorite  development environment or in a Jupyter interactive notebook.

You can use the STREAMING_ANALYTICS_SERVICE context to submit a Python application to the {{site.data.keyword.streaminganalyticsshort}} service. The {{site.data.keyword.streaminganalyticsshort}} service requires Python 3.5.

Check out the sample stream-processing Python applications in notebooks on the [community page of IBM Data Science Experience](http://datascience.ibm.com){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon"). 

### {{site.data.keyword.sparkl}} updates: Notebook support now in Data Science Experience
New as of: 11 April 2017

Your new platform to work with notebooks and Spark is Data Science Experience. Sign up to [Data Science Experience](http://datascience.ibm.com/), and start creating notebooks and sharing your expertise with other data scientists.

If you worked with notebooks in {{site.data.keyword.sparks}}, you can migrate your notebooks to Data Science Experience. For more information, see the [Migrating notebooks documentation](/docs/services/AnalyticsforApacheSpark/index-gentopic2.html#migration_to_dsx).

### {{site.data.keyword.DRA_full}} Beta service is now generally available
New as of: 17 March 2017

{{site.data.keyword.DRA_full}} is a new cloud-based monitoring service for IBM UrbanCode Deploy. {{site.data.keyword.DRA_short}}, which is part of IBM Cloud DevOps Insights, aggregates metrics information from one or more IBM UrbanCode Deploy installations into a manageable, customizable report. Your reports can show data about application and deployment successes and failures over many filter conditions.

{{site.data.keyword.DRA_short}} aggregates your IBM UrbanCode Deploy environments into logical environments so that you can see information about related environments in one set of charts. If you have several production environments for several apps, you can group all of the environments into one logical environment and combine metrics for all of the environments into one production environment dashboard. Mapping happens by search string, so you can group environments in any way that makes sense for your IBM UrbanCode Deploy servers.

To join the beta and set up {{site.data.keyword.DRA_short}} for your system, add the {{site.data.keyword.DRA_short}} service and then configure {{site.data.keyword.DRA_short}} for your IBM UrbanCode Deploy servers. For instructions, see 
[Integrating {{site.data.keyword.DRA_short}} with IBM UrbanCode Deploy](https://console.ng.bluemix.net/docs/services/DevOpsInsights/uc_insights_overview.html){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

### {{site.data.keyword.SecureGateway}} dashboard and client updates
New as of: 17 March 2017

The {{site.data.keyword.SecureGateway}} service is updated to version 1.7.0. This release includes three new plan levels for the {{site.data.keyword.SecureGateway}} service, which are Essentials, Professional, and Enterprise. New features include the consolidation of controls on the dashboard user interface, the ability to set gateways and destinations to active or inactive, and dedicated cloud IPs for Enterprise customers. Additionally, this release delivers a number of optimizations and critical fixes to improve the stability and performance of connections. Download the latest client to take advantage of all fixes and features. For more information, see [Getting started with the {{site.data.keyword.SecureGateway}}](https://console.ng.bluemix.net/docs/services/SecureGateway/secure_gateway.html){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

### {{site.data.keyword.product-insights_full}} is now generally available
New as of: 13 March 2017

{{site.data.keyword.HybridConnect_short}} is now available as a GA service through, and it helps IT administrators easily connect IBM products to the cloud and create a product inventory that they can use to manage their active products across the enterprise. Once software is connected to 
{{site.data.keyword.HybridConnect_short}}, then it will send back frequent usage metrics to the user dashboard that allows the administrator (or capacity planner) to know how they are using that product. Now organizations can know how they are utilizing their middleware at a glance from a single dashboard view.

The dashboard allows IT operations staff to identify when they are under or over using their software and optimize it to achieve a more efficient result. {{site.data.keyword.HybridConnect_short}} also helps the administrator identify other {{site.data.keyword.Bluemix_notm}} services that can connect to a product instance and advise them on how it can improve their current ROI.

What’s new since the experimental refresh on 21 February 2017:

* Product Insights Gateway (http proxy) to route data securely and verify call home data
* New getting started guidance
* Updates tab shows the latest product/instance version
* Usage metrics at group and product level

To learn more about {{site.data.keyword.HybridConnect_short}}, see [IBM Marketplace](https://www.ibm.com/us-en/marketplace/product-insights){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") or the [Technical Community](https://developer.ibm.com/product-insights/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon"). Further details can also be found in the release announcement [IBM Cloud Product Insights: Open for Business](https://developer.ibm.com/product-insights/2017/03/08/product-insights-open-business/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon"). IBM Cloud Product Insights supports IBM WebSphere Application Server, IBM WebSphere Liberty, IBM MQ, IBM Integration Bus (IIB), IBM Operational Decision Manager (ODM) and ODM on Cloud.

### {{site.data.keyword.evtmgt_full}}: Ride the storm!
New as of: 6 March 2016

Restore service and resolve operational incidents fast! {{site.data.keyword.evtmgt_short}} empowers your DevOps and Operations teams to correlate disparate sources of events into actionable incident views, synchronize teams, and automate incident resolution. The service sets you on course to achieve efficient and reliable operational health, service quality, and continuous improvement.

Start experimenting now by visiting the [Catalog](https://console.ng.bluemix.net/catalog/labs/?category=devops){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").


### {{site.data.keyword.iot_short}} changes to application status API for applications
New as of: 2 March 2017

{{site.data.keyword.iot_short_notm}} will be making changes to application status messages published to the application monitor topic.

Currently subscribers to the application status API immediately receive Connect and Disconnect messages for currently and recently connected applications, as well as updates when applications connect and disconnect.

After this update, subscribers will still immediately receive Connect messages for currently connected applications. However, Disconnect messages are only sent at the time of disconnection; they are not available when making a new subscription. If an application that you want to monitor is not connected at the time of the subscription then no messages will be received for that application until it reconnects. See the [Changes to Application status API for applications}(https://developer.ibm.com/iotplatform/2017/01/20/changes-to-application-status-api-for-applications/){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon"). blog post for more information. 


### {{site.data.keyword.uccr_full}} experimental service is now generally available
New as of: 03 February 2017

{{site.data.keyword.uccr_full}} for {{site.data.keyword.Bluemix_notm}} is an enterprise-scale release management solution designed to support both cloud native and on-premises deployment tools. With {{site.data.keyword.uccr_short}}, you can increase the cadence of your software deployments and decrease risks. {{site.data.keyword.uccr_short}} works seamlessly with IBM UrbanCode Deploy to automate software deployment. 

{{site.data.keyword.uccr_short}} provides the following key features:

 * Manage multiple applications with a single deployment plan. Orchestrate multi-application deployments. Dynamically assign application versions and environments.
 * Manage project and application dependencies. Ensure all prerequisites are met for critical tasks. Use delay-type tasks to define milestones for critical tasks.
 * Release execution, monitoring and control. Task status is always available. Deployment status alerts you when deployments fall behind schedule.
 * Integration capabilities. Integrate with your on-prem UrbanCode products. Run IBM UrbanCode Deploy applications with {{site.data.keyword.uccr_short}} tasks. Import IBM UrbanCode Release deployment plans.
 * Organization and team-based security model
 
For more information, see [Getting started with {{site.data.keyword.uccr_short}} (Experimental)](https://console.ng.bluemix.net/docs/services/UCCR/index.html){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

### {{site.data.keyword.mobileanalytics_full}} is now generally available
New as of: 12 January 2017

{{site.data.keyword.mobileanalytics_short}} is now available as a GA service. By using this service, developers, app owners, product managers, or anyone else in your organization can gain valuable insight into how your app is performing and how it is being used. This kind of information is the key to building better apps that are hyper-relevant to users and that stand out in the veritable sea of mobile apps that are available in the marketplace or within your organization.

For more information about the {{site.data.keyword.mobileanalytics_short}} service, refer to the [Getting started with {{site.data.keyword.mobileanalytics_short}}](/docs/services/mobileanalytics/index.html) documentation or the [{{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} Now Generally Available](https://www.ibm.com/blogs/bluemix/2017/01/mobile-analytics-generally-available/){: new_window} blog post.
