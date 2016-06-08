---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuring tool integrations
{: #integrations}

*Last updated: 8 June 2016*

You can configure tool integrations that support development, deployment, and operations tasks while you create a toolchain, or you can add and configure tool integrations to customize an existing toolchain.  
{:shortdesc}

**Important**: This capability is experimental. Toolchains might not be stable and might change in ways that are not compatible with earlier versions. They are not recommended for use in production environments. To use toolchains, you must make a one-time [request for access](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}. Toolchains are available in the US South region only.

**Tip**: If you want to start developing with your source code, make sure that you configure the GitHub and GitHub Issues tool integrations before you configure the {{site.data.keyword.deliverypipeline}}.

## Configuring the delivery pipeline
{: #deliverypipeline}

The {{site.data.keyword.deliverypipeline}} automates the continuous deployment of your projects through sequences of stages that retrieve input and run jobs, such as builds, tests, and deployments. 

Configure the {{site.data.keyword.deliverypipeline}} to automate the continuous building, testing, and deployment of your apps: 

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Delivery Pipeline**. Depending on the template that you use, different fields might be available. Review the default field values and if needed, change those settings.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**. Then, click **Tool Integrations**. 
1. Click the add button (+).
1. In the Tool Integrations section, click **Delivery Pipeline**.
1. Specify a name for your new pipeline.
1. If you plan to use your pipeline to deploy a user interface, select the **Viewable App** check box. All of the apps that your pipeline creates are shown in the **VIEW APP** list on the toolchain's Tool Integrations page.
1. Click **Create Integration** to add the {{site.data.keyword.deliverypipeline}} to your toolchain.
1. Click the tile for {{site.data.keyword.deliverypipeline}} to view the pipeline and configure it. To learn the basics of configuring a pipeline, see [Building and deploying pipelines](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Tip**: If you want to trigger the pipeline when you push changes to your GitHub repository (repo), you must configure GitHub for your toolchain before you define the stages for your pipeline. The pipeline stages need the Git URLs for your GitHub repos. Each pipeline stage can refer to only one of the GitHub repos that is associated with your toolchain. For instructions to configure GitHub, see the [GitHub and GitHub Issues](#github) section.
  
1. Optional: If you want Sauce Labs to run tests on your app, configure the {{site.data.keyword.deliverypipeline}} to add a Sauce Labs test job. For instructions to configure the test job, see the [Configuring a Sauce Labs test job in your pipeline](#config_saucelabs) section.

### Configuring a Sauce Labs test job in your pipeline
{: #config_saucelabs}

Before you configure a Sauce Labs test job in your pipeline, you need a working pipeline that has stages to build and deploy your app, and you must configure Sauce Labs for your toolchain. For instructions to configure Sauce Labs, see the [Sauce Labs](#saucelabs) section.

Configure the {{site.data.keyword.deliverypipeline}} to add a Sauce Labs test job:

1. If you don't have a stage that deploys a test version of your app, create one.
1. In the stage, add a test job after the deploy job. By placing these jobs in the same stage, they can access the same set of environment properties.   
  ![Test job](images/toolchain_test_job.png) 

1. Configure the stage: 

  a. On the **ENVIRONMENT PROPERTIES** tab, create three properties: CF_APP_NAME, SAUCE_USERNAME, and SAUCE_ACCESS_KEY.
  
  b. Enter your Sauce Labs user name and access key. By doing so, you externalize those values so that you can use them in your tests.
  
1. Configure the deploy job. In the **Deploy Script** field, include this command: export CF_APP_NAME="$CF_APP". That command exports the app name as an environment property.
1. Configure the test job. The values in the following image are examples. The **Service Instance**, **Target**, **Organization**, and **Space** fields are populated with the Sauce Labs user name, region, org, and space that you are currently using.  
![Configure job](images/toolchain_configure_job.png)

  a. For the tester type, select **Sauce Labs**.
  
  b. For the service instance, select the Sauce Labs user name that you used when you configured Sauce Labs for your toolchain. 
  
   **Tip**: To see the user name and access key that you used when you configured Sauce Labs for your toolchain, click **Configure**. 
  
  c. In the **Test Execution Command** field, enter the commands that install the dependencies that are required by your tests and then run the tests. For example, for a hypothetical Node.js app, you might enter:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. If you want to see your test reports in the test job logs, select the **Enable Test Report** check box, and set the Test Result File Pattern to `test/*.xml`.
  
1. Click **SAVE**. Now, whenever your pipeline runs, your Sauce Labs tests run.

To learn more, see [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.

## Adding Deployment Risk Analytics
{: #dra}

Deployment Risk Analytics collects and analyzes the results from unit tests, functional tests, and code coverage tools to determine whether your code meets predefined criteria at specified gates in your deployment process. If your code does not meet or exceed the criteria, the deployment is halted, preventing risks from being released. You can use Deployment Risk Analytics as a safety net for your continuous delivery environment or as a way to implement and improve quality standards over time. 

 **Tip**: This tool integration is pre-configured. It does not require any configuration parameters and you cannot reconfigure it.
 
Add the Deployment Risk Analytics tool integration to maintain and improve the quality of your code in Bluemix by monitoring your deployments to identify risks before they are released:

1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**. Then, click **Tool Integrations**. 
1. Click the add button (+).
1. In the Tool Integrations section, click **Deployment Risk Analytics**. 
1. Click **Create Integration**.
1. Click the tile for Deployment Risk Analytics to walk through the steps to get started with this tool integration: create criteria, connect the criteria to the pipeline, and then run the pipeline. 

To learn more, see [Deployment Risk Analytics](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.

## Adding the Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

The Eclipse Orion {{site.data.keyword.webide}} is an integrated web-based environment where you can create, edit, run, debug, and complete source control tasks. You can seamlessly move from editing to running to submitting to deploying. 

 **Tip**: This tool integration is pre-configured. It does not require any configuration parameters and you cannot reconfigure it.
 
Add the Eclipse Orion {{site.data.keyword.webide}} tool integration to complete source control tasks:

1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**. Then, click **Tool Integrations**. 
1. Click the add button (+).
1. In the Tool Integrations section, click **Eclipse Orion Web IDE**. 
1. Click **Create Integration**.
1. Click the tile for the new Eclipse Orion Web IDE. Your workspace is pre-populated with your GitHub repos. The repos that are associated with your current toolchain are highlighted.

To learn more, see [Web IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}.


## Configuring GitHub and GitHub issues
{: #github}

GitHub is a web-based hosting service for Git repos. You can have both local and remote copies of your repos, which makes it easy to collaborate. 

GitHub Issues is a tracking tool that keeps your work and your plans all in one place. It is integrated with your development repo so that you can focus on important tasks.

Configure GitHub and GitHub Issues to manage your source code on the cloud:

1. If you are configuring this tool integration as you are creating the toolchain, follow these steps:

 a. In the Configurable Integrations section, click **GitHub**. If you have not authorized {{site.data.keyword.Bluemix}} to access GitHub, click **Authorize** to go to the GitHub website. If you don't have an active GitHub session, you are prompted to log in. Click **Authorize Application** to allow {{site.data.keyword.Bluemix}} to access your GitHub account. If you have an active GitHub session but you haven't entered your password recently, you might be prompted to enter your GitHub password to confirm.
 
 b. If you have an active GitHub session but you haven't entered your password recently, you might be prompted to enter your GitHub password to confirm.
   
 c. Review the default target repo locations for the GitHub repos. Those repos are cloned from the sample repos. If needed, change the names of the target repos.
 ![Default target repo locations](images/toolchain_github_config.png)
   
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**. Then, click **Tool Integrations**. 
1. Click the add button (+).
1. In the Tool Integrations section, click **GitHub**. If you have not authorized {{site.data.keyword.Bluemix}} to access GitHub, click **Authorize** to go to the GitHub website. If you don't have an active GitHub session, you are prompted to log in. Click **Authorize Application** to allow {{site.data.keyword.Bluemix}} to access your GitHub account. If you have an active GitHub session but you haven't entered your password recently, you might be prompted to enter your GitHub password to confirm.
1. If you have a GitHub repo and want to use it, type the URL for the repo and select **link** as the repository type.
1. If you want to use a new GitHub repo, type a name for the GitHub repo, type the URL for the repo that you are cloning or forking, and select the repository type: 

 a. To create an empty repo, select **new**. 
 
 b. To create a copy of a GitHub repo, select **clone**.
 
 c. To fork a GitHub repo so that you can contribute changes through pull requests, select **fork**.
 
1. If you want to use GitHub's Issues for issue tracking, select the **Enable GitHub Issues** check box.
1. Click **Create Integration**.
1. Click the tile for the GitHub repo that you want to work with to go to github.com and view the contents of the repo.
 
  **Tip**: You can use the integrated source code management tools in Eclipse Orion Web IDE to edit the GitHub repo and deploy an app from your workspace.

1. If you enabled GitHub Issues, click the tile for GitHub Issues to go to GitHub Issues.

To learn more, see [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} and [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configuring PagerDuty
{: #pagerduty}

PagerDuty integrates data from multiple monitoring systems into a single view. When a problem occurs, PagerDuty ensures that the team member who is best able to fix it at the time is notified. If the team member does not respond to the problem, escalations can be configured to route it to secondary engineers or operations managers.

Configure PagerDuty to send notifications when pipeline stage failures occur so that you can fix problems faster and reduce downtime:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **PagerDuty**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**. Then, click **Tool Integrations**. 
1. Click the add button (+).
1. In the Tool Integrations section, click **PagerDuty**
1. Type the PagerDuty site name that is associated with your PagerDuty account. If you don't have a PagerDuty account, [register for one](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Type the API access key for your PagerDuty account. For instructions to find the key, see [API Authentication](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Type the name of your PagerDuty service.
1. Type the email address for the primary PagerDuty contact.
1. Type the phone number for the primary PagerDuty contact.
1. Click **Create Integration**.
1. Click the tile for PagerDuty to go to pagerduty.com. You can view the events that are associated with the PagerDuty service that you specified when you configured this tool integration for your toolchain. 

To learn more, see [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuring Sauce Labs
{: #saucelabs}

Sauce Labs runs functional unit tests. When a Sauce Labs test suite is configured as a test job in the {{site.data.keyword.deliverypipeline}}, the test suite can run tests against your web or mobile app as part of your continuous delivery process. These tests can provide valuable flow control for your projects, acting as gates to prevent the deployment of bad code.

Configure Sauce Labs to run automated functional tests on multiple operating systems and browsers so that you can emulate the way that a user might use a website or an application:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Sauce Labs**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**. Then, click **Tool Integrations**. 
1. Click the add button (+).
1. In the Tool Integrations section, click **Sauce Labs**.
1. Type the user name that is associated with your Sauce Labs account. You can [find your user name in the welcome message at the top of your Sauce Labs account page](https://saucelabs.com/account){: new_window}.
1. Type the access key for your Sauce Labs account. You can [find the key in the lower-left corner of your Sauce Labs account page](https://saucelabs.com/account){: new_window}.
1. Click **Create Integration**.
1. Click the tile for Sauce Labs to go to saucelabs.com and view the test activity for the toolchain.

 **Tip**: If you added a Sauce Labs test job to the {{site.data.keyword.deliverypipeline}}, you can select the service instance.

To learn more, see [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configuring Slack
{: #slack}

**Important**: Notifications that are posted to public Slack channels are visible to everyone on the team. Remember that you are responsible for the content that you post.

Slack is a cloud-based, real-time messaging and notification system. Slack provides persistent chat, which is a more interactive alternative to email for team collaboration. You can communicate with your team on a dedicated channel or on a set of channels that is directly related to your work. You can also share files and images through the channels or in direct messages between two or more people. The communications in direct messages and on channels are retained so that you can search them. 

Configure Slack to receive notifications about your toolchain from the tool integrations, such as test and deployment activities:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Slack**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the **Toolchains** tab, click the toolchain to open its Tool Integrations page. Alternatively, on the app's Overview page, on the Continuous Delivery tile, click **View Toolchain**. Then, click **Tool Integrations**.
1. Click the add button (+).
1. In the Tool Integrations section, click **Slack**.
1. Type the API authentication token for your Slack account. You must use a generated full-access token to authenticate with Slack. For instructions to find the token, see [Slack authentication](https://api.slack.com/web#authentication){: new_window}.
1. Type the name of the Slack channel that you want notifications to be sent to. If the channel that you specify doesn't exist, it is created. If the channel was archived, it is reactivated.
1. Click **Create Integration**.
1. Click the tile for Slack. You can view all of the activity for your toolchain in the configured Slack channel.

To learn more, see [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
