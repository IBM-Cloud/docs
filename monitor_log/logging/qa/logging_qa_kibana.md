---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kibana FAQ
{: #logging_qa_kibana}

Here are the answers to common questions about using {{site.data.keyword.Bluemix}} logging capabilities. {:shortdesc}

* [What can I do if I cannot see data in the Discover page in Kibana](logging_qa_kibana.html#logging_qa_no_data_discover_kibana)
* [What can I do if I get an authentication exception](logging_qa_kibana.html#logging_qa_no_data_dashboard_kibana)
* [How do I launch Kibana 3](logging_qa_kibana.html#logging_qa_kibana3)
* [Why do I see the symbol ? by fields in the Kibana Discover page](logging_qa_kibana.html#logging_qa_kibana_question)

## What can I do if I cannot see data in the Discover page in Kibana
{: #logging_qa_no_data_discover_kibana}

There are different scenarios by which you might not see data in Kibana:

1. When you launch Kibana, you might not see any data in the Discover page. You receive the following message: **No results found.**. 
2. You might be working in the Discover page in Kibana. However, after a sort period of time, you receive the message: **No results found.** when you try to perform a task in Kibana.

To resolve this problem, complete the following steps:

1. Check the *Time Picker* that is set in the Discover page and increase the time period. 

    **Note**: By default, in {{site.data.keyword.Bluemix_notm}}, the *Time Picker* is set to show data for the last 15 minutes.

    For more information on how to set the *Time Picker*, see [Setting a time filter](../kibana4/k4_filter_logs.html#set_time_filter).
       
2. Click the magnifying glass that is located in the *Discover* page search bar. The page data is refreshed based on the default search query.

    Alternatively, you can set an *Auto refresh* period.

    **Note**: By default, in {{site.data.keyword.Bluemix_notm}}, the *Auto refresh* period is set to **OFF**.
    
    For more information on how to enable it, see [Automatically refreshing the data](../kibana4/logging_kibana_analize_logs_interactively.html#kibana_discover_view_refresh_interval).



## What can I do if I get an authentication exception
{: #logging_qa_no_data_dashboard_kibana}

When you cannot see data displayed in your visualizations in a Dashboard page, and you get the error message: **Error: Authorization Exception.**, check your permissions to see data in each visualization.

Consider the following information:
You can configure one ore more visualizations in a Dashboard page. When the Dashboard page makes a request to gather the data that is displayed thorugh those visualizations, only one request is issued for all the visualizations. If your do not have permissions to see data one of the visualizations, the entire request fails.

To resolve this problem, complete the following steps:

1. Identify the visualizations for which you do not have permissions.

    1. Click the *pencil* icon of a visualization in the *Dashboard* page. The visualization opens in the *Visualize* page. Alternatively, in the *Visualize* page, load one visualization. 
    2. Verify you can see data.
    
    Repeat these steps for each visualization.

2. Request access to see data in those visualizations from your cloud administrator.

3. Create a new Dashboard page that excludes the visualizations for which you do not have permissions while you are granted access to see data in the visualizations that are causing the problem. 

    If you share the Dashboard, do not delete visualizations since that will affect other team members that use the same dashboard.

## How do I launch Kibana 3
{: #logging_qa_kibana3}

**Note:** Kibana 3 is deprecated.

You can launch Kibana 3 from a browser.

Complete the following step to launch Kibana 3 from a browser:

1. Open [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) to log in to the Kibana user interface.
    
2. Select the version of Kibana that you want to use to analyze your logs.
    * Select the **Kibana 4** tab to work with Kibana 4. The Discovery page opens. For more information, see [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Select the **Kibana 3** tab to work with Kibana 3. The default Kibana dashboard opens. For information about using Kibana 3 to analyze your logs, see [Analyzing logs in Kibana 3 (Deprecated)](../logging_view_kibana3.html#analyzing_logs_Kibana3). For more information about customizing a Kibana 3 dashboard, see [this blog post ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     

## Why do I see the symbol ? by fields in the Kibana Discover page
{: #logging_qa_kibana_question}

When you open the Discover page in Kibana, you might see a `?` by fields that are listed in the available fields section instead of the character `t`. When you reload the list of fields, the type of fields is analyzed, and the `?` is replaced by the character `t`. For more information, see [Reloading the list of fields](../kibana4/logging_kibana_analize_logs_interactively.html#kibana_discover_view_reload_fields).



