---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-19"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Advanced log analysis with Kibana
{:#analyzing_logs_Kibana}

In {{site.data.keyword.Bluemix}}, you can use Kibana, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. Use Kibana to perform advanced analytical tasks.
{:shortdesc}

Kibana is a browser-based interface where you can analyze data interactively and customize dashboards that you can then use to analyze log data and perform advance management tasks. For more information, see [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

The data that a Kibana page displays is constrained by a search. The default data set is defined by the pre-configured index pattern. To filter the information, you can add new search queries and apply filters to the default data set. Then, you can save the search for future reuse. 

Kibana includes different pages that you can use to analyze your logs:

| Kibana page | Description |
|-------------|-------------|
| Discover | Use this page to define searches and analyze your logs interactively through a table and a histogram. |
| Visualize | Use this page to create visualizations such as graphs and tables that you can use to analyze your log data and compare results.  |
| Dashboard | Use this page to analyze your logs through collections of saved visualizations and searches.  |
{: caption="Table 1. Kibana pages" caption-side="top"}

**Note:** You can only analyze 1 complete day at a time through the Visualize page or the Dashboard page, even though you can go back 7 days. Log data is stored for 7 days by default. 

| Kibana page | Time period information |
|-------------|-------------------------|
| Discover | Analyze data for a maximum of 7 days. |
| Visualize | Analyze data for a period of 24 hours. <br> You can filter log data for a custom period that elapses 24 hours.  |
| Dashboard | Analyze data for a period of 24 hours. <br> You can filter log data for a custom period that elapses 24 hours. <br> The time picker that you set is applied to all visualizations that are included in the dashboard. |
{: caption="Table 2. Time period information" caption-side="top"}

For example, this is how you can use Kibana to show information about a CF app or container in your space through the different pages:

## Navigate to the Kibana dashboard
{: #launch_Kibana}

You can launch Kibana in any of the following ways:

* From {{site.data.keyword.Bluemix_notm}}

    You can launch to your specific CF app logs in Kibana, within the context of that specific App.
    
    You can launch to your specific Docker container logs in Kibana, within the context of that specific container. This feature applies only to containers that are deployed in the {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure.
    
    For CF apps, the query that is used to filter the data that is available for analysis in Kibana retrieves log entries for the Cloud Foundry application. The log information that Kibana displays by default is all related to a single Cloud Foundry application and all its instances. 
    
    For containers, the query that is used to filter the data that is available for analysis in Kibana retrieves log entries for all instances of the container. The log information that Kibana displays by default is all related to a single container or to a container group and all its instances. 
    
    For more information, see [Navigating to the Kibana dashboard from the Bluemix dashboard](k4_launch.html#launch_Kibana_from_bluemix).

* From a direct browser link

    You may want to launch Kibana so the data that you see aggregates logs from services within a provided {{site.data.keyword.Bluemix_notm}} space.
    
    The query that is used to filter the data that is displayed in the dashboard retrieves log entries for a space in the 
    {{site.data.keyword.Bluemix_notm}} organization. The log information that Kibana displays includes records for 
    all resources that are deployed within the space of the {{site.data.keyword.Bluemix_notm}} organization that you are logged in. 
    
    For more information, see [Navigating to the Kibana dashboard from a web browser](k4_launch.html#launch_Kibana_from_browser).
    
    When you launch Kibana from a browser, you can choose to work with Kibana 4 or Kibana 3. **Note:** Kibana 3 is deprecated. For information about using Kibana 3 to analyze your logs, see [Analyzing logs in Kibana 3 (Deprecated)](../logging_view_kibana3.html#analyzing_logs_Kibana3).


## Analyze data interactively
{: #analyze_discover}

In the Discover page, you can define new search queries and apply filters per query. The log data is displayed through a table and a  histogram. You can use these visualizations to analyze the data interactively. For more information, see [Analyzing logs interactively in Kibana](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).

You can configure filters from log fields, for example, message_type and instance_ID, and set a time period. You can enable or disable dynamically these filters. The table and histogram will display the log entries that meet the query and filtering criteria that you enable. For more information, see [Filtering logs in Kibana](k4_filter_logs.html#k4_filter_logs).

## Analyze data through a visualization
{: #analyze_visualize}
    
In the Visualize page, you can define new search queries and visualizations.

To analyze the data, you can create visualizations based on an existing search or a new search. Kibana includes different types of visualizations such as table, trends, and histogram that you can use to analyze the information. The objective of each visualization varies. Some visualizations are organized into rows that provide the results of a one or more queries. Other visualizations display documents or custom information. The data in a visualization can be fixed or change if a search query is updated. You can embed the visualization in a web page or share it. For more information, see [Analyzing logs by using visualizations](logging_kibana_visualizations.html#logging_kibana_visualizations).

## Analyze data in a dashboard
{: #analyze_dashboard}

In the Dashboard page, you can customize, save, and share multiple visualizations and searches simultaneously. 

You can add, remove, and rearrange visualizations in the dashboard. For more information, see [Analyzing logs in Kibana through a dashboard](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard).
    
After you customize a Kibana dashboard, you can analyze the data through its visualizations and save it for future reuse. For more information, see [Saving a Kibana dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save).

In Kibana, there is also a *Settings* page that you can use to configure Kibana, and to save, delete, export, and import searches, visualizations, and dashboards.


