---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.contdelivery_short}} troubleshooting
{: #ts_cd}

Get answers to common troubleshooting questions about using {{site.data.keyword.contdelivery_full}}.
{:shortdesc}


## Cannot authorize with GitHub
{: #cannot_authorize_github}

You are not authorized with GitHub.
{:shortdesc}

If you have not authorized {{site.data.keyword.Bluemix_notm}} to access your GitHub account, any of these issues can occur:
{: tsSymptoms}

 * When you try to add the GitHub tool integration to your toolchain, the tool integration is not added.
 * The pipeline does not automatically run when you push changes to your GitHub or GitHub Enterprise repository.

{{site.data.keyword.Bluemix_notm}} is not authorized to access GitHub.  
{: tsCauses}
 
If you are configuring the GitHub tool integration while you are creating your toolchain, follow these steps:
{: tsResolve}
 
  1. In the Configurable Integrations section, click **GitHub**. 
  1. If you are creating the toolchain on {{site.data.keyword.Bluemix_notm}} Public and you have not authorized {{site.data.keyword.Bluemix_notm}} to access GitHub, click **Authorize** to go to the GitHub website. 
  1. If you don't have an active GitHub session, you are prompted to log in. Click **Authorize Application** to allow {{site.data.keyword.Bluemix_notm}} to access your GitHub account. If you have an active GitHub session but you haven't entered your password recently, you might be prompted to enter your GitHub password to confirm.
  
If you already have a toolchain, update the GitHub tool integration's configuration:

 1. On the DevOps dashboard, on the **Toolchains** page, click the toolchain to open its Overview page. Alternatively, on the app's Overview page, on the Continuous delivery card, click **View Toolchain**, and then click **Overview**.
 1. On the GitHub card, click the menu and click **Configure**.
 1. Update the configuration settings to authorize {{site.data.keyword.Bluemix_notm}} to access GitHub. Click **Authorize** to go to the GitHub website. If you don't have an active GitHub session, you are prompted to log in. Click **Authorize Application** to allow {{site.data.keyword.Bluemix_notm}} to access your GitHub account. If you have an active GitHub session but you haven't entered your password recently, you might be prompted to enter your GitHub password to confirm.
 1. When you are finished updating the settings, click **Save Integration**.


## Tool integration is not configured
{: #tool_integration_error}

After you configure a tool integration for your toolchain, the `Setup failed` error is displayed on its tool card.
{:shortdesc}

After you configure a tool integration, you view its tool card on the toolchain's Overview page and notice that the setup failed.
{: tsSymptoms}

 ![Setup failed error](images/tool_setup_failed.png)
 
When you add a tool integration, the toolchain communicates with the tool that is represented by the tool integration to provision any necessary resources and associate them with the toolchain. If an error occurs during the setup process or if the communication between the toolchain and the tool does not complete properly, the tool integration is put into an error state.
{: tsCauses}

Configure the tool integration again:
{: tsResolve}

1. On its tool card, hover over the `Setup failed` message and click **Reconfigure**.

 ![Reconfigure button](images/tool_reconfigure.png)
 
1. Make sure that you are using valid configuration parameters. If the error was caused by an invalid configuration, an error message is displayed; for example, `The integration could not be set up. Check the settings and try again. Reason: Invalid api_key:fakeKey`. Update the settings for the tool integration and click **Save integration**.
1. If the error was caused by a communication problem, click **Save integration** to try again.
