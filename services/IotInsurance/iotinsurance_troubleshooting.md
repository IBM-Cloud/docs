---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iotinsurance_short}} troubleshooting
{: #ts}

Here are the answers to common troubleshooting questions about using {{site.data.keyword.iotinsurance_full}} on {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problem deploying apps
{: #deployingapps}
You might be unable to deploy the apps for {{site.data.keyword.iotinsurance_short}} if you do not have enough free memory in your {{site.data.keyword.Bluemix_notm}} organization. You can either reduce the memory that your apps use or increase the memory quota for your account.
{:shortdesc}

When you open the {{site.data.keyword.iotinsurance_short}} service, the Deploy function is not enabled, and you cannot deploy any apps.
{: tsSymptoms}

At least 2 GB of free memory must be available in your organization to enable the Deploy function. Trial accounts have a maximum memory quota of 2 GB. If you created services or apps other than {{site.data.keyword.iotinsurance_short}}, your organization does not have enough memory to deploy the {{site.data.keyword.iotinsurance_short}} apps.
{: tsCauses}

You can either increase the memory quota of your account or reduce the memory that your services and apps use.
- To increase the memory quota of your account, you can [convert your trial account to a pay account](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).
- To reduce the memory in use quickly, remove all services and apps other than {{site.data.keyword.iotinsurance_short}}. Restart the {{site.data.keyword.iotinsurance_short}} service for the changes to take effect.
- For paid accounts that have more than 2 GB of total memory, you might be able to avoid removing other apps or services by adjusting the amount of memory that they use. For information, see [Org's memory limit is exceeded](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
{: tsResolve}

## Performance issues
{: #performance_issues}

During periods of peak activity, you might experience slow performance.
{:shortdesc}

Busy systems that make frequent API calls might experience delays in response times.
{: tsSymptoms}

By default, {{site.data.keyword.iotinsurance_short}} deploys a trial version of {{site.data.keyword.cloudantfull}}. This version limits the number of API calls that can be made per second.
{: tsCauses}

Upgrade to the standard version of {{site.data.keyword.cloudant}}.
{: tsResolve}

## Getting help and support for {{site.data.keyword.iotinsurance_short}}
{: #gettinghelp}

If you have problems or questions when using {{site.data.keyword.iotinsurance_full}}, you can check {{site.data.keyword.Bluemix_notm}}, or get help by searching for information or by asking questions through a forum. You can also open a support ticket.

- You can check whether {{site.data.keyword.Bluemix_notm}} is available by going to the [Bluemix status page ![External link icon](../../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#status){:new_window}.

- You can review the forums to see whether other users ran into the same problem. When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
- If you have technical questions about developing or deploying an app with {{site.data.keyword.iotinsurance_short}}, post your question on [Stack Overflow ![External link icon](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "iot-for-insurance".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
- For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window} forum. Include the  "iot-for-insurance" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.

- If you still can't resolve the problem, you can open an IBM support ticket. For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](../support/index.html#contacting-support).
