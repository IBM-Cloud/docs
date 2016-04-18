---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Setting up toolchains (Experimental)
{: #toolchains-setup}

*Last updated: 18 April 2016*  

You can create a toolchain in two ways: add a toolchain to an existing app or use a predefined template to create a toolchain. Depending on the toolchain or template that you use, the toolchain might include a GitHub repository (repo) that is populated with app starter code and a preconfigured delivery pipeline. The pipeline builds any changes to the GitHub repo and then deploys the app to {{site.data.keyword.Bluemix}}. 
{: shortdesc}  

**Important**: This capability is experimental. Toolchains might not be stable and might change in ways that are not compatible with earlier versions. They are not recommended for use in production environments. To use toolchains, you must make a one-time [request for access](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}.  Toolchains are available in the Dallas region only.

##Creating a toolchain from an app
{: #creating_a_toolchain_from_an_app}

After your access request to toolchains is approved, you can create a toolchain from your app to configure continuous development, deployment, monitoring, and more. The toolchain is associated with your app. Each app can be associated with a toolchain. When you push changes to the toolchain's GitHub repo, the delivery pipeline automatically builds and deploys the app.  

1. On your app's Overview page, on the Continuous Delivery tile, click **Add Toolchain**. Your app is configured for continuous delivery from a new GitHub repo that is populated with the app starter code.
1. On the toolchain creation page, review the diagram of the toolchain that you are about to create. The diagram shows each tool integration in its lifecycle phase in the toolchain.
1. Review the default information for the toolchain settings. The toolchain's name identifies it in {{site.data.keyword.Bluemix}}. If you already have a toolchain with that name, or if you want to use a specific name, change the toolchain's name.
1. If you want to create the toolchain before you configure any tool integrations, click **CREATE** and confirm that you want to create the toolchain without any tool integrations. Continue to the "Creating a toolchain" section that describes the steps that run automatically to set up your toolchain.  
1. If you want to configure any tool integrations before you create the toolchain, in the Configurable Integrations section, select each of the tool integrations that you want to configure. For information about configuring the tool integrations, continue to the "Configuring a tool integration" section that describes how to configure each of the tool integrations included in your toolchain.

##Creating a toolchain from a template   
{: #creating_a_toolchain_from_a_template}

After your access request to toolchains is approved, you can use a template as a starting point to create a toolchain that includes a specific set of tool integrations.

1. On the DevOps dashboard, on the **Toolchains** tab, click **Create a Toolchain** to create your first toolchain. If you already have one or more toolchains, click the add button (+) to create another toolchain.
1. Click the template that you want to use to create your toolchain. For example, click **Cloud-native toolchain for microservices** to use this online store sample to create your toolchain. 
1. On the toolchain creation page, review the diagram of the toolchain that you are about to create. The diagram shows each tool integration in its lifecycle phase in the toolchain. 
1. Review the default information for the toolchain settings. The toolchain's name identifies it in {{site.data.keyword.Bluemix}}. If you already have a toolchain with that name, or if you want to use a specific name, change the toolchain's name.  
1. If you want to create the toolchain before you configure any tool integrations, click **CREATE** and confirm that you want to create the toolchain without any tool integrations. Continue to the "Creating a toolchain" section that describes the steps that run automatically to set up your toolchain.  
1. If you want to configure any tool integrations before you create the toolchain, in the Configurable Integrations section, select each of the tool integrations that you want to configure. For information about configuring the tool integrations, continue to the "Configuring a tool integration" section that describes how to configure each of the tool integrations included in your toolchain. 

##Configuring a tool integration
{: #configuring_a_tool_integration}

Configure any of the following tool integrations that are included in your toolchain.

###Configuring the Sauce Labs integration
Sauce Labs runs automated functional tests on multiple operating systems and browsers so that you can emulate the way that a user might use a website or an application. 

1. Click **Sauce Labs**.
1. Type the user name that is associated with your Sauce Labs account. You can [find your user name in the welcome message at the top of your Sauce Labs account page](https://saucelabs.com/account){: new_window}.
1. Type the access key for your Sauce Labs account. You can [find the key in the lower-left corner of your Sauce Labs account page](https://saucelabs.com/account){: new_window}.

###Configuring the PagerDuty integration
PagerDuty sends notifications when problems occur so that you can fix problems faster and reduce downtime.

1. Click **PagerDuty**.
1. Type the Account ID that is associated with your PagerDuty account. If you don't already have a PagerDuty account, [register for one](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Type the API access key for your PagerDuty account. For instructions to find the key, see [API Authentication](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Type the name of your PagerDuty service.
1. Type the email address for the primary PagerDuty contact.
1. Type the phone number for the primary PagerDuty contact.

###Configuring the Delivery Pipeline integration
With the Delivery Pipeline, you can automate the continuous building, testing, and deployment of your apps.

1. Click **Delivery Pipeline**.
1. Review the default name of the app and the default region, organization, and space for the dev, test, and prod stages. Change those settings as needed.

###Configuring the GitHub integration
You can use GitHub to manage your source code on the cloud.

1. Click **GitHub**. If you have not already authorized {{site.data.keyword.Bluemix}} to access GitHub, you are prompted to allow access. On the GitHub website, if you don't have an active GitHub session, you are prompted to log in. Click **Authorize Application** to allow {{site.data.keyword.Bluemix}} to access your GitHub account. If you have an active GitHub session but you haven't entered your password recently, you might be prompted to enter your GitHub password to confirm.
1. Review the default target repository locations for the GitHub repos. Those repos are cloned from the sample repos. Change the names of the target repositories as needed.

###Configuring the Slack integration
With Slack, you can collaborate with your team and receive notifications about your test and deployment activities.

1. Click **Slack**.
1. Type the API authentication token for your Slack account. You must use a generated full-access token to authenticate with Slack. For instructions to find the token, see [Slack authentication](https://api.slack.com/web#authentication){: new_window}.
1. Type the name of the Slack channel that you want notifications to be sent to. You can use an existing, archived, or new channel. If the channel that you specify doesn't exist, it is created. If the channel was archived, it is reactivated.

## Creating a toolchain
{: #creating_a_toolchain}

If you haven't created your toolchain yet, click **CREATE**. Several steps run automatically to set up your toolchain:

1. The toolchain is created.
1. If you configured the Delivery Pipeline tool integration, the pipelines run.
1. If you configured the Sauce Labs tool integration, the Sauce Labs integration is configured to add jobs to the pipelines and run tests.
1. If you configured the PagerDuty tool integration, the PagerDuty integration is configured to send notifications to the channel that you configured in Slack. These notifications indicate when a problem occurs.
1. If you configured the Slack tool integration, the Slack integration is configured to send notifications to the channel that you configured in Slack. These notifications indicate the progress of the deployment; for example, `Connected with Project XYZ`, `Pipeline Configured`, and `Stage 'build' started`.
1. If you configured the GitHub tool integration, the sample GitHub repo is cloned into your GitHub account.  
1. If your toolchain contains starter code in a GitHub repo, the app is deployed to {{site.data.keyword.Bluemix}}.

##Viewing a toolchain
{: #viewing_a_toolchain}

After the toolchain and all tool integrations are configured, the Tool Integrations page opens.

1. Review the page to see a visual representation of the toolchain for your app.
1. To access a tool integration that is included in your toolchain, click the tool tile. 
 
 **Tip**: If you have more than one GitHub repo, you might have multiple tiles for the same tool integration since each repo needs its own pipeline.
