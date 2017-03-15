---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Troubleshooting for accessing {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


General problems with accessing {{site.data.keyword.Bluemix}} might include difficulties logging in to {{site.data.keyword.Bluemix_notm}} or an account that is in a pending state. In many cases, you can recover from these problems by following a few easy steps. 
{:shortdesc}

## Can't log in to {{site.data.keyword.Bluemix_notm}}: Incorrect password
{: #ts_logintobm}

You must have a valid IBMid to log in to the {{site.data.keyword.Bluemix_notm}} console.

You must have a valid IBMid or SoftLayer ID to log in through the [Customer Portal](https://control.softlayer.com).

When you try to log in to {{site.data.keyword.Bluemix_notm}}, the following error message is displayed: 
{: tsSymptoms} 

`The password that you entered is not correct.`

The IBMid and password that you used to log in to {{site.data.keyword.Bluemix_notm}} is invalid.
{: tsCauses} 
 
Use one of the following solutions:
{: tsResolve}
 * Enter the correct password. To check whether your IBMid and password are valid, you can go to the My IBM profile page, click **Log in** and enter your IBMid and password on the Log in page. 
 * If you forgot your password, click **Forgot your password** to reset your password. Then return to the [Bluemix console](https://console.{DomainName}) or the [Customer Portal](https://control.softlayer.com) and log in again.
 * If you forgot your IBMid or continue to have problems with your password, contact the Worldwide IBM Registration Help Desk for help. 
 * To obtain a valid IBMid and password, go to the My IBM profile page, then click **Register**.
  
**Notes:** 
 * For IBM employees, your IBMid might be different from your intranet ID.
 * If you are on the Sign in to IBM page and the login process is disrupted for any reason (for example, resetting your password), return to the [Bluemix console](https://console.{DomainName}) or the [Customer Portal](https://control.softlayer.com) and start the log in process again.
 

## Can't log in to {{site.data.keyword.Bluemix_notm}}: Invalid login credentials
{: #ts_login_invalid_credentials}

When you log in using your IBMid, the following message is displayed:
{: tsSymptoms}

`Invalid login credentials provided. If you have an IBMid associated with your account, please log in here` 

* You switched to an IBMid, but you tried to log in through the [Customer Portal](https://control.softlayer.com) using your previous SoftLayer username and password. 
{: tsCauses}

* You tried to log in through the [Customer Portal](https://control.softlayer.com), but you entered your IBMid and password in the Username and Password fields. 

Click **log in here** in the message, or go to the IBMid Account Login section and click **Log in with IBMid**.
{: tsResolve}

Don't use the **Username** and **Password** fields that you used with your previous Softlayer ID.


## Can't log in to {{site.data.keyword.Bluemix_notm}}: Unrecognized IBMid or email
{: #ts_softlayer_username}

When you log in to the {{site.data.keyword.Bluemix_notm}} console, the following message is displayed: 
{: tsSymptoms} 

`We didn't recognize this IBMid or email.`

You tried to log in to the {{site.data.keyword.Bluemix_notm}} console, but did not use a valid IBMid. For example, you did not enter a fully qualified email address for the IBMid, or you tried to use a SoftLayer username and password.
{: tsCauses}
 
You must have a valid IBMid and password to log in to {{site.data.keyword.Bluemix_notm}}.

 * Ensure that you enter a fully qualified email address for the IBMid.
 {: tsResolve}
 * If you are a SoftLayer user with a SoftLayer ID, you must switch to IBMid authentication in the Customer Portal in each account that you have access to before you can log in by using IBMid authentication. 
 For more information, see [Switching to IBMid](docs/admin/softlayerlink.html#ibmid_switch).


## Can't log in to {{site.data.keyword.Bluemix_notm}}: IBMid is not associated with any IBM Cloud accounts
{: #ts_login_noswitch}

When you log in using your IBMid, the following message is displayed:
{: tsSymptoms}

`You have reached this page because your authentication was successful, however, this IBMid is not associated with any IBM Cloud accounts. If you believe this to be in error, contact your Account Owner or Master User.`

You logged in from the [Customer Portal](https://control.softlayer.com) with a valid IBMid, but you aren't switched to IBMid authentication in SoftLayer.
{: tsCauses} 
 
Complete the following checks, as appropriate:
{: tsResolve}
 * Contact your master user or account administrator to check that you are enabled to switch to IBMid authentication.
 * Ensure that you complete the Switch to IBMid step in your Softlayer account. See [Switching to IBMid](/docs/admin/softlayerlink.html#ibmid_switch).
 * Ensure that you follow the actions in the **Associate your SoftLayer user with an IBMid** email. Check your inbox and your junk mail folder for the email. To get the email again, for example, if it has expired, go to the Edit User Profile page in the Control Portal and click **Resend Email**. Alternatively, contact [{{site.data.keyword.Bluemix_notm}} Support ![External link icon](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport.com){: new_window}.

**Note:** If you created your IBMid directly with IBMid, you receive two emails to process; one from IBMid registration, and one from Softlayer. Ensure that you follow the actions in both emails.

Depending on how your account is set up, some of these log in options might apply to you: 
 * SoftLayer users with SoftLayer IDs must log in through the [Customer Portal](https://control.softlayer.com).
 * SoftLayer users with an IBMid and with or without a linked Bluemix account can log in through the [Customer Portal](https://control.softlayer.com) to open the SoftLayer Customer Portal or through the [Bluemix console](https://console.{DomainName}) to open the Infrastructure dashboard. 


## Can't log in to {{site.data.keyword.Bluemix_notm}}: IBMid is not associated with any {{site.data.keyword.Bluemix_notm}} accounts
{: #ts_unabletologin}

When you log in to {{site.data.keyword.Bluemix_notm}}, the following message is displayed: 
{: tsSymptoms} 
 
`You have reached this page because your authentication was successful, however, this IBMid is not associated with any  {{site.data.keyword.Bluemix_notm}} accounts.`

You logged in from the [Bluemix console](https://console.{DomainName}) with a valid IBMid, but you don't have a {{site.data.keyword.Bluemix_notm}} account created yet. 
{: tsCauses} 

To create a {{site.data.keyword.Bluemix_notm}} account, follow the sign up process. 
{: tsResolve}

Depending on how your account is set up, some of these log in options might apply to you: 
 * Bluemix users without a linked SoftLayer account must log in through the Bluemix console.
 * Bluemix users with a linked SoftLayer account can log in through the [Bluemix console](https://console.{DomainName}) or the [Customer Portal](https://control.softlayer.com).
 

## Can't log in to {{site.data.keyword.Bluemix_notm}}: Console doesn't open
{: #ts_login_stalls}

When you log in using your IBMid, a login success message is displayed, but you don't return to the [Bluemix console](https://console.{DomainName}) or the [Customer Portal](https://control.softlayer.com)
{: tsSymptoms}

Use one of the following solutions:
{: tsResolve}
 * Close your browser, clear the cache and cookies, then try to log in again.
 * Ensure that you log in from the [Bluemix console](https://console.{DomainName}) or the [Customer Portal](https://control.softlayer.com), rather than directly from the IBMid authentication service.
 
 
## Can't log in to {{site.data.keyword.Bluemix_notm}}: IBMid login doesn't complete
{: #ts_login_ibmid}

When you log in to {{site.data.keyword.Bluemix_notm}}, authenticating with IBMid doesn't complete.
{: tsSymptoms}

There might be a problem with the IBMid authentication service.
{: tsCauses}

Check the status of the service at [IBM BlueID ![External link icon](../icons/launch-glyph.svg "External link icon")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window}, then try again.
{: tsResolve}


## Can't log in to {{site.data.keyword.Bluemix_notm}}: Account is pending
{: #ts_accntpding}

If your account is pending, you can't log in to {{site.data.keyword.Bluemix_notm}}.
 
After you register for a {{site.data.keyword.Bluemix_notm}} trial account, you might not be able to log in to {{site.data.keyword.Bluemix_notm}}. The following message is displayed:
{: tsSymptoms}

<code>Your account is pending. Please wait up to 24 hours for email confirmation and also check your spam folder. If you still have not received your email confirmation, contact <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix Support</a>.</code>

After you register for a {{site.data.keyword.Bluemix_notm}} trial account, you receive a confirmation email. You must click the link that is in the confirmation email to complete the registration process.
{: tsCauses} 

The confirmation email is sent to the email address that you provided. Check your inbox and your junk mail folder. If you haven't received the confirmation email, contact [{{site.data.keyword.Bluemix_notm}} Support ![External link icon](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}


<!-- begin STAGING ONLY --> 

## Can't log in to {{site.data.keyword.Bluemix_notm}}: Problem accessing external website
{: #ts_bmlinkid}

To log in to {{site.data.keyword.Bluemix_notm}} by using your IBM intranet ID, you must link your intranet ID with your IBMid.

After you select **Sign in with your intranet ID** from the {{site.data.keyword.Bluemix_notm}} Sign in page, the following message might be displayed::
{: tsSymptoms} 

`Problem Accessing External Website`

This problem occurs when you log in to {{site.data.keyword.Bluemix_notm}} by using an IBM intranet ID that isn't linked to an IBMid. Your IBMid is the ID that you use to log in to www.ibm.com.
{: tsCauses}

As an IBM employee, before you can log in to {{site.data.keyword.Bluemix_notm}} by using your IBM intranet ID, you must link your intranet ID with your external IBMid. To link the two IDs, complete the following steps:
{: tsResolve} 

  1. On the [Central Sign-on ![External link icon](../icons/launch-glyph.svg "External link icon")](https://w3-03.sso.ibm.com/tools/cso/index.jsp){: new_window} page, click **My Sign-ons**.
  2. On the My Sign-ons page, click **Link IDs**, and enter your IBMid and password on the {{site.data.keyword.Bluemix_notm}} Sign in page. After that, your intranet ID and IBMid will be automatically linked.
  

<!-- end STAGING ONLY -->

## You have unsaved changes
{: #ts_unsaved_changes}

When you navigate on the app details page, you might be unable to perform any actions and might be prompted to save changes before you can proceed. 

When you try to check your app or services on the app details page, you keep getting the following error message:
{: tsSymptoms} 

`You have unsaved changes in page app_name. Save or cancel the changes.`

When you scroll your mouse over the **INSTANCES** or **MEMORY QUOTA** field on the runtime pane, the values change. This behavior is by design; however, the error message prompts you to save the memory or instance settings before you navigate away from the page. 
{: tsCauses}

Close the message window, and then click the **RESET** button in your runtime pane. 
{: tsResolve} 
  
    
## Automatic failover between {{site.data.keyword.Bluemix_notm}} regions isn't available
{: #ts_failover}

You can't use automatic failover between {{site.data.keyword.Bluemix_notm}} regions. However, you can use a DNS provider that supports failover among multiple IP addresses as a workaround.

When a {{site.data.keyword.Bluemix_notm}} region becomes unavailable, the apps that are running in that region are also unavailable, even if the same apps are running in another {{site.data.keyword.Bluemix_notm}} region.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} doesn't yet provide automatic failover from one region to another.
{: tsCauses}
 
You can use a DNS provider that supports intelligent failover among multiple ID addresses, and manually configure your DNS settings to enable the automatic failover between {{site.data.keyword.Bluemix_notm}} regions. DNS providers with this capability include NSONE, Akamai, Dyn.
{: tsResolve}

When you configure your DNS settings, you must specify the public IP addresses of the {{site.data.keyword.Bluemix_notm}} regions that your apps are running in. To get the public IP address of a {{site.data.keyword.Bluemix_notm}} region, use the `nslookup` command. For example, you can type the following command in a command line window:
```
nslookup stage1.mybluemix.net
```

## Can't add users to an org
{: #ts_adduser}

You can invite more than one user to work under the same organization. You can invite users to your organization only if you are the account owner, or if you are both a manager and a member of the organization.
 
You can't see the **Invite a New User** link in your **Manage Organizations** section. 
{: tsSymptoms}

Only the following {{site.data.keyword.Bluemix_notm}} users can invite users to an organization:
{: tsCauses}
  * The account owner of the organization
  * Organization managers who are also members, not collaborators, of the organization
  
In {{site.data.keyword.Bluemix_notm}}, you can be either a member or a collaborator of an organization:

<dl><dt>Collaborator</dt>
<dd>You are a collaborator of an organization if you already have a {{site.data.keyword.Bluemix_notm}} account, and someone else invites you to the organization.</dd>
<dt>Member</dt>
<dd>You are a member of an organization if you don't have a {{site.data.keyword.Bluemix_notm}} account, but then someone invites you to the organization and you sign up for {{site.data.keyword.Bluemix_notm}} from the invitation.</dd>
</dl>

You can't invite users to your organization if you are a collaborator of the organization, even if you have been assigned as an organization manager.

**Note:** All organization managers, including those who are collaborators of an organization, can add, modify, and remove users that are already in the organization.

If can't invite users to your organization and need a different role to do so, contact your organization manager to change your role. To identify your organization manager, complete the following steps:
{: tsResolve}

  1. Go to the {{site.data.keyword.Bluemix_notm}} Dashboard. From the menu bar, click the **Account** menu item and click **Manage Organizations**.
  2. Go to your organization, and view the information of organization manager on the **USERS** tab.  
  
If you can't invite users because you are a collaborator and not a member, you must delete your previous {{site.data.keyword.Bluemix_notm}} account and then be invited to join the account as a member of the organization. To delete your previous account and join the account as a member, complete the following steps: 

  1. Contact [{{site.data.keyword.Bluemix_notm}} Support ![External link icon](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport){: new_window} to open a support ticket and request that your account be deleted. If you have data that is associated with your old account that you want to save and move to the new account, include this information in your email. 
  2. After your account is deleted, have a user with the organization manager role invite you to the organization as an organization manager. Then, sign up for {{site.data.keyword.Bluemix_notm}} from the invitation. 

## Batch registration of users isn't supported
{: #ts_batchregistration}

When you register users for {{site.data.keyword.Bluemix_notm}}, you must register each user individually.

{{site.data.keyword.Bluemix_notm}} doesn't provide the capability to register multiple users at the same time.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} doesn't support batch registration of users. To register users for {{site.data.keyword.Bluemix_notm}}, you must register each user individually.
{: tsCauses}
 
To register multiple users for {{site.data.keyword.Bluemix_notm}}, complete the following steps for each user:
{: tsResolve}

  1. Click **SIGN UP** in the {{site.data.keyword.Bluemix_notm}} console.
  2. Complete the steps by following the wizard.
    

## {{site.data.keyword.Bluemix_notm}} page can't be loaded
{: #ts_err}

When you use the {{site.data.keyword.Bluemix_notm}} console, you might not be able to load a {{site.data.keyword.Bluemix_notm}} page. Instead, you might see error messages BXNUI0001E or BXNUI0016E.
 
You might see one of the following error messages when you use the {{site.data.keyword.Bluemix_notm}} console:
{: tsSymptoms}

`BXNUI0001E: The page wasn't loaded because Bluemix didn't detect whether a session exists.`

`BXNUI0016E: The apps and services weren't retrieved because a Bluemix page didn't load.`

Complete one or more of the following actions, as necessary:
{: tsResolve}

  * Refresh or restart your browser.
  * Log out of {{site.data.keyword.Bluemix_notm}} and log in again.
  * Use the private browsing mode of your browser. 
  * Clear the cookies and the cache of the browser.
  * Use a different browser. For information about the versions of the browsers that are supported by {{site.data.keyword.Bluemix_notm}}, see [{{site.data.keyword.Bluemix_notm}} Prerequisites ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * If you installed the cf command line interface, enter the `cf apps` command to see whether your app is running.
