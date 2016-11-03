---

 

copyright:

  years: 2016
lastupdated: "2016-11-03"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Upgrading and unifying {{site.data.keyword.Bluemix_notm}} and SoftLayer billing accounts
{: #softlayerlink}

If you have a {{site.data.keyword.Bluemix_notm}} trial account and you want to access the Infrastructure dashboard, you must upgrade to a {{site.data.keyword.Bluemix_notm}} Pay-As-You-Go account. You also must upgrade if you want to use other chargeable resources that are not available within a trial account, or your trial account finishes. 

You can unify your existing {{site.data.keyword.Bluemix_notm}} and SoftLayer billing accounts by linking the accounts. When you link your accounts, you are billed through {{site.data.keyword.Bluemix_notm}} for both {{site.data.keyword.Bluemix_notm}} and SoftLayer resources.
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

## Credits for {{site.data.keyword.Bluemix_notm}} usage when accounts are linked
{: #slcredit}

When you link your {{site.data.keyword.Bluemix_notm}} account from your SoftLayer account, you receive a $200.00 credit that you can use within {{site.data.keyword.Bluemix_notm}} only. The credit must be used within 30 days of linking the accounts.

For information about how to view the credits and expiration date, see [Viewing credits](https://console.ng.bluemix.net/docs/pricing/index.html#credits).

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

Authentication in SoftLayer now uses IBMid to provide a single login for {{site.data.keyword.Bluemix_notm}}. If you have an existing SoftLayer account, you can switch to an IBMid. A migration wizard will guide you through this switch. 
{:shortdesc}

After you begin the switch to IBMid, as long as you do not complete the process, you can cancel it. But, you will still be prompted to switch to IBMid the next time that you log in.

To begin the switch of your existing SoftLayer username to an IBMid, complete the following steps:

 1. In the {{site.data.keyword.slportal}}, go to the Edit User Profile page and click **Switch to IBMid**.
 2. Follow the migration wizard prompts to create your IBMid. Once you create your IBMid, you cannot change the ID, which is an email address. You can update the email associated with your profile, but by default that value is set as what you defined for your IBMid. After you complete the wizard, an email is sent to you.
 3. When you receive the email, follow the link or copy the URL into a browser and enter your registration code. The code is good for 7 days and it is a one-time use only code.  After it is used, it cannot be used again.
 After you set up the IBMid to SoftLayer user link, you can log in to your account only with IBMid.  On the login dialog, you must use the **Log in with IBMid** button instead of entering your SoftLayer username and password.
 
If you are a new customer, you are asked for an email address for your existing IBMid account, or to create a new IBMid account, when you check out your order. 

### Mapping multiple SoftLayer accounts to one IBMid
{: #map_multiple_accounts}

You can associate one IBMid with multiple SoftLayer accounts by using an existing IBMid email address when setting up the account. Only one SoftLayer user for each account can be mapped to the single IBMid. The IBMid must be unique within each SoftLayer account. However, one user with access to multiple SoftLayer accounts can use one IBMid to access multiple SoftLayer accounts.

For example, an IBMid can map to the master user in accounts A and B, and to an additional user in accounts C and D. One of the accounts mapped to that IBMid is the default account.  Usually, the default account is the account that was first mapped to the IBMid. However, you can switch which account is the default account  through an account switching feature in the Customer Portal.

For a user with IBMid access to multiple accounts with two-factor authentication enabled, an appropriate two-factored authentication verification code per account is required during account log in and account switching.

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

Modernize your application development by using containers with services like {{site.data.keyword.activedeployshort}} and {{site.data.keyword.deliverypipeline}}. You can then use the {{site.data.keyword.vpn_short}} service to tunnel back to SoftLayer to connect your container in a private network to the SoftLayer private network. All of the usage charges of the compute resources and services are reflected in your {{site.data.keyword.Bluemix_notm}} bill. 

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
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
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

