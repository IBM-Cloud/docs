---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.DRA_short}} (Experimental)
{: #gettingstarted}

Use {{site.data.keyword.DRA_full}} to identify risks to your builds and deployments.
{:shortdesc}

{{site.data.keyword.DRA_short}} aggregates and analyzes the results from unit tests, functional tests, and code coverage tools to determine whether your code meets predefined policies at specified gates in your deployment process. If your code does not meet or exceed a policy, the deployment is halted, preventing risky changes from being released. You can use {{site.data.keyword.DRA_short}} as a safety net for your continuous delivery environment, a way to implement and improve quality standards over time, and a data visualization tool to help you understand your project's health.

{{site.data.keyword.DRA_short}} is an experimental offering and is provided as-is for development and experimentation purposes only. To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

{: #catalog}
To access the {{site.data.keyword.DRA_short}} UI, complete the following steps from an existing toolchain:

1. Click the **Add a Tool** button.

2. Click **{{site.data.keyword.DRA_short}}**.

3. Click **Create Integration**.

4. Click **{{site.data.keyword.DRA_short}}**.

5. Complete your setup with the remaining tasks:

	1. [Configure your {{site.data.keyword.deliverypipeline}} integration](/docs/services/DevOpsInsights/pipeline_integration.html).
	2. Run the pipeline and [review the {{site.data.keyword.deliverypipeline}} dashboards](/docs/services/DevOpsInsights/pipeline_decision_reports.html).
	3. [Define policies](/docs/services/DevOpsInsights/create_criteria.html) for {{site.data.keyword.DRA_short}} to manage.
	4. Run the pipeline again to verify that your project passes your policies.


# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Using analytics to advise on the likelihood of successful deployments](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window} ![External link icon, link opens in a new window](images/launch--glyph.svg)

## Related Links
{: #general}

* [Getting started with toolchains](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window} ![External link icon, link opens in a new window](images/launch--glyph.svg)
* [Getting started with Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window} ![External link icon, link opens in a new window](images/launch--glyph.svg)
* [IBM Bluemix Pricing Sheet](https://new-console.ng.bluemix.net/pricing/){:new_window} ![External link icon, link opens in a new window](images/launch--glyph.svg)
