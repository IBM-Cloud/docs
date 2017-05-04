---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Linking your Bluemix and SoftLayer accounts
{: #unifyingaccounts}

You can link your {{site.data.keyword.Bluemix_notm}} and SoftLayer accounts to make use of the combined resources. When you link your {{site.data.keyword.Bluemix_notm}} and Softlayer accounts, you will receive a single {{site.data.keyword.Bluemix_notm}} invoice. If you have an existing {{site.data.keyword.Bluemix_notm}} account, billing through {{site.data.keyword.Bluemix_notm}} for SoftLayer resources takes effect for the new billing cycle that starts after the accounts are linked.

**Important:** All linked accounts in {{site.data.keyword.Bluemix_notm}} must be Pay-As-You-Go accounts. You can create a new Pay-As-You-Go account, link an existing Pay-As-You-Go account, or link an existing trial account (which will then be upgraded to a Pay-As-You-Go account). You cannot link subscription {{site.data.keyword.Bluemix_notm}} accounts.

You must be a master user in the SoftLayer account to link accounts.

When your accounts are linked:

* You must use your IBMid credentials to access both your SoftLayer and your {{site.data.keyword.Bluemix_notm}} accounts.
* Any existing SoftLayer discounts are applied across {{site.data.keyword.Bluemix_notm}} charges.
* You will receive one invoice in United States dollars (USD).
* You can monitor the usage of your {{site.data.keyword.BluSoftlayer}} resources in the {{site.data.keyword.Bluemix_notm}} console.

**Attention:** After you link your accounts, they cannot be unlinked.  

As a master user, complete the following steps to link your {{site.data.keyword.Bluemix_notm}} and SoftLayer accounts:

 1. From the {{site.data.keyword.slportal}}, click **Link a {{site.data.keyword.Bluemix_notm}} Account**.
 2. Read and accept the terms for linking SoftLayer and {{site.data.keyword.Bluemix_notm}} accounts.
 3. When requested, provide the email address that is associated with your {{site.data.keyword.Bluemix_notm}} account. If you don't have a {{site.data.keyword.Bluemix_notm}} account, provide the email address that you want to use, then follow the instructions to be invited to {{site.data.keyword.Bluemix_notm}} and create an account.

After you link your accounts, **Go to {{site.data.keyword.Bluemix_notm}}** is available in the SoftLayer console menu bar. Clicking this link takes you to the {{site.data.keyword.Bluemix_notm}} login page.

## Billing for {{site.data.keyword.Bluemix_notm}} usage when accounts are linked
{: #bill_usage}

After you've linked your {{site.data.keyword.Bluemix_notm}} and SoftLayer billing accounts, the next billing cycle will be charged in a single {{site.data.keyword.Bluemix_notm}} bill.
{:shortdesc}

Your {{site.data.keyword.Bluemix_notm}} usage cycle is on a calendar month basis, so your account is billed each month on the billing day that was established for your charge agreement. With SoftLayer, your usage cycle begins from when you started with SoftLayer, so you are billed each month on the same day of the month as when you signed up for your SoftLayer account. 

When your accounts are linked, your {{site.data.keyword.Bluemix_notm}} usage will continue to be measured for the current month's cycle, and you will be billed for that usage on a {{site.data.keyword.Bluemix_notm}} invoice. Starting on the first of the next month, your {{site.data.keyword.Bluemix_notm}} and SoftLayer charges will be combined on your {{site.data.keyword.Bluemix_notm}} invoice.

For example, if you linked your accounts on 16 April 2017, you will get a Bluemix invoice for your April usage. Depending on when you linked your accounts, you might get a separate bill for your SoftLayer usage. Your May usage for both SoftLayer and {{site.data.keyword.Bluemix_notm}} will be billed through your {{site.data.keyword.Bluemix_notm}} account.

![Linking Bluemix and SoftLayer accounts summary](/docs/pricing/BluemixSoftLayerBill.svg)

After your bills are linked, your {{site.data.keyword.Bluemix_notm}} invoice lists the different charges for each resource that you have used.
