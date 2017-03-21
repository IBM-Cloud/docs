---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtering logs in Kibana
{:#kibana_filtering_logs}

In the Discover page, you can create search queries and apply filters to constrain the information that is displayed for analysis.
{:shortdesc}

* You can define one or more search queries in the search bar of the Discover page. A search query defines a subset of log entries. Use the Lucene query language to define a search query. 

* You can add filters from the *Fields list* or from the table entries. A filter refines the data selection by including or excluding information. You can enable or disable a filter, invert the filter action, toggle the filter on or off, or remove it entirely. 

After you define a new search, save it so you can reuse it for future analysis in the Discover page or to create visualizations that you can use in custom dashboards. For more information, see [Saving a search](logging_kibana_filtering_logs.html#k4_save_search).

When you perform a new search, the histogram, the table, and the Fields list are updated automatically to show the search results. To find out what data is shown, see [Identifying the data that is displayed in the Discover page](k4_identify_data.html#k4_identify_data).

The following list outline scenarios of how to filter data in your logs:

* You can create custom searches to filter your logs. For more information, see [Filtering logs by defining custom queries](k4_filter_queries.html#k4_filter_queries).

* You can search your log for entries that include a specific text in the value of a field. For more information, see [Filtering your logs for a specific text in a field value](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text).
 
* You can search your log for a specific field value or exclude entries from the log for a specific field value. For more information, see [Filtering your logs for a specific field value](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field).

    * You can filter your logs by log type. For more information, see [Filtering your logs by log type](k4_filter_logs_by_log_type.html#k4_filter_logs_by_log_type).
    * You can filter your CF app logs by source. For more information, see [Filtering your CF app logs by source](k4_filter_logs_by_source.html#k4_filter_logs_by_source).
    * You can filter your logs by instance ID. For more information, see [Filtering your logs by instance ID](k4_filter_logs_by_instance_id.html#k4_filter_logs_by_instance_id).   
    * You can filter your logs by message type. For more information, see [Filtering your logs by message type ID](k4_filter_cf_logs_by_msg_type.html#k4_filter_cf_logs_by_msg_type).  
 
* You can filter your logs to show entries within a time period. For more information, see [Setting a time filter](logging_kibana_set_time_filter.html#set_time_filter).
     

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


## Reloading a search
{: #k4_reload_search}

Complete the following steps to load a saved search:

1. In the toolbar of the Discover page, click the **Load Search** button ![Load search](images/k4_load_icon.jpg "Load search").

2. Select the search that you want to load. 


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




