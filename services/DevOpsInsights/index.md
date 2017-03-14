---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.DRA_short}} (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} applies developer, team, and deployment analytics to your busiest DevOps projects. Use it to learn how compliant your team is with DevOps and developer practices, to manage risk in your codebase, and to automatically enforce quality standards in continuous delivery projects.
{:shortdesc}

{{site.data.keyword.DRA_short}} comprises several groups of capabilities:

   * Developer Insights provides a comprehensive way to explore your project’s development maturity. You can identify files with high error proneness and get a compliance view of the project against developer practices.

   * Team Dynamics uses social coding analysis to help you learn how your team collaborates and understand how it can work better.

   * Deployment Risk is like a continuous delivery safety net. It analyzes the results from unit tests, functional tests, application scans, and code coverage tools at specified gates in your deployment process and prevents risky changes from being released.

   * Delivery Insights shows deployment statistics, metrics, and other information about your IBM UrbanCode Deploy installation. For example, it can show charts of deployment duration, successes, and failures, all sorted by logically grouped environments. See [Integrating DevOps Insights with IBM UrbanCode Deploy](uc_insights_overview.html).

{{site.data.keyword.DRA_short}} is an integration in the Bluemix toolchain catalog. For more information about toolchains, see [Working with toolchains](/docs/services/ContinuousDelivery/toolchains_working.html).

To use {{site.data.keyword.DRA_short}}, you must add it to a toolchain. Many toolchain templates already include {{site.data.keyword.DRA_short}}. Be sure to also [add it to your {{site.data.keyword.Bluemix_notm}} org as a service](/docs/services/reqnsi.html) so that you can see information about {{site.data.keyword.DRA_short}} and access some of the toolchain templates that include it from your {{site.data.keyword.Bluemix_notm}} dashboard.  

## Adding {{site.data.keyword.DRA_short}} to a toolchain
{: #catalog}

{{site.data.keyword.DRA_short}} is part of {{site.data.keyword.contdelivery_short}}. You can add {{site.data.keyword.DRA_short}} to any toolchain by selecting it from the tool integration catalog.

{{site.data.keyword.DRA_short}} is also part of many toolchain templates. If you create a toolchain from a template that includes {{site.data.keyword.DRA_short}}, skip to [Using Insights](#using).

To add {{site.data.keyword.DRA_short}} to a toolchain:

1. Click **Add a Tool**.

2. Click **{{site.data.keyword.DRA_short}}**.

3. Click **Create Integration**.

{{site.data.keyword.DRA_short}} is now available on your toolchain's Overview page.

**Important**: When you first add {{site.data.keyword.DRA_short}} to a toolchain, it does not gather data by default. You must enable data collection from the **Settings** menu before you can fully use {{site.data.keyword.DRA_short}}.

If you create a toolchain from a template that includes {{site.data.keyword.DRA_short}}, data collection is enabled by default. 

## Using {{site.data.keyword.DRA_short}}
{: #using}

If your toolchain includes GitHub, GitLab, or JIRA, {{site.data.keyword.DRA_short}} automatically provides you with information about your codebase and team after some initial data gathering and analysis. If your toolchain does not include any of those integrations, add one of them and then follow these steps: 

1. From your toolchain's Overview page, click **{{site.data.keyword.DRA_short}}**.

2. From the left navigation, click **Team Dynamics** or **Developer Insights** and then choose a data category. 

3. Explore your project's data by viewing the dashboards in the data category. If you want to know more about a graph or what you might do with its information, click **Information** or **Guidance**. 

After you explore Team Dynamics and Developer Insights, [configure Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html) to help you enforce code quality. Deployment Risk is compatible with both the {{site.data.keyword.contdelivery_short}} pipeline and Jenkins.   

# Related Links
{: #rellinks notoc}

## Tutorials and Samples
{: #samples notoc}

* [Using analytics to advise on the likelihood of successful deployments](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window} ![External link icon, link opens in a new window](images/launch--glyph.svg)

## Related Links
{: #general notoc}

* [Getting started with toolchains](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window} ![External link icon, link opens in a new window](images/launch--glyph.svg)
* [Getting started with Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window} ![External link icon, link opens in a new window](images/launch--glyph.svg)
* [IBM Bluemix Pricing Sheet](https://new-console.ng.bluemix.net/pricing/){:new_window} ![External link icon, link opens in a new window](images/launch--glyph.svg)
