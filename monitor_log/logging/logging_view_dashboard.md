---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing CF app logs from the Bluemix Dashboard
{: #analyzing_logs_bmx_ui}

In {{site.data.keyword.Bluemix}}, you can view, filter, and analyze logs through the **Log** tab that is available for each Cloud Foundry application. Use the {{site.data.keyword.Bluemix}} dashboard to view the latest actvity of the application.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public offers an integrated Logging service. When you run your applications in Cloud Foundry, 
the Logging service captures log data from system components that interact with your application, about your application, and even log data from within your application when you use stdout and stderr.

Logs for {{site.data.keyword.Bluemix_notm}} applications are displayed in a fixed format, similar to the following pattern:

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>     <var class="keyword varname">message</var>     <var class="keyword varname">timestamp</var></code>
   
For more information about the log format, see [Log format for Cloud Foundry app logs](logging_view_dashboard.html#log_format_cf).

**Note:** In {{site.data.keyword.Bluemix_notm}} Public, log data is stored for 7 days by default. You can search up to 1 GB of data per day.



##  Getting to the Bluemix log tab
{: #launch_logs_tab_bmx_ui}

To see the deployment or runtime logs of a Cloud Foundry application, complete the following steps:

1. Log in to {{site.data.keyword.Bluemix_notm}}, and then click the app name on the {{site.data.keyword.Bluemix_notm}} **Apps** dashboard. 

    The app details page is displayed.
    
2. In the navigation bar, click **Logs**.

    The logs tab opens. 
    
    In the **Logs** tab, you can view the recent logs for your app or tail logs in real time. In addition, you can filter logs by component (log type), by app instance ID, and by error.



## Log format for Cloud Foundry app logs
{: #log_format_cf}

Every log entry contains the following fields:

<dl>
<dt><strong>Time stamp</strong></dt>
<dd>
<p>The time of the log statement. The timestamp is defined up to the millisecond.</p>
</dd>

<dt><strong>Component</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>The component that produces the log. </p>
<p>Each component type is followed by a slash and a digit that indicates the application instance. 0 is the digit allocated to the first instance, 1 is the digit allocated to the second, and so on. Note that you can filter to see only one App instance in dashboard.</p>
<p>The following list outlines the different types of components:</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: The LGR component provides information about the Cloud Foundry Loggregator, which forwards logs from inside of Cloud Foundry.</dd>

<dt><strong>RTR</strong></dt>
<dd>Router: The RTR component provides information about HTTP requests to an application.</dd>

<dt><strong>STG</strong></dt>
<dd>Staging: The STG component provides information on how an application is staged or restaged.</dd>

<dt><strong>APP</strong></dt>
<dd>Application: The APP component provides logs from the application. This is where stderr and stdout in your code will show up.
</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API: The API component provides information about the internal actions that result from a user's request to change the state of an application.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent: The DEA component provides information about the start, stop, or crash of an application. 
<p>This component is only available if your application is deployed in the Cloud Foundry architecture that is based on DEA.</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Diego cell: The CELL component provides information about the start, stop, or crash of an application. 
<p>This component is only available if your application is deployed in the Cloud Foundry architecture that is based on Diego.</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: The SSH component provides information every time a user accesses an application by using the **cf ssh** command. 
<p>This component is only available if your application is deployed in the Cloud Foundry architecture that is based on Diego.</p></dd>

</dl>
</dd>

<dt><strong>Message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>The message that is issued by the component. The message varies depending on the context.</p>
</dd>
</dl>

The following figure shows the different components (log types) in a Cloud Foundry architecture that is based on the Droplet Execution Agent (DEA): 
![Log types in a DEA architecture.](images/logging_F1.png "Components (log types) in a Cloud Foundry architecture that is based on the Droplet Execution Agent (DEA).")



