---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtering your logs by log type
{:#k4_filter_logs_by_log_type}

View and filter {{site.data.keyword.Bluemix}} logs by log type.
{:shortdesc}

Complete the following steps to search for entries that include a specific log type:

1. Look at the Kibana Discover page to see what subset of your data it displays. For more information, see [Identifying the data that is displayed in your Kibana Discover page](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. In the *Field List*, select the field **type**.

    For example, in the following figure, only one log type is available: *syslog*
    
    ![Filter list that shows the field log type](images/k4_filter_log_type_F1.jpg "Filter list that shows the field log type")
   
3. To add a filter that searches for a specific log type, choose the magnifying button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") for the type of log that you want to analyze.

    For example, to add a filter that includes log entries for *syslog*, select the magnifying glass button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") that is available for the value *syslog* in the *Fields list* section. The following figure shows the filter that includes entries for the log type *syslog*.

    ![Filter that includes log type entries for syslog](images/k4_filter_log_type_F2.jpg "Filter that includes log type entries for syslog")

    To add a filter that searches for entries that do not include a specific log type, choose the magnifying button ![Magnifying glass button in exclusive mode](images/k4_exclude_field_icon.jpg "Magnifying glass button in exclusive") for the value.

     For example, to add a filter that excludes log entries for *syslog*, select the magnifying glass button ![Magnifying glass button in exclusive mode](images/k4_exclude_field_icon.jpg "Magnifying glass button in exclusive") that is available for the value *syslog* in the *Fields list* section. The following figure shows the filter that excludes entries for the log type *syslog*.
     
     ![Filter that excludes log type entries for syslog](images/k4_filter_log_type_F3.jpg "Filter that excludes log type entries for syslog")



