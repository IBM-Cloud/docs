---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-11"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Upgrading and unifying {{site.data.keyword.Bluemix_notm}} and SoftLayer billing accounts
{: #softlayerlink}

If you have a {{site.data.keyword.Bluemix_notm}} trial account and you want to access the Infrastructure dashboard, you must upgrade to a {{site.data.keyword.Bluemix_notm}} Pay-As-You-Go account. You also must upgrade if you want to use other chargeable resources that are not available within a trial account, or your trial account finishes. 

You can unify your existing {{site.data.keyword.Bluemix_notm}} and SoftLayer billing accounts by linking the accounts. When you link your accounts, you are billed through {{site.data.keyword.Bluemix_notm}} for both {{site.data.keyword.Bluemix_notm}} and SoftLayer resources.

**Attention:** A {{site.data.keyword.Bluemix_notm}} subscription account cannot be linked with a SoftLayer account. To access the Infrastructure dashboard you must create a Pay-As-You-Go account, a second account, which is automatically linked with a SoftLayer account. You will then receive two invoices, one for each {{site.data.keyword.Bluemix_notm}} account. Although your infrastructure resources will be invoiced in a separate Pay-As-You-Go account, the resources can be used with apps and services in your subscription account. For example, if you activate a Watson service in your subscription account, you can copy the service credentials and then add the credentials to your bare metal application that is sourced from your Pay-As-You-Go account. 
{:shortdesc}

## Upgrading to a {{site.data.keyword.Bluemix_notm}} Pay-As-You-Go account
{: #upgradetopayg}

When you log in to {{site.data.keyword.Bluemix_notm}} by using a trial account, you cannot access the {{site.data.keyword.Bluemix_notm}} Infrastructure dashboard. If you want your apps to use the infrastructure resources, you must upgrade to a Pay-As-You-Go account.

To upgrade your trial account to a {{site.data.keyword.Bluemix_notm}} Pay-As-You-Go account, complete the following steps:

 1. Click **Account** &gt; **Billing**.
 2. Then, click **Add Credit Card**.
 3. Enter the required billing details. 
 4. Read and accept the terms and conditions for the Pay-As-You-Go account. 
 5. When you are finished, click **Upgrade**. 
 
After you upgrade to a Pay-As-You-Go account, the **Infrastructure** options are listed in the {{site.data.keyword.Bluemix_notm}} **Catalog**. If you use more than the free allowance, you will receive a monthly {{site.data.keyword.Bluemix_notm}} invoice. The invoice will be in United States dollars (USD) and will detail your resource charges. 

## Unifying your {{site.data.keyword.Bluemix_notm}} and SoftLayer accounts
{: #unifyingaccounts}

You can unify your {{site.data.keyword.Bluemix_notm}} and SoftLayer accounts to make use of the combined resources. When you link your {{site.data.keyword.Bluemix_notm}} and Softlayer accounts, you will receive a single {{site.data.keyword.Bluemix_notm}} invoice. If you have an existing {{site.data.keyword.Bluemix_notm}} account, billing through {{site.data.keyword.Bluemix_notm}} for SoftLayer resources takes effect for the new billing cycle that starts after the accounts are linked.

**Important:** All linked accounts in {{site.data.keyword.Bluemix_notm}} must be Pay-As-You-Go accounts. You can create a new Pay-As-You-Go account or link an existing Pay-As-You-Go account. Or, you can link an existing trial account, but it will be upgraded to a Pay-As-You-Go account. Subscription {{site.data.keyword.Bluemix_notm}} accounts cannot be linked.  

After your accounts are linked:

* You must use your IBMid credentials to access both your SoftLayer and your {{site.data.keyword.Bluemix_notm}} accounts.
* Any existing SoftLayer discounts are applied across {{site.data.keyword.Bluemix_notm}} charges. 
* You will receive one invoice in United States dollars (USD).
* You can monitor the usage of your {{site.data.keyword.BluSoftlayer}} resources in the {{site.data.keyword.Bluemix_notm}} user interface. 

**Attention:** After accounts are linked, they cannot be unlinked. 

If you have a SoftLayer account, and you want to link SoftLayer and {{site.data.keyword.Bluemix_notm}} accounts, complete these steps:

 1. From the {{site.data.keyword.slportal}}, click **Link a {{site.data.keyword.Bluemix_notm}} Account**.
 2. Read and accept the terms for linking SoftLayer and {{site.data.keyword.Bluemix_notm}} accounts.
 3. When requested, provide the email address that is associated with your {{site.data.keyword.Bluemix_notm}} account. If you don't have a {{site.data.keyword.Bluemix_notm}} account, provide the email address that you want to use, then follow the instructions to be invited to {{site.data.keyword.Bluemix_notm}} and create an account.

You must be a Master User in the SoftLayer account to link accounts.

After you have linked your accounts, the **Go to {{site.data.keyword.Bluemix_notm}}** link is available in the SoftLayer global header. Clicking this link takes you to the {{site.data.keyword.Bluemix_notm}} login page. In addition, the **SoftLayer** link is now available in the {{site.data.keyword.Bluemix_notm}} header. Clicking the link takes you to the home page of the {{site.data.keyword.slportal}} in a new window.

{{site.data.keyword.Bluemix_notm}} infrastructure offerings are connected to a three-tiered network, segmenting public, private, and management traffic. Infrastructure offerings on a customer's {{site.data.keyword.Bluemix_notm}} account might transfer data between one another across the private network at no cost. Infrastructure offerings, such as bare metal servers, virtual servers, and cloud storage, connect to other applications and services in the {{site.data.keyword.Bluemix_notm}} catalog, such as Watson services, containers, or runtimes, across the public network. Data transfer between those two types of offerings is metered and charged at standard public network bandwidth rates.

## Inviting SoftLayer team members to {{site.data.keyword.Bluemix_notm}}
{: #invite_users}

You can invite your SoftLayer team members to join {{site.data.keyword.Bluemix_notm}} when you link your {{site.data.keyword.Bluemix_notm}} and SoftLayer accounts. Or, you can invite SoftLayer team members later from the {{site.data.keyword.Bluemix_notm}} user interface.
{:shortdesc}

From the {{site.data.keyword.Bluemix_notm}} user interface, you can select to invite all members of your SoftLayer account or you can select individual members. When inviting team members, you must set the {{site.data.keyword.Bluemix_notm}} account role for the invitees. For more information about the different roles in {{site.data.keyword.Bluemix_notm}}, see [User roles](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo).

You must be a Master User in the SoftLayer account to invite team members to the {{site.data.keyword.Bluemix_notm}} account.

To invite team members through {{site.data.keyword.Bluemix_notm}}, complete the following steps:

 1. Click **Account** &gt; **Invite Team Members**.
 2. Click **Add** to authenticate into your SoftLayer account and view a list of team members from your {{site.data.keyword.BluSoftlayer}} account.
 3. Select the team members to invite and click **Send**.
 
The team member receives an email that includes a **Join the organization** link. If the team member does not have an IBMid, the team member is redirected to a registration page. Next, the team member can enter some basic information and create their {{site.data.keyword.Bluemix_notm}} account.

For more information about inviting team members through the {{site.data.keyword.Bluemix_notm}} user interface, see [Inviting team members](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers).

## Switching to  IBMid
{: #ibmid_switch}

Authentication in SoftLayer now uses IBMid to provide a single login for all of {{site.data.keyword.Bluemix_notm}}. Existing SoftLayer accounts are being enabled to switch to IBMid authentication, and a migration wizard will guide you through this switch. 
{:shortdesc}

If you are a master user and do not see a prompt to switch to IBMid in the {{site.data.keyword.slportal}}, [Contact IBM support](https://console.ng.bluemix.net/docs/support/index.html#contacting-support) for help with enabling the feature.

As you begin the switch to IBMid, you can always cancel this switch before completing the process. However, you will continue to be prompted to switch to IBMid the next time that you log in. Each account that you plan to link to a {{site.data.keyword.Bluemix_notm}} account must be owned by a unique IBMid with a unique email address.

To switch your existing SoftLayer username to an IBMid, complete the following steps:

 1. If you selected **Later** in the inital prompt after log in, but decided that you want to begin the switch to IBMid authentication in the current session, go to the Edit User Profile page and click **Switch to IBMid**.
 2. Follow the wizard prompts to create your IBMid. Your IBMid is a unique email address and cannot be changed after it is created. You can update the email associated with your profile later, the default email is set to what you defined for your IBMid. You will receive an email with your registration code indicating you have completed the migration wizard. 
 3. When you receive the email, follow the link or copy the URL into a browser and enter your registration code. The code is valid for 7 days and can be used only once.
 
 
After you switch to IBMid authentication, you can log in to your account only with your IBMid. At the login prompt, click **Log in with IBMid** instead of entering your SoftLayer username and password.
 
When you check out your order as a new customer, you are asked for an email address for your existing IBMid account or to create a new IBMid account. If you create a new IBMid, enter the email address for your new IBMid. The email address is where the invitation email is sent, and it is also the user name for your new IBMid.

### Enabling users to switch to IBMid
{: #link_accounts_resellers}

In some cases, before a user can switch to an IBMid, a reseller or distributor must enable the account to use IBMid authentication. 

 * To enable an existing account with legacy SoftLayer credentials to use IBMid authentication, [Contact IBM support](https://console.ng.bluemix.net/docs/support/index.html#contacting-support) to enable IBMid migration. This must be enabled for each existing end user account that you want to link to a {{site.data.keyword.Bluemix_notm}} account.
 
 * To ensure that new user accounts are created with an IBMid, the `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION`       attribute must be set on the immediate master user account. [Contact IBM support](https://console.ng.bluemix.net/docs/support/index.html#contacting-support) or your vendor to have this set for your accounts.
 
### Linking your user accounts
{: #link_user_accounts}
After your users switch to IBMid authentication, resellers and distributors can link SoftLayer and {{site.data.keyword.Bluemix_notm}} accounts.

**Note:** 
  * The master user of the account that is being linked must be an IBMid.
  * Log in to each end user account as the master user. Go to the user profile page, and click **Switch to IBMid**.
  * Each account that you link to a {{site.data.keyword.Bluemix_notm}} account must be owned by a unique IBMid with a unique email address. Although one IBMid can own multiple SoftLayer accounts, you cannot link the accounts to {{site.data.keyword.Bluemix_notm}} accounts. If one IBMid is the master user for multiple SoftLayer accounts and you want to link those accounts to {{site.data.keyword.Bluemix_notm}} accounts, you must change the master users to be a unique IBMid for each account. Contact [IBM SoftLayer support ![External link icon](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window} to change the master user on a SoftLayer account.
  
Complete the following steps to link each account to a {{site.data.keyword.Bluemix_notm}} account: 

 1. To create a new {{site.data.keyword.Bluemix_notm}} account or to link to an existing {{site.data.keyword.Bluemix_notm}} account, log in to your SoftLayer account as the master user and click the **{{site.data.keyword.Bluemix_notm}}** link. This will give you the opportunity to either create a new {{site.data.keyword.Bluemix_notm}} account or link to an existing {{site.data.keyword.Bluemix_notm}} account. The IBMid that is the master user for the SoftLayer account must be the owner of the Bluemix account you're linking to. Follow the wizard prompts, including adding the users in the SoftLayer account to the {{site.data.keyword.Bluemix_notm}} account. 
 2. After you link the account, inform the end users of the account to migrate to IBMid. End users can then access the Infrastructure, Applications, and Services dashboards in the {{site.data.keyword.Bluemix_notm}} console.
 3. When new users are added to the linked account, you will need to add them to both the SoftLayer account and the {{site.data.keyword.Bluemix_notm}} account in order for them to have access to all the capabilities within the unified console.
 
**Recommendation:** Migrate only the end user accounts to IBMid. Do not migrate brand accounts, which are parent accounts for end user accounts and do not contain any resources. Brand account users that migrate to IBMid lose the ability to log in to the Brand Agent Portal (BAP) portal.

<!--
### Mapping multiple SoftLayer accounts to one IBMid
{: #map_multiple_accounts}

You can associate one IBMid with multiple SoftLayer accounts by using an existing IBMid email address when setting up the account. Only one SoftLayer user for each account can be mapped to the single IBMid. The IBMid must be unique within each SoftLayer account. However, one user with access to multiple SoftLayer accounts can use one IBMid to access multiple SoftLayer accounts.

For example, an IBMid can map to the master user in accounts A and B, and to an additional user in accounts C and D. One of the accounts mapped to that IBMid is the default account.  Usually, the default account is the account that was first mapped to the IBMid. However, you can switch which account is the default account  through an account switching feature in the Customer Portal.

For a user with IBMid access to multiple accounts with two-factor authentication enabled, an appropriate two-factored authentication verification code per account is required during account log in and account switching.
-->


## Using {{site.data.keyword.Bluemix_notm}} services with SoftLayer assets
{: #bluemix_services}

You can easily use API-based public {{site.data.keyword.Bluemix_notm}} services with your SoftLayer assets. All APIs are secure and encrypted so that your data is protected.
{:shortdesc}

For example, have you ever wanted to add cognitive capabilities from Watson to your apps running on bare metal servers from SoftLayer? You can add a service such as {{site.data.keyword.personalityinsightsshort}} to help understand your app's user in four easy steps:

1. Find the service in the {{site.data.keyword.Bluemix_notm}} catalog.
2. Provision an instance of the service with just a few clicks.
3. Set up the service to run with your existing code by copying the service credentials and adding them to your application.
4. After the update to the app, deploy the new version on your SoftLayer infrastructure.

You can gain *Insights and Cognitive* knowledge by calling Watson APIs from your apps in SoftLayer to make them more personalized. Or, use *Data and Analytics* services to tap into high performance analytics for your apps. Or, choose database-as-a-service where you can leave the management to {{site.data.keyword.Bluemix_notm}}.

Modernize your application development by using containers with services like {{site.data.keyword.activedeployshort}} and {{site.data.keyword.deliverypipeline}}. You can then use the {{site.data.keyword.vpn_short}} service to communicate with SoftLayer to connect your container in a private network to the SoftLayer private network. All of the usage charges of the compute resources and services are reflected in your {{site.data.keyword.Bluemix_notm}} bill. 

### API-based {{site.data.keyword.Bluemix_notm}} services
Not all {{site.data.keyword.Bluemix_notm}} services can be used with SoftLayer. The following services can be set up to run with your application code:
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifiershort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**Note:** Not all plans for these services are available. Only the plans enabled for Pay-As-You-Go accounts are available to use with linked accounts. However, you can use any plan for any of these services if you have a separate {{site.data.keyword.Bluemix_notm}} account that is billed separately.

## Billing for {{site.data.keyword.Bluemix_notm}} usage when accounts are linked
{: #bill_usage}

After you've linked your {{site.data.keyword.Bluemix_notm}} and SoftLayer billing accounts, the next billing cycle will be charged in a single {{site.data.keyword.Bluemix_notm}} bill.
{:shortdesc}

Your {{site.data.keyword.Bluemix_notm}} usage cycle is on a calendar month basis, so your account is billed each month on the billing day that was established for your charge agreement. With SoftLayer, your usage cycle begins from when you started with SoftLayer, so you are billed each month on the same day of the month as when you signed up for your SoftLayer account. 

When your accounts are linked, your {{site.data.keyword.Bluemix_notm}} usage will continue to be measured for the current month's cycle, and you will be billed for that usage on a {{site.data.keyword.Bluemix_notm}} invoice. Starting on the first of the next month, your {{site.data.keyword.Bluemix_notm}} and SoftLayer charges will be combined on your {{site.data.keyword.Bluemix_notm}} invoice.

For example, if you linked your accounts on April 16th, you will get a Bluemix invoice for your April usage. Depending on when you linked your accounts, you might get a separate bill for your SoftLayer usage. Your May usage for both SoftLayer and {{site.data.keyword.Bluemix_notm}} will be billed through your {{site.data.keyword.Bluemix_notm}} account.

![Linking Bluemix and SoftLayer accounts summary](images/BluemixSoftLayerBill.svg)

After your bills are linked, your {{site.data.keyword.Bluemix_notm}} invoice will list the different charges for each resource that you have used under the following headings:

* **Bare Metal Servers and Attached Services**
* **Virtual Servers and Attached Services**
* **Unattached Services**

For information about how to view {{site.data.keyword.Bluemix_notm}} usage, see [Viewing usage details](https://console.ng.bluemix.net/docs/pricing/index.html#usage).

