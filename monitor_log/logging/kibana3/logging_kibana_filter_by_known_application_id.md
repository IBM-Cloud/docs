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


# Filtering your Cloud Foundry App logs by known application ID in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_known_application_id}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

If you know the application ID of your Cloud Foundry app, you can quickly view and filter the logs by the application ID (application_id) of your app on the Kibana dashboard. You can access the Kibana dashboard from the **Logs** tab for your Cloud Foundry app. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Complete the following tasks to view and filter your Cloud Foundry app logs by a known application ID on the Kibana dashboard:

1. Access the **Logs** tab of your Cloud Foundry app. 

    1. Click the app name on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard.
    2. Click the **Logs** tab. 
    
    The logs for your app are displayed.

2. Access the Kibana dashboard for your app. Click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg). The Kibana dashboard is displayed.

3. On the Kibana dashboard, click the **Folder** icon ![Folder icon](images/logging_folder.jpg) to display a menu that lists all recent dashboards. 

    **Note:** In addition to dashboards that you saved by name, the menu lists unnamed dashboards according to the following format: *ALCH_TENANT_ID_application_id*. 

    ![List of dashboards](images/logging_list_of_dashboards.jpg)

4. Select the dashboard with a name that contains your known application_id. 

    The dashboard loads and displays information filtered for your application_id.

5. Optionally, you can add more fields to your filter section, for example, **instance_id** to enable or disable filtering of records by instance ID. 
  
    1. In the **ALL EVENTS** window, click a log event row to display the details for that event. 
	
        ![All Events window displaying details for a selected log event](images/logging_selected_log_event.jpg)
	
    2. Choose an event that displays the field value that you want to filter.
	
    3. Add a filter.
    
        To add a filter that includes information about that specific field value, click the **Magnifying Glass** ![Magnifying glass icon](images/logging_magnifying_glass.jpg) icon in the row of the table that contains the field you want to filter. 
	
        To add a filter that excludes information about that specific field value, click the **Exclusion** ![Exclusion icon](images/logging_exclusion_icon.png) icon in the row of the table that contains the field you want to filter.  

        A new filter condition is added to the Kibana dashboard.
	
	    ![Filter condition for instance_id field](images/logging_instance_id_filter.jpg)
	
6. Save this dashboard with a recognizable name. 

    Click the **Save** icon ![Save icon](images/logging_save.jpg) and enter a name for your dashboard. 

    **Note:** If you try to save a dashboard with a name containing blank spaces, it will not save. Enter a name without spaces and click the **Save** icon.

    ![Save dashboard name ](images/logging_save_dashboard.jpg).


You have created a dashboard that filters your log entries by application ID and instance ID. You can load your saved dashboard at any time by clicking the **Folder** icon ![Folder icon](images/logging_folder.jpg) and by selecting your dashboard by name.
