---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# About Deployment Risk

{{site.data.keyword.DRA_short}} provides a wealth of information about your deployments, particularly risk. You can use it to automate quality protection in your delivery pipeline by using policies and gates. 
{:shortdesc}

After you open {{site.data.keyword.DRA_short}} from your toolchain, click **Deployment Risk**. From there, you can get an overview of the applications in your staging and production environments and drill down to understand code coverage, test performance, and security reports. The dashboards are automatically populated with the most recent information from your pipelines' {{site.data.keyword.DRA_short}} tests.

You can use Deployment Risk to enforce quality standards in your toolchain through policies and gates. Policies comprise sets of rules; gates enforce policies. For example, you might create a "Unit Testing and Test Coverage" policy that requires builds to meet unit testing and test coverage standards. You then add a gate that refers to the policy to your continuous delivery process. Builds that do not satisfy the policy are stopped at that gate. 

## Integration information

Deployment Risk integrates with {{site.data.keyword.deliverypipeline}}, which is part of {{site.data.keyword.contdelivery_full}}, and with Jenkins projects. At a high level, the instructions for using either are similar.  

If you are using {{site.data.keyword.deliverypipeline}}, follow these steps:

1. [Create policies and rules](risk_policies.html) for {{site.data.keyword.DRA_short}} to manage.
2. [Prepare your pipeline's stages](risk_cd.html) for integration with {{site.data.keyword.DRA_short}}.
3. [Create or edit test jobs](risk_cd.html) in the pipeline that upload results to {{site.data.keyword.DRA_short}}.
4. [Add gates](risk_cd.html) to the pipeline that makes promotion decisions based on those results and your policies.
5. Run the pipeline and [view the results](results.html).

If you are using Jenkins, follow these steps:

1. [Create policies and rules](risk_policies.html) for {{site.data.keyword.DRA_short}} to manage.
2. [Install and configure the Jenkins plugin](risk_jenkins.html).
3. [Create test jobs and gates as described in the plugin instructions](risk_jenkins.html). The tests upload results to {{site.data.keyword.DRA_short}} for analysis and the gates use those results to make promotion decisions.
4. Run the project and [view the results](results.html). 

No matter how you build and deploy your code, the results are the same: the builds that meet standards will move past the Deployment Risk gates, and builds that don't meet standards are stopped. 

## Prerequisites
{: #prerequisites}

Deployment Risk requires some configuration beyond what is described in [Getting Started with {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

To use Deployment Risk, you need two things:

* An instance of {{site.data.keyword.deliverypipeline}} or a Jenkins project
* Tests that you want to use to evaluate your project