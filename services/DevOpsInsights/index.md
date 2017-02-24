---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.DRA_short}} (Experimental)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} brings code, team, and continuous delivery analytics to bear on your busiest DevOps projects.  
{:shortdesc}

{{site.data.keyword.DRA_short}} is an end-to-end analytics solution that you can use to learn how compliant your team is with DevOps practices. It gathers developer, test, build, and deploy insights in one place so that you can view them and then take appropriate actions. DevOps Insights reduces risk by highlighting defect likelihood and stops problem deployments before they happen.

It comprises three groups of capabilities:

_Developer Insights_ gives you a comprehensive way to explore your project’s development risk. You can identify files with high error proneness and get a compliance view of the project against DevOps best practices.

_Team Dynamics_ employs social coding analysis to identify the level of interaction between team members and helps you fix unproductive practices.

_Deployment Risk_ is like a safety net for your continuous delivery pipeline. It analyzes the results from unit tests, functional tests, application scans, and code coverage tools at specified gates in your deployment process and prevents risky changes from being released. It also offers data visualizations and analysis to help you understand your project's health at a glance.

_Note_: Developer Insights and Team Dynamics are only available to IBM employees and a limited number of external parties at this time. 

You can add {{site.data.keyword.DRA_short}} to any Continous Delivery toolchain that uses the {{site.data.keyword.deliverypipeline}}. {{site.data.keyword.DRA_short}} is also part of many toolchain templates. 

{: #catalog}
To add {{site.data.keyword.DRA_short}} to an existing toolchain, complete all of the following steps. Proceed to step 5 if you created a toolchain from a template that includes {{site.data.keyword.DRA_short}}.

1. Click the **Add a Tool** button.

2. Click **{{site.data.keyword.DRA_short}}**.

3. Click **Create Integration**.

4. Click the **{{site.data.keyword.DRA_short}}** tile on the toolchain Overview page.

5. Complete your setup with the remaining tasks:

	1. [Configure your {{site.data.keyword.deliverypipeline}} integration](/docs/services/DevOpsInsights/pipeline_integration.html).
	2. Run the pipeline and review the [Developer Insights](/docs/services/DevOpsInsights/insights_developer.html), [Team Dynamics](/docs/services/DevOpsInsights/insights_team.html), and [Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html) dashboards.
	3. [Define policies](/docs/services/DevOpsInsights/create_criteria.html) for {{site.data.keyword.DRA_short}} to manage.
	4. Run the pipeline again to verify that your project passes your policies.

_Note_: IBM internal organizations, as well as a limited number of other organizations, may configure Jenkins projects to integrate with {{site.data.keyword.DRA_short}}. For more information, [see Integrating DevOps Insights with Jenkins](/docs/services/DevOpsInsights/jenkins_integration.html).

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
