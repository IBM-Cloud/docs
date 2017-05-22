---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}    

# Configuring tool integrations
{: #integrations}

You can configure tool integrations that support development, deployment, and operations tasks while you create an open toolchain, or you can add and configure tool integrations to customize an existing toolchain.  
{:shortdesc}

The tool integrations that are available to add and configure for your toolchain are different depending on whether you are using toolchains on {{site.data.keyword.Bluemix_notm}} Public or {{site.data.keyword.Bluemix_notm}} Dedicated. If you are using toolchains on {{site.data.keyword.Bluemix_notm}} Dedicated, the tool integrations that are available to you depend on how {{site.data.keyword.contdelivery_full}} was set up on your specific environment.

|Tool integration |Available on {{site.data.keyword.Bluemix_notm}} Public	|Available on {{site.data.keyword.Bluemix_notm}} Dedicated (environment dependent)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.alertnotificationshort}}		|Yes		|No		|
|Artifactory		|Yes		|No		|
|Availability Monitoring		|Yes		|No		|
|Cloud Event Management		|Yes		|No		|
|{{site.data.keyword.deliverypipeline}} 		|Yes	   	|Yes  		|
|{{site.data.keyword.DRA_short}} 		|Yes		|No			|
|Eclipse Orion {{site.data.keyword.webide}}		|Yes		|Yes			|
|{{site.data.keyword.gitrepos}}	|Yes		|No		|
|GitHub and Issues		|Yes		|Yes		|
|Dedicated {{site.data.keyword.ghe_short}} and Issues			|No		|Yes		|
|Jenkins		|Yes		|No		|
|JIRA		|Yes		|No		|
|Nexus			|Yes		|No		|
|Other Tool			|Yes		|Yes		|
|PagerDuty			|Yes		|Yes		|
|Rational Team Concert			|Yes		|No		|
|Sauce Labs		|Yes		|No		|
|Slack			|Yes		|Yes		|
|SonarQube			|Yes		|No		|
{: caption="Table 1. Tool integrations available for toolchains on {{site.data.keyword.Bluemix_notm}} Public and Dedicated" caption-side="top"}

**Tip:** If you want to start developing with your source code on {{site.data.keyword.Bluemix_notm}} Public, configure the GitHub tool integration or the {{site.data.keyword.gitrepos}} tool integration before you configure the {{site.data.keyword.deliverypipeline}}. If you want to start developing with your code on {{site.data.keyword.Bluemix_notm}} Dedicated, configure the {{site.data.keyword.ghe_short}} tool integration or the GitHub tool integration before you configure the {{site.data.keyword.deliverypipeline}}.


## Configuring Alert Notification (Experimental)
{: #alertnotification}

{{site.data.keyword.alertnotificationfull}} is a hybrid cloud-based solution that you can use to centralize and simplify your notification strategy. It works with other cloud-based and on-premises applications. Alerts are forwarded to {{site.data.keyword.alertnotificationshort}} by using a secure RESTful API.

Configure {{site.data.keyword.alertnotificationshort}} to receive notifications about issues during your DevOps process.

### Prerequisites

1. If you don't have an {{site.data.keyword.alertnotificationshort}} account, sign up for one:

 a. Open the [IBM {{site.data.keyword.alertnotificationshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/us-en/marketplace/alert-notification){: new_window} page in IBM Marketplace.

 b. Either purchase a subscription or sign up for the free 90-day trial.

1. After your {{site.data.keyword.alertnotificationshort}} account is set up, open your [My IBM Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://myibm.ibm.com/dashboard/){: new_window}.
1. Next to IBM {{site.data.keyword.alertnotificationshort}}, click **Launch**.
1. Click **Manage API Keys** and click **Create API Key**.
1. In the **Create API Key** field, type a description.
1. Click **Generate**. The new API Key information, including the name and password, is displayed. You need that information for the tool integration configuration, so keep the New API Key window open. For security purposes, you cannot retrieve the API key password later.

### Configuring Alert Notification

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **{{site.data.keyword.alertnotificationshort}}**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain**. Then, click **Overview**.  

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **{{site.data.keyword.alertnotificationshort}}**.

1. Type the URL for the {{site.data.keyword.alertnotificationshort}} API that you want to use. You can find the URL on the Manage API Keys page of the {{site.data.keyword.alertnotificationshort}} service; for example, `https://ibmnotifybm.mybluemix.net/api/alerts/v1`.
1. Type the name of the API key for {{site.data.keyword.alertnotificationshort}}. You can find the API key name in the New API Key window.
1. Type the password that {{site.data.keyword.alertnotificationshort}} generated for the API key. You can find the API key password in the New API Key window.
1. Click **Create Integration**.
1. From your toolchain, click **{{site.data.keyword.alertnotificationshort}}**.

For more information, see [IBM {{site.data.keyword.alertnotificationshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/manage/tool_alert_notification/){: new_window}.


## Configuring Artifactory
{: #artifactory}

Configure the Artifactory repository manager to store build artifacts in your Artifactory repository (repo):

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Artifactory**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain**. Then, click **Overview**.  

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Artifactory**.

1. Type the URL for the Artifactory repo that you want to open when you click the Artifactory card.
1. Select the repository type that you want to connect to.
1. If you are using an Artifactory npm registry, follow these steps:

 a. Type the email address that is associated with your registry.

 b. Type the authentication token that is associated with your registry.

 c. Type the URL for your Artifactory release repo, which is your private registry on the Artifactory server.

 d. Type the URL for the Mirror or Public registry that you use to combine multiple public and private npm registries. For example, this URL might be the URL of the virtual registry on your Artifactory server that can access both your private registry and a cache of the npm global registry.

1. If you are using an Artifactory Maven repo, follow these steps:

 a. Type the user ID that is associated with your repo.

 b. Type the password that is associated with your repo.

 c. Type the URL for your Artifactory release repo, which is your private release repo on the Artifactory server.

 d. Type the URL for your Artifactory snapshot repo, which is your private snapshot repo on the Artifactory server.

 e. Type the URL for the Mirror or Public repo that you use to combine multiple public and private Maven repos. For example, this URL might be the URL of the virtual repo on your Artifactory server that can access both your private repos and a cache of the Maven central repo.

1. Click **Create Integration**.
1. Click the card for the Artifactory repo that you want to work with. The Artifactory website opens, where you can view the contents of the repo.
1. Optional: If you are using a toolchain on {{site.data.keyword.Bluemix_notm}} Public and you want to build your app by using Artifactory with npm, configure your pipeline to add an npm build job. For instructions to configure the build job, see the [Configuring an Artifactory npm build job in your pipeline](#config_artifactory_npm) section.
1. Optional: If you are using a toolchain on {{site.data.keyword.Bluemix_notm}} Public and you want to build your app by using Artifactory with Maven, configure your pipeline to add a Maven build job. For instructions to configure the build job, see the [Configuring an Artifactory Maven build job in your pipeline](#config_artifactory_maven) section.

### Configuring an Artifactory npm build job in your pipeline
{: #config_artifactory_npm}

Before you configure an npm build job in your pipeline, you must have a working pipeline that can use your build SCM repo as input and you must configure Artifactory for your toolchain. For instructions to configure Artifactory, see the [Artifactory](#artifactory) section.

Configure {{site.data.keyword.deliverypipeline}} to add an npm build job:

1. Create a stage and set the input to the appropriate SCM repo.
1. On the stage, add a build job.
1. Configure the build job:
  ![npm build job](images/artifactory_npm_job.png)

  a. For the builder type, select **NPM Build**.

  b. If you configured multiple instances of the Artifactory tool integration, enter the name of the Artifactory tool integration that you want to configure the npm build job for.

  c. For the tool integration type, select **Artifactory**.

  d. For the build command, enter the commands to build your npm module or publish it to your registry. This example shows the commands to either build the module or publish it.
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Tip:** You can find the URL and user credentials that you used to connect to your registry in the configuration settings for the Artifactory tool integration.

  e. If your build job publishes to the Artifactory registry and the format of your node module version is `x.y.z-SNAPSHOT.w`, select the **Increment snapshot module version** check box. The build job automatically updates the module version before the job publishes to the Artifactory registry. The job selects the highest version of the module from the npm registry and the local `package.json` file, and increments the module version by using semver. The build job does not deliver the changes to the SCM repo.

1. Click **SAVE**. Whenever your pipeline runs, this build job uses the configuration information from the Artifactory tool integration to connect to your npm registry.

### Configuring an Artifactory Maven build job in your pipeline
{: #config_artifactory_maven}

Before you configure a Maven Build job in your pipeline, you need a working pipeline that can use your build SCM repo as input, and you must configure Artifactory for your toolchain. For instructions to configure Artifactory, see the [Artifactory](#artifactory) section.

Configure the {{site.data.keyword.deliverypipeline}} to add a Maven Build job:

1. Create a stage and set the input to the appropriate SCM repo.
1. On the stage, add a build job.
1. Configure the build job:
  ![Maven build job](images/artifactory_maven_job.png)

  a. For the builder type, select **Maven Build**.

  b. If you configured multiple instances of the Artifactory tool integration, enter the name of the Artifactory tool integration that you want to configure the Maven Build job for.

  c. For the tool integration type, select **Artifactory**.

  d. For the build command, enter the commands to build your Maven module or publish it to your snapshot registry. This example shows the commands to either build the module or publish it to a snapshot registry.
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Tip:** You can find the URL and user credentials that you used to connect to your registry in the configuration settings for the Artifactory tool integration.

1. Click **SAVE**. Whenever your pipeline runs, this build job uses the configuration information from the Artifactory tool integration to connect to your Maven repo.

To learn more, see [Artifactory ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_artifactory/){: new_window}.


## Adding Availability Monitoring
{: #availabilitymonitoring}

{{site.data.keyword.prf_hublong}} isolates problems, identifies patterns, and improves performance before users are affected. You can test your app from locations around the world, integrate with delivery pipelines, and gain insights on how to continuously optimize your code.

**Note:** This tool integration is preconfigured and does not require any configuration parameters. You cannot reconfigure this tool integration.

To test, monitor, and improve your app's health as you build it, add the {{site.data.keyword.prf_hubshort}} tool integration:

1. On the DevOps dashboard, on the Toolchains page, click the toolchain that you want to add {{site.data.keyword.prf_hubshort}} to. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **{{site.data.keyword.prf_hubshort}}**.

1. Click **Create Integration**.
1. Click **{{site.data.keyword.prf_hubshort}}** to open the {{site.data.keyword.prf_hubshort}} dashboard, select an app, and configure monitoring for the app.

To learn more, see [{{site.data.keyword.prf_hublong}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/manage/tool_bluemix_availability_monitoring/){: new_window}.


## Adding Cloud Event Management (Experimental)
{: #cloudeventmanagement}

{{site.data.keyword.evtmgt_full}} provides a consolidated view of problems that occur with your services, applications, and infrastructure. You can set up real-time incident management to resolve the problems more efficiently.

**Note:** This tool integration is preconfigured and does not require any configuration parameters. You cannot reconfigure it.

To help your DevOps team achieve reliable operational health, service quality, and continuous improvement goals, add Cloud Event Management to your toolchain:

1. From the DevOps dashboard, click **Toolchains**. Click the toolchain that you want to add Cloud Event Management to. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Cloud Event Management**.

1. Click **Create Integration**.
1. From your toolchain, click any of the following tool cards:

 * **Cloud Event Management** to get started with Cloud Event Management.

 * **{{site.data.keyword.alertnotificationshort}}** to create policies that determine when users receive incident notifications.

 * **Runbook Automation** to manage your catalog of runbooks in Cloud Event Management.

To learn more, see [Cloud Event Management ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/manage/tool_cloud_event_mgt/){: new_window}.


## Configuring Delivery Pipeline
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} automates the continuous deployment of your projects through sequences of stages that retrieve input and run jobs, such as builds, tests, and deployments.

Configure {{site.data.keyword.deliverypipeline}} to automate the continuous building, testing, and deployment of your apps:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **{{site.data.keyword.deliverypipeline}}**. Depending on the template that you use, different fields might be available. Review the default field values and if needed, change those settings.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **{{site.data.keyword.deliverypipeline}}**.

1. Specify a name for your new pipeline.
1. If you plan to use your pipeline to deploy a user interface, select the **Show apps in the VIEW APP menu** check box. All of the apps that your pipeline creates are shown in the **View App** list on the toolchain's Overview page.
1. Click **Create Integration** to add the {{site.data.keyword.deliverypipeline}} to your toolchain.
1. Click **{{site.data.keyword.deliverypipeline}}** to view the pipeline and configure it. To learn the basics of configuring a pipeline, see [Building and deploying pipelines](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}.

  **Tip:** If you want the pipeline to automatically run when a commit is pushed to your GitHub, {{site.data.keyword.ghe_short}}, or Git repository (repo), follow these steps:

   a. Configure GitHub, {{site.data.keyword.ghe_short}}, or {{site.data.keyword.gitrepos}} for your toolchain before you define the stages for your pipeline. The pipeline stages need the Git URLs for your repos. Each pipeline stage can refer to only one of the GitHub, {{site.data.keyword.ghe_short}}, or Git repos that are associated with your toolchain. For instructions to configure GitHub, see the [GitHub](#github) section. For instructions to configure Dedicated {{site.data.keyword.ghe_short}}, see [Getting started with {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}. For instructions to configure {{site.data.keyword.gitrepos}}, see the [{{site.data.keyword.gitrepos}}](##gitbluemix) section.

   b. Use a webhook. Without a webhook, you can run pipelines manually only. To use a webhook when you link to a GitHub or {{site.data.keyword.ghe_short}} repo, you need admin priviledges. To link to a {{site.data.keyword.gitrepos}} repo, you need Master or Owner priviledges.

1. Optional: If you are using a toolchain on {{site.data.keyword.Bluemix_notm}} Public and you want Sauce Labs to run tests on your app, configure the {{site.data.keyword.deliverypipeline}} to add a Sauce Labs test job. For instructions to configure the test job, see the [Configuring a Sauce Labs test job in your pipeline](#config_saucelabs) section.

### Configuring a Sauce Labs test job in your pipeline
{: #config_saucelabs}

Before you configure a Sauce Labs test job in your pipeline, you need a working pipeline that has stages to build and deploy your app, and you must configure Sauce Labs for your toolchain. For instructions to configure Sauce Labs, see the [Sauce Labs](#saucelabs) section.

Configure the {{site.data.keyword.deliverypipeline}} to add a Sauce Labs test job:

1. If you don't have a stage that deploys a test version of your app, create one.
1. On the stage, add a test job after the deploy job. By placing these jobs in the same stage, they can access the same set of environment properties.   
  ![Test job](images/toolchain_test_job.png)

1. Configure the stage:

  a. On the **ENVIRONMENT PROPERTIES** tab, create three properties: CF_APP_NAME, SAUCE_USERNAME, and SAUCE_ACCESS_KEY.

  b. Enter your Sauce Labs user name and access key. By doing so, you externalize those values so that you can use them in your tests.

1. Configure the deploy job. In the **Deploy Script** field, include this command: `export CF_APP_NAME="$CF_APP"`. That command exports the app name as an environment property.
1. Configure the test job. The values in the following image are examples. The **Service Instance**, **Target**, **Organization**, and **Space** fields are populated with the Sauce Labs user name, region, org, and space that you are using.  
![Configure job](images/toolchain_configure_job.png)

  a. For the tester type, select **Sauce Labs**.

  b. For the service instance, select the Sauce Labs user name that you used when you configured Sauce Labs for your toolchain.

   **Tip:** To see the user name and access key that you used when you configured Sauce Labs for your toolchain, click **Configure**.

  c. In the **Test Execution Command** field, enter the commands that install the dependencies that are required by your tests and then run the tests. For example, for a Node.js app, you might enter these commands:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```

    d. If you want to see your test reports in the test job logs, select the **Enable Test Report** check box, and set the Test Result File Pattern to `test/*.xml`.

1. Click **SAVE**. Whenever your pipeline runs, your Sauce Labs tests run.

To learn more, see [Delivery Pipeline ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_delivery_pipeline/){: new_window}.


## Adding DevOps Insights (Beta)
{: #dra}

{{site.data.keyword.DRA_full}} collects and analyzes the results from unit tests, functional tests, and code coverage tools to determine whether your code meets predefined criteria at specified gates in your deployment process. If your code does not meet or exceed the criteria, the deployment is stopped to prevent risks from being released. You can use {{site.data.keyword.DRA_short}} as a safety net for your continuous delivery environment or as a way to implement and improve quality standards.

 **Note:** This tool integration is available only on {{site.data.keyword.Bluemix_notm}} Public. It is preconfigured and does not require any configuration parameters. You cannot reconfigure this tool integration.

Add {{site.data.keyword.DRA_short}} to maintain and improve the quality of your code in {{site.data.keyword.Bluemix_notm}} by monitoring your deployments to identify risks before they are released.

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **{{site.data.keyword.DRA_short}}**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **{{site.data.keyword.DRA_short}}**.

1. Click **Create Integration**.
1. Click **{{site.data.keyword.DRA_short}}**, and then complete the getting started steps: create criteria, connect the criteria to the pipeline, and run the pipeline.

To learn more, see [{{site.data.keyword.DRA_short}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window}.


## Adding the Eclipse Orion Web IDE
{: #webide}

The Eclipse Orion {{site.data.keyword.webide}} is an integrated web-based environment where you can create, edit, run, debug, and complete source control tasks. You can seamlessly move from editing to running to submitting to deploying.

 **Note:** This tool integration is preconfigured. It does not require any configuration parameters and you cannot reconfigure it.

To complete source control tasks, add the Eclipse Orion {{site.data.keyword.webide}} tool integration:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Eclipse Orion {{site.data.keyword.webide}}**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Eclipse Orion {{site.data.keyword.webide}}**.

1. Click **Create Integration**.
1. Click **Eclipse Orion {{site.data.keyword.webide}}**. Your workspace is pre-populated with your GitHub or {{site.data.keyword.ghe_short}} repos. The repos that are associated with your current toolchain are highlighted.

To learn more, see [Editing code with the Eclipse Orion {{site.data.keyword.webide}}](/docs/services/ContinuousDelivery/web_ide.html){: new_window} and [Eclipse Orion {{site.data.keyword.webide}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_eclipse_orion_web_ide/){: new_window}.


## Configuring Git Repos and Issue Tracking
{: #gitbluemix}

The {{site.data.keyword.gitrepos}} tool integration is based on GitLab Community Edition, which is a web-based hosting service for Git repos. You can have both local and remote copies of your repos. To learn more, see [{{site.data.keyword.gitrepos}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help){:new_window}.

If you are configuring {{site.data.keyword.gitrepos}} as you are creating the toolchain, follow these steps:    

1. In the Configurable Integrations section, click **Git Repos and Issue Tracking**.
1. Review the default target locations for the Git repos. Those repos are cloned from the sample repos. If needed, change the names of the target repos.

If you have a toolchain and are adding {{site.data.keyword.gitrepos}} to it, follow these steps:    

1. On the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.
1. Click **Add a Tool**.
1. In the Tool Integrations section, click **Git Repos and Issue Tracking**.
1. Select a repository type:     

  a. To create an empty repo, for the repository type, click **New** and type a repository name.    
  b. To fork a Git repo so that you can contribute changes through merge requests, for the repository type, click **Fork**. Type the URL for the source repo.    
  c. To create a copy of a Git repo, for the repository type, click **Clone**. Type a new repo name and the URL for the source repo.     
  d. If you have a Git repo and want to use it, for the repository type, click **Existing**. Type the URL.    

1. If you want to use Issues for issue tracking, select the **Enable Issues** check box.
1. If you want to track the deployment of code changes by creating tags and comments on commits, and labels and comments on issues that are referenced by the commits, select the **Track deployment of code changes** check box. For more information, see [Track where your code is deployed with toolchains ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Click **Create Integration**.
1. Click the card for the Git repo that you want to work with. Your project overview page opens.    

**Note:** If you don't have Master or Owner privileges for the repo that you are linking to, your integration is limited because you can't use a webhook. Webhooks are required to automatically run a pipeline when a commit is pushed to the repo. Without a webhook, you must start your pipelines manually.


## Configuring GitHub and Issues
{: #github}

GitHub is a web-based hosting service for Git repos. You can have both local and remote copies of your repos, which makes it easy to collaborate.

GitHub Issues is a tracking tool that keeps your work and your plans all in one place. It is integrated with your development repo so that you can focus on important tasks.

Configure GitHub to manage your source code on the cloud:

1. If you are configuring this tool integration as you are creating the toolchain, follow these steps:

 a. In the Configurable Integrations section, click **GitHub**. If you are creating the toolchain on {{site.data.keyword.Bluemix_notm}} Public and you have not authorized {{site.data.keyword.Bluemix_notm}} to access GitHub, click **Authorize** to go to the GitHub website. If you don't have an active GitHub session, you are prompted to log in. Click **Authorize Application** to allow {{site.data.keyword.Bluemix_notm}} to access your GitHub account. If you have an active GitHub session but you haven't entered your password recently, you might be prompted to enter your GitHub password to confirm.

 b. Review the default target repo locations for the GitHub repos. Those repos are cloned from the sample repos. If needed, change the names of the target repos.
 ![Default target repo locations](images/toolchain_github_config.png)

1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **GitHub**.

1. If you have a GitHub repo and want to use it, for the repository type, click **Existing** and type the URL.
1. If you want to use a new GitHub repo, type a name for the GitHub repo, type the URL for the repo that you are cloning or forking, and select the repository type:

 a. To create an empty repo, click **New**.

 b. To create a copy of a GitHub repo, click **Clone**.

 c. To fork a GitHub repo so that you can contribute changes through pull requests, click **Fork**.

1. If you want to use GitHub's Issues for issue tracking, select the **Enable GitHub Issues** check box.
1. If you want to track the deployment of code changes by creating tags and comments on commits, and labels and comments on issues that are referenced by the commits, select the **Track deployment of code changes** check box. For more information, see [Track where your code is deployed with toolchains ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Click **Create Integration**.
1. Click the card for the GitHub repo that you want to work with. The GitHub website opens, where you can view the contents of the repo.

  **Tip:** You can use the integrated source code management tools in Eclipse Orion {{site.data.keyword.webide}} to edit the GitHub repo and deploy an app from your workspace.

1. If you enabled GitHub Issues, click **GitHub Issues** to open it. You can use this instance of GitHub Issues for your entire toolchain, even if the toolchain contains multiple GitHub repos.    

**Note:** If you don't have admin privileges for the repo that you are linking to, your integration is limited because you can't use a webhook. Webhooks are required to automatically run a pipeline when a commit is pushed to the repo. Without a webhook, you must start your pipelines manually.

For more information, see [GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} and [GitHub Issues ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configuring GitHub Enterprise and Issues on Bluemix Dedicated
{: #configghe}

 **Note:** These instructions apply to {{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}}. If you are using your own managed version of {{site.data.keyword.ghe_short}}, some steps might differ depending on your internal procedures.

{{site.data.keyword.ghe_long}} is an on-premises, web-based hosting service for Git repos. Dedicated {{site.data.keyword.ghe_short}} is for {{site.data.keyword.Bluemix_notm}} Dedicated customers only. GitHub Issues is a tracking tool that keeps your work and your plans in one place. It is integrated with your development repo so that you can focus on important tasks. For more information about Dedicated {{site.data.keyword.ghe_short}} and GitHub Issues, see [Getting started with {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window} and [GitHub Issues ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

You can configure {{site.data.keyword.ghe_short}} as a tool integration in your toolchain so that you can manage source code in your company's [{{site.data.keyword.Bluemix_notm}} Dedicated](/docs/dedicated/index.html#dedicated){: new_window} instance.

1. If you are configuring this tool integration as you are creating the toolchain, follow these steps:

 a. Before you log in to Dedicated {{site.data.keyword.ghe_short}} for the first time, ask your company's region administrator to add your user ID to your {{site.data.keyword.Bluemix_notm}} Dedicated instance from your company's user registry by using LDAP. For information about setting up your {{site.data.keyword.ghe_short}} account, see [Getting started with {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}.

 b. In the Configurable Integrations section, click **{{site.data.keyword.ghe_short}}**.    

 c. Review the default name for the new {{site.data.keyword.ghe_short}} repo. If needed, change the name of the new repo. The following image shows an example of a repo that is cloned from a sample repo. You can use an existing repo or a new repo. To use a new repo, you can create an empty repo, clone a repo, or fork a repo.
 ![Default repo locations](images/toolchain_ghe_config.png)

1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **{{site.data.keyword.ghe_short}}**.

1. If you have a {{site.data.keyword.ghe_short}} repo that you want to use, type the URL for the repo. For the repository type, click **Existing**.
1. If you want to use a new {{site.data.keyword.ghe_short}} repo, type a name for the repo, type the URL for the repo that you are cloning or forking, and select the repository type:

 a. To create an empty repo, click **New**.

 b. To create a copy of a repo, click **Clone**.

 c. To fork a repo so that you can contribute changes through pull requests, click **Fork**.

1. To use GitHub Issues for issue tracking, select the **Enable GitHub Issues** check box.
1. Click **Create Integration**.
1. Click the card for the {{site.data.keyword.ghe_short}} repo that you want to work with. Your company's {{site.data.keyword.ghe_short}} repo opens.

  **Tip:** You can use the integrated source code management tools in Eclipse Orion {{site.data.keyword.webide}} to edit the {{site.data.keyword.ghe_short}} repo and deploy an app from your workspace.

1. If you enabled GitHub Issues, click **GitHub Issues**. You can use this instance of GitHub Issues for your entire toolchain, even if the toolchain contains multiple GitHub repos.    

**Note:** If you don't have admin privileges for the repo that you are linking to, your integration is limited because you can't use a webhook. Webhooks are required to automatically run a pipeline when a commit is pushed to the repo. Without a webhook, you must start your pipelines manually.


## Configuring Jenkins
{: #jenkins}

Jenkins is an open source, server-based tool that builds and tests software continuously, supporting the practices of continuous integration and continuous delivery.

**Important:** Before you create a Jenkins tool integration, you must have a Jenkins server.

With the Jenkins tool integration, you can send your Jenkins job notifications to other tools in your toolchain, such as Slack and PagerDuty. To trace code in deployments you can add deployment messages to your Git commits and your related Git or JIRA issues. You can also view your deployments on the Toolchain Connections page. You can feed test results to {{site.data.keyword.DRA_short}}, add automated quality gates, and track your deployment risk.

Configure Jenkins to automate the continuous building, testing, and deployment of your apps:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Jenkins**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain**. Then, click **Overview**.  

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Jenkins**.

1. Type the name that you want to display for this tool integration on the Jenkins card in your toolchain.
1. Type the URL for the Jenkins server that you want to open when you click the Jenkins card from your toolchain.
1. Copy the generated toolchain webhook.
1. In your Jenkins server, complete these steps:

 a. Install the [Cloud Foundry CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}.

 b. Install the IBM Cloud DevOps Cloud Foundry plug-in by entering one of these commands:

  * Mac OS: `cf install-plugin https://icd.ng.bluemix.net/icd_darwin_amd64`

  * Linux or Docker: `cf install-plugin https://icd.ng.bluemix.net/icd_linux_amd64`

 c. Install and configure the IBM Cloud DevOps Jenkins plug-in for DevOps Insights and Notifications. For more information, see [Installing and configuring the plug-in](/docs/services/DevOpsInsights/insights_risk.html#integrate_jenkins){: new_window}.

 d. In each job for which you want to send notifications to your toolchain, complete these steps:

  * Select the **This project is parameterized** check box.

  * Add the `ICD_WEBHOOK_URL` string parameter.

  * Paste the generated toolchain webhook.
 ![Webhook URL](images/jenkins_webhook_url.png)

  * Add a post-build action for IBM Cloud DevOps - Webhook Notification and select the **Job Completed** check box.
 ![Post-build action](images/jenkins_postbuild_action.png)  

 e. In your deploy jobs, complete these steps:

  * Add the `ICD_WEBHOOK_URL`, `CF_API`, `CF_ORG`, `CF_SPACE`, and `CF_APP` string parameters. These examples show how to add each of the string parameters.
 ![Webhook URL string parameter](images/jenkins_set_webhook_url.png)
 ![CFI API string parameter](images/jenkins_set_cfapi.png)
 ![CFI ORG string parameter](images/jenkins_set_cforg.png)
 ![CFI SPACE string parameter](images/jenkins_set_cfspace.png)
 ![CFI APP string parameter](images/jenkins_set_cfapp.png)

  * Configure your bindings for the Cloud Foundry CLI by using the `CF_CREDS_USR` username variable and the `CF_CREDS_PSW` password variable.
 ![Cloud Foundry CLI bindings](images/jenkins_config_bindings.png)  

  * In the **Build** field, enter these commands to log in and use the IBM Cloud DevOps Cloud Foundry plug-in to send the application deployable mappings, with Git commit traceability, to your toolchain:
 ![Build commands](images/jenkins_build_commands.png)    

  * In the **Build** field, enter the `cf icd --create-connection $ICD_WEBHOOK_URL $CF_APP` command to send the application deployable mappings to the toolchain.    

 f. Save your changes and return to the Configure the Integration page for the Jenkins tool integration.

1. Click **Create Integration**.
1. From your toolchain, click **Jenkins** to view the Jenkins server.  

For more information, see [Jenkins ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_jenkins/){: new_window}.


## Configuring JIRA
{: #jira}

JIRA is a tool that tracks issues and bugs that are related to your software. The JIRA tool integration updates your project's issues whenever Jenkins or {{site.data.keyword.deliverypipeline}} runs a deployment. In order for the JIRA tool integration to track your issues, you must use JIRA Smart Commits in your commit messages. To learn more about JIRA Smart Commits, see [Using Smart Commits ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://confluence.atlassian.com/fisheye/using-smart-commits-298976812.html){: new_window}.

Configure JIRA to plan, track, and deliver quality code:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **JIRA**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain**. Then, click **Overview**.  

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **JIRA**.

1. If you have a JIRA project and want to connect to it, for the JIRA type, click **Existing**:

 a. Type the JIRA project key for the JIRA project. You can find the project key in the JIRA project's URL.

 b. Type the base API URL for your JIRA instance. You can find the API URL from the header of your JIRA instance. Click the **Administration** icon and click **System**.

 c. Optional: Type your JIRA user name. Your user name is required only if you are connecting to a private JIRA instance or if you are connecting to a public instance and you want to receive traceability information.

 d. Optional: Type your JIRA password. Your password is required only if you are connecting to a private JIRA instance or if you are connecting to a public instance and you want to receive traceability information.

 e. To track the deployment of code changes for the project by creating labels and comments for referenced issues, select the **Track deployment of code changes** check box. Make sure that you use JIRA Smart Commit to reference the JIRA issues in your GitHub commits. If you don't select this option, the JIRA tool integration ignores any commits.

1. If you want to create a JIRA project, for the JIRA type, click **New**:

 a. Type a JIRA project key to use for the new project. This key is used as a unique identifier in the project URL.

 b. Type a name for the JIRA project.

 c. Type the base API URL for your JIRA instance. You can find the API URL from the header of your JIRA instance. Click the **Administration** icon and click **System**.

 d. Type the user name for the JIRA project lead that you want to use for this project. To specify someone as the JIRA project lead, that person must have the project lead permission in JIRA.

 e. Type the administrator's user name for this instance of JIRA.

 f. Type the administrator's password for this instance of JIRA.

 g. To track the deployment of code changes for the project by creating labels and comments for referenced issues, select the **Track deployment of code changes** check box. Make sure that you use JIRA Smart Commit to reference the JIRA issues in your GitHub commits. If you don't select this option, the JIRA tool integration ignores any commits.

1. Click **Create Integration**.
1. From your toolchain, click **JIRA** to view the dashboard for the JIRA project that you connected to.

To learn more, see [JIRA ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_jira/){: new_window}.


## Configuring Nexus
{: #nexus}

Configure the Nexus Repository Manager to store build artifacts in your Nexus repository (repo):

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Nexus**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain**. Then, click **Overview**.  

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Nexus**.

1. Type a name for this instance of the Nexus tool integration.
1. Type the URL for the Nexus repo that you want to open when you click the Nexus card from your toolchain.
1. Select the repository type that you want to connect to.
1. If you selected **npm registry**, follow these steps:

 a. Type the email address that is associated with your registry.

 b. Type the authentication token that is associated with your registry.

 c. Type the URL for your Nexus release repo, which is your private registry on the Nexus server.

 d. Type the URL for the Mirror or Public registry that you use to combine multiple public and private npm registries. For example, this URL might be the URL of the virtual registry on your Nexus server that can access both your private registry and a cache of the npm global registry.

1. If you selected **Maven repository**, follow these steps:

 a. Type the user ID that is associated with your repo.

 b. Type the password that is associated with your repo.

 c. Type the URL for your Nexus release repo, which is your private release repo on the Nexus server.

 d. Type the URL for your Nexus snapshot repo, which is your private snapshot repo on the Nexus server.

 e. Type the URL for the Mirror or Public repo that you use to combine multiple public and private Maven repos. For example, this URL might be the URL of the virtual repo on your Nexus server that can access both your private repos and a cache of the Maven central repo.

1. Click **Create Integration**.
1. From your toolchain, click the card for the Nexus repo that you want to work with. The Nexus website opens, where you can view the contents of the repo.
1. Optional: If you are using a toolchain on {{site.data.keyword.Bluemix_notm}} Public and you want to build your app by using Nexus with npm, configure your pipeline to add an npm build job. For instructions to configure the build job, see the [Configuring a Nexus npm build job in your pipeline](#config_nexus_npm) section.
1. Optional: If you are using a toolchain on {{site.data.keyword.Bluemix_notm}} Public and you want to build your app by using Nexus with Maven, configure your pipeline to add a Maven build job. For instructions to configure the build job, see the [Configuring a Nexus Maven build job in your pipeline](#config_nexus_maven) section.

### Configuring a Nexus npm build job in your pipeline
{: #config_nexus_npm}

Before you configure an npm build job in your pipeline, you need a working pipeline that can use your build SCM repo as input, and you must configure Nexus for your toolchain. For instructions to configure Nexus, see the [Nexus](#nexus) section.

Configure the {{site.data.keyword.deliverypipeline}} to add an npm build job:

1. Create a stage and set the input to the appropriate SCM repo.
1. On the stage, add a build job.
1. Configure the build job:
  ![npm build job](images/nexus_npm_job.png)

  a. For the builder type, select **NPM Build**.

  b. If you configured multiple instances of the Nexus tool integration, enter the name of the Nexus tool integration that you want to configure the npm build job for.

  c. For the tool integration type, select **Nexus**.

  d. For the build command, enter the commands to build your npm module or publish it to your registry. This example shows the commands to either build the module or publish it.
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Tip:** You can find the URL and user credentials that you used to connect to your registry in the configuration settings for the Nexus tool integration.

  e. If your build job publishes to the Nexus registry and the format of your node module version is `x.y.z-SNAPSHOT.w`, select the **Increment snapshot module version** check box. The build job automatically updates the module version before it publishes to the Nexus registry. The build job selects the highest version of the module from the npm registry and the local `package.json` file, and increments the module version by using semver. The build job does not deliver the changes to the SCM repo.

1. Click **SAVE**. Whenever your pipeline runs, this build job uses the configuration information from the Nexus tool integration to connect to your npm registry.

### Configuring a Nexus Maven build job in your pipeline
{: #config_nexus_maven}

Before you configure a Maven Build job in your pipeline, you need a working pipeline that can use your build SCM repo as input, and you must configure Nexus for your toolchain. For instructions to configure Nexus, see the [Nexus](#nexus) section.

Configure the {{site.data.keyword.deliverypipeline}} to add a Maven Build job:

1. Create a stage and set the input to the appropriate SCM repo.
1. On the stage, add a build job.
1. Configure the build job:
  ![Maven build job](images/nexus_maven_job.png)

  a. For the builder type, select **Maven Build**.

  b. If you configured multiple instances of the Nexus tool integration, enter the name of the Nexus tool integration that you want to configure the Maven Build job for.

  c. For the tool integration type, select **Nexus**.

  d. For the build command, enter the commands to build your Maven module or publish it to your snapshot registry. This example shows the commands to either build the module or publish it.
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Tip:** You can find the URL and user credentials that you used to connect to your registry in the configuration settings for the Nexus tool integration.

1. Click **SAVE**. Whenever your pipeline runs, this build job uses the configuration information from the Nexus tool integration to connect to your Maven repo.

For more information, see [Nexus ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_nexus/){: new_window}.


## Configuring a custom tool (Other Tool)
{: #othertool}

If your team uses a tool that isn't included in the toolchains integrations list, you can integrate a custom tool.

Configure a custom tool so that it works with other tools in your toolchain and is available to your team:

1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Other Tool**.

1. Type the tool name.
1. Select the lifecycle phase that is most closely associated with the tool. This selection determines which category your tool is listed under on the Overview page.
1. Add an icon URL. The icon is shown on your tool integration's card.
1. Add a documentation URL.
1. Specify a tool instance name. For example: My Team Tool.
1. Add a tool instance URL. This URL opens whenever the tool integration's card is clicked.
1. Add a description of your tool.
1. (Advanced) Add more properties as needed. For example, list any information or attributes that are required for your tool to integrate with other tools in the toolchain.  
1. Click **Create Integration**.

To learn more, see [Introducing custom tool integration for {{site.data.keyword.Bluemix_notm}} toolchains ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2016/10/custom-tool-integration-with-bluemix-toolchains/){: new_window}.


## Configuring PagerDuty
{: #pagerduty}

PagerDuty integrates data from multiple monitoring systems into a single view. When a problem occurs, PagerDuty ensures that the team member who is best able to fix it at the time is notified. If the team member does not respond to the problem, escalations can be configured to route it to secondary engineers or operations managers.

Configure PagerDuty to send notifications when pipeline stage failures occur so that you can fix problems faster and reduce downtime:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **PagerDuty**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **PagerDuty**.

1. Type the API access key for your PagerDuty account. If you don't have a PagerDuty account, [register for one ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://signup.pagerduty.com/accounts/new){: new_window}. For instructions to find the key, see [Generating an API Key ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.pagerduty.com/hc/en-us/articles/202829310-Generating-an-API-Key){: new_window}.
1. Type the name of your PagerDuty service.
1. Type the email address for the primary PagerDuty contact.
1. Type the phone number for the primary PagerDuty contact.
1. Click **Create Integration**.
1. Click **PagerDuty** to go to pagerduty.com. You can view the events that are associated with the PagerDuty service that you specified when you configured this tool integration for your toolchain.

To learn more, see [PagerDuty ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuring Rational Team Concert (Experimental)
{: #rationalteamconcert}

IBM Rational Team Concert&trade; is a team collaboration tool that integrates development tasks, including iteration planning, change management, defect tracking, source control, build automation, and reporting.

Configure Rational Team Concert to practice a DevOps approach and continuous delivery in your development environment:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Rational Team Concert**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain**. Then, click **Overview**.  

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Rational Team Concert**.

1. Type the URL for the Rational Team Concert server that you want to open when you click the Rational Team Concert card from your toolchain.
1. Type the user ID that you use to access the Rational Team Concert server.
1. Type the password that you use to access the Rational Team Concert server.
1. If you have a Rational Team Concert project area that you want to add to your toolchain, follow these steps:

 a. From the **Project Area type** list, select **Existing project area**. 

 b. Type the name of the project area to add to your toolchain.
 
1. If you want to create a Rational Team Concert project area to add to your toolchain, follow these steps:
 
 a. From the **Project Area type** list, select **New project area**. 

 b. Type a name for the new project area to add to your toolchain.
 
 c. Type the name of the Rational Team Concert process template to use to create the project.
 
1. To track the deployment of code changes for the project by creating tags and comments on work items, select the **Track deployment of code changes** check box.
1. Click **Create Integration**.
1. From your toolchain, click **Rational Team Concert** to open the Rational Team Concert dashboard that you configured.

For more information, see [IBM Rational Team Concert ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/think/tool_rtc/){: new_window}.



## Configuring Sauce Labs
{: #saucelabs}

Sauce Labs runs functional unit tests. When a Sauce Labs test suite is configured as a test job in the {{site.data.keyword.deliverypipeline}}, the test suite can run tests against your web or mobile app as part of your continuous delivery process. These tests can provide valuable flow control for your projects, acting as gates to prevent the deployment of bad code.

 **Note:** This tool integration is available only on {{site.data.keyword.Bluemix_notm}} Public.

Configure Sauce Labs to run automated functional tests on multiple operating systems and browsers so that you can emulate the way that a user might use a website or an application:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Sauce Labs**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Sauce Labs**.

1. Type the user name that is associated with your Sauce Labs account. You can [find your user name in the welcome message at the top of your Sauce Labs account page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://saucelabs.com/account){: new_window}.
1. Type the access key for your Sauce Labs account. You can [find the key on your Sauce Labs account page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://saucelabs.com/account){: new_window}.
1. Click **Create Integration**.
1. Click **Sauce Labs** to go to saucelabs.com and view the test activity for the toolchain.

 **Tip:** If you added a Sauce Labs test job to the {{site.data.keyword.deliverypipeline}}, you can select the service instance.

To learn more, see [Sauce Labs ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_sauce_labs/){: new_window}.


## Configuring Slack
{: #slack}

**Important:** Notifications that are posted to public Slack channels are visible to everyone on the team. Remember that you are responsible for the content that you post.

Slack is a cloud-based, real-time messaging and notification system. Slack provides persistent chat, which is a more interactive alternative to email for team collaboration. You can communicate with your team on a dedicated channel or on a set of channels that is directly related to your work. You can also share files and images through the channels or in direct messages between two or more people. The communications in direct messages and on channels are retained so that you can search them.

Configure Slack to receive notifications about your toolchain from the tool integrations, such as test and deployment activities:

1. If you are configuring this tool integration as you are creating the toolchain, in the Configurable Integrations section, click **Slack**.
1. If you have a toolchain and are adding this tool integration to it, on the DevOps dashboard, on the Toolchains page, click the toolchain to open its Overview page. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain** and click **Overview**.

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **Slack**.

1. Type the Slack webhook URL, which is generated by Slack as an incoming webhook. You need a Slack webhook URL for a Slack channel to receive notifications about your toolchain from the tool integrations. For instructions to create or find your webhook, see [Incoming Webhooks ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://api.slack.com/incoming-webhooks){: new_window}.

 **Tip:** If you have been using an API key for your Slack channel to receive notifications about your toolchain from the tool integrations, you must update your configuration to use a webhook instead.

1. Type the name of the Slack channel that you want notifications to be sent to. The channel must exist and be active in your Slack team.
1. Type the URL host name for your Slack team, which is the word or phrase before `.slack.com` in your team URL. For example, if your team URL is `https://team.slack.com`, the host name is `team`.
1. Click **Create Integration**.

 **Tip:** If the Slack channel and team that you specified cannot be reached, the `Setup Failed` error is displayed on the Slack card. Hover over the `Setup Failed` message and click **Reconfigure**. Make sure that you are using valid configuration parameters for the Slack webhook URL, Slack channel, and URL host name for your Slack team. Update the settings as required, and click **Save Integration**.

1. Click **Slack**. You can view all of the activity for your toolchain in the configured Slack channel.

To learn more, see [Slack ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.


## Configuring SonarQube
{: #sonarqube}

SonarQube provides an overview of the overall health and quality of your source code and highlights issues that are found in new code. The code analyzers detect tricky bugs, such as null-pointer dereferences, logic errors, and resource leaks, for more than 20 coding languages.

Configure SonarQube to continuously analyze and measure the quality of your source code:

1. From the DevOps dashboard, click **Toolchains**. Click the toolchain that you want to add SonarQube to. Alternatively, on your app's Overview page, on the Continuous delivery card, click **View Toolchain**. Then, click **Overview**.  

 a. Click **Add a Tool**.

 b. In the Tool Integrations section, click **SonarQube**.

1. Type a name for this instance of the SonarQube tool integration.
1. Type the URL for the SonarQube instance that you want to open when you click the SonarQube card from your toolchain.
1. Optional: Type the user name that you use to connect to the SonarQube server.

 **Tip:** You need to specify a user name only if you use a password to connect to the SonarQube server. If you use an authentication token to connect, leave this field empty.

1. Type the password or authentication token that you use to connect to the SonarQube server.
1. Click **Create Integration**.
1. From your toolchain, click **SonarQube** to view the dashboard for the SonarQube instance that you connected to.

To learn more, see [SonarQube ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/learn/tool_sonarqube/){: new_window}.
