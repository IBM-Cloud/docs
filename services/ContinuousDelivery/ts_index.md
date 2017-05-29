---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-25"

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


## Cannot create a toolchain
{: #cannot_create_toolchain}

An error is displayed when you create a toolchain.
{:shortdesc}

When you create a toolchain, you see the following error message:
{: tsSymptoms}

`This organization contains 200 toolchains, which is the maximum limit. Before you can add another toolchain, remove one or more toolchains from the organization.`

You cannot have more than 200 toolchains in an organization (org).  
{: tsCauses}

Remove one or more toolchains from your org and then create your toolchain again.
{: tsResolve}


## Org's memory limit is exceeded
{: #org_outofmemory}

You might be unable to deploy an app to {{site.data.keyword.Bluemix_notm}} if you have exceeded the memory limit of your organization. You can either reduce the memory that your apps use or increase the memory quota of your account. The maximum memory quota for a trial account is 2 GB and can only be increased by moving to a paid account.

When you deploy an app to {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms}

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

This error occurs when the amount of memory that is remaining for your organization is less than the amount of memory that is required by the app that you want to deploy. The maximum memory quota for a trial account is 2 GB.
{: tsCauses}

You can either increase the memory quota of your account, or reduce the memory that your apps use.
{: tsResolve}

  * To increase the memory quota of your account, convert your trial account to a pay account. For information about how to convert your trial account to a pay account, see [Pay accounts](/docs/pricing/index.html#pay-accounts).
  * To reduce the memory that your apps use, use either the {{site.data.keyword.Bluemix_notm}} console or the cf command line interface.

    If you use the {{site.data.keyword.Bluemix_notm}} console, complete the following steps:

    1. In the Apps Dashboard, select your app. The app details page opens.
    2. In the runtime pane, you can reduce the maximum memory limit or the numbers of app instances, or both, for your app.

    If you use the cf command line interface, complete the following steps:

    1. Check how much memory is being used for your apps:

	  ```
	  cf apps
	  ```

	  The cf apps command lists all the apps that you deployed in your current space. The status of each app is also displayed.

    2. To reduce the amount of memory that is used by your app, reduce the number of app instances or the maximum memory limit, or both:

	  ```
	  cf push appname -p app_path -i instance_number -m memory_limit
      ```

    3. Restart your app for the changes to take effect.

For more information about general problems with managing your apps, see [Troubleshooting for managing apps](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#managingapps).


## Toolchain does not load
{: #toolchains_load}

When you click a toolchain to view its Overview page, the toolchain does not load.
{:shortdesc}

On the DevOps dashboard, on the **Toolchains** page, click the toolchain to open the its Overview page. Alternatively, on the app's overview page, on the Continuous Delivery card, click **View toolchain**. Then, click **Overview**. The Overview page for the toolchain does not open.
{: tsSymptoms}

Check the {{site.data.keyword.Bluemix_notm}} status to see if the problem is caused by an outage.
{: tsCauses}

View the {{site.data.keyword.Bluemix_notm}} Status page to determine whether there are known issues that are affecting the {{site.data.keyword.Bluemix_notm}} platform and the major services in {{site.data.keyword.Bluemix_notm}}.
{: tsResolve}

You can find the Status page by choosing either of the following options:

  * Log in to the {{site.data.keyword.Bluemix_notm}} console. From the menu bar, click **Support** and select **Status**. Check the listed resources for the ![some issues](../../support/images/some_issues.svg) icon. This icon might indicate an outage.
  * Access it directly at [IBM {{site.data.keyword.Bluemix_notm}} - System Status ![External link icon](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixstatus){: new_window}.

For more information about the {{site.data.keyword.Bluemix_notm}} Status page, see [Viewing {{site.data.keyword.Bluemix_notm}} status](https://console.ng.bluemix.net/docs/support/index.html#viewing-bluemix-status).


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
