---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtering your logs by instance ID
{:#k4_filter_logs_by_instance_id}

View and filter {{site.data.keyword.Bluemix}} logs by instance ID.
{:shortdesc}

Complete the following steps to view and filter your logs by instance ID on the Kibana dashboard:

1. Look at the Kibana Discover page to see what subset of your data it displays. For more information, see [Identifying the data that is displayed in your Kibana Discover page](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. In the *Field List*, select one of the following fields to search for a specific instance ID:

    * **instance_ID**: This field lists the different instance IDs that are available in the log for a Cloud Foundry application. 
    * **instance**: This field lists the different GUIDs of all the instances for a container group. 

    For example, the following figure shows different values of instances for a CF app:
    
    ![Filter list that shows the field instance_id](images/k4_filter_instanceid_f1.jpg "Filter list that shows the field instance_id")
   
3. To add a filter that searches for a specific log type, choose the magnifying button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") for the type of log that you want to analyze.

   For example, to add a filter that includes entries for CF app instance *2*, select the magnifying glass button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") that is available for the value *2* in the Fields list section. The following figure shows the filter that includes entries for instance *2*.
    
    ![Filter that includes instance_id entries for instance 2](images/k4_filter_instanceid_f2.jpg "Filter that includes instance_id entries for instance 2")

    To add a filter that searches for entries that do not include a specific instance ID, choose the magnifying button ![Magnifying glass button in exclusive mode](images/k4_exclude_field_icon.jpg "Magnifying glass button in exclusive") for the value.

     For example, to add a filter that excludes entries for CF app instance *2*, select the magnifying glass button ![Magnifying glass button in exclusive mode](images/k4_exclude_field_icon.jpg "Magnifying glass button in exclusive") that is available for the value *2* in the Fields list section. The following figure shows the filter that excludes entries for instance *2*.
     
      ![Filter that excludes instance_id entries for instance 2](images/k4_filter_instanceid_f3.jpg "Filter that excludes instance_id entries for instance 2")

