---

copyright:
  years: 2016
lastupdated: "2016-09-26"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Troubleshooting
{: #troubleshooting}

You can find the answers to common troubleshooting questions about using {{site.data.keyword.iotinsurance_full}} on {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problem deploying the apps
{: #deployingapps}

You might be unable to deploy the apps for {{site.data.keyword.iotinsurance_short}} if you do not have enough free memory in your {{site.data.keyword.Bluemix_notm}} organization. You can either reduce the memory that your apps use or increase the memory quota for your account.

### What's happening

When you open the {{site.data.keyword.iotinsurance_short}} service, the Deploy function is not enabled, and you cannot deploy any apps.

### Why it's happening

At least 2 GB of free memory must be available in your organization to enable the Deploy function. Trial accounts have a maximum memory quota of 2 GB. If you created services or apps other than {{site.data.keyword.iotinsurance_short}}, your organization does not have enough memory to deploy the {{site.data.keyword.iotinsurance_short}} apps.

### How to fix it

You can either increase the memory quota of your account or reduce the memory that your services and apps use.

  - To increase the memory quota of your account, you can [convert your trial account to a pay account](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

  - To reduce the memory in use quickly, remove all services and apps other than {{site.data.keyword.iotinsurance_short}}. Restart the {{site.data.keyword.iotinsurance_short}} service for the changes to take effect.

  - For paid accounts that have more than 2 GB of total memory, you might be able to avoid removing other apps or services by adjusting the amount of memory that they use. For information, see [Org's memory limit is exceeded](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
