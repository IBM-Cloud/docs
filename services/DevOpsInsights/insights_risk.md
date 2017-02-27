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

# Deployment Risk (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_short}} provides a wealth of information about your deployments, particularly risk. You can use it to automate quality protection in your delivery pipeline by using policy gates. 
{:shortdesc}

After you open {{site.data.keyword.DRA_short}} from your toolchain, click **Deployment Risk**. From there, you can get a high-level overview of the applications in your staging and production environments and drill down to understand code coverage, test performance, and security reports. You can also see an overview of only your builds by clicking **Build Verification**. The dashboards are automatically populated with the most recent information from your pipelines' {{site.data.keyword.DRA_short}} tests.  

## Configuration 

For Deployment Risk to analyze your deployments accurately, you must define staging and production stages in your delivery pipeline. 

1. On the staging stage, set the `LOGICAL_ENV_NAME` property to `STAGING`. 

2. On the production stage, set the `LOGICAL_ENV_NAME` property to `PRODUCTION`. 

For more information, see [Configure your {{site.data.keyword.deliverypipeline}} integration](/docs/services/DevOpsInsights/pipeline_integration.html).

## Gates and policies

Deployment Risk shows gate policy evaluation as part of its dashboard reports. 

Policies control the gates in your delivery pipeline. If your code does not meet or exceed a policy that is enacted at a particular gate, the deployment is halted to prevent risky changes from being released.

For more information about defining policies, see [Defining policies](/docs/services/DevOpsInsights/create_criteria.html). For more information about creating gates in your pipelines, see [the pipeline integration documentation](/docs/services/DevOpsInsights/create_criteria.html).
