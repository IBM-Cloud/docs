---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# FAQ {: #faq}

*Last updated: 19 October 2016*
{: .last-updated}

This FAQ provides answers to common questions about the {{site.data.keyword.objectstorageshort}} service.
{: shortdesc}


## What accounts and payment plans can I use for {{site.data.keyword.objectstorageshort}}? {: #account-payment}

The {{site.data.keyword.objectstorageshort}} service offers two plan options, Free and Standard. [Pricing](https://console.ng.bluemix.net/pricing/) varies depending on the chosen plan.

<table>
  <tr>
    <th> Free plan </th>
    <th> Standard plan </th>
  </tr>
  <tr>
    <td> Allows only one service instance to exist in a {{site.data.keyword.Bluemix_notm}} organization at a time </td>
    <td> Unlimited service instances </td>
  </tr>
  <tr>
    <td> Available to everyone </td>
    <td> Available only to {{site.data.keyword.Bluemix_notm}} paid accounts and IBM internal users </td>
  </tr>
  <tr>
    <td> Free </td>
    <td> Pay-as-you-go or subscription payment plans </td>
  </tr>
  <tr>
    <td> Includes an introductory 5 GB storage usage limit </td>
    <td> Unlimited storage </td>
  </tr>
</table>

Table 1: Comparison of Free and Standard plans

**Attention**: Users working with a {{site.data.keyword.Bluemix_notm}} trial account are able to use the Free plan. After the time in your trial expires, the associated {{site.data.keyword.objectstorageshort}} service instance will be disabled, meaning that you will be unable to access the storage account. After 30 days, your {{site.data.keyword.Bluemix_notm}} account will be purged and all data deleted. To avoid data loss, upgrade to a [Paid {{site.data.keyword.Bluemix_notm}} account](https://new-console.ng.bluemix.net/docs/admin/account.html) as soon as possible.

## How do I change my plan? {: #changeplan}  
Instances that are created through the Beta or on the Free plan can be upgraded to the Standard plan. The associated organization must be a {{site.data.keyword.Bluemix_notm}} paid account. Trial accounts with Object Storage instances cannot be upgraded to the Standard plan, and instances on the Standard plan cannot be downgraded to other plans. When you upgrade, your service instance and customer data are moved to the new plan.

To upgrade:
1.	In the {{site.data.keyword.objectstorageshort}} user interface, click **Plan**.
2.	Select **Standard** as the new plan and then click **Save**.

You can also [change your payment plan](../../pricing/index.html#changing) by using the command line interface.

## How will I be charged and billed for my use of {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

The {{site.data.keyword.objectstorageshort}} service charges only for what you use.  There are no set-up fees or commitments to begin using the service. You are not charged for API requests or inbound data network traffic.

{{site.data.keyword.objectstorageshort}} is billed based on your storage usage within the billing cycle. This includes all object data in containers that you created within your {{site.data.keyword.Bluemix_notm}} organization.

An Outbound Data Transfer charge applies whenever data is read from any of your object containers over the public network. All bandwidth that is consumed in the billing cycle is billed as Public Outbound Bandwidth.

At the end of the billing cycle, {{site.data.keyword.Bluemix_notm}} automatically bills you for usage during that billing period. You can view your charges for the current billing period via {{site.data.keyword.Bluemix_notm}} reporting.
