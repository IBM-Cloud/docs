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

# Understanding Deployment Risk (Experimental)
{: #gettingstarted}

{{site.data.keyword.DRA_short}} provides you with a wealth of information about your deployments, particularly risk. It also allows you to automate quality protection into your delivery pipeline through policy gates. 
{:shortdesc}

After opening {{site.data.keyword.DRA_short}} from the tile in your toolchain, click **Deployment Risk**. From there, you can get a high-level overview of applications in your staging and production environments, as well as drill down to understand code coverage, test performance, and security reports. You can also see an overview of your builds only by clicking **Build Verification**. 

The dashboards are automatically populated with the most recent information from your pipelines' {{site.data.keyword.DRA_short}} tests. Click the elements within the dashboards for more information about them.

## Configuration 

For Deployment Risk to analyze your deployments accurately, you must define staging and production stages in your delivery pipeline. Set the `LOGICAL_ENV_NAME` property in these stages to `STAGING` and `PRODUCTION` respectively. 

For more information, see [Configure your {{site.data.keyword.deliverypipeline}} integration](/docs/services/DevOpsInsights/pipeline_integration.html).

## Gates and policies

Deployment Risk shows gate policy evaluation as part of its dashboard reports. 

Policies control the gates in your continuous delivery pipeline. If your code does not meet or exceed a policy enacted at a particular gate, the deployment is halted, preventing risky changes from being released.

For more information about defining policies, see [Defining policies](/docs/services/DevOpsInsights/create_criteria.html). For more information about creating gates in your pipelines, see [the pipeline integration documentation](/docs/services/DevOpsInsights/create_criteria.html).
