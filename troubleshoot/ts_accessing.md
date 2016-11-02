---

copyright:
  years: 2015, 2016
  
lastupdated: "2016-10-23"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Troubleshooting for accessing {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


General problems with accessing {{site.data.keyword.Bluemix}} might include a user that is unable to log in to {{site.data.keyword.Bluemix_notm}}, an account that is stuck in a pending state, and so on. However, in many cases, you can recover from these problems by following a few easy steps. 
{:shortdesc}

## Unable to log in to {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

You must have a valid {{site.data.keyword.Bluemix_notm}} account to log in.


When you try to log in to {{site.data.keyword.Bluemix_notm}}, you see one of the following error messages: 
{: tsSymptoms} 

 * From the Customer Portal
  
   `You have reached this page because your authentication was successful, however, this IBMid is not associated with any IBM Cloud accounts. If you believe this to be in error, contact your Account Owner or Master User.`

 * From the {{site.data.keyword.Bluemix_notm}} console
  
  `You have reached this page because your authentication was successful, however, this IBMid is not associated with any  {{site.data.keyword.Bluemix_notm}} accounts.`


One of the most likely reasons for getting this error message is that you do not have a {{site.data.keyword.Bluemix_notm}} account created yet or you need to switch to IBMid authentication. 
{: tsCauses} 
 

Follow the sign up process to create a {{site.data.keyword.Bluemix_notm}} account or contact your master user or account administrator for switching to IBMid. 
{: tsResolve}

Depending on how your account is set up, some of these log in options might apply to you: 
 * SoftLayer users with SoftLayer IDs must log in through the [Customer Portal](https://control.softlayer.com).
 * SoftLayer users with an IBMid and with or without a linked Bluemix account can log in through the [Customer Portal](https://control.softlayer.com) to open the SoftLayer Customer Portal or through the [Bluemix console](https://console.{DomainName}) to open the Infrastructure dashboard. 
 * Bluemix users without a linked SoftLayer account must log in through the Bluemix console.
 * Bluemix users with a linked SoftLayer account can log in through the [Bluemix console](https://console.{DomainName}) or the [Customer Portal](https://control.softlayer.com).
 

## Password is invalid
{: #ts_logintobm}

You must have a valid IBMid to log in to the {{site.data.keyword.Bluemix_notm}} console.

When you try to log in to {{site.data.keyword.Bluemix_notm}}, you see the following error message: 
{: tsSymptoms} 

`The password that you entered is not correct.`

The IBMid and password that you use to log in to {{site.data.keyword.Bluemix_notm}} is invalid.
{: tsCauses} 
 
To get a valid IBMid and password, go to the My IBM profile page, then complete one of the following steps:
{: tsResolve}
  * If you have already registered for an IBMid and you want to check whether your ID and password are valid, click **Log in** and enter your IBMid and password on the Log in page. If you have forgotten your password, click **Forgot your password** on the Log in page to reset your password. If you have forgotten your IBMid or continue to have problems with your password, contact the Worldwide IBM Registration Help Desk for help. 
  * If you don't have an IBMid, click **Register** to register for an IBMid and password. 



## Cannot log in with a Softlayer username
{: #ts_softlayer_username}

You must have a valid IBMid and password to log in to {{site.data.keyword.Bluemix_notm}}.


When you try logging in to the {{site.data.keyword.Bluemix_notm}} console with your Softlayer username, you receive the following message: 
{: tsSymptoms} 

`We didn't recognize this IBMid or email.`

You must have an IBMid to log in to use the Infrastructure dashboard in the Bluemix console.
{: tsCauses} 
 
If you are a SoftLayer user who is using a SoftLayer ID, you must switch to IBMid authentication in the Customer Portal within each account that you have access to before you are able to log in by using IBMid authentication. 

Contact your master user or account administrator for switching to IBMid. 
{: tsResolve}



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

  
    
## Automatic failover between {{site.data.keyword.Bluemix_notm}} regions is not available
{: #ts_failover}

You are unable to use automatic failover between {{site.data.keyword.Bluemix_notm}} regions. However, you can use a DNS provider that supports failover among multiple IP addresses as a workaround.
 

When a {{site.data.keyword.Bluemix_notm}} region becomes unavailable, the apps that are running in that region are also unavailable, even if the same apps are running in another {{site.data.keyword.Bluemix_notm}} region.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}} does not yet provide automatic failover from one region to another.
{: tsCauses}

 
You can use a DNS provider that supports intelligent failover among multiple ID addresses, and manually configure your DNS settings to enable the automatic failover between {{site.data.keyword.Bluemix_notm}} regions. DNS providers with this capability include NSONE, Akamai, Dyn.
{: tsResolve}

When you configure your DNS settings, you must specify the public IP addresses of the {{site.data.keyword.Bluemix_notm}} regions that your apps are running in. To get the public IP address of a {{site.data.keyword.Bluemix_notm}} region, use the `nslookup` command. For example, you can type the following command in a command line window:
```
nslookup stage1.mybluemix.net
```



## Account is pending
{: #ts_accntpding}

If your account is pending, you cannot log in to {{site.data.keyword.Bluemix_notm}}.

 
After you register for a {{site.data.keyword.Bluemix_notm}} trial account, you might not be able to log in to {{site.data.keyword.Bluemix_notm}}. Instead, you see the following message:
{: tsSymptoms}

<code>Your account is pending. Please wait up to 24 hours for email confirmation and also check your spam folder. If you still have not received your email confirmation, contact <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix Support</a>.</code>


After you register for a {{site.data.keyword.Bluemix_notm}} trial account, you receive a confirmation email. You must click the link that is in the confirmation email to complete the registration process.
{: tsCauses} 

The confirmation email is sent to the email address that you provided. Check your inbox and your junk mail folder. If you haven't received the confirmation email, contact [{{site.data.keyword.Bluemix_notm}} Support](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



## Unable to add users to an org
{: #ts_adduser}

You can invite more than one user to work under the same organization. You can invite users to your organization only if you are the account owner, or if you are both a manager and a member of the organization.
 

You cannot see the **Invite a New User** link in your **Manage Organizations** section. 
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


You cannot invite users to your organization if you are a collaborator of the organization, even if you have been assigned as an organization manager.

**Note:** All organization managers, including those who are collaborators of an organization, can add, modify, and remove users that are already in the organization.

 

If you are unable to invite users to your organization and need a different role to do so, contact your organization manager to change your role. To identify your organization manager, complete the following steps:
{: tsResolve}

  1. Go to the {{site.data.keyword.Bluemix_notm}} Dashboard. From the menu bar, click the **Support** menu item and click **Manage Organizations**.
  2. Go to your organization, and view the information of organization manager on the **USERS** tab.  
  
If you are unable to invite users because you are a collaborator and not a member, you must delete your previous {{site.data.keyword.Bluemix_notm}} account and then be invited to join the account as a member of the organization. To delete your previous account and join the account as a member, complete the following steps: 

  1. Contact [{{site.data.keyword.Bluemix_notm}} Support](http://ibm.biz/bluemixsupport){: new_window} to open a support ticket and request that your account be deleted. If you have data that is associated with your old account that you want to save and move to the new account, include this information in your email. 
  2. After your account is deleted, have a user with the organization manager role invite you to the organization as an organization manager. Then, sign up for {{site.data.keyword.Bluemix_notm}} from the invitation. 




## Batch registration of users is not supported
{: #ts_batchregistration}

When you register users for {{site.data.keyword.Bluemix_notm}}, you must register each user individually.
 

{{site.data.keyword.Bluemix_notm}} does not provide the capability to register multiple users at the same time.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} doesn't support batch registration of users. To register users for {{site.data.keyword.Bluemix_notm}}, you must register each user individually.
{: tsCauses}
 

To register multiple users for {{site.data.keyword.Bluemix_notm}}, you must complete the following steps for each user:
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

 
You can complete one or more of the following actions as necessary:
{: tsResolve}

  * Refresh or restart your browser.
  * Log out of {{site.data.keyword.Bluemix_notm}} and log in again.
  * Use the private browsing mode of your browser. 
  * Clear the cookies and the cache of the browser.
  * Use a different browser. For information about the versions of the browsers that are supported by {{site.data.keyword.Bluemix_notm}}, see [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * If you have installed the cf command line interface, enter the `cf apps` command to see whether your application is running.
  
  
  
  
  

