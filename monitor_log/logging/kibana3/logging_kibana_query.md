---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"

---
<!-- Copyright info and last updated date at top of file: REQUIRED
    The copyright and lastupdated info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    The value "lastupdated" must be followed by a machine date in quotes in the following format: "YYYY-MM-DD"
    The value for "years" must be indented 2 spaces under "copyright", followed by "lastupdated" which should start on its own non-indented line.

-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

<!-- Additional task topic: OPTIONAL
This is the template for additional task topics that are needed beyond the basic tasks in the getting started index.md.  As needed, other task topics can be included, with titles such as "Configuring x", "Administering y", "Managing z", etc. This topic is a peer of the getting started index.md in the <servicename>.ditamap. This topic can have one level of children and they also can be referenced in <servicename>.ditamap -->

# Filtering your Cloud Foundry App logs with queries in Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_query}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Use Kibana to create queries to search your logs for key terms and filter by those terms. With Kibana, you can compare queries visually on the dashboard. You can access the Kibana dashboard from the **Logs** tab for your Cloud Foundry app. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Complete the following tasks to create a query for your Cloud Foundry app logs on the Kibana dashboard:

1. Access the **Logs** tab of your Cloud Foundry app. 

    1. Click the app name on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard.
    2. Click the **Logs** tab. 
    
    The logs for your app are displayed.

2. Access the Kibana dashboard for your app. Click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg). The Kibana dashboard is displayed.

3. On the Kibana dashboard, click **QUERY** ![Query icon](images/logging_query.jpg) to display the field. When you access Kibana to view your app logs from the **Logs** tab for your app, a query is created to show all logs for the application_id of your app.
	
    To edit your query, click the **QUERY** field and enter a search term.

    * To search for a keyword, or part of a keyword, enter a word, followed by a wildcard symbol \*; for example, `Java*`. 
	* To search for a particular phrase, enter that phrase in double quotation marks; for example, `"Java/1.8.0"`.
	* To create more complex searches, you can use the logical terms AND and OR; for example `"Java/1.8.0" OR "Java/1.7.0"`.
	* To search for a value within a particular field, enter your search in the following form: *log_field_name:search_term*; for example, `instance_id:1`.
	* To search for a range of values for a particular log field, enter your search in the following form: *log_field_name:[start_of_range TO end_of_range]*; for example, `instance_id:[1 TO 2]`.

4. If you want to compare the results of two seperate queries, you can add another query term to your dashboard. To add another query, click the **+** icon at the end of the **QUERY** field.

    ![Query field](images/logging_query_field.jpg)
	
    A new **QUERY** field that contains the wildcard \* is displayed. This query tells Kibana to include all entries.
	
    ![Additional Query field](images/logging_additional_query_field.jpg)
	
    Your dashboard is updated with the results of your new query. The **EVENTS BY TIME** pane displays a graphical representation for both queries, along with the number of terms for each query in parentheses. 
	
    ![Dashboard displaying graph for both queries](images/logging_dashboard_queries.jpg)
	
5. Click the new **QUERY** field to edit its contents and add a query condition; for example, `instance_id:1`. Use the **EVENTS BY TIME** pane to compare the results of your queries.

    ![Dashboard displaying graph for both queries](images/logging_dashboard_queries2.jpg)

6. To delete a query, move your mouse over the **QUERY** field that you want to delete to reveal the **delete** icon. Click the **delete** icon.

    ![Query field with delete icon](images/logging_delete_query.jpg)

7. To save this dashboard with a recognizable name, click the **Save** icon ![Save icon](images/logging_save.jpg) and enter a name for your dashboard. 

    **Note:** If you try to save a dashboard with a name containing blank spaces, it will not save. Enter a name without spaces and click the **Save** icon.

    ![Save dashboard name ](images/logging_save_dashboard.jpg)


