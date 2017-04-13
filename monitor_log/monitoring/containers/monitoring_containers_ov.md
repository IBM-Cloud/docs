---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-27"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Monitoring for the IBM Bluemix Container service
{: #monitoring_bmx_containers_ov}

In {{site.data.keyword.Bluemix}}, container metrics are collected automatically from outside of the container, without having to install and maintain agents inside of the container.
{:shortdesc}

In-container agents can have significant overheads and setup times for short-lived, lightweight cloud instances and auto-scaling groups, where containers can be rapidly created and destroyed. This out-of-band data collection approach eliminates these challenges and removes the burden of monitoring from the users.

A process that is running in the host performs agentless monitoring for metrics. This process, which is also called the crawler, constantly collects the following metrics from all of the containers by default:

* CPU
* Memory
* Network information

Metric data is collected in Graphite and is displayed in both the {{site.data.keyword.Bluemix_notm}} UI and Grafana. 

You can launch Grafana from the {{site.data.keyword.Bluemix_notm}} UI or directly from a browser. For more information, see [Analyzing metrics in Grafana](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana).

Docker conventions and groups accounting information are used as the basic mechanism for the collection of monitoring data.

## Metrics retention

Up to one data point per minute is collected. Container metrics that have not been written to in 7 days are deleted.
    
## Metrics sorting

The data is displayed and ordered by container ID. 

From the command line, you can run the `cf ic ps` command to view a list of the container IDs for the containers in your private {{site.data.keyword.Bluemix_notm}} images registry.

