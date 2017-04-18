---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtering your Cloud Foundry App logs by time in Kibana
{: #logging_kibana_time_filter}


View and filter {{site.data.keyword.Bluemix_notm}} application logs by time on the Kibana dashboard. You can access the Kibana dashboard from the **Logs** tab for your Cloud Foundry app. 
{:shortdesc}

Complete the following tasks to view and filter your Cloud Foundry app logs by time on the Kibana dashboard:

1. Access the **Logs** tab of your Cloud Foundry app. 

    1. Click the app name on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard.
    2. Click the **Logs** tab. 
    
    The logs for your app are displayed.

2. Access the Kibana dashboard for your app. Click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg "Advanced view link"). The Kibana dashboard is displayed.


3. On the Kibana dashboard, click the **Time Filter**; ![Kibana time filter](images/logging_kibana_time_filter.jpg "Kibana time filter") then, select **Custom** from the drop-down menu. The following window is displayed:

    ![Custom time filter on the Kibana dashboard](images/logging_custom_time_filter.jpg "Custom time filter on the Kibana dashboard")

4. Click the **From** and **To** fields to edit the beginning and end time for your filter. 
    
    To include logs to the present moment, click the **now** link. 
    When you are satisfied with your time range, click **Apply**. 

The Kibana dashboard now displays logged events for your customized time filter.
