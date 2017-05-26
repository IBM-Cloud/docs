---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-26"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Creating a Grafana dashboard
{:#create_grafana_dashboard}

Create a custom Grafana dashboard to display metrics for all of the containers that run in a space of your {{site.data.keyword.Bluemix}} organization.
{:shortdesc}

Complete the following steps to create a Grafana dashboard:

1. Launch Grafana from a web browser. For more information, see [Navigating to the Grafana dashboard from a web browser](navigating_grafana.html#launch_grafana_from_browser).

2. Save the default dashboard.

    1. In the toolbar, click the Save icon.
    2. Enter a name for the dashboard.
    3. Next to the name field, click the Save icon.
   
3. Disable the automatic page refresh while you work on your dashboard. 

    1. Click the time picker in the header.
    2. Select **Auto-refresh**.
    3. Click **Off**.
 
 5. Delete the example rows.
 
     1. Next to the *Welcome to Grafana* header, hover your cursor on the Row menu slider and then, click the Row menu icon that slides out.
     2. Click **Delete row**, and then click **Yes**.
     
     Repeat these steps to remove the Documentation Links and the First Graph rows. 
     
     In the page header, adjust the time picker to ensure you can see data. The default value is 6 hours to a few seconds ago. Select **Last 30d**.
     
6. Add a visualization.

    * To add a CPU idle visualization, see [Adding a CPU idle visualization](create_grafana_dashboard.html#grafana_add_cpu).
    * To add a memory used visualization, see [Adding a memory used visualization](create_grafana_dashboard.html#grafana_add_mem).
        
7. Save the custom dashboard.

    1. In the toolbar, click the Save icon.
    2. Enter a name for the dashboard.
    3. Next to the name field, click the Save icon.
    

## Adding a CPU idle visualization
{:#grafana_add_cpu}

To add a CPU idle graph that includes data from all of the containers in your space, complete the following steps:

1. Click the **Add a row** button. A Row menu slider is displayed on the side of the row.
    
2. Hover your cursor on the row menu slider and then click the Row menu icon that slides out.

3. Click **Add Panel**. Then, click **graph**.

4. Click the graph title to open the panel menu and click **Edit**. 

    The rest of the dashboard is hidden; only the editor for this graph and a preview of the graph is displayed.
    
5. In the Metrics tab, construct a query to collect data for the graph. 

    For example, when you work with containers that are deployed in a {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure, the query format includes the space ID, a container group ID, and a single container instance ID in the following format: `space_ID.group_ID.instance_ID.metric`
        
    1. In the A row, click **Select metric**. Then, select your space ID.
    2. Click **Select metric** and select the asterisk (\*).
    
    When you select (\*), the data includes metrics from every container group in the space. Optionally, you can manipulate this format with a regular expression to include metrics only from certain containers. For example, if you wanted to see metrics only from single containers and exclude container groups, you click **Select metric** and select **0000**.
        
    3. Click **Select metric** and select the asterisk (\*) again. This format includes metrics from every single container in the space.
        
    4. Click **Select metric** and **cpu-0**.
        
    5. Click **Select metric** and **cpu-idle**. The graph preview updates to display the metrics that match this query.
    
6. Optional: Customize the display of the graph.
    
    * To give the graph a name, click the General tab, and in the Title field, enter a name for the graph, for example: CPU Idle
    * To give the vertical axis a label, click the Axes and grid tab, and in the Left Y Axis section, in the Label field, enter CPU.
    * To change the background color of the graph, in the Grid threshholds section, for Level 2, click the Background color picker icon and change the background color to white or light gray.
    
    In the header, click **Back to dashboard**.
    
7. To save the changes you made to this dashboard, in the header, click the Save icon and then, click the Save icon in the menu.


## Adding a memory used visualization
{:#grafana_add_mem}

Complete the following steps to add a memory used visualization:

1. Click the Add a row button. A Row menu slider row menu slider is displayed on the side of the row.
   
2. Hover your cursor on the row menu slider and then click the Row menu icon that slides out.

    1. Click Add Panel > graph.
    2. Click Edit. The rest of the dashboard is hidden; only the editor for this graph and a preview of the graph is displayed.
    
3. In the Metrics tab, construct a query to collect data for the graph. 

    For example, when you work with containers that are deployed in a {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure, the query format includes the space ID, a container group ID, and a single container instance ID in the following format: space_ID.group_ID.instance_ID.metric
        
    1. In the A row, click **Select metric**. Then, select your space ID.
    2. Click **Select metric** and select the asterisk (\*).
    
    When you select (\*), the data includes metrics from every container group in the space. Optionally, you can manipulate this format with a regular expression to include metrics only from certain containers. For example, if you wanted to see metrics only from single containers and exclude container groups, you click **Select metric** and select **0000**.
    
    3. Click **Select metric** and select the asterisk (\*) again. This format includes metrics from every single container in the space.
        
    4. Click **Select metric** and **memory**.
        
    5. Click **Select metric** and **memory-used**. The graph preview updates to display the metrics that match this query.
    
6. Optional: Customize the display of the graph.
    
    * To give the graph a name, click the General tab, and in the Title field, enter a name for the graph, for example: Memory Used
    *  To change the format for the vertical axis values, click the Axes and grid tab, and in the Left Y Axis section, for the Format, select bytes.
    * To give the vertical axis a label, in the Label field, enter Memory.
    * To change the background color of the graph, in the Grid threshholds section, for Level 2, click the Background color picker icon and change the background color to white or light gray.
    
    In the header, click **Back to dashboard**.

7. To save the changes you made to this dashboard, in the header, click the Save icon and then, click the Save icon in the menu.

