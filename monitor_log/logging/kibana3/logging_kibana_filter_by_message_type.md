---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-16"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtering your Cloud Foundry App logs by message type in Kibana
{: #logging_kibana_message_type_filter}

View and filter {{site.data.keyword.Bluemix_notm}} application logs by message type on the Kibana dashboard. You can access the Kibana dashboard from the **Logs** tab for your Cloud Foundry app. 
{:shortdesc}

Complete the following tasks to view and filter your Cloud Foundry app logs by message type on the Kibana dashboard:

1. Access the **Logs** tab of your Cloud Foundry app. 

    1. Click the app name on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard.
    2. Click the **Logs** tab. 
    
    The logs for your app are displayed.

2. Access the Kibana dashboard for your app. Click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg "Advanced view link"). The Kibana dashboard is displayed.

3. In the **ALL EVENTS** window, click the right arrow icon to show all fields. 

    ![All Events window with right arrow icon](images/logging_all_events_no_fields.jpg "All Events window with right arrow icon")

4. In the **Fields** pane, select **message_type** to display the component that generated each log entry in the **ALL EVENTS** window.

    ![All Events window with message_type field selected](images/logging_message_type.png "All Events window with message_type field selected")

5. In the **ALL EVENTS** window, click a log event row to display the details for that event. Choose an event that displays the **message_type** that you want to filter.

    ![All Events window displaying details for a selected log event](images/logging_message_type_add_filter.png "All Events window displaying details for a selected log event")

6. Add a filter to include or exclude information about a message type. 

    * To add a filter that includes information about a message type, click the **Magnifying Glass** ![Magnifying glass icon](images/logging_magnifying_glass.jpg "Magnifying glass icon") icon in the message_type row of the table. 
    
           ![Filter condition for message_type field](images/logging_message_type_filter.png "Filter condition for message_type field")
    
    * To add a filter that excludes information about a message type, click the **Exclusion** ![Exclusion icon](images/logging_exclusion_icon.png "Exclusion icon") icon in the message_type row of the table. 
    
    A new filter condition is added to the Kibana dashboard.

7. Optionally, repeat the previous step to add a filter for other message types. To see the full list of message types, see [Log format](../logging_view_kibana3.html#kibana_log_format_cf).

9. Save the dashboard.    
        
    When you are finished creating your filters, click the **Save** icon ![Save icon](images/logging_save.jpg "Save icon") and enter a name for your dashboard. 
      
    **Note:** If you try to save a dashboard with a name containing blank spaces, it will not save. Enter a name without spaces and click the **Save** icon.
    
    ![Save dashboard name](images/logging_save_dashboard.jpg "Save dashboard name").

You have created a dashboard that filters your log entries by message type. You can load your saved dashboard at any time by clicking the **Folder** icon ![Folder icon](images/logging_folder.jpg "Folder icon") and by selecting your dashboard by name.
