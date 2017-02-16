---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-02"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing logs
{: #analyzing_logs}

In {{site.data.keyword.Bluemix}}, you can view, filter, and analyze logs through the {{site.data.keyword.Bluemix}} dashboard, Kibana, and the command line interface. In addition, you can stream log records to an external log management tool. 
{:shortdesc}


## Viewing logs from external hosts
{: #viewing_logs_external}


When logs are generated, after a short delay you can view messages in your external log host that are similar to the messages that you view from the {{site.data.keyword.Bluemix_notm}} user interface or from the cf command line interface.  If you have multiple instances of your app, the logs are aggregated and you can see all the logs for your app. In addition, the logs are persisted between app crashes and deployments. For more information, see [Configuring external log hosts](/logging/external/logging_external_hosts.html#thirdparty_logging).

**Note:** Logs that you view in the command line interface are not in the syslog format, and might not exactly match the messages that are displayed in your external log host.
