---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing logs interactively in Kibana
{:#kibana_analize_logs_interactively}

In the the Discover page, you can view and analyze your {{site.data.keyword.Bluemix}} logs interactively. You can define search queries to filter that data by using the Lucene query language. For each search query, you can apply filters to refine the entries that are available for analysis. You can save a search for future reuse.
{:shortdesc}

In {{site.data.keyword.Bluemix_notm}}, by default, the set of data that is displayed in the Discover page when you launch Kibana from the {{site.data.keyword.Bluemix_notm}} UI is configured to only show the entries for the Cloud Foundry (CF) application or container from which you launch Kibana. For more information on how to see what subset of your data the Discover page displays, see [Identifying the data that is displayed](logging_kibana_analize_logs_interactively.html#k4_identify_data).

The following table shows the default query per resource when you launch Kibana from {{site.data.keyword.Bluemix_notm}}:

| Resource | Default Kibana Search Query |
|---------------|---------------|
| CF application   | `application_id:<app_GUID>`    |
| Single Docker container | `instance:<instance_GUID>`    |
| Container group with 2 instances | `instance:<instance_GUID> OR instance:<instance_GUID>` |
{: caption="Table 1. Default query searches" caption-side="top"}

**Note:** 
* Every time you launch Kibana from the {{site.data.keyword.Bluemix_notm}} UI, the data that you can see corresponds to the query that is pre-defined by default and is based on the index pattern.
* A maximum of 500 entries, that correspond to the most recent entries, are displayed in the Discover page. You can modify this value in the Settings page.

When you launch Kibana from a browser, the data that is displayed in the Discover page includes all the log data that is available in the space where you are logged in. The page is not limited to specific containers or apps.

The Discover page includes a histogram and a table that you can customize so you can analyze the data interactively. 

You can perform any of the following tasks to customize the table in the Discover page:

| Task | Description | 
|------|-------------|
| [Add a field column](logging_kibana_analize_logs_interactively.html#kibana_discover_add_fields_to_table) | Add fields to see specific data that is required for analysis instead of the full message. |
| [Rearrange a field column](logging_kibana_analize_logs_interactively.html#kibana_discover_rearrange_fields_in_table) | Move the position of a field in the table to the position where you want it. |
| [View an entry](logging_kibana_analize_logs_interactively.html#kibana_discover_view_entry_in_table) | Expand an entry in the table to see the details of the entry parsed by field or as JSON. |
| [Remove a field column](logging_kibana_analize_logs_interactively.html#kibana_discover_remove_fields_from_table) | Remove a field when it is not required in the view for analysis. |
| [Order entries by value of an indexed field](logging_kibana_analize_logs_interactively.html#kibana_discover_sort_by_table) | Reorder the entries for easier analysis. |
| [Automatically refresh the data](logging_kibana_analize_logs_interactively.html#kibana_discover_view_refresh_interval) | Refresh the data displayed in the table with the latest entries. By default, refresh is **OFF**. |
{: caption="Table 2. Tasks to customize a table" caption-side="top"}

<br>

The following figure shows a sample of a table in the Discover page:

![Discover page in Kibana](images/k4_discover_page.jpg "Discover page in Kibana")

You can define other searches. For more information, see [Filtering logs by defining custom searches](k4_filter_queries.html#k4_filter_queries). When you define a new search, the data that is displayed in the histogram and the table is automatically updated.

To define a new search, use the default search query as your starting point, and then refine the search by performing the following tasks:

* Apply field filters to refine the set of data that you can see. You can toggle each filter, pin it to the page, enable or disable it as needed, and configure it to include or exclude the value. For more information, see [Filtering logs in Kibana](logging_kibana_filtering_logs.html#kibana_filtering_logs).

    **Tip:** If you cannot find a field in the *Fields list* that you expect to see, or some of the magnifying glasses by the listed fields are disabled in the Discover page, reload the list of fields by refreshing the index pattern in the Settings page. For more information, see [Reloading the Field List](logging_kibana_analize_logs_interactively.html#kibana_discover_view_reload_fields).

    For example, if your CF app has multiple instances, you might want to analyze data for a specific instance. You can define a field filter for the specific intance ID value that you want to analyze. 
    
* Customize the *Time Picker* for time-based data. You can define an absolute time range for a query, a relative one, or choose from a set of pre-defined values. For more information, see [Setting a time filter](logging_kibana_set_time_filter.html#set_time_filter).

After you have configured the search that defines the data subset that you want to analyze, you can save it for later reuse.

You can perform any of the following tasks with searches that you define in the Discover page:

| Task | Description |
|------|-------------|
| [Save a search](logging_kibana_filtering_logs.html#k4_save_search) | Save the search for later reuse.  |
| [Delete a search](logging_kibana_filtering_logs.html#k4_delete_search) | Delete a search when is no longer needed. |
| [Export a search](logging_kibana_filtering_logs.html#k4_export_search) | Export a search to share it.  |
| [Reload a search](logging_kibana_filtering_logs.html#k4_reload_search)  | Upload an existing search to analyze a set of data again. |
| [Refresh the data of a search](logging_kibana_filtering_logs.html#k4_refresh_search) | Configure automatic refresh of the data that is displayed through the search.  |
| [Import a search](logging_kibana_filtering_logs.html#k4_import_search) | Import a search.  |
{: caption="Table 3. Tasks to work with searches" caption-side="top"}

<br>

You can also look at statistics in the Discover page:
* You can see stats per field. 
* You can see stats in the histogram per the `@timestamp` that you have configured.

For more information, see [Viewing Field Data Statistics](logging_kibana_analize_logs_interactively.html#kibana_discover_view_fields_stats).

**Note:** The data that is shown in the table and the histogram is static. To keep viewing the latest entries, you must set a refresh interval. 


## Adding field columns to the table
{: #kibana_discover_add_fields_to_table}

The table that is available to analyze data in the Discover page includes the following fields by default:
* **time:** This field indicates when the entry was captured and recorded in {{site.data.keyword.Bluemix_notm}}.
* **_source:**  This field includes the original data of the entry.

You can add a field column to the table by choosing any of the following options:

* Add a field column from the Field list that is available on the page.

    1. In the Discover page, identify the field in the section `Selected Fields`.
    2. Hover over a field in the Fields list.
    
        ![Add field from table view](images/k4_add_field_column_hover.jpg "Add field from table view")
    
    3. To add a field, click **Add**.
    
 * Add a field column from the table view of an expanded entry.

    1. Expand an entry in the table.
    2. In the Table view, identify the field that you want to add.
    
        ![Add field from table view](images/k4_add_field_column.jpg "Add field from table view")
    
    3. Click the **Toggle Column in table** icon ![Toggle column in table](images/k4_toggle_field_icon.jpg).
    

**Note:** When you add one field column to the table for the first time, the *_source* field column that is displayed in the table is hidden. The *_source* field shows the value of each field for each log entry. To see other field values for a log entry in the table after you add a column to the table, see the table view tab or the JSON tab of each entry.

For example, if you add the *application_id* field to the table, the table changes to look as follows:

![Table view after adding a new field](images/k4_add_field_filter_new_table_look.jpg "Table view after adding a new field")


## Automatically refreshing the data
{: #kibana_discover_view_refresh_interval}

By default, in {{site.data.keyword.Bluemix_notm}}, the *Auto refresh* period is set to **OFF** and the data that you can see in Kibana corresponds to the last 15 minutes since you launched Kibana. The 15 minutes correspond to the time filter that is pre-configured. You can change it by setting a different time period. For more information, see [Setting a time filter](logging_kibana_set_time_filter.html#set_time_filter).

Complete the following steps to set an *Auto refresh* period:

1. In the Discover page menu bar, click the Time Picker ![Time picker](images/k4_time_picker_icon.jpg "Time picker").

2. Select the auto-refresh button ![Auto refresh button](images/k4_auto_refresh_icon.jpg "Auto refresh button").

3. Choose a refresh interval.

    ![Options to set an auto refresh time](images/k4_change_autorefresh.jpg "Options to set an auto refresh time")


You can pause the refresh interval by clicking the pause button ![Pause button](images/k4_auto_refresh_pause_icon.jpg "Pause") 


## Identifying the data that is displayed in the Discover page
{:#k4_identify_data}

When you use Kibana to analyze {{site.data.keyword.Bluemix_notm}} logs, the data that you can see depends on how you launch Kibana, the index pattern that is configured, and the custom query and filters that you might have applied.

Consider the following information to identify the data that is available in the table and histogram of the Discover page:

1. Check the index pattern in the Settings page.

    The index pattern defines the search query that is applied by default to show entries in your Kibana pages. By default, the index pattern in pre-configured and set to all the data that is available in a {{site.data.keyword.Bluemix_notm}} space. For example,

    * If you launch Kibana from the {{site.data.keyword.Bluemix_notm}} UI, that is, from the *Log* section of the UI pages of a specific resource like a Cloud Foundry (CF) application or a container, the index pattern that is applied includes all entries that are available in the space.
    
    * If you launch Kibana from a browser, the index pattern that is applied includes all entries that are available in the space that Kibana shows where you are logged in.
        
2. Check the query in the Discover page.  

    The query that is displayed in the Discover page is used to filter the entries that are available by default for analysis. For example:

    * If you type any string in the search bar, the query scans all fields for that string.
    
    * If the query is set to `application_id:<GUID>` where *GUID* is the ID of a CF app, the entries that you can see correspond to all the entries that are available for that CF app in the space that is configured in the index pattern.
    
    * If the query is set to `instance_id:<GUID>` where *GUID* is the ID of a container instance, the entries that you can see correspond to all the entries that are available for that container in the space that is configured in the index pattern.
    
    * If the query is set to `instance_id:<GUID> AND instance_id:<GUID>` where *GUID* is the ID of a container instance, the entries that you can see correspond to all the entries that are available for that container group in the space that is configured in the index pattern.
   
    * If the query is set to `*`, the data is set to all entries that are available in the space that is configured in the index pattern.
    
    * If the query is set to `application_id:<GUID> AND message:"MY_search_text"` where *GUID* is the ID of a CF app and *My_search_text* is the string that you want to search for, the entries that you can see correspond to all the entries that include *My_search_text* in the message field for that CF app entries that are available in the space that is configured in the index pattern.
    
3. Check the field filters that are applied to your query in the Discover page.

    You can define 0 or more field filters to toggle entries based on the value of the field. For example, if a field filter is enabled, the entries that you can see correspond to entries where the value of that field matches.
    

## Ordering entries by value of an indexed field 
{: #kibana_discover_sort_by_table}

You can only sort out entries in the table for fields that are indexed.

To find out what fields are indexed, complete the following steps:

1. In the Discover page, click the configure icon ![Configure icon](images/k4_configure_icon.jpg "configure icon"). The section where you can filter fields in the **Selected fields** section of the page is displayed.

    ![Configuration section to show fields with specific attributes](images/k4_reset_filters.jpg "Configuration section to show fields with specific attributes")
    
2. To identify the fields that are indexed, select **Yes** for the search field **Indexed**.

    ![Indexed attribute](images/k4_reset_filters_indexed_options.jpg "Indexed attribute")
    
 The list of indexed fields is shown.
 
 ![List of indexed fields](images/k4_list_indexed_fields.jpg "List of indexed fields")
  	
 
To sort the entries in a table by the values of an indexed field, complete the following steps: 

1. Hover the mouse over the name of the field that is in the table by which you want to sort the data. The different action buttons appear.
2. Click the sort button for the field by which you want to sort out data. Click the field sort icon a second time to reverse the sort order.

**Note:** When you sort by a time field, by default the entries are sorted in reverse chronological order. The newest entries appear first.


## Rearranging field columns in the table
{: #kibana_discover_rearrange_fields_in_table}

You can rearrange the field columns in the table. Mouse over the header of the column you want to move, and click the **Move column to the left** button or the **Move column to the right** button.
<br>
![Move field in the table](images/k4_add_field_filter_new_table_look.jpg "Move field in the table")


## Reloading the list of fields
{: #kibana_discover_view_reload_fields}

Complete the following steps to reload the list of fields that are displayed in Kibana:

1. Select the Settings page.

    When you select the Settings page, the *Indices* tab opens.
   
2. Select the index pattern to see every field and the field's associated core type as recorded by Elasticsearch. 

3. Click the *Reload field list* button ![Reload field list](images/k4_reload_field_list_icon.jpg "Reload field list") to reload the index pattern fields. 

The list of fields is refreshed.


## Removing field columns from the table
{: #kibana_discover_remove_fields_from_table}

To remove fields from the table, complete the following steps:

1. In the table, identify the field that you want to remove from the table view.
2. Click **Remove column**.
    
    ![Remove a field from table view](images/k4_remove_field_column.jpg "Remove a field from table view")


## Viewing an entry in the table
{: #kibana_discover_view_entry_in_table}

To see the data of an entry in the table, click the expand button ![expand button icon](images/k4_expand_icon.jpg "expand button icon") of the entry that you want to analyze. 

![Table in the Discover page in Kibana](images/k4_table_discover.jpg "Table in the Discover page in Kibana") 	

Then, choose one of the following options to see the data:

* To see the data in a table format, click **Table**. You can see the value of each field that is available for analysis in a table format. For each field, you also have filter buttons and a toggle button.
* To see the data in Json format, click **JSON**.

## Viewing Field Data Statistics
{: #kibana_discover_view_fields_stats}

In the Discover page, you can view statistics for each field in the *Fields list* and in the *histogram*. 

You can see the following information in the Fields list:
* How many entries in the table contain a particular field.
* What are the top 5 values.
* What percentage of entries contain each value.

You can see the following information in the histogram:
* Number of entries in a time range.

To see the stats in the histogram, click a timestamp to see the stats for that period. For example, 

![See stats on a field in the histogram](images/k4_see_stats_on_histogram.jpg "See stats on a field in the histograms")
   	
 	
To see the stats on a field in the Fields list, click the name. For example,

![See stats on a field in the Fields list](images/k4_stats_field_list.jpg "See stats on a field in the Fields list")


