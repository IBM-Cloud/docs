---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Filtering your Cloud Foundry App logs by log type in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_component_filter}
<!-- Provide an appropriate ID above -->

View and filter {{site.data.keyword.Bluemix_notm}} application logs by component (log type) on the Kibana dashboard. You can access the Kibana dashboard from the **Logs** tab for your Cloud Foundry app. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Complete the following tasks to view and filter your Cloud Foundry app logs by log type on the Kibana dashboard:

1. Access the **Logs** tab of your Cloud Foundry app. 

    1. Click the app name on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard.
    2. Click the **Logs** tab. 
    
    The logs for your app are displayed.

2. Access the Kibana dashboard for your app. Click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg). The Kibana dashboard is displayed.

3. In the **ALL EVENTS** window, click the right arrow icon to show all fields. 

    ![All Events window with right arrow icon](images/logging_all_events_no_fields.jpg)

4. In the **Fields** pane, select **source_id** to display the component that generated each log entry in the **ALL EVENTS** window.

    ![All Events window with source_id field selected](images/logging_component.png)

5. In the **ALL EVENTS** window, click a log event row to display the details for that event. Choose an event that displays the source_id that you want to filter.

    ![All Events window displaying details for a selected log event](images/logging_component_add_filter.png)

6. Add a filter to include or exclude information for a component (log type). 

    * To add a filter that includes a component value, click the **Magnifying Glass** ![Magnifying glass icon](images/logging_magnifying_glass.jpg) icon in the source_id row of the table. 

        ![Filter condition for source_id field](images/logging_component_filter.png) 

    * To add a filter that excludes a component value, click the **Exclusion** ![Exclusion icon](images/logging_exclusion_icon.png) icon in the source_id row of the table. 
    
         ![Filter condition to exclude source_id field](images/logging_component_add_exclusion_filter.png) 
     
     A new filter condition is added to the Kibana dashboard.

7. Optionally, you can repeat the previous step and add filters for each component. To see the full list of components, see [Log format](../logging_log_ov.md#log_format).

    The following image shows the dashboard with multiple filters for different components:
    
    ![Multiple filter conditions for the source_id field](images/logging_component_multiple_filters.png)

8. Save the dashboard. 

    When you are finished adding filters and customizing the dashboard, click the **Save** icon ![Save icon](images/logging_save.jpg) and enter a name for your dashboard. 
      
    **Note:** If you try to save a dashboard with a name containing blank spaces, it will not save. Enter a name without spaces and click the **Save** icon.
    
    ![Save dashboard name ](images/logging_save_dashboard.jpg)

You have created a dashboard that filters your log entries by component (log type). You can load your saved dashboard at any time by clicking the **Folder** icon ![Folder icon](images/logging_folder.jpg) and by selecting your dashboard by name.


