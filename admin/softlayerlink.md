---



copyright:

  years: 2016, 2017
lastupdated: "2017-06-06"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Switching to IBMid
Authentication in SoftLayer now uses an IBMid to provide a single login for all of {{site.data.keyword.Bluemix_notm}}. Existing SoftLayer accounts are being enabled to switch to IBMid authentication. A migration wizard guides you through this switch. 
{:shortdesc}

When you begin the process to switch to an IBMid, you can always cancel the switch before you complete the process. However, each time that you log in, the prompt to switch to an IBMid is displayed. Each SoftLayer account that you plan to link to a {{site.data.keyword.Bluemix_notm}} account must be owned by a unique IBMid with a unique email address.

To switch your existing SoftLayer account to an IBMid, complete the following steps:
1. Log in to your SoftLayer account, and click **OK** when the prompt to switch to an IBMid is displayed.

   If you are a master user and a prompt to switch to an IBMid is not displayed in the {{site.data.keyword.slportal}}, [Contact IBM support](/docs/support/index.html#contacting-support) for help.
  
   If you previously logged in and you clicked **Later** in the prompt, but you want to switch to IBMid authentication in the current session, go to the Edit User Profile page and click **Switch to IBMid**.

2. Follow the wizard prompts to create your IBMid. 

   Enter an email address that is not currently is use by any IBMid. This email address is used as the user name for the new IBMid, and it's where your registratin code is sent after the IBMid is created. You can update the email address that is associated with the IBMid later on, but you can't change the user name.

3. When you receive your registration code, click the link in the email or copy the URL into a browser and enter your registration code.

   The registration code is valid for seven days and you can use it only once.
  
4. After you submit your registration code, use your IBMid to log in to the {{site.data.keyword.slportal}}.

   At the Account Login prompt, go to the **IBMid Account Login** section and click **Log in with IBMid**. Do not use the **Username** and **Password** fields that you used previously with your SoftLayer ID.

If you are a new customer, you're asked for your existing IBMid or to create a new IBMid when you check out your order. 
  * To use an existing IBMid, enter the user name or the email address of the IBMid it if is unique (that is, it's not shared across multiple IBMids).
  
  * To create a new IBMid, enter an email address that is not currently in use by any IBMid. This email address is the user name for the IBMid, and it's where your registration code is sent after the IBMid is created. You can update the email address that's associated with the IBMid later on, but you can't change the user name. 
  
To resolve any problems with logging in with your IBMid, see [Troubleshooting for accessing Bluemix](/docs/troubleshoot/ts_accessing.html#accessing).

## Enabling user accounts for IBMid authentication
{: #link_accounts_resellers}

In some cases, before a user can switch to an IBMid, a reseller or distributor must enable the account to use IBMid authentication. 

  * IBMid authentication must be enabled for each existing user account that you want to link to a Bluemix account. Then, each user must complete the process to switch to an IBMid by using the migration wizard, as described in the previous section. Contact [IBM support](/docs/support/index.html#contacting-support) to enable an existing SoftLayer account to use IBMid authentication. 
  
  * To ensure new user accounts are created with an IBMid, the `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION` attribute must be set on the immediate master user account. Contact [IBM support](/docs/support/index.html#contacting-support) or your vendor to set the attribute for your accounts.  

## Linking IBMid user accounts
{: #link_user_accounts}

After your user accounts switch to IBMid authentication, resellers and distributors can link SoftLayer and {{site.data.keyword.Bluemix_notm}} accounts to make use of combined infrastructure and platform resources.

**Note**:
  * The master user of the account that's being linked must have an IBMid.
  * Each user account that you link to a {{site.data.keyword.Bluemix_notm}} account must be owned by a unique IBMid with a unique email address. Even though a single IBMid can own multiple SoftLayer accounts, you must change the master user to be a unique IBMid for each account. Contact [IBM SoftLayer support ![External link icon](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window} to change the master user of a SoftLayer account.
  * When you add new users to a linked account, you must add them to both the SoftLayer account and the {{site.data.keyword.Bluemix_notm}} account so that they can access all the capabilities of the unified console. 
  
Complete the following steps to link each account to a {{site.data.keyword.Bluemix_notm}} account:
1. To link to an existing {{site.data.keyword.Bluemix_notm}} account or to create a new one, log in to your SoftLayer account as the master user and click the {{site.data.keyword.Bluemix_notm}} link.

   The IBMid that is the master user of the SoftLayer account must be the owner of the {{site.data.keyword.Bluemix_notm}} account you're linking to. 
   
2. Follow the wizard prompts, including adding the users in the SoftLayer account to the {{site.data.keyword.Bluemix_notm}} account.
3. After you link the account, inform the end user of each account to migrate to IBMid by following the procedure described in the previous section.

**Recommendation**: Migrate only end user accounts to IBMid. Do not migrate brand accounts, which are parent accounts for end user accounts and do not contain any resources. Brand account users that migrate to IBMid lose the ability to log in to the Brand Agent Portal (BAP).  
  
