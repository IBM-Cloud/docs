---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.DRA_short}} (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} applies code, team, and continuous delivery analytics to your busiest DevOps projects.  
{:shortdesc}

{{site.data.keyword.DRA_short}} is an end-to-end analytics solution that you can use to learn how compliant your team is with DevOps practices. It gathers developer, test, build, and deployment insights in one place so that you can view them and take the appropriate actions. It reduces risk by highlighting defect likelihood and stops problem deployments before they happen.

{{site.data.keyword.DRA_short}} comprises three groups of capabilities:

   * Developer Insights provides a comprehensive way to explore your project’s development risk. You can identify files with high error proneness and get a compliance view of the project against DevOps practices.

   * Team Dynamics uses social coding analysis to help you learn how your team collaborates and understand what it can change to work better.

   * Deployment Risk is like a safety net for your continuous delivery pipeline. It analyzes the results from unit tests, functional tests, application scans, and code coverage tools at specified gates in your deployment process and prevents risky changes from being released. It also offers data visualizations and analysis that you can use to understand your project's health at a glance.

**Note:** Developer Insights and Team Dynamics are available only to IBM employees and a limited number of external parties. 

{{site.data.keyword.DRA_short}} is part of {{site.data.keyword.contdelivery_full}}. You can add {{site.data.keyword.DRA_short}} to any toolchain that uses {{site.data.keyword.deliverypipeline}} in {{site.data.keyword.contdelivery_short}}. {{site.data.keyword.DRA_short}} is also part of many toolchain templates. 

##Adding {{site.data.keyword.DRA_short}} to a toolchain
{: #catalog}

To add {{site.data.keyword.DRA_short}} to a toolchain, complete these steps. If you created a toolchain from a template that includes {{site.data.keyword.DRA_short}}, skip to step 5.

1. Click **Add a Tool**.

2. Click **{{site.data.keyword.DRA_short}}**.

3. Click **Create Integration**.

4. On the toolchain's Overview page, click **{{site.data.keyword.DRA_short}}**.

5. Complete your setup:

	1. [Configure your {{site.data.keyword.deliverypipeline}} integration](/docs/services/DevOpsInsights/pipeline_integration.html).
	2. Run the pipeline and review the [Developer Insights](/docs/services/DevOpsInsights/insights_developer.html), [Team Dynamics](/docs/services/DevOpsInsights/insights_team.html), and [Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html) dashboards.
	3. [Define policies](/docs/services/DevOpsInsights/create_criteria.html) for {{site.data.keyword.DRA_short}} to manage.
	4. Run the pipeline again to verify that your project passes your policies.

**Note:** IBM internal organizations and a limited number of other organizations can configure Jenkins projects to integrate with {{site.data.keyword.DRA_short}}. For more information, [see Integrating DevOps Insights with Jenkins](/docs/services/DevOpsInsights/jenkins_integration.html).

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
