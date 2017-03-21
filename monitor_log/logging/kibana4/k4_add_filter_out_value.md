---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Adding a filter for a value that is not listed in the *Fields list*
{:#k4_add_filter_out_value}

To add a filter for a value that is not shown in the *Field list*, search for records that include that value through a query. Then. add the filter from the table entry that is available in the Discover page. 
{:shortdesc}

Complete the following steps to add a filter for value that is not available in the list shown in the *Fields list* section:

1. Look at the Kibana Discover page to see what subset of your data it displays. For more information, see [Identifying the data that is displayed in your Kibana Discover page](logging_kibana_analize_logs_interactively.html#k4_identify_data).

    For example, the following figure shows the values of instances for a CF app in the *Fields list*. 
    
    ![Show values in Field list](images/k4_add_filter_f1.jpg "Show values in Field list")
    
    You are interested in instance number *3*, but it is not available in the list that you can see.

2. In the Discover page, modify the query to search for a specific field value.

    For example, to search for instance *3*, the query that you enter is the following: 
   `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![Modify query](images/k4_add_filter_f2.jpg "Modify query")
    
    In the table, you can see any records that match your query. 
    
 3. Expand one record, and select the magnifying glass button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") to add a filter.
 
     For example, to add a filter for the instance ID with value *3*, click the magnifying glass button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") by the field *instance_id*.
     
     ![Show table](images/k4_add_filter_f3.jpg "Show table")
     
4. Check that the filter has been added.

    For example, the following figure shows the filter enabled after you add it from the table.
    
    ![Show filter](images/k4_add_filter_f4.jpg "Show filter")
    
    
