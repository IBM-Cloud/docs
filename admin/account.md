---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing your {{site.data.keyword.Bluemix_notm}} account
{: #mngacct}

Go to the **Account** link to set notifications, view your account usage, or view your bill.
{:shortdesc}

## Signing up for {{site.data.keyword.Bluemix_notm}}
{: #signup}

You can sign up for a {{site.data.keyword.Bluemix_notm}} account by using an existing IBMid, by creating a new IBMid, or by using a federated ID. A federated ID is an ID within a company's domain that has been registered with IBM so that the domain and user credentials can be used to access IBM web applications.  

A federated ID can be used to sign up for {{site.data.keyword.Bluemix_notm}} only if your company has already worked with IBM to register.  Registering a company's domain with IBM enables users to log in to IBM products and services by using their existing company user credentials. Authentication is then handled by your company's identity provider. When you log in to {{site.data.keyword.Bluemix_notm}} with a federated ID, you are prompted to log in through your company's login page. For information about requesting to register your company or organization's domain with IBM, or for more information about the process, see [IBMid Enterprise Federation Adoption Guide ![External link icon](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}. An IBM sponsor, such as an offering advocate or client advocate, is required when you request to register federated IDs.

| Sign up methods | Details |    
|-----------------|---------|
|Existing IBMid | If you already have an IBMid, sign up for {{site.data.keyword.Bluemix_notm}} with your existing credentials that you use for other IBM products and services. You are required to enter a phone number when signing up. |
|New IBMid | If you don't yet have an IBMid, you can select to create one. The IBMid enables you to use one login user name for all IBM products and services that you use, including {{site.data.keyword.Bluemix_notm}}. You are required to enter your personal information including first and last name, phone number, and password for the new credentials. You can use this IBMid to log in when using other IBM products and services.  |
|Federated ID | If your company has requested to register the user credentials from your company's domain with IBM, you can sign up for {{site.data.keyword.Bluemix_notm}} by using the credentials that you already use for your company's login. You are required to enter a phone number when signing up. |
{:caption="Table 1. Sign up methods" caption-side="top"}

## Setting notifications
{: #notifications}

Click **Account** &gt; **Notifications** to set up general account and spending notifications. Spending notifications are available only for Subscription and Pay-As-You-Go {{site.data.keyword.Bluemix_notm}} account owners.

You can set platform email notifications for {{site.data.keyword.Bluemix_notm}} incidents and planned maintenance, and you can set spending notifications that alert you when your account is close to the spending threshold that you specified. Complete the following tasks to set different notification types for your account.

### Setting platform notifications

Click **Account** &gt; **Notifications** &gt; **Platform** to set email notifications for {{site.data.keyword.Bluemix_notm}} incidents and planned maintenance. You can select or clear each option to enable or disable the email notification.

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### Setting spending notifications
{: #spendingnotifications}

If you are a Subscription or Pay-As-You-Go {{site.data.keyword.Bluemix_notm}} account owner, you can set up email spending notifications. Set notifications for total account, runtime, container, and service spending, as well as spending for individual services, excluding third-party services. You receive notifications when you reach 80%, 90%, and 100% of the spending thresholds that you specify. You can edit each spending notification at any time as your needs change.

Complete the following steps to set up email notifications for spending limits:

<ol>
<li>Click **Account** &gt; **Notifications** &gt; **Spending**.</li>
<li>Enter a numeric value to set the spending threshold for triggering a notification for each type of notification:<br />
<ul>
<li>Total account</li>
<li>Total runtime</li>
<li>Total services</li>
<li>Total container</li>
<li>Spending for a specific service</li>
</ul>
</li>
<li>When you are finished, click **Save**.</li>
</ol>

**Note**: If you have a trial account, you can upgrade to a Subscription or Pay-As-You-Go account to set spending limits. For more information about Pay-As-You-Go and Subscription accounts, see [How you are billed](/docs/pricing/index.html#pay-accounts).

## Viewing usage
{: #acctusage}

As an account owner or a billing manager for an org, you can use the Usage Dashboard page to see the real-time charges for the runtimes, containers, services, and support that are used per month in your organizations. You can see the runtime GB-hours and service consumption in all regions, or you can select to see a particular region.

To open the Usage Dashboard page, click **Account** &gt; *your_account_name* &gt; **Usage Dashboard**. Billing managers can see the details for only the organizations in which they are billing managers.

The account owner is charged for the total usage that is incurred across all organizations at the end of each billing cycle. As an account owner, you can filter the usage summary by region and organization. You can also click a particular month to see the usage for that month. Select **All Organizations** from the **Organization** list to see the usage for all organizations in the account.

## Updating billing information
{: #account_billing}

As the account owner, you can edit, add, or remove saved credit card information that is associated with your {{site.data.keyword.Bluemix_notm}} account. Click **Account** &gt; *your_account_name* &gt; **Billing**.

If you have a SoftLayer account linked with your {{site.data.keyword.Bluemix_notm}} account, see [Billing for {{site.data.keyword.Bluemix_notm}} usage when accounts are linked](/docs/admin/softlayerlink.html#bill_usage) for more information about how you are billed.
