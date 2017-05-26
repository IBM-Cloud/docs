---

copyright:
  years: 2017

lastupdated: "2017-05-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing container metrics from the Bluemix console
{: #analyzing_metrics_bmx_ui}

In {{site.data.keyword.Bluemix}}, you can view, and analyze metrics through the *Monitoring* tab that is available for Docker containers that are deployed in a {{site.data.keyword.Bluemix_notm}}-managed cloud infrastructure.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public offers integrated monitoring capabilities. 

Consider the following information about metrics availability for analysis and data retention:

* In {{site.data.keyword.Bluemix_notm}} Public, metrics are stored for 7 days by default. 
* You can store up to 1 GB of data per day. 
* By default, metrics that are available for analysis from the {{site.data.keyword.Bluemix_notm}} console include data for the last 24 hours.

**Tip:** Use Grafana to analyze data for a custom period that precedes the last 24 hours.


##  Navigating to the metrics of a Docker container that is managed in Bluemix
{: #launch_metrics_tab_bmx_ui_containers}

To see the metrics for a Docker container that is deployed in the {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure, complete the following steps:

1. From the Apps dashboard, click the single container or container group. 
    
2. From the app details page, click **Monitoring and Logs**.

3. Select the **Monitoring** tab.
    
    From the **Monitoring** tab, you can view the metrics for your container.
