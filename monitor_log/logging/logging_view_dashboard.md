---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing logs from the Bluemix console
{: #analyzing_logs_bmx_ui}

In {{site.data.keyword.Bluemix}}, you can view, filter, and analyze logs through the log tab that is available for each Cloud Foundry app or Docker container.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public offers integrated logging capabilities. For example, when you run your applications in Cloud Foundry (CF), log data is captured from system components that interact with your application, about your application, and even log data from within your application when you use stdout and stderr.

Consider the following information about log data availability for analysis and log retention:

* In {{site.data.keyword.Bluemix_notm}} Public, log data is stored for 7 days by default. 
* You can store up to 1 GB of data per day. 
* By default, the logs that are available for analysis from the {{site.data.keyword.Bluemix_notm}} console include data for the last 24 hours.

**Tip:** To analyze data for a custom period that precedes the last 24 hours, see [Advanced log analysis with Kibana](kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana). 

##  Navigating to the logs of a Cloud Foundry app
{: #launch_logs_tab_bmx_ui_cf}

To see the deployment or runtime logs of a Cloud Foundry app, complete the following steps:

1. From the Apps dashboard, click the name of your Cloud Foundry app. 
    
2. From the app details page, click **Logs**.
    
    From the **Logs** tab, you can view the recent logs for your app or tail logs in real time. In addition, you can filter logs by component (log type), by app instance ID, and by error.
    

##  Navigating to the logs of a Docker container that is managed in Bluemix
{: #launch_logs_tab_bmx_ui_containers}

To see the deployment or runtime logs of a Docker container that is deployed in the {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure, complete the following steps:

1. From the Apps dashboard, click the single container or container group. 
    
2. From the app details page, click **Monitoring and Logs**.

3. Select the **Logging** tab.
    
    From the **Logging** tab, you can view the recent logs for your container or tail logs in real time. 

## Log format for CF app logs
{: #log_format_cf}

Logs for {{site.data.keyword.Bluemix_notm}} Cloud Foundry apps are displayed in a fixed format, similar to the following pattern:

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>/<var class="keyword varname">message</var>/<var class="keyword varname">timestamp</var></code>

Each log entry contains the following fields:

| Field | Description |
|-------|-------------|
| Time stamp | The time of the log statement. The timestamp is defined up to the millisecond. |
| Component | The component that produces the log. For the list of the different components, see [Log sources for CF apps](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). <br> Each component type is followed by a slash and a digit that indicates the application instance. 0 is the digit allocated to the first instance, 1 is the digit allocated to the second, and so on. |
| Message | The message that is issued by the component. The message varies depending on the context. |
{: caption="Table 1. CF app log entry fields" caption-side="top"}


## Log format for container logs
{: #log_format_containers}

Logs for containers are displayed in a fixed format, similar to the following pattern:

<code><var class="keyword varname">timestamp</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

Each log entry contains the following fields:

| Field | Description |
|-------|-------------|
| Date/Time | The time of the log statement. The timestamp is defined up to the millisecond. |
| Machine | The host name where the container is running. |
| Message | The message that is issued. The message varies depending on the context. |
{: caption="Table 2. Docker container log entry fields" caption-side="top"}

