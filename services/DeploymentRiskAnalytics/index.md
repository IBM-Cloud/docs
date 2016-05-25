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

*Last updated: 24 May 2016*

{{site.data.keyword.DRA_full}} allows you to maintain and improve the quality of your code in {{site.data.keyword.Bluemix_notm}} by monitoring your deployments to identify risks before they are released.
{:shortdesc}

{{site.data.keyword.DRA_short}} collects and analyzes the results from unit tests, functional tests, and code coverage tools to determine whether your code meets predefined criteria at specified gates in your deployment process. If your code does not meet or exceed the criteria, the deployment is halted, preventing risks from being released. You can use {{site.data.keyword.DRA_short}} as a safety net for your continuous delivery environment or as a way to implement and improve quality standards over time.

{{site.data.keyword.DRA_short}} is an experimental offering and is provided as-is for development and experimentation purposes only.  To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

{: #DRA_catalog}
To access the {{site.data.keyword.DRA_short}} criteria UI, complete the following steps.

1. From the DevOps category under Experimental in the {{site.data.keyword.Bluemix_notm}} catalog, click **{{site.data.keyword.DRA_short}}**.

2. Click **Create** to add the service to your {{site.data.keyword.Bluemix_notm}} organization.

3. On the {{site.data.keyword.DRA_short}} Manage tab, click **OPEN DEPLOYMENT RISK ANALYTICS DASHBOARD** to open the criteria UI

4. Complete your setup with the remaining tasks:

	1. [Define criteria](./create_criteria.html) for {{site.data.keyword.DRA_short}} to manage.
	2. Add {{site.data.keyword.DRA_short}} to a toolchain and [configure your {{site.data.keyword.deliverypipeline}}](./pipeline_integration.html).
	3. [Run your {{site.data.keyword.deliverypipeline}}](./pipeline_decision_reports.html)


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
