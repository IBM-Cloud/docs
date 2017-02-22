---



copyright:

  years: 2016, 2017

lastupdated: "2016-10-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# Monitoring and logging for Cloud Foundry apps in Dedicated and Local
{: #dedicated_apps_ml_ov}


In {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm:}}, Cloud Foundry apps come with built-in logging. You can review the data that is collected from your apps on the {{site.data.keyword.Bluemix_notm}} console.
{:shortdesc}

Cloud Foundry apps use Cloud Foundry loggregator to monitor and forward logs from outside of the app. You don't need to install agents inside of the app.

## Hardware requirements


| **Requirement** |    **1 node**     | **3 nodes for high availability** |
|-----------------|-------------------|-------------------|
vCPU | 19 | 57 |
Memory | 80 GB | 240 GB |
Local storage | 2.98 TB | 8.94 TB |
{: caption="Table 1. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm:}}" caption-side="top"}

## Setup

In {{site.data.keyword.Bluemix}} Dedicated and {{site.data.keyword.Bluemix}} Local, logs are active for all apps by default. To view information about reading standard logs, see Logging for apps running on Cloud Foundry. In addition, advanced logging can be enabled in {{site.data.keyword.Bluemix}} Dedicated and {{site.data.keyword.Bluemix}} Local environments.

## Log retention

In {{site.data.keyword.Bluemix}} Dedicated and {{site.data.keyword.Bluemix}} Local Cloud Foundry apps, log data is stored for 30 days by default.

## Viewing logs for Cloud Foundry apps in {{site.data.keyword.Bluemix}} Dedicated and {{site.data.keyword.Bluemix}} Local
{: #dedicated_apps_ml_logs_dash}

You can review logs for the apps that you are running on {{site.data.keyword.Bluemix_notm}} Dedicated and {{site.data.keyword.Bluemix_notm}} Local.
{:shortdesc}

To view your app logs, follow these steps.
1. Select a running app.
2. Click **Logs**. In the **Logs** view, you can view logs from your running app..
4. Click the **Advanced View** button. **Advanced View** shows a more detailed view of the logs by using Kibana, a visualization tool that uses logs and time-stamped data to create custom visualizations. For more information about using the advanced view, see the [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) documentation.

Next, you can customize a Kibana dashboard. See [Customizing log display in Kibana dashboard](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom) for more information.

<!-- audience blue staging only end comment -->
