---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtering your Cloud Foundry App logs by instance ID in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_instance_id}
<!-- Provide an appropriate ID above -->

View and filter {{site.data.keyword.Bluemix_notm}} instance logs by the instance ID (instance_id) of your app on the Kibana dashboard. You can access the Kibana dashboard from the **Logs** tab for your Cloud Foundry app. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Complete the following tasks to view and filter your Cloud Foundry app logs by instance_id on the Kibana dashboard:

1. Access the **Logs** tab of your Cloud Foundry app. 

    1. Click the app name on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard.
    2. Click the **Logs** tab. 
    
    The logs for your app are displayed.

2. Access the Kibana dashboard for your app. Click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg). The Kibana dashboard is displayed.

3. On the Kibana dashboard, click the **Go to saved default** icon; ![Go to saved default icon](images/logging_default_dash.jpg) to display all the logs for a space. In the **ALL EVENTS** window, click the right arrow icon to show all fields. 

    ![All Events window with right arrow icon](images/logging_all_events_no_fields.jpg)

4. In the **Fields** pane, select **application_id** and **instance_id** to display the application_id and instance_id fields in the **ALL EVENTS** window.

    ![All Events window with application_id and instance_id fields selected](images/logging_all_events_app_instance_select.jpg)

5. In the **ALL EVENTS** window, click a log event row to display the details for that event. Choose an event that displays the instance_id that you want to filter.

    ![All Events window displaying details for a selected log event](images/logging_selected_log_event.jpg)

6. Add a filter to include or exclude information about an app ID. 

    * To add a filter that includes information about a specific application ID, click the **Magnifying Glass** ![Magnifying glass icon](images/logging_magnifying_glass.jpg) icon in the application_id row of the table. 
    
           ![Filter condition for application_id field](images/logging_application_id_filter.jpg)
    
    * To add a filter that excludes information about a specific application ID, click the **Exclusion** ![Exclusion icon](images/logging_exclusion_icon.png) icon in the application_id row of the table. 
    
           ![Filter condition to exclude an application ID](images/logging_application_id_exclude_filter.jpg)
    
    A new filter condition is added to the Kibana dashboard.
 

7. Add a filter to include or exclude information about an app instance ID. 

    * To add a filter that includes information about a specific instance ID, click the **Magnifying Glass** ![Magnifying glass icon](images/logging_magnifying_glass.jpg) icon in the instance_id row of the table. 

    ![Filter condition for instance_id field](images/logging_instance_id_filter.jpg)

     * To add a filter that excludes information about a specific instance ID, click the **Exclusion** ![Exclusion icon](images/logging_exclusion_icon.png) icon in the instance_id row of the table. 
    
           ![Filter condition to exclude an instance ID](images/logging_application_instance_id_exclude_filter.jpg)
    
    A new filter condition is added to the Kibana dashboard.

9. Save the dashboard. When you are finished creating your filter, click the **Save** icon ![Save icon](images/logging_save.jpg) and enter a name for your dashboard. 

    **Note:** If you try to save a dashboard with a name containing blank spaces, it will not save. Enter a name without spaces and click the **Save** icon.

    ![Save dashboard name ](images/logging_save_dashboard.jpg).

You have created a dashboard that filters your log entries by instance_id. You can load your saved dashboard at any time by clicking the **Folder** icon ![Folder icon](images/logging_folder.jpg) and by selecting your dashboard by name. 
