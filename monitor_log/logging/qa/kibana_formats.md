---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-23"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana log formats
{: #kibana_formats}

You can configure Kibana to display in the *Discover* page different fields for each log entry.
{:shortdesc}



## Kibana log format for Cloud Foundry applications
{: #kibana_log_format_cf}

You can configure Kibana to display in the *Discover* page the following fields for each log entry:

| Field | Description |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> The time of the logged event. <br> The timestamp is defined up to the millisecond. |
| @version | Version of the event. |
| ALCH_TENANT_ID | ID of the {{site.data.keyword.Bluemix_notm}} space. |
| \_id | The unique id for your log document. |
| \_index | The index for your log entry. |
| \_type | The type of log; for example, *syslog*. |
| app_name | The name of your {{site.data.keyword.Bluemix_notm}} application. |
| application_id | The unique id of your {{site.data.keyword.Bluemix_notm}} application. |
| host | The name of your application that produced the log data. |
| instance_id | The instance id of your application instance that produced the log data. |
| loglevel | The severity of the logged event. |
| message | The message that is issued by the component. <br> The message varies depending on the context. |
| message_type | The stream that the log message is written to. <br> * **OUT** refers to the stdout stream <br> * **ERR** refers to the stderr stream. |
| org_id | The unique id of your {{site.data.keyword.Bluemix_notm}} organization |
| org_name | The name of the {{site.data.keyword.Bluemix_notm}} organization where your app is staged. |
| origin | Component where the event was originated. |
| source_id | The component that produces logs. <br> The following list describes the logs from each component: <br> * **API**: Logged responses to API calls that request a change to your app state. <br> * **APP**: Logged responses from your app. <br> * **CELL**: Logged responses from the Diego cell that indicate when an app starts, stops, or crashes <br> * **LGR**: Logged responses from the loggregator that indicate problems with the logging process. <br> * **RTR**: Logged responses from the Router when it routes HTTP requests to your app. <br> * **SSH**: Logged responses from the Diego cell when a user accesses an app container by using the `cf ssh` command. <br> * **STG**: Logged responses from the Diego cell or the Droplet Execution Agent when your app is staged or restaged. |
| space_name | The name of the {{site.data.keyword.Bluemix_notm}} space where where your app is staged. |
| timestamp | The time of the logged event. The timestamp is defined up to the millisecond. |
{: caption="Table 1. Fields for CF apps" caption-side="top"}



## Kibana log format for Docker containers that are deployed in a Bluemix-managed infrastructure
{: #kibana_log_format_containers}

You can configure Kibana to display in the *Discover* page the following fields for each log entry:

| Field | Description |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> The time of the logged event. <br> The timestamp is defined up to the millisecond. |
| @version | Version of the event. |
| ALCH_TENANT_ID | ID of the {{site.data.keyword.Bluemix_notm}} space. |
| \_id | The unique id for your log document. |
| \_index | The index for your log entry. |
| \_type | The type of log; for example, *logs*. |
| group_id | Group ID <br> * For a single container, the value is **0000**. <br> * For a container group, the value is the GUID of the group.  |
| host | Host name where the container runs. |
| instance | GUID of the instance for a single container. List of instance IDs for a container group.|
| log | Short message. |
| message | Full message. |
| path | Path and log name where the log is located inside the container. |
| stream | Specifies the type of log: stdout, stderr |
| time | The date and time of the event when it happened. The timestamp is defined up to the millisecond.|
| timestamp | The date and time of the logged event. The timestamp is defined up to the millisecond. |
{: caption="Table 2. Fields for Docker containers" caption-side="top"}

## Kibana log format for Docker containers that are deployed in a Kubernetes cluster
{: #kibana_log_format_containers_kubernetes}

You can configure Kibana to display in the *Discover* page the following fields for each log entry. These fields are set by {{site.data.keyword.IBM}} and include your message data. 

| Field | Description | Other information |
|-------|-------------|---------------------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> The time of the logged event. <br> The timestamp is defined up to the millisecond. | |
| @version | Version of the event. | |
| ALCH_TENANT_ID | ID of the {{site.data.keyword.Bluemix_notm}} space. | |
| \_id | The unique ID for your log document. | |
| \_index | The index for your log entry. | |
| \_score |  |  |
| \_type | The type of log; for example, *logs*. | |
| crn_str | Information about the source of the log. | By default, this field is set by {{site.data.keyword.IBM_notm}}. <br> **Note**: If you send the log message in valid JSON format, and one of the fields is named `crn`, the value of the field is overwritten with the value that is set in the message.  |  
| docker.container_id_str | GUID of the container running in a pod. | |
| ibm-containers.account_str | GUID of the {{site.data.keyword.Bluemix_notm}} account.  |  |
| ibm-containers.cluster_id_str | GUID of the Kubernetes cluster.  |  |
| ibm-containers.cluster_type_str |  | Value reserved for {{site.data.keyword.IBM_notm}} internal use. |
| ibm-containers.region_str | Region in {{site.data.keyword.Bluemix_notm}}.  |  |
| kubernetes.container_name_str | Name of the container where an app is deployed.  |  |
| kubernetes.host | Public IP address of the worker where the container is running. |  |
| kubernetes.labels.*example_label_name*\_str | Key-value pair that you attach to a Kubernetes object such as a pod. | Each label that you attach to a Kubernetes object is listed as a field in the log entry displayed in Kibana. <br> You can have 0 or more labels. |
| kubernetes.namespace_name_str | Kubernetes namespace where the container is deployed. |  |
| kubernetes.pod_id_str | GUID of the pod where the container is deployed. |  |
| kubernetes.pod_name_str | Name of the pod. |  |
| message | Full message. | If you send a valid JSON formatted message, each field is individually parsed and displayed in Kibana.  |
| stream_str |  | Value reserved for {{site.data.keyword.IBM_notm}} internal use. |
|tag_str |  | Value reserved for {{site.data.keyword.IBM_notm}} internal use. |
{: caption="Table 3. Fields for Docker containers" caption-side="top"}


## Kibana log format for Message Hub
{: #kibana_log_format_messagehub}

You can configure Kibana to display in the *Discover* page the following fields for each log entry:

| Field | Description |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> The time of the logged event. <br> The timestamp is defined up to the millisecond. |
| @version | Version of the event. |
| ALCH_TENANT_ID | ID of the {{site.data.keyword.Bluemix_notm}} space. |
| \_id | The unique ID for your log document. |
| \_index | The index for your log entry. |
| \_type | The type of log; for example, *syslog*. |
| loglevel | The severity of the logged event, for example, **Info**. |
| module | This field is set to **MessageHub**. |
{: caption="Table 4. Fields for Message Hub events" caption-side="top"}

Example of a log entry:

```
March 8th 2017, 17:15:16.454	

message:
    Creating topic ABC
@version:
    1
@timestamp:
    March 8th 2017, 17:15:16.454
loglevel:
    Info
module:
    MessageHub
ALCH_TENANT_ID:
    3d8d2eae-f3f0-44f6-9717-126113a00b51
&#95;id:
    AVqu6vJl1zcfr8KYMI95
&#95;type:
    logs
&#95;index:
    logstash-2017.03.08
```
