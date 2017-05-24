---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Defining custom search queries
{:#k4_define_search}

In the search bar of the Discover page, you can define and save search queries by using the Lucene query language. For each search, you can apply filters to refine the entries that are available for analysis.
{:shortdesc}

Complete the following tasks to define a custom search:

1. Launch Kibana.

    For Cloud Foundry (CF) apps or containers that run in the {{site.data.keyword.Bluemix}}-managed cloud infrastructure, complete the following steps:
    
    1. Access the **Logs** tab of your Cloud Foundry (CF) app or container. 

        Click the app name or container in the {{site.data.keyword.Bluemix_notm}} dashboard. Then, for CF applications, click the **Logs** tab; for containers click **Monitoring and logs**, and then select the **Logging** tab. The logs are displayed.

    2. Access Kibana. Click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg "Advanced view link"). The Kibana dashboard is displayed.
    
    For containers that run in a Kubernetes cluster, [launch Kibana from the browser](k4_launch.html#launch_Kibana_from_browser). 
    
    When you access Kibana, the default search is applied. You can see the logs for the list of instances of the resource you launched Kibana for. You can filter the logs for any or all of the {{site.data.keyword.Bluemix_notm}} resources in that space.

2. Look at the Discover page to see what subset of your data it displays. For more information, see [Identifying the data that is displayed in your Kibana Discover page](logging_kibana_analize_logs_interactively.html#k4_identify_data). Then, modify the default query to filter entries.

    **Note:** Use the Lucene query language to define your custom query. For more information, see [Apache Lucene - Query Parser Syntax  ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    When Kibana is launched from {{site.data.keyword.Bluemix_notm}}, to modify the query and define multiple search criteria, you can use the logical terms **AND** and **OR**. These operators must be in uppercase.    
    
    * To search for a keyword, or part of a keyword, enter a word, followed by a wildcard symbol \*; for example, `Java*`. 
    * To search for a particular phrase, enter that phrase in double quotation marks; for example, `"Java/1.8.0"`.
    * To create more complex searches, you can use the logical terms AND and OR; for example `"Java/1.8.0" OR "Java/1.7.0"`.
    * To search for a value within a particular field, enter your search in the following form: *log_field_name:search_term*; for example, `instance_id:"1"`.
    * To search for a range of values for a particular log field, enter your search in the following form: *log_field_name:[start_of_range TO end_of_range]*; for example, `instance_id:["1" TO "2"]`.

     For example, for a CF app, you can create a query `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]`  that only lists entries for instances *0* and *1*. 

3. Save the query so you can reuse it later. For more information, see [Saving a search](logging_kibana_filtering_logs.html#k4_save_search). 

**Note:** If you need to delete a query, see [Deleting a search](logging_kibana_filtering_logs.html#k4_delete_search).



## Deleting a search
{: #k4_delete_search}

To delete a search, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Searches** tab, select the search that you want to delete.

3. Click **Delete**.


## Exporting a search
{: #k4_export_search}

To export a search, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Searches** tab, select the search that you want to export.

3. Click **Export**.

4. Save the file.

 
## Importing a search
{: #k4_import_search}

To import a search, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Searches** tab, select **Import**.

3. Select a file and click **Open**.

The search is added to the list of searches.

## Refreshing the content of a search
{: #k4_refresh_search}

To manually refresh the content of a search, you can click the magnifying glass that is available in the search bar. 

To refresh automatically the data that is shown in the Discover page, you can configure a refresh interval. The current value of the refresh interval is displayed in the menu bar of the Discover page. By default, auto-refresh is set to **OFF**.

Complete the following steps to set a refresh interval:

1. In the Discover page, click the **Time Filter** that is available in the menu bar.

2. Click **Auto Refresh** ![Auto Refresh](images/k4_auto_refresh_icon.jpg "Auto Refresh").

3. Choose a refresh interval from the list. 

    ![Refresh interval options](images/k4_change_autorefresh.jpg "Refresh interval options")


**Note**: After you enable an auto-refresh interval, you can pause it by clicking the pause button ![Pause](images/k4_auto_refresh_pause_icon.jpg "Pause").


## Reloading a search
{: #k4_reload_search}

Complete the following steps to load a saved search:

1. In the toolbar of the Discover page, click the **Load Search** button ![Load search](images/k4_load_icon.jpg "Load search").

2. Select the search that you want to load. 

## Starting a new search
{: #k4_new_search}

To start a new search, click the **New Search** button ![New search](images/k4_new_search_icon.jpg "New search") in the Discover page toolbar.

## Saving a search 
{: #k4_save_search}

When you save a search, the search query string and the currently selected index pattern are saved.

Complete the following steps to save the current search in the Discovery page:

1. In the toolbar of the Discover page, click the **Save Search** button ![Save search](images/k4_save_search_icon.jpg "Save search").

2. Enter a name for the search.

3. Click Save. 
