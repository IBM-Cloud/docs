---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Getting to the Kibana dashboard from the Bluemix dashboard
{: #launch_Kibana_from_bluemix}

Launch Kibana from the {{site.data.keyword.Bluemix}} UI to see the specific logs of a Cloud Foundry application or Docker container.
{:shortdesc}

The query that is used to filter the data that is displayed in Kibana retrieves log entries for the {{site.data.keyword.Bluemix_notm}} CF app or container from where you launch Kibana. 

To see the logs of a Cloud Foundry application or Docker container in Kibana, complete the following steps:

1. Log in to {{site.data.keyword.Bluemix_notm}}, and then click the app name or container from the {{site.data.keyword.Bluemix_notm}} dashboard. 
    
2. Open the log tab in the {{site.data.keyword.Bluemix_notm}} UI.

    * For CF apps, click **Logs** in the navigation bar. 
    * For containers, select **Monitoring and logs** in the navigation bar and then click the **Logging** tab. 
    
    The logs tab opens. 
    
3. Click **Advanced view**. The **Kibana 4** dashboard opens.

    By default, the **Discover** page loads with the default index pattern selected and a time filter set to the last 30 seconds. The search query is set to match all entries for the your CF app or Docker container.

    If the Discover page does not show any log entries, adjust the time picker. For more information, see [Setting a time filter](logging_kibana_set_time_filter.html#set_time_filter).

For more information about Kibana, see the [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

