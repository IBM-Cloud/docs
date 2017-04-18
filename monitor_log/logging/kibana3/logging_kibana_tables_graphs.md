---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Creating tables and graphs from queries in Kibana
{: #logging_kibana_tables_graphs}


Use Kibana to create graphs and tables for your queries to visualize your log data and compare results. You can access the Kibana dashboard from the **Logs** tab for your Cloud Foundry app. 
{:shortdesc}

The Kibana dashboard is laid out as a series of rows, with each row containing one or more panels. You can configure panels to display graphical representations of your data. Use queries to determine which data to display. To create a graph or table, you must first create a blank row; then, create a panel. If you access the Kibana dashboard from the **Logs** tab on your CF app, the dashboard automatically displays two panels: a histogram and a table.

Complete the following tasks to add a graph or table on the Kibana dashboard:

1. To access the **Logs** tab of your Cloud Foundry app, click the app name in the **Cloud Foundry Apps** table on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard; then, click the **Logs** tab. The logs for your app are displayed.

2. To access the Kibana dashboard display for your app, click **Advanced View** ![Advanced view link](images/logging_advanced_view.jpg "Advanced view link"). The Kibana dashboard is displayed.

3. On the Kibana dashboard, scroll to the bottom of the dashboard and click **ADD A ROW** ![Add a row icon](images/logging_add_row.jpg "Add a row icon") to create a row for the panel you want to add. The Dashboard Settings pane is displayed. 
	
	![Dashboard settings pane](images/logging_dashboard_settings.jpg "Dashboard settings pane")
	
	In the Add Row pane, enter a name for your row in the **Title** field; then, click **Create Row**. A new row is added. You can adjust the order of the rows by clicking the **Up arrow** or **Down arrow** icons next to the row titles. When you have set the order of rows, click **Save**. An empty row is created on the Kibana dashboard.

4. Add a panel by clicking **Add panel to empty row**. The Row Settings pane is displayed.

    ![Row settings pane](images/logging_row_settings.jpg "Row settings pane")
	
	You can choose different panel types such as **table**, **histogram**, or **terms** from the **Select Panel Type** drop-down list. Select **terms** to create a bar chart, pie chart, or table based on your queries. A range of configuration options are displayed in the Row Settings pane.
	
	![Adding a panel in the row settings pane](images/logging_add_panel.jpg "Adding a panel in the row settings pane")
	
	Configure your panel. Enter a **Title** for your graphical display. Select the **Span** of your panel from the drop-down list; the **Span** determines the width of your panel across the dashboard. In the Parameters section, delete the contents of **Field** and enter a valid log field; for example, `instance_id`. 

5. In the View Options section, select **bar**, **pie**, or **table** from the **Style** drop-down list to choose a bar chart, pie chart, or table. In the Queries section, select **selected** from the **Queries** drop-down list to use the log data from your dashboard queries. Finally, click **Save**. Your new panel is displayed on the dashboard.

	![Dashboard displaying panel containing bar chart](images/logging_bar_chart_panel.jpg "Dashboard displaying panel containing bar chart")
	
6. To change this panel so that it displays a table, click the **Configure** icon ![Configure icon](images/logging_dashboard_config_panel.jpg "Configure icon"). The Terms Settings pane is displayed. 

	![Terms Settings pane](images/logging_terms_settings.jpg "Terms Settings pane")
	
	Click the **Panel** tab; then, select **table** from the **Style** drop-down list. Click **Save** to update the panel and return to the dashboard.

7. Add further rows and panels to your dashboard. When you are finished, save the changes to this dashboard by clicking the **Save** icon.

    **Note:** If you try to save a dashboard with a name containing blank spaces, it will not save. Enter a name without spaces and click the **Save** icon.

    ![Save dashboard name](images/logging_save_dashboard.jpg "Save dashboard name").


