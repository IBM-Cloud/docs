---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtering logs by defining custom search queries
{:#k4_filter_queries}

In the search bar of the Discover page, you can define and save search queries by using the Lucene query language. For each search, you can apply filters to refine the entries that are available for analysis.
{:shortdesc}

Complete the following tasks to filter your logs by using a custom search:

1. Access the **Logs** tab of your Cloud Foundry (CF) app or container. 

    1. Click the app name or container in the {{site.data.keyword.Bluemix}} dashboard.
    2. For CF applications, click the **Logs** tab. For containers, click **Monitoring and logs**, and then select the **Logging** tab.
    
    The logs are displayed.

2. Access Kibana. Click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg). The Kibana dashboard is displayed.

    When you access Kibana, the default search is applied. You can see the logs for the list of instances of the resource you launched Kibana for. You can filter the logs for any or all of the {{site.data.keyword.Bluemix_notm}} resources in that space.

Rather than "keyword", the correct term is "term" for Lucene.

3. Look at the Discover page to see what subset of your data it displays. For more information, see [Identifying the data that is displayed in your Kibana Discover page](logging_kibana_analize_logs_interactively.html#k4_identify_data). Then, modify the default query to filter entries.

    **Note:** Use the Lucene query language to define your custom query. For more information, see [Apache Lucene - Query Parser Syntax  ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    When Kibana is launched from {{site.data.keyword.Bluemix_notm}}, to modify the query and define multiple search criteria, you can use the logical terms **AND** and **OR**. These operators must be in uppercase.    
    
    * To search for a keyword, or part of a keyword, enter a word, followed by a wildcard symbol \*; for example, `Java*`. 
    * To search for a particular phrase, enter that phrase in double quotation marks; for example, `"Java/1.8.0"`.
    * To create more complex searches, you can use the logical terms AND and OR; for example `"Java/1.8.0" OR "Java/1.7.0"`.
    * To search for a value within a particular field, enter your search in the following form: *log_field_name:search_term*; for example, `instance_id:"1"`.
    * To search for a range of values for a particular log field, enter your search in the following form: *log_field_name:[start_of_range TO end_of_range]*; for example, `instance_id:["1" TO "2"]`.

     For example, for a CF app, you can create a query `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]`  that only lists entries for instances *0* and *1*. 

4. Save the query so you can reuse it later. For more information, see [Saving a search](logging_kibana_filtering_logs.html#k4_save_search). 

**Note:** If you need to delete a query, see [Deleting a search](logging_kibana_filtering_logs.html#k4_delete_search).



