---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Logging for the IBM Bluemix Container Service
{: #logging_containers_ov}

In {{site.data.keyword.Bluemix}}, you can view, filter, and analyze container logs through the {{site.data.keyword.Bluemix_notm}} dashboard, Kibana, and the command line interface.
{:shortdesc}

Container logs are monitored and forwarded from outside of the container by using crawlers. The data is sent by the crawlers to a
multi-tenant Elasticsearch in {{site.data.keyword.Bluemix_notm}}.

**Note:** You can analyze container logs in {{site.data.keyword.Bluemix_notm}} for Docker containers that are deployed in the {{site.data.keyword.IBM}}-managed cloud infrastructure.

The following figure shows a high level view of logging for {{site.data.keyword.containershort}}:

![High level component overview for containers](images/logging_containers_ov.jpg "High level component overview for containers")

Logging of containers is automatically enabled when you deploy that container in {{site.data.keyword.Bluemix_notm}}.


## Methods to analyze container logs
{: #logging_containers_ov_methods}
 
You can choose any of the following methods to analyze the logs of your container:

* Analyze the log in {{site.data.keyword.Bluemix_notm}} to view the latest activity of the container.
    
    You can view, filter, and analyze logs through the **Monitoring and Logs** tab that is available for each container. For more information, see [Analyzing logs from the Bluemix dashboard](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analyze logs in Kibana to perform advanced analytical tasks.
    
    You can use Kibana, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. For more information, see [Analyzing logs in Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

* Analyze logs through the CLI to use commands to manage logs programmatically.
    
    You can view, filter, and analyze logs through the command line interface by using the **cf ic logs** command. For more information, see [Analyzing logs from the command line interface](../logging_view_cli.html#analyzing_logs_cli).

## Logs collected for containers
{: #logging_containers_ov_logs_collected}

By default, the following logs are collected:

<table>
  <caption>Table 1. Logs</caption>
  <tbody>
    <tr>
      <th align="center">Log</th>
      <th align="center">Description</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> By default, Docker messages are stored in the /var/log/messages folder of the container. This log includes system messages.
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">This log is the Docker log. <br> The Docker log file is not stored as a file inside of the container, but it is collected anyway. This log file is collected by default as it is the standard Docker convention for exposing the stdout (standard output) and stderr (standard error) information for the container. If any container process prints to stdout or stderr, that information is collected. 
      </td>
     </tr>
  </tbody>
</table>

To collect additional logs, add the **LOG_LOCATIONS** environment variable with a path to the log file when you create the container. You can add multiple log files by separating them with commas. For more information, see [Collecting non-default log data from a container](logging_containers_other_logs.html#logging_containers_collect_data).



## Log retention
{: #logging_containers_ov_log_retention}

Consider the following information about log retention:

* A maximum of 1 GB per space of data is stored per day. Any logs beyond that 1 GB cap are discarded. Cap allotments reset each 
day at 12:30 AM UTC. 

    You can increase your cap by contacting support. In the support ticket, include your space ID for the cap increase request, the new cap size, and the reason for the request.

* Up to 7 GB of data is searchable for a maximum of 7 days. Log data rolls over (First In, First Out) after either 7 GB of data is reached or 7 days.

