---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Logging for the IBM Bluemix Container Service
{: #logging_containers_ov}

You can view, filter, and analyze logs for Docker containers that are deployed in the {{site.data.keyword.IBM}}-managed cloud infrastructure and for Docker containers that run in Kubernetes clusters. Logging of containers is automatically enabled when you deploy a container in {{site.data.keyword.Bluemix_notm}} or in a Kubernetes cluster.
{:shortdesc}

Container logs are monitored and forwarded from outside of the container by using crawlers. The data is sent by the crawlers to a
multi-tenant Elasticsearch in {{site.data.keyword.Bluemix_notm}}.



## Collecting logs for a container that runs in a Kubernetes cluster
{: #logging_containers_ov_logs_collected_kubernetes}

The following figure shows a high level view of logging for the {{site.data.keyword.containershort}}:

![High level component overview for containers deployed in a Kubernetes cluster](images/containers_kube.gif "High level component overview for containers deployed in a Kubernetes cluster")

In {{site.data.keyword.Bluemix_notm}}, when you deploy applications in a Kubernetes cluster, consider the following information:

* In a {{site.data.keyword.Bluemix_notm}} account, you can have 1 or more organizations. 
* Each organization can have 1 or more {{site.data.keyword.Bluemix_notm}} spaces. 
* You can have 1 or more Kubernetes clusters in an organization. 
* Collection of logs is enabled automatically when you create a Kubernetes cluster. 
* A Kubernetes cluster is agnostic of {{site.data.keyword.Bluemix_notm}} spaces. However, the log data of a cluster and its resources is associated with a {{site.data.keyword.Bluemix_notm}} space.
* Log data is collected for an application as soon as the pod is deployed.
* To analyze log data for a cluster, you must access the Kibana dashboards for the Cloud Public region where the cluster is created.

Before you create a cluster, either through the [{{site.data.keyword.Bluemix_notm}} UI](../../../containers/cs_cluster.html#cs_cluster_ui) or through the [command line](../../../containers/cs_cluster.html#cs_cluster_cli), you must log into a specific {{site.data.keyword.Bluemix_notm}} region, account, organization, and space. The space where you are logged in is the space where logging data for the cluster and its resources is collected.

By default, information that any container process prints to stdout (standard output) and stderr (standard error) is collected. Sending information to stdout and stderr is the standard Docker convention for exposing the information of a container. 

If you forward the log data of an app that runs in a container to the Docker log collector in JSON format, you can search and analyze log data in Kibana by using JSON fields. For more information, see [Configuring custom fields as Kibana search fields](logging_containers_ov.html#send_data_in_json).

**Note:** When you work with a Kubernetes cluster, the namespaces *ibm-system* and *kube-system* are reserved. Do not create, delete, modify, or change permissions of resources that are available in these namespaces. Logs for these namespaces are for {{site.data.keyword.IBM_notm}} use.


## Collecting logs for a container managed by Bluemix
{: #logging_containers_ov_logs_collected}

The following figure shows a high level view of logging for the {{site.data.keyword.containershort}}:

![High level component overview for containers deployed in a {{site.data.keyword.Bluemix_notm}}-managed cloud infrastructure](images/container_bmx.gif "High level component overview for containers deployed in a {{site.data.keyword.Bluemix_notm}}-managed cloud infrastructure")

By default, the following logs are collected for a container that is deployed in the {{site.data.keyword.Bluemix_notm}}-managed cloud infrastructure:

<table>
  <caption>Table 2. Logs collected for containers deployed in the Bluemix-managed cloud infrastructure</caption>
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
      <td align="left">This log is the Docker log. <br> The Docker log file is not stored as a file inside of the container, but it is collected anyway. This log file is collected by default as it is the standard Docker convention for exposing the stdout (standard output) and stderr (standard error) information for the container. Information that any container process prints to stdout or stderr is collected. 
      </td>
     </tr>
  </tbody>
</table>

To collect additional logs, add the **LOG_LOCATIONS** environment variable with a path to the log file when you create the container. You can add multiple log files by separating them with commas. For more information, see [Collecting non-default log data from a container](logging_containers_other_logs.html#logging_containers_collect_data).


##  Configuring custom fields as Kibana search fields 
{: #send_data_in_json}

By default, logging is automatically enabled for containers. Every entry in the Docker log file is displayed in Kibana in the field `message`. If you need to filter and analyze your data in Kibana by using a specific field that is part of the container log entry, configure your application to send valid JSON formatted output.

Consider the following information:

* For containers that are deployed in a Kubernetes cluster, log the message in JSON format to stdout (standard output) and stderr (standard error).

    Each field that is available in the message is parsed to the type of field that matches is value. For example, each field in the following JSON message:
    
    ```
    {"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
    ```
    
    is available as a field that you can use for filtering and searches:
    
    * `field1` is parsed as `field1_str` of type string.
    * `field2` is parsed as `field1_int` of type integer.
    * `field3` is parsed as `field3_bool` of type boolean.
    * `field4` is parsed as `field4_str` of type string.
    
* For containers that are deployed in the {{site.data.keyword.Bluemix_notm}}-managed cloud infrastructure, complete the following steps to parse container log entries into individual fields:

    1. Log the message to a file. 
    2. Add the log file to the list of non-default logs that are available for analysis from a container. For more information, see [Collecting non-default log data from a container](logging_containers_other_logs.html#logging_containers_collect_data). 
    
   If you log the message to a file, and a message is determined to be valid JSON, the fields are parsed and new fields are created for each field in the message. Only string-type field values are available for filtering and sorting in Kibana


## Viewing container logs for a container that runs in a Kubernetes cluster
{: #logging_containers_ov_methods_view_kube}

You can view the latest logs for a container in a Kubernetes pod by using any of the following methods:

* View logs through the Kubernetes UI. For each pod, you can select it and access its logs. For more information, see [Web UI Dashboard ![(External link icon)](../../../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/){: new_window}.

* View logs by using the Kubernetes CLI command [kubectl logs ![(External link icon)](../../../icons/launch-glyph.svg "External link icon")](http://vishh.github.io/docs/user-guide/kubectl/kubectl_logs/){: new_window}. 

To view long-term logs, you can use Kibana. Check the [Log retention](logging_containers_ov.html#logging_containers_ov_log_retention) information to learn about the data retention period policies.



## Viewing container logs for a container managed by Bluemix
{: #logging_containers_ov_methods_view_bmx}

You can view the latest logs for a container that is deployed in the {{site.data.keyword.Bluemix_notm}}-managed cloud infrastructure by using any of the following methods:

* View logs through the {{site.data.keyword.Bluemix_notm}} UI to monitor the latest activity of the container.
    
    You can view, filter, and analyze logs through the **Monitoring and Logs** tab that is available for each container. For more information, see [Analyzing logs from the Bluemix dashboard](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
    
* View logs by using the {site.data.keyword.containershort}} CLI. Use commands to manage logs programmatically.
    
    You can view, filter, and analyze logs through the command line interface by using the **cf ic logs** command. For more information, see [Analyzing logs from the command line interface](../logging_view_cli.html#analyzing_logs_cli).


## Analyzing container logs
{: #logging_containers_ov_methods}

To analyze container log data, use Kibana to perform advanced analytical tasks. You can use Kibana, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. For more information, see [Analyzing logs in Kibana](../kibana4/analyzing_logs_Kibana.html#analyzing_logs_Kibana).


## Log retention
{: #logging_containers_ov_log_retention}

Consider the following information about log retention:

* A maximum of 1 GB per space of data is stored per day. Any logs beyond that 1 GB cap are discarded. Cap allotments reset each 
day at 12:30 AM UTC. 

    You can increase your cap by contacting support. In the support ticket, include your space ID for the cap increase request, the new cap size, and the reason for the request.

* Up to 7 GB of data is searchable for a maximum of 7 days. Log data rolls over (First In, First Out) after either 7 GB of data is reached or 7 days.

## Tutorial: Analyze logs in Kibana for an app that is deployed in a Kubernetes cluster
{: #tutorial1}

To learn how to use Kibana to analyze the logs of a container that is deployed in a Kubernetes cluster, see [Tutorial: Analyze logs in Kibana for an app that is deployed in a Kubernetes cluster](tutorials/kibana_tutorial_1.html#kibana_tutorial_1).


