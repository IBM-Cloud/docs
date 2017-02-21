---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-16"

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

 * You can create integrated DevOps toolchains to enable tool integrations that support your development, deployment, and operations tasks. 
 
  A toolchain is an integrated set of tools that you can use to collaboratively develop, build, deploy, test, and manage applications. You can create toolchains that include {{site.data.keyword.Bluemix_notm}} services, open source tools, and third-party tools, such as GitHub, PagerDuty, and Slack, that make development and operations repeatable and easier to manage.
 
 * Deliver continuously by using automated pipelines. 
 
  Automate builds, unit tests, deployments, and more. Build, test, and deploy in a repeatable way with minimal human intervention. Be ready to release into production at any time.
 
 * Edit and push your code from anywhere by using the web-based IDE. 
 
  Create, edit, run, and debug, and complete source-control tasks in GitHub. Seemlessly move from editing your code to deploying it to production.
 
 * Improve quality through {{site.data.keyword.DRA_short}}. 
 
  Understand the dynamics of your team as it develops and delivers code. Learn how users interact with your application. Review data to help you manage your application's operations.
  
  
## Public compared to Dedicated
{: #public_and_dedicated}

{{site.data.keyword.contdelivery_short}} is available on {{site.data.keyword.Bluemix_notm}} Public and {{site.data.keyword.Bluemix_notm}} Dedicated. Toolchains differ depending on whether you use {{site.data.keyword.contdelivery_short}} on {{site.data.keyword.Bluemix_notm}} Public or {{site.data.keyword.Bluemix_notm}} Dedicated.

|Toolchains |{{site.data.keyword.Bluemix_notm}} Public	|{{site.data.keyword.Bluemix_notm}} Dedicated |
|:----------|:------------------------------|:------------------|
|Tool integrations 		|For a list of supported tool integrations, see [Configuring tool integrations](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}. 		|The tool integrations that are available depend on how {{site.data.keyword.contdelivery_short}} was set up in your environment.			|
|Creating a toolchain from a template		|Log in to [{{site.data.keyword.Bluemix_notm}}![External link icon](../../icons/launch-glyph.svg "External link icon")](http://console.ng.bluemix.net/devops){:new_window}		|Log in to your Dedicated environment on {{site.data.keyword.Bluemix_notm}}.			|
|Creating a toolchain from an app		|The app is configured for continuous delivery from a new GitHub repo that is populated with app starter code.		|The app is configured for continuous delivery from a new GitHub or GitHub Enterprise repo that is populated with app starter code.		|  
|Delivery pipeline deployment regions		|All {{site.data.keyword.Bluemix_notm}} Public regions are available for Cloud Foundry deployment jobs. 		|The {{site.data.keyword.Bluemix_notm}} Dedicated region is available. Other Dedicated or Local regions within the same customer account might also be available depending on how {{site.data.keyword.contdelivery_short}} was set up in your specific environment.		|
|Delivery pipeline deployment jobs		|All [job types](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs) are available.		|Job types that depend on {{site.data.keyword.Bluemix_notm}} services that are not installed in the Dedicated environment might not be available.	For example, container build and deploy job types might not be available in environments that do not have the {{site.data.keyword.Bluemix_notm}} Container service.	|
{: caption="Table 1. Differences between toolchains on {{site.data.keyword.Bluemix_notm}} Dedicated and {{site.data.keyword.Bluemix_notm}} Public" caption-side="top"}

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Create a pipeline![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_first_pipeline){:new_window}
* [Create and use your first toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create a toolchain that includes {{site.data.keyword.DRA_short}}![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_devops_insights){:new_window}
* [Create and use a microservices toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window} 
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Related Links
{: #general}

* [{{site.data.keyword.contdelivery_full}}![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_continuous_delivery/){:new_window}
* [Empty toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/toolchain_empty){:new_window}
* [Microservices toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple Cloud Foundry toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [Simple Cloud Foundry toolchain with {{site.data.keyword.DRA_short}}![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/toolchain_devops_insights){:new_window}
* [Simple container toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/toolchain_simple_container){:new_window}
* [Simple secure container toolchain![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/toolchains/toolchain_simple_secure_container){:new_window}
* [IBM Bluemix Garage Method![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method){:new_window}
