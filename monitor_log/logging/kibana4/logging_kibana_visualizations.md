---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing logs in Kibana by using visualizations 
{:#logging_kibana_visualizations}

Use the *Visualize* page in Kibana to create visualizations such as graphs and tables that you can use to analyze your log data and compare results. 
{:shortdesc}

You can use a visualization individually to analyze your logs. 

* You can create visualizations from a search that you define and save in the *Discover* page or from a new query that you define in the *Visualize* page. The search define the subset of data that a visualization displays.

* The type of visualization that you choose determines how the data is displayed for analysis.

The following table lists different visualization types:

| Type of visualization | Description |
|-----------------------|-------------|
| Area chart | Displays graphically quantitative data. Use to compare two or more sets of aggregated data. |
| Data table | Displays raw data in tabular form for a composed aggregation. |
| Line chart | Displays time based data. Use to compare two or more sets of time-based aggregated data. |
| Markdown widget | Use to display text information. |
| Metric | Use to show a count of hits, or the exact average a numeric field. |
| Pie chart | Use to display different values of a field. | 
| Vertical bar chart | Displays data that is time-based and data that is not time-based. Use to group data. |
{: caption="Table 1. Visualization types" caption-side="top"}

In the Visualize page, you can perform any of the following tasks:

| Task | More information |
|------|------------------|
| [Create a new visualization](logging_kibana_visualizations.html#logging_k4_visualizations_create) | You can create visualizations from a search that you define and save in the *Discover* page or from a new query that you define in the *Visualize* page. |
| [Save a visualization](logging_kibana_visualizations.html#logging_kibana_visualizations_save) | You can save visualizations for later reuse. |
| [Load a visualization](logging_kibana_visualizations.html#logging_kibana_visualizations_reload) | You can upload a visualization to either update its data, mofify it, analyze the data. |
| [Delete a visualization](logging_kibana_visualizations.html#logging_kibana_visualizations_delete) | Delete visualizations that are not required. |
| [Export a visualization](logging_kibana_visualizations.html#logging_kibana_visualizations_export) | You can export a visualization as a JSON file.  |
| [Import a visualization](logging_kibana_visualizations.html#logging_kibana_visualizations_import) | You can import a visualization as a JSON file.  |
| [Share a visualization](logging_kibana_visualizations.html#logging_kibana_visualizations_share) | You can share a visualization through your HTML source or through the Kibana dashboard.  |
{: caption="Table 2. Tasks to work with visualizations" caption-side="top"}


## Creating visualizations from queries in Kibana
{:#logging_k4_visualizations_create}

Complete the following steps to create a visualization from the Visualize page:

1. Launch Kibana, and then, select the **Visualize** page.

2. Create a new visualization. In the toolbar, click the **New Visualization** button ![New visualization](images/k4_visualization_new_icon.jpg "New visualization").

3. Select a visualization.
    
4. Select a search source. Choose one of the following options:

    * Click **From a new search**.
    * Click **From a saved search**. 
  
5. Configure the query.

    * If you select **From a saved search**, select a search query. The query is used to retrieve the data that is used for the visualization. 

        After you select a search, the visualization builder opens and loads the data for the selected query. The following message is displayed: *This visualization is linked to a saved search: your_search_name*. 
	
	**Note**: Any changes that you make to a saved search are automatically reflected in the visualization. To disable automatic updates that you make to the query that is linked to this visualization, double click the message *This visualization is linked to a saved search: your_search_name* 

    * If you select **From a new search**, define a new query. The query is used to define the subset of data that is retrieved and used by  the visualization.

        For more information, see [Filtering logs by defining custom queries](k4_filter_queries.html#k4_filter_queries).

6. In the visualization builder, select a metric aggregations for the Y axis.

7. In the visualization builder, select a bucket type. Then, select one bucket aggregation.
  
8. Add sub-buckets to break down the data.

For more information about Kibana, see the [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

## Deleting a visualization
{:#logging_kibana_visualizations_delete}

To delete a visualization, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Visualizations** tab, select the visualizations that you want to delete.

3. Click **Delete**.


## Exporting a visualization
{:#logging_kibana_visualizations_export}

To export a visualization as a JSON file, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Visualizations** tab, select the visualization that you want to export.

3. Click **Export**.

4. Save the file.

## Importing a visualization
{:#logging_kibana_visualizations_import}

To import a visualization as a JSON file, complete the following steps in the Settings page:

1. In the Settings page, select the **Objects** tab.

2. In the **Visualizations** tab, select **Import**.

3. Select a file and click **Open**.

The visualization is added to the list of visualizations.


 
## Loading a visualization
{:#logging_kibana_visualizations_reload}

Complete the following steps to load a saved visualization:

1. In the toolbar of the Visualize page, click the **Load Saved Visualization** button ![Load saved visualization](images/k4_visualization_open_icon.jpg "Load saved visualization").

2. Select the visualization that you want to load. 


## Saving a visualization
{:#logging_kibana_visualizations_save}

Complete the following steps to save a visualization in the Visualize page:

1. In the toolbar of the Visualize page, click the **Save Visualization** button ![Save visualization](images/k4_visualization_save_icon.jpg "Save visualization").

2. Enter a name for the visualization.

3. Click Save. 



## Sharing a visualization
{:#logging_kibana_visualizations_share}

Complete the following steps to share a visualization in the Visualize page:

1. In the toolbar of the Visualize page, click the **Share Visualization** button ![Share visualization](images/k4_visualization_share_icon.jpg "Share visualization").

2. Choose one of the following actions:

    * **Embed this visualization**: Select this option to share the visualization through your HTML source. 
    
        Click the copy button ![Copy to clipboard](images/k4_copy_to_clipboard.jpg "Copy to clipboard") to copy the HTML code that you can use to embed the visualization in your HTML source. 
	
	**Note**: To see the visualization, the users must be able to access Kibana.
	
    * **Share a link**:  Select this option to share the visualization in Kibana with other users.



