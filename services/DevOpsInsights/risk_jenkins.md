---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrating with freeform Jenkins projects

After you add {{site.data.keyword.DRA_full}} to an open toolchain and define the policies that it monitors, you can integrate it with your freeform Jenkins project. Freeform Jenkins projects are configured and administered from the Jenkins web interface. 

The IBM Cloud DevOps plugin for Jenkins integrates Jenkins projects with toolchains. A _toolchain_ is a set of tool integrations that support development, deployment, and operations tasks. The collective power of a toolchain is greater than the sum of its individual tool integrations. Open toolchains are part of the {{site.data.keyword.contdelivery_full}} service. To learn more about the {{site.data.keyword.contdelivery_short}} service, see [its documentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

After you install the IBM Cloud DevOps plugin, you can publish test results to {{site.data.keyword.DRA_short}}, add automated quality gates, and track your deployment risk. You can also send job notifications to other tools in your toolchain, such as Slack and PagerDuty. To help you track deployments, the toolchain can add deployment messages to Git commits and their related Git or JIRA issues. You can also view your deployments on the toolchain's Connections page. 

The plugin provides post-build actions and CLIs to support the integration. {{site.data.keyword.DRA_short}} aggregates and analyzes the results from unit tests, functional tests, code coverage tools, static security code scans, and dynamic security code scans to determine whether your code meets predefined policies at gates in your deployment process. If your code does not meet or exceed a policy, the deployment is halted, preventing risky changes from being released. You can use {{site.data.keyword.DRA_short}} as a safety net for your continuous delivery environment, a way to implement and improve quality standards over time, and a data visualization tool to help you understand your project's health.

## Prerequisites
{: #jenkins_prerequisites}

You must have access to a server that is running a Jenkins project.

## Creating a toolchain
{: #jenkins_create}

Before you can integrate {{site.data.keyword.DRA_short}} with a Jenkins project, you must create a toolchain. 

1. To create a toolchain, go to the [Create a Toolchain page](https://console.ng.bluemix.net/devops/create) and follow the instructions on that page. 

2. After you create the toolchain, add {{site.data.keyword.DRA_short}} to it. For instructions, see the [{{site.data.keyword.DRA_short}} documentation](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

## Installing the plugin
{: #jenkins_install}

First, install the plugin on your Jenkins server. Open the server interface, and then:

1. Click **Manage Jenkins**.
2. Click **Manage Plugins**. 
3. Click the **Available** tab
4. Filter for `IBM Cloud DevOps`. 
5. Select IBM Cloud DevOps.
6. Click **Download now and install after restart**. 

The plugin is available after the server restarts.  

## Configuring Jenkins jobs for the Deployment Risk dashboard
{: #jenkins_configure}

After the plugin is installed, you can integrate {{site.data.keyword.DRA_short}} into your Jenkins project. 

Follow these steps to use Deployment Risk's gates and dashboard with your project.

1. Open the configuration of any jobs that you have, such as build, test, or deployment.

2. Add a post-build action for the corresponding type:

   * For build jobs, use **Publish build information to IBM Cloud DevOps**.
   
   * For test jobs, use **Publish test result to IBM Cloud DevOps**.
   
   * For deployment jobs, use **Publish deployment information to IBM Cloud DevOps**.
   
3. Complete the required fields. These will vary depending on job type. 

   * From the **Credentials** list, select your {{site.data.keyword.Bluemix_notm}} ID and password. If they are not saved in Jenkins, click **Add** to add and save them. Test your connection with {{site.data.keyword.Bluemix_notm}} by clicking **Test Connection**.
   
   * In the **Build Job Name** field, specify your build job's name exactly as it is in Jenkins. If the build occurs with the test job, leave this field empty. If the build job occurs outside of Jenkins, select the **Builds are being done outside of Jenkins** check box and specify the build number and build URL.
   
   * For the environment, if the tests are running in build stage, select only the build environment. If the tests are running in the deployment stage, select the deploy environment and specify the environment name. Two values are supported: `STAGING` and `PRODUCTION`.
   
   * For the **Result File Location** field, specify the result file's location. If the test doesn't generate a result file, leave this field empty. The plugin uploads a default result file that is based on the status of current test job.

   These images show example configurations:
   
   ![Upload Build Information](images/Upload-Build-Info.png "Publish Build Information to DRA")
   _Publish build information_
   
   ![Upload Test Result](images/Upload-Test-Result.png "Publish Test Result to DRA")
   _Publish test result_
   
   ![Upload Deployment Information](images/Upload-Deployment-Info.png "Publish Deployment Information to DRA")
   _Publish deployment information_

4. If you want to use {{site.data.keyword.DRA_short}} policy gates to control a downstream deployment job, add a post-build action, **IBM Cloud DevOps Gate**. Choose a policy and specify the scope of the test results. To allow the policy gates to prevent downstream deployments, select the **Fail the build based on the policy rules** check box. The following image shows an example configuration:

    ![DevOps Insights Gate](images/DRA-Gate.png "DevOps Insights Gate")

5. Run your Jenkins Build job.

6. View the Deployment Risk dashboard by going to [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops), selecting your toolchain, and clicking **DevOps Insights**.

The Deployment Risk dashboard relies on the presence of a gate after a staging deployment job. If you want to use the dashboard, make sure that you have a gate after you deploy to the staging environment, but before you deploy to a production environment.
    
## Configuring notifications
{: #jenkins_notifications}

You can configure your Jenkins jobs to send notifications to tools like Slack or PagerDuty by following the instructions in the [Bluemix Docs](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).