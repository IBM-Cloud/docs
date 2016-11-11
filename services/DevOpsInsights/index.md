---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.DRA_short}} (Experimental)
{: #DRA_gettingstarted}

*Last updated: 8 November 2016*
{: .last-updated}

{{site.data.keyword.DRA_full}} allows you to maintain and improve the quality of your code in {{site.data.keyword.Bluemix_notm}} by monitoring your deployments to identify risks before they are released.
{:shortdesc}

{{site.data.keyword.DRA_short}} collects and analyzes the results from unit tests, functional tests, and code coverage tools to determine whether your code meets predefined policies at specified gates in your deployment process. If your code does not meet or exceed a policy, the deployment is halted, preventing risks from being released. You can use {{site.data.keyword.DRA_short}} as a safety net for your continuous delivery environment or as a way to implement and improve quality standards over time.

{{site.data.keyword.DRA_short}} is an experimental offering and is provided as-is for development and experimentation purposes only.  To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

{: #DRA_catalog}
To access the {{site.data.keyword.DRA_short}} UI, complete the following steps from an existing toolchain:

1. Click the **Add a Tool** button.

2. Click **{{site.data.keyword.DRA_short}}**.

3. Click **Create Integration**.

4. Click the **{{site.data.keyword.DRA_short}}** tile.

5. Complete your setup with the remaining tasks:

	1. [Configure your {{site.data.keyword.deliverypipeline}} integration](./pipeline_integration.html).
	2. Run the pipeline and [review the {{site.data.keyword.deliverypipeline}} dashboards](./pipeline_decision_reports.html).
	3. [Define policies](./create_criteria.html) for {{site.data.keyword.DRA_short}} to manage.
	4. Run the pipeline again to verify that your project passes your policies.


# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Using analytics to advise on the likelihood of successful deployments](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## Related Links
{: #general}

* [Getting started with toolchains](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Getting started with Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [IBM Bluemix Pricing Sheet](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [IBM Bluemix prerequisites](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
