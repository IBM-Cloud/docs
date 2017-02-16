---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Logging for Cloud Foundry apps in Bluemix
{: #logging_bluemix_cf_apps}

In {{site.data.keyword.Bluemix}}, you can view, filter, and analyze logs through the {{site.data.keyword.Bluemix}} dashboard, Kibana, and the command line interface. In addition, you can stream log records to an external log management tool. 
{:shortdesc}

When you run your apps in a cloud platform-as-a-service (PaaS) like Cloud Foundry on {{site.data.keyword.Bluemix_notm}}, you cannot SSH or FTP into the infrastructure where your apps are running to access the logs. The platform is controlled by the cloud provider. Cloud Foundry apps running on {{site.data.keyword.Bluemix_notm}} use the Loggerator component to forward log records from inside of the Cloud Foundry infrastructure. The Loggregator automatically picks up STDOUT and STDERR data. You can visualize and analyze these logs through the {{site.data.keyword.Bluemix}} dashboard, Kibana, and the command line interface.

The following figure shows a high level view of logging Cloud Foundry apps in {{site.data.keyword.Bluemix_notm}}:

![High level component overview for CF apps](images/logging_cf_apps_ov.jpg)
 
Logging of Cloud Foundry apps is automatically enabled when you use the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. To view cloud foundry runtime logs, you must write your logs to STDOUT and STDERR. For more information, see [Runtime application logging through CF apps](cfapps/logging_writing_to_log_from_cf_app.html#logging_writing_to_log_from_cf_app).

You can choose any of the following methods to analyze the logs of your Cloud Foundry application:

* Analyze the log in {{site.data.keyword.Bluemix_notm}} to view the latest actvity of the application.
    
    In {{site.data.keyword.Bluemix}}, you can view, filter, and analyze logs through the **Log** tab that is available for each Cloud Foundry application. For more information, see [Analyzing CF app logs from the Bluemix dashboard](logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analyze logs in Kibana to perform advanced analytical tasks.
    
    In {{site.data.keyword.Bluemix}}, you can use Kibana, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. For more information, see [Analyzing logs in Kibana](logging_view_kibana3.html#analyzing_logs_Kibana).

* Analyze logs through the CLI to use commands to manage logs programmatically.
    
    In {{site.data.keyword.Bluemix}}, you can view, filter, and analyze logs through the command line interface by using the **cf logs** command. For more information, see [Analyzing Cloud Foundry app logs from the command line interface](logging_view_cli.html#analyzing_logs_cli).

{{site.data.keyword.Bluemix_notm}} keeps a limited amount of log information. When information is logged, the old information is replaced by the newer information. If you have to comply with organizational or industry policies that require you to keep part or all the log information for audit or other purposes, you can stream your logs to an external log host, such as a third-party log management service or other host. For more information, see [Configuring external log hosts](logging_view_external.html#viewing_logs_external).



