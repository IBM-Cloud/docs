---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kibana log format for Cloud Foundry applications
{: #kibana_log_format_cf}

You can configure Kibana to display in the *Discover* page the following fields for each log entry:
{:shortdesc}

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




