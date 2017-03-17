---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtering your CF app logs by source
{:#k4_filter_logs_by_source}

View and filter by source type Cloud Foundry application logs through the Kibana dashboard.
{:shortdesc}

Complete the following steps to search for entries that include a specific log source:

1. Look at the Kibana Discover page to see what subset of your data it displays. For more information, see [Identifying the data that is displayed in your Kibana Discover page](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. In the *Field List*, select the field **source_id**.

    ![Filter list that shows the field source_id](images/k4_filter_sourceid_F1.jpg "Filter list that shows the field source_id")     

3. To add a filter that searches for entries that include a specific source_id, choose the magnifying button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") for that value.

    For a list of log sources that are available for CF apps, see [Log sources for CF apps](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources).

    For example, to add a filter that includes log entries about the start, stop, or crash of a CF application, select the magnifying glass button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") that is available for the value *CELL* in the *Fields list* section. The following figure shows the filter for the source_id value *CELL* enabled.
    
    ![Filter that includes the field value](images/k4_filter_sourceid_F2.jpg "Filter that includes the field value")

    To add a filter that searches for entries that do not include a specific source_id, choose the magnifying button ![Magnifying glass button in exclusive mode](images/k4_exclude_field_icon.jpg "Magnifying glass button in exclusive mode") for the value.
    
    For example, to add a filter that excludes log entries about the start, stop, or crash of a CF application, select the magnifying glass button ![Magnifying glass button in inclusive mode](images/k4_exclude_field_icon.jpg "Magnifying glass button in inclusive") that is available for the value *CELL* in the *Fields list* section. The following figure shows the filter that excludes entries for the source_id value *CELL*.

    ![Filter that excludes the field value](images/k4_filter_sourceid_F3.jpg "Filter that excludes the field value")




