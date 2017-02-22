---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Monitoring in Bluemix
{: #monitoring_bmx_ov}

{{site.data.keyword.Bluemix_notm}}, by default, collects and displays performance metrics for CPU usage, memory utilization, and network I/O. These metrics provide information about the performance of individual cloud resources. You can monitor the performance of these resources in your cloud environment through the {{site.data.keyword.Bluemix_notm}} UI. You can view near real-time data and historical data.
{:shortdesc}

You can use the monitoring capabilities in {{site.data.keyword.Bluemix_notm}} to automatically collect and measure key metrics from your environment and applications. No special instrumentation is required to collect metrics. For example, you can use information provided by performance metrics to monitor how a service is running in the cloud, detect resource bottlenecks, and keep an eye on the service level agreement (SLA). When you analyze performance data for a service, you can detect situations that can lead to a resource bottleneck and consequently affect your service SLA to your clients. By taking early action, you can prevent situations that can impact your business negatively.  

You also can configure and monitor more performance metrics. You can visualize and analyze these metrics outside {{site.data.keyword.Bluemix_notm}}. For example, you can use Grafana to monitor more metrics when you run your app in the {{site.data.keyword.containershort}}. You can cutomize dashboards per container instance or per space where you visualize and analyze the performance data.

![Grafana monitoring view of a container running in {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

You can use the {{site.data.keyword.Bluemix_notm}} platform monitoring to:

* Gain insight on application operations, for example, detect the potential bottlenecks or when upgrades are required.
* Define trends that you can use to plan future app requirements in your cloud platform.

For more information about monitoring apps that run on Cloud Foundry, see [Monitoring apps that run on Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

For more information about monitoring in {{site.data.keyword.containershort}}, see [Monitoring in {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

