---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Logging for CF apps in Dedicated and Local
{: #hybrid_apps_logs_ov}

In {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}}, Cloud Foundry apps come with built-in logging. You can review the data that is collected from your apps on the {{site.data.keyword.Bluemix_notm}} console.
{:shortdesc}

Cloud Foundry apps use Cloud Foundry loggregator to monitor and forward logs from outside of the app. You don't need to install agents inside of the app.

## Hardware requirements


| **Requirement** |    **1 node**     | **3 nodes for high availability** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Memory | 80 GB | 240 GB |
| Local storage | 2.98 TB | 8.94 TB |
{: caption="Table 2. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

## Setup

In {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}}, logs are active for all apps by default. To view information about reading standard logs, see [Logging for apps running on Cloud Foundry](../logging_cf_apps.html#logging_bluemix_cf_apps). In addition, advanced logging can be enabled in {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}} environments.

* To confirm that advanced logging is enabled in your {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}} environments, follow the steps in [Viewing logs](#hybrid_apps_logs_dash). If you do not have the **Advanced View** button, then this feature is not enabled.

* To add advanced logging to your environment, follow the steps in the [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) or [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) documentation.

## Log retention

In {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}} Cloud Foundry apps, log data is stored for 30 days by default.

## Viewing logs for Cloud Foundry apps in Dedicated and Local
{: #hybrid_apps_logs_dash}

You can review logs for the apps that you are running on {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}}.
{:shortdesc}

To view your app logs, follow these steps.
1. Select a running app.
2. Click **Logs**. In the **Logs** view, you can view logs from your running app..
4. Click the **Advanced View** button. **Advanced View** shows a more detailed view of the logs by using Kibana, a visualization tool that uses logs and time-stamped data to create custom visualizations. For more information about using the advanced view, see the [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) documentation.

Next, you can customize a Kibana dashboard. See [Analyzing logs in Kibana](../logging_view_kibana3.html#analyzing_logs_Kibana3) for more information.
