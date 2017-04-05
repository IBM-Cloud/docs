---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-4"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# About {{site.data.keyword.contdelivery_short}}    
{: #cd_about}  

With {{site.data.keyword.contdelivery_full}}, you can build, test, and deliver applications by using DevOps practices and industry-leading tools.
{:shortdesc}

The {{site.data.keyword.contdelivery_short}} service supports your DevOps workflows:

 * You can create integrated DevOps open [toolchains](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window} to enable tool integrations that support your development, deployment, and operations tasks.

  A toolchain is an integrated set of tools that you can use to collaboratively develop, build, deploy, test, and manage applications. You can create toolchains that include {{site.data.keyword.Bluemix_notm}} services, open source tools, and third-party tools, such as GitHub, PagerDuty, and Slack, that make development and operations repeatable and easier to manage.

 * Deliver continuously by using automated [pipelines](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window}.

  Automate builds, unit tests, deployments, and more. Build, test, and deploy in a repeatable way with minimal human intervention. Be ready to release into production at any time.

 * Edit and push your code from anywhere by using the [web-based IDE](/docs/services/ContinuousDelivery/web_ide.html){: new_window}.

  Create, edit, run, and debug, and complete source-control tasks in GitHub. Seemlessly move from editing your code to deploying it to production.

 * Improve quality through [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window}.

  Understand the dynamics of your team as it develops and delivers code. Learn how users interact with your application. Review data to help you manage your application's operations.


## Toolchain availability on {{site.data.keyword.Bluemix_notm}} Public compared to {{site.data.keyword.Bluemix_notm}} Dedicated
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} Public is an open-standards, cloud-based platform where you can build, run, and manage applications that are accessed by [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}. {{site.data.keyword.Bluemix_notm}} Dedicated provides the capabilities of {{site.data.keyword.Bluemix_notm}} in a dedicated SoftLayer environment that is securely connected to both the {{site.data.keyword.Bluemix_notm}} Public environment and your network. Your company's {{site.data.keyword.Bluemix_notm}} Dedicated environment might not contain the same tool integrations as the {{site.data.keyword.Bluemix_notm}} Public site.

For source-code management and issue tracking, {{site.data.keyword.Bluemix_notm}} Public generally uses github.com. {{site.data.keyword.Bluemix_notm}} Dedicated can also use github.com, but it generally uses {{site.data.keyword.ghe_short}} that is either installed by your company or managed by IBM.

{{site.data.keyword.contdelivery_short}} is available on {{site.data.keyword.Bluemix_notm}} Public and {{site.data.keyword.Bluemix_notm}} Dedicated. Toolchains differ depending on whether you use {{site.data.keyword.contdelivery_short}} on {{site.data.keyword.Bluemix_notm}} Public or {{site.data.keyword.Bluemix_notm}} Dedicated.

|Toolchains |{{site.data.keyword.Bluemix_notm}} Public	|{{site.data.keyword.Bluemix_notm}} Dedicated |
|:----------|:------------------------------|:------------------|
|Tool integrations 		|For a list of supported tool integrations, see [Configuring tool integrations](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}. 		|The tool integrations that are available depend on how {{site.data.keyword.contdelivery_short}} was set up in your environment.			|
|Creating a toolchain from a template		|Log in to [{{site.data.keyword.Bluemix_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://console.ng.bluemix.net/devops){:new_window}		|Log in to your Dedicated environment on {{site.data.keyword.Bluemix_notm}}.			|
|Creating a toolchain from an app		|The app is configured for continuous delivery from a new GitHub repo that is populated with app starter code.		|The app is configured for continuous delivery from a new GitHub or GitHub Enterprise repo that is populated with app starter code.		|  
|Delivery pipeline deployment regions		|All {{site.data.keyword.Bluemix_notm}} Public regions are available for Cloud Foundry deployment jobs. 		|The {{site.data.keyword.Bluemix_notm}} Dedicated region is available. Other Dedicated or Local regions within the same customer account might also be available depending on how {{site.data.keyword.contdelivery_short}} was set up in your specific environment.		|
|Delivery pipeline deployment jobs		|All [job types](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs) are available.		|Job types that depend on {{site.data.keyword.Bluemix_notm}} services that are not installed in the Dedicated environment might not be available.	For example, container build and deploy job types might not be available in environments that do not have the {{site.data.keyword.Bluemix_notm}} Container service.	|
{: caption="Table 1. Differences between toolchains on {{site.data.keyword.Bluemix_notm}} Dedicated and {{site.data.keyword.Bluemix_notm}} Public" caption-side="top"}


## Toolchain templates
{: #templates}

You can use a template as a starting point to [create a toolchain ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/create){: new_window}. Toolchain templates include specific sets of tool integrations that support development, deployment, and operations tasks.

**Tip**: Your company's {{site.data.keyword.Bluemix_notm}} Dedicated environment might not contain the same toolchain templates as the {{site.data.keyword.Bluemix_notm}} Public site. Toolchain templates that are available on both {{site.data.keyword.Bluemix_notm}} Public and {{site.data.keyword.Bluemix_notm}} Dedicated might contain a different set of tool integrations on {{site.data.keyword.Bluemix_notm}} Dedicated.

Some toolchain templates include tool integrations that are part of the {{site.data.keyword.contdelivery_short}} service. If an instance of that service isn't already in your organization, when you click **Create** to create the toolchain, the service is automatically added at no cost to you. For more information and terms, see the [Bluemix catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}.

The microservices toolchain templates deploy an app with Catalog and Orders APIs that are backed by a Cloudant store. As part of deploying the app, a no-cost Cloudant service instance is created. For more information and terms, see the [Bluemix catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}.

|Template |Description	|
|:----------|:------------------------------|
|[Garage Method cloud-native tutorial toolchain ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|This toolchain demonstrates the DevOps practices that are featured in the Garage Method. The toolchain is preconfigured for continuous delivery, source control, test automation, and automated monitoring and operations. It comes with a sample app that is written in Node.js Express 4, which you can further extend. 		|
|[Microservices toolchain with {{site.data.keyword.DRA_short}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|With this cloud-native toolchain, you can use a sample to create an online store that consists of three microservices: a Catalog API, an Orders API, and a UI that calls both of the APIs. The toolchain is preconfigured for continuous delivery, source control, functional testing, issue tracking, online editing, and alert notification. 		|
|[Microservices toolchain with {{site.data.keyword.DRA_short}} (v2) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|With this cloud-native toolchain, you can use a sample to create an online store that consists of three microservices: a Catalog API, an Orders API, and a UI that calls both of the APIs. The toolchain is preconfigured for continuous delivery, source control, functional testing, issue tracking, online editing, and alert notification. 		|
|[Secure container toolchain ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|With this toolchain, you can develop and deploy a secure Docker container app. By default, the toolchain uses a sample Node.js "Hello World" app, but you can link to your own GitHub repo instead. The toolchain is preconfigured for continuous delivery with Vulnerability Advisor, source control, issue tracking, and online editing. 		|
|[Simple Cloud Foundry toolchain ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|With this toolchain, you can develop and deploy a Cloud Foundry app. By default, this toolchain uses a sample Node.js "Hello world" app, but you can link to your own GitHub repo instead. The toolchain is preconfigured for continuous delivery, source control, issue tracking, and online editing. 		|
|[Simple Cloud Foundry toolchain	(v2) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|With this toolchain, you can develop and deploy a Cloud Foundry app. By default, this toolchain clones a sample Node.js "Hello world" app into an IBM hosted Git repo, which you can then modify. The toolchain is preconfigured for continuous delivery, source control, issue tracking, and online editing. 		|
|[Simple Cloud Foundry toolchain with {{site.data.keyword.DRA_short}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|With this cloud-native toolchain, you can use {{site.data.keyword.DRA_short}} to gate the deployment of a simple Cloud Foundry app. By default, this toolchain uses a sample Node.js weather app, or you can link to your own GitHub repo. 		|
|[Simple Container toolchain ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|With this toolchain, you can develop and deploy a Docker container app. By default, the toolchain uses a sample Node.js "Hello World" app, but you can link to your own GitHub repo instead. The toolchain is preconfigured for continuous delivery, source control, issue tracking, and online editing. 		|
|[Delivery Insights with IBM UrbanCode Deploy ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|With this toolchain, you can view deployment metrics from IBM UrbanCode Deploy. Enable this toolchain to communicate with IBM UrbanCode Deploy by downloading and configuring DevOps Connect from the Settings page in {{site.data.keyword.DRA_short}}. 		|
|[Deployment Risk Analytics with GitHub and Jenkins ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|With this toolchain, you can gain insights into your Jenkins process for continuous integration and delivery. You can configure the Jenkins server to send data to {{site.data.keyword.DRA_short}} when the jobs are run by Jenkins. You can also implement quality gates to block deployments based on policies. You can view results on the Deployment Risk dashboard in {{site.data.keyword.DRA_short}}. If you configure a GitHub repo to indicate the source repo that is used by Jenkins, change traceability is available.  		|
|[Developer Insights and Team Dynamics with GitHub and JIRA ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|With this toolchain, you can explore your project's development risk and use social coding analysis to understand interaction patterns between developers. You can analyze GitHub source code in conjunction with GitHub issues, JIRA issues, or both. Use Developer Insights to identify files that are highly prone to errors, and see how the project complies with DevOps practices. The social coding analysis in Team Dynamics identifies the level of interaction between team members so that the team can fix unproductive practices. 		|
|[Build your own toolchain ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|This toolchain has no preconfigured tools. If you are already familiar with toolchains, you can set up your own toolchain. 		|
{: caption="Table 2. Toolchain templates" caption-side="top"}


# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Learning Lab![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/category/courses){:new_window}

## Related Links
{: #general}

* [{{site.data.keyword.contdelivery_full}}![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_continuous_delivery/){:new_window}
* [IBM Cloud Garage Method![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method){:new_window}
