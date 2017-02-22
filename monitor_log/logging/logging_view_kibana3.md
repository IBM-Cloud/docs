---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing logs in Kibana
{: #analyzing_logs_Kibana3}

In {{site.data.keyword.Bluemix}}, you can use Kibana, an open source analytics and visualization platform, to monitor, search, analyze, and visualize your data in a variety of graphs, for example charts and tables. Use Kibana to perform advanced analytical tasks.
{:shortdesc}

You can launch Kibana in any of the following ways:

* From the Cloud Foundary App dashboard

    You can launch to your specific CF App logs in Kibana, in context to that specific App.
    
    The query that is used to filter the data that is displayed in the dashboard retrieves log entries for the Cloud Foundry application. The log information that the Kibana dashboard displays by default is all related to a single Cloud Foundry application and all its instances. For more information, see [Getting to the Kibana dashboard from the {{site.data.keyword.Bluemix}} dashboard](logging_view_kibana3.html#launch_Kibana_from_bluemix).

* From a direct browser link

    You may want to launch to custom Kibana dashboard that aggregates data from services within a provided {{site.data.keyword.Bluemix}} space.
    
    The query that is used to filter the data that is displayed in the dashboard retrieves log entries for a space in the {{site.data.keyword.Bluemix}} organization. The log information that the Kibana dashboard displays includes records for all resources that are deployed within the space of the {{site.data.keyword.Bluemix}} organization that you are logged in. For more information, see [Getting to the Kibana dashboard from a web browser](logging_view_kibana3.html#launch_Kibana_from_browser).
    
    You can also change or remove the initial query, and add more queries. For more information, see  [Filtering your Cloud Foundry App logs with queries in Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).


Kibana is a browser-based interface where you can customize dashboards that you can then use to analyze log data and perform advance management tasks. 

In {{site.data.keyword.Bluemix}}, you can analyze data by using the default Kibana dashboard that is available for each Cloud Foundry app and for each space of your organization. By default, these dashboards display all the data that is available for the last 24 hours through a panel that includes a Histogram row and a Table of events row. 

To constraint the information displayed through any default dashboard, you can add queries and filters to a default dashboard. Then, you can save the dashboard for future reuse. 

The data that a Kibana dashboard displays is controlled by the query. To modify the information that is displayed in a dashboard, you can change the query, add multiple queries, and then save the dashboard. You can customize, save, and share multiple dashboards simultaneously. This is how Kibana shows information about a single app in your space, for example.

You also can configure filters from log fields, for example, message_type and instance_ID. For more information, see [Kibana log format](logging_view_kibana3.html#kibana_log_format_cf). You can enable or disable dynamically this filters. The dashboard will display the log entries that meet the query and filtering criteria that you enable. For more information, see [Filtering data in a Kibana dashboard](logging_view_kibana3.html#filter_data_kibana_dashboard).

To visualize the data, you can configure panels. Kibana includes different panels such as table, trends, and histogram that you can use to analyze the information. You can add, remove, and rearrange panels in the dashboard. The objective of each panel varies. Some panels are organized into rows that provide the results of a one or more queries. Other panels display documents or custom information. For more information, see [Customizing a Kibana dashboard](logging_view_kibana3.html#customize_kibana_dashboard).

After you customize a dashboard, you can choose from any of the following actions:

* You can save the dashboard for future reuse. For more information, see [Saving a Kibana dashboard](logging_view_kibana3.html#save_Kibana_dashboard).

* You can export or share a direct link to a Kibana dashboard with another user. For more information, see [Exporting and sharing your Kibana dashboards](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash).

* You can embed the dashboard in a web page. For a user to see an embedded dashboard, that user must have permissions to access Kibana.

For more information, see the [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) documentation.

**Note:** Kibana 4 and Kibana 3 are supported. Kibana 3 is deprecated.


##  Getting to the Kibana dashboard from the Bluemix dashboard
{: #launch_Kibana_from_bluemix}

The query that is used to filter the data that is displayed in the dashboard retrieves log entries for the Cloud Foundry application. The log information that the Kibana dashboard displays by default is all related to a single Cloud Foundry application and all its instances.

To see the logs of a Cloud Foundry application in Kibana, complete the following steps:

1. Log in to {{site.data.keyword.Bluemix_notm}}, and then click the app name on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard. The app details page opens.
    
2. In the navigation bar, click **Logs**. The logs tab opens. 
    
3. Click **Advanced view**. The **Kibana 3** dashboard opens.

If you don't see any logs, adjust the time picker in the header.

For more information about customizing a Kibana dashboard, see [this blog post](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) or the [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) documentation.

##  Getting to the Kibana dashboard from a web browser
{: #launch_Kibana_from_browser}

The query that is used to filter the data that is displayed in the dashboard retrieves log entries for a space in the {{site.data.keyword.Bluemix}} organization. The log information that the Kibana dashboard displays includes records for all resources that are deployed within the space of the {{site.data.keyword.Bluemix}} organization that you are logged in.

Complete the following steps to open a Kibana dashboard from a browser:

1. Open [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) to log in to the Kibana user interface.

2. Select the **Kibana 3** tab to work with Kibana 3. Select the **Kibana 4** tab to work with Kibana 4. The default Kibana dashboard opens. 

If you don't see any logs, adjust the time picker in the header.

For more information about customizing a Kibana dashboard, see [this blog post](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) or the [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) documentation.



## Filtering data in a Kibana dashboard
{: #filter_data_kibana_dashboard}

In {{site.data.keyword.Bluemix}}, you can analyze data by using the default Kibana dashboard that is provided per resource or by {{site.data.keyword.Bluemix}} space. By default, these dashboards display all the data that is available for the last 24 hours. However, you can constraint the information displayed through a dashboard. You can add queries and filters to a default dashboard, and then save it for future reuse.

In a dashboard, you can add multiple queries and filters. A query defines a subset of log entries.  A filter refines the data selection by including or excluding information. 

For Cloud Foundry apps, the following list outline examples of how to filter data:
* If you you are looking for information in your logs that include key terms, you can create queries to filter by those terms. With Kibana, you can compare queries visually on the dashboard. For more information, see [Filtering your Cloud Foundry App logs with queries in Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).

* If you are looking for information within a specific period of time, you can filter data within a time range. For more information, see [Filtering your Cloud Foundry App logs by time in Kibana](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter).

* If you are looking for information for a specific instance ID, you can filter data by instance ID. For more information, see [Filtering your Cloud Foundry App logs by instance ID in Kibana](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id) and [Filtering your Cloud Foundry App logs by known application ID in Kibana](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id).

* If you are looking for information for a specific component, you can filter data by component (log type). For more information, see [Filtering your Cloud Foundry App logs by log type in Kibana](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter).

* If you are looking for information, for example, error messages, you can filter data by message type. For more information, see [Filtering your Cloud Foundry App logs by message type in Kibana](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter).

## Customizing a Kibana dashboard
{: #customize_kibana_dashboard}

There are different types of dashboards that you can customize to visualize and analyze the data, for example:
* Single-cf-app dashboard: This is a dashboard that shows information for a single Cloud Foundry application.  
* Multi-cf-app dashboard: This is a dashboard that shows information for all the Cloud Foundry applications that are deployed in the same  {{site.data.keyword.Bluemix}} space. 

When you customize a dashboard, you can configure queries and filters to select a subset of the log data to show through the dashboard.

To visualize the data, you can configure panels. Kibana includes different panels such as table, trends, and histogram that you can use to analyze the information. You can add, remove, and rearrange panels in the dashboard. The objective of each panel varies. Some panels are organized into rows that provide the results of a one or more queries. Other panels display documents or custom information. For example, you can configure a bar chart, pie chart, or table to visualize the data and analyze it.  


## Saving a Kibana dashboard
{: #save_Kibana_dashboard}

Complete the following steps to save a Kibana dashboard after you customize it:

1. In the toolbar, click the **Save** icon.

2. Enter a name for the dashboard.

    **Note:** If you try to save a dashboard with a name containing blank spaces, it will not save.

3. Next to the name field, click the **Save** icon.



## Analyzing logs through a Kibana dashboard
{: #analyze_kibana_logs}

After you customize a Kibana dashboard, you can visualize and analyze the data through its panels. 

To search for information, you can pin or unpin queries. 

* You can pin a query to the dashboard and automatically the search is activated.
* To remove content from the dashboard, you can deactivate a query.

To filter information, you can enable or disable filters. 

* You can select the **Toggle** checkbox ![Toggle box to include a filter](images/logging_toggle_include_filter.jpg) in a filter to enable it.   
* You can unselect the **Toggle** checkbox ![Toggle box to include a filter](images/logging_toggle_exclude_filter.jpg) in a filter to disable it. 

The graphs and charts in your dashboard display the data. You can use the graphs and charts in your dashboard to monitor the data. 

For example, for a single-cf-app dashboard, the dashboard includes information about one Cloud Foundry application. The data that you can visualize and analyze is limited to that app. You can use the dashboard to analyze data for all instances of the app. You can compare instances. You can filter by instance ID the information. 

You can define and pin a query for each instance ID to the dashboard. 

![Dashboard with queries pinned](images/logging_kibana_dash_activate_query.jpg)

Then, you can activate or deactivate individual queries depending on the instance information that you want to see in the dashboard. 

The following figure shows one query activated and the other deactivated:

![Dashboard with queries pinned](images/logging_kibana_dash_deactivate_query.jpg)

If you want to compare 2 instances in a Histogram, you can define two queries in the same dashboard, one for each instance ID. You can give them an alias and a unique color to identify them easily. Kibana handles multiple queries by joining them with a logical OR. 

The following figure shows the panel to configure an alias and a color for a query, to pin it to the dashboard, and to deactivate it:

![Dashboard wizard to configure query](images/logging_kibana_query_def.jpg)



## Kibana log format for Cloud Foundry applications
{: #kibana_log_format_cf}

You can configure a Kibana dashboard to display the following fields for each log entry:

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>The time of the logged event. The timestamp is defined up to the millisecond.</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>The id of the {{site.data.keyword.Bluemix_notm}} resource.</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>The unique id for your log document.</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>The index for your log entry.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>The type of log; for example, <samp>syslog</samp>.</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>The name of your {{site.data.keyword.Bluemix_notm}} application.</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>The unique id of your {{site.data.keyword.Bluemix_notm}} application.</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>The name of your application that produced the log data.</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>The instance id of your application instance that produced the log data.</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>The severity of the logged event.</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>The message that is issued by the component. The message varies depending on the context.</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>The stream that the log message is written to. <samp class="ph codeph">OUT</samp> refers to the <samp class="ph codeph">stdout</samp> stream and <samp class="ph codeph">ERR</samp> refers to the <samp class="ph codeph">stderr</samp> stream.</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>The unique id of your {{site.data.keyword.Bluemix_notm}} organization.</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>The name of the {{site.data.keyword.Bluemix_notm}} organization where your app is staged.</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>The component that produces logs. The following list describes the logs from each component:</p>

<dl>
<dt><strong>API</strong></dt>
<dd>Logged responses to API calls that request a change to your app state.</dd>

<dt><strong>APP</strong></dt>
<dd>Logged responses from your app.</dd>

<dt><strong>CELL</strong></dt>
<dd>Logged responses from the Diego cell that indicate when an app starts, stops, or crashes.</dd>

<dt><strong>LGR</strong></dt>
<dd>Logged responses from the loggregator that indicate problems with the logging process.</dd>

<dt><strong>RTR</strong></dt>
<dd>Logged responses from the Router when it routes HTTP requests to your app.</dd>

<dt><strong>SSH</strong></dt>
<dd>Logged responses from the Diego cell when a user accesses an app container by using the **cf ssh** command.</dd>

<dt><strong>STG</strong></dt>
<dd>Logged responses from the Diego cell or the Droplet Execution Agent when your app is staged or restaged.</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>The name of the {{site.data.keyword.Bluemix_notm}} space where where your app is staged.</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>The time of the logged event. The timestamp is defined up to the millisecond.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>The type of log, for example <samp>syslog</samp>.</p>
</dd>
</dl>




