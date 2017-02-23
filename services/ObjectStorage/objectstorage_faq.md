---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-23"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# FAQ {: #faq}

This FAQ provides answers to common questions about the {{site.data.keyword.objectstorageshort}} service.
{: shortdesc}


## What accounts and payment plans can I use for {{site.data.keyword.objectstorageshort}}? {: #account-payment}

The {{site.data.keyword.objectstorageshort}} service offers two plan options, Free and Standard. [Pricing](https://www.ibm.com/cloud-computing/bluemix/pricing/) varies depending on the chosen plan.

<table>
<caption> Table 1. Comparison of Free and Standard plans </caption>
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

**Attention**: Users working with a {{site.data.keyword.Bluemix_notm}} trial account are able to use the Free plan. After the time in your trial expires, the associated {{site.data.keyword.objectstorageshort}} service instance will be disabled, meaning that you will be unable to access the storage account. After 30 days, your {{site.data.keyword.Bluemix_notm}} account will be purged and all data deleted. To avoid data loss, upgrade to a [Paid {{site.data.keyword.Bluemix_notm}} account](/docs/admin/account.html) as soon as possible.

## How do I change my plan? {: #changeplan}  
Instances that are created through the Beta or on the Free plan can be upgraded to the Standard plan. The associated organization must be a {{site.data.keyword.Bluemix_notm}} paid account. Trial accounts with Object Storage instances cannot be upgraded to the Standard plan, and instances on the Standard plan cannot be downgraded to other plans. When you upgrade, your service instance and customer data are moved to the new plan.

To upgrade:
1.	In the {{site.data.keyword.objectstorageshort}} user interface, click **Plan**.
2.	Select **Standard** as the new plan and then click **Save**.

You can also [change your payment plan](/docs/pricing/index.html#changing) by using the command line interface.

## How will I be charged and billed for my use of {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

The {{site.data.keyword.objectstorageshort}} service charges only for what you use.  There are no fees or commitments to begin using the service. You are not charged for API requests or inbound data network traffic.

{{site.data.keyword.objectstorageshort}} is billed based on your storage usage within the billing cycle. This includes all object data in containers that you created within your {{site.data.keyword.Bluemix_notm}} organization.

An Outbound Data Transfer charge applies whenever data is read from any of your object containers over the public network. All bandwidth that is consumed in the billing cycle is billed as Public Outbound Bandwidth.

At the end of the billing cycle, {{site.data.keyword.Bluemix_notm}} automatically bills you for usage during that billing period. You can view your charges for the current billing period via {{site.data.keyword.Bluemix_notm}} reporting.

## Are my {{site.data.keyword.Bluemix_notm}} region and my storage region the same thing? {: #region}

The {{site.data.keyword.objectstorageshort}} service supports the Dallas and London storage regions. These storage regions are independent of the {{site.data.keyword.Bluemix_notm}} region, such as US-South and United Kingdom, in which the {{site.data.keyword.objectstorageshort}} service instance is created. If you create an instance in the US-South {{site.data.keyword.Bluemix_notm}} region, you can read and write data to either the Dallas or London storage region. The storage region defaultsbased on your {{site.data.keyword.Bluemix_notm}} region. You can switch regions by selecting another region in from the drop-down list in the UI.
