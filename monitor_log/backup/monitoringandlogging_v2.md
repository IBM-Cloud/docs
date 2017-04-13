---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Monitoring and logging
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} is {{site.data.keyword.IBM_notm}}'s cloud computing platform for building, running, and managing apps and services. {{site.data.keyword.Bluemix_notm}} combines platform as a service (PaaS) with infrastructure as a service (IaaS). Additionally, {{site.data.keyword.Bluemix_notm}} has a rich catalog of cloud services that can be easily integrated with PaaS and IaaS to rapidly build business applications. {{site.data.keyword.Bluemix_notm}} includes integrated logging and monitoring services across the platform. 
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} offers logging and monitoring services across different compute services, such as Cloud Foundry and {{site.data.keyword.containershort}}. You can develop, run, and manage applications in any compute runtime without the complexity of building and maintaining the infrastructure that is typically associated with developing and launching an app. 

**Note:** Monitoring and logging capabilities are available in the US South region and in the United Kingdom region.

You can use the monitoring capabilities in {{site.data.keyword.Bluemix_notm}} to automatically collect and measure key metrics from your environment and applications. No special instrumentation is required to collect metrics. For example, you can use information provided by performance metrics to monitor how a service is running in the cloud, detect resource bottlenecks, and keep an eye on the service level agreement (SLA). For example, when you analyze performance data for a service, you can detect situations that can lead to a resource bottleneck and consequently affect your service SLA to your clients. By taking early action, you can prevent situations that can impact your business negatively.  

You can use the logging capabilities in {{site.data.keyword.Bluemix_notm}} to understand the behavior of the cloud platform and the resources that are running in it. No special instrumentation is required to collect the standard out and the standard err logs. For example, you can use logs to provide an audit trail for an application, detect problems in your service, identify vulnerabilities, troubleshoot your app deployments and runtime behavior, detect problems in the infrastructure where your app is running, trace your app across components in the cloud platform, and detect patterns that you can use to preempt actions that could affect your service SLA.

## Monitoring compute infrastructure resources
{: #monitoring_sl_ov}

Every {{site.data.keyword.Bluemix_notm}} server includes monitoring and easily readable reports that are always available. For more information, see [Infrastructure Monitoring & Reporting ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}.


## Monitoring in {{site.data.keyword.Bluemix}} for compute services
{: #monitoring_bmx_ov}

{{site.data.keyword.Bluemix_notm}}, by default, collects and displays performance metrics for CPU usage, memory utilization, and network I/O. These metrics provide information about the performance of individual cloud resources. You can monitor the performance of these resources in your cloud environment through the {{site.data.keyword.Bluemix_notm}} UI. You can view near real-time data and historical data. 

You also can configure and monitor more performance metrics. You can visualize and analyze these metrics outside {{site.data.keyword.Bluemix_notm}}. For example, you can use Grafana to monitor more metrics when you run your app in the {{site.data.keyword.containershort}}. You can cutomize dashboards per container instance or per space where you visualize and analyze the performance data.

![Grafana monitoring view of a container running in {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

You can use the {{site.data.keyword.Bluemix_notm}} platform monitoring to:

* Gain insight on application operations, for example, detect the potential bottlenecks or when upgrades are required.
* Define trends that you can use to plan future app requirements in your cloud platform.

For more information about monitoring apps that run on Cloud Foundry, see [Monitoring apps that run on Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

For more information about monitoring in {{site.data.keyword.containershort}}, see [Monitoring in {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

## Logging in {{site.data.keyword.Bluemix}}
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix_notm}} logging capabilities are integrated in the platform and collection of data is automatically enabled for cloud resources. {{site.data.keyword.Bluemix_notm}}, by default, collects and displays logs for your apps, apps runtimes, and compute runtimes where those apps run. 

When you run your apps in the cloud, you might not be able to SSH or FTP into the infrastructure where your apps are running to access the logs, for example if your app runs in Cloud Foundry. On the other hand, you can run your app in {{site.data.keyword.containershort}}, another compute runtime that is available in {{site.data.keyword.Bluemix_notm}}, where you can SSH and access the logs. Regardless of the compute runtime, access to logs is critical and {{site.data.keyword.Bluemix_notm}} provides a common experience to visualize and analyze logs in your cloud platform.

{{site.data.keyword.Bluemix_notm}} records log data that is generated by the Cloud Foundry platform and by Cloud Foundry applications. In the logs, you can view the errors, warnings, and informational messages that are produced for your app. For more information about logging in Cloud Foundry, see [Logging for Cloud Foundry apps in {{site.data.keyword.Bluemix}}](logging_cf_apps.html#logging_bluemix_cf_apps).

{{site.data.keyword.Bluemix_notm}} records log data that is generated by the {{site.data.keyword.containershort}}. For more information about logging in {{site.data.keyword.containershort}}, see [Logging in {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs).   


By using the logging functionality that {{site.data.keyword.Bluemix_notm}} offers, you can:

* Have visibility into your cloud resources and how they are performing and running.
* Define trends that help you identify scenarios that require your action.
* Define trails of data for an app, for example, that you can use for auditing.
* Reduce the time and effort that is required to locate an issue in an app and repair it. 
* Monitor the deployment of your apps in the cloud platform.
* Detect when a service or an app is down or crashed.
* Follow application execution and data flow.
* Identify vulnerabilities in your app.
* Detect problems in the infrastructure.
* Detect problems in the app runtime.


