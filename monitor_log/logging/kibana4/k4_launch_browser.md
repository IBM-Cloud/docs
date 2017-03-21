---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Getting to the Kibana dashboard from a web browser
{: #launch_Kibana_from_browser}

Launch Kibana from a browser if you need to analyze log entries in a {{site.data.keyword.Bluemix}} space.
{:shortdesc}

The query that is used to filter the data that is displayed in Kibana retrieves log entries for a space in the {{site.data.keyword.Bluemix_notm}} organization. The log information that Kibana displays includes records for all resources that are deployed within the space of the {{site.data.keyword.Bluemix_notm}} organization that you are logged in.

Complete the following steps to launch Kibana from a browser:

1. Open [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) to log in to the Kibana user interface.

2. Select the version of Kibana that you want to use to analyze your logs.
    * Select the **Kibana 4** tab to work with Kibana 4. The Discovery page opens. For more information, see [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Select the **Kibana 3** tab to work with Kibana 3. The default Kibana dashboard opens. For more information about customizing a Kibana 3 dashboard, see [this blog post](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Note:** Kibana 3 is deprecated.

    If the Discover page does not show any log entries, adjust the time picker. For more information, see [Setting a time filter](logging_kibana_set_time_filter.html#set_time_filter).

For more information about Kibana, see the [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
