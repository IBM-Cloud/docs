---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Monitoring and logging with Cloud Foundry
{: #monitoringandlogging}


By monitoring your apps and reviewing logs, you can follow application execution and data flow to get a better understanding of your deployment. In addition, you can reduce the time and effort that is required to locate any issues and repair them.
{:shortdesc}

{{site.data.keyword.Bluemix}} applications can be widely distributed, multi-instance applications, and the execution of your application and its data can be shared across many services. In this complex environment, monitoring your apps and reviewing logs is important for you to manage your apps.

## Monitoring and logging Cloud Foundry apps
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} has a built-in logging mechanism to produce log files for your apps as they are running. In the logs, you can view the errors, warnings, and informational messages that are produced for your app. In addition, you can also configure your app to write log messages to the log file. For more information about log formats and how to view logs, see [Logging for apps running on Cloud Foundry](#logging_for_bluemix_apps).

Monitoring your app enables you to see and control your app deployment. With monitoring, you can accomplish the following tasks:

* Collect and monitor performance information for app instances, and check whether they are functional.
* Gain insight on application operations, for example, detect the potential bottlenecks or when upgrades are required.
* Estimate resource usage and charges.

For stable operations of your deployments on {{site.data.keyword.Bluemix_notm}} platform, you want to detect problems promptly and determine causes efficiently. To accomplish this objective, keep troubleshooting in mind when you design your apps, and use services or tools for monitoring and logging when your app is deployed to {{site.data.keyword.Bluemix_notm}}.

### Monitoring apps running on Cloud Foundry
{: #monitoring_bluemix_apps}

When you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}, you'll want to keep up with performance information such as health status, resource usage, and traffic metrics. With this performance information, you can then make decisions or take actions accordingly.

To monitor {{site.data.keyword.Bluemix_notm}} apps, use one of the following methods:

* {{site.data.keyword.Bluemix_notm}} services. Monitoring and Analytics offers a service that you can use to monitor your application performance. In addition, this service also provides analytic features such as log analysis. For more information, see [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate).
* Third-party options. For example, [New Relic ![External link icon](../icons/launch-glyph.svg "External link icon")](http://newrelic.com/){:new_window}.

### Logging for apps running on Cloud Foundry
{: #logging_for_bluemix_apps}

Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. When you encounter errors in any stage from deployment to runtime, you can check the logs for clues that might help solve your issue.


<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



### Log format and retention
{: #log_format}

In {{site.data.keyword.Bluemix_notm}} Public Cloud Foundry apps, log data is stored for 7 days by default. You can search up to 1 GB of data per day.

Logs for {{site.data.keyword.Bluemix_notm}} applications are displayed in a fixed format, similar to the following pattern:

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

Every log entry contains four fields. Refer to the following list for the brief description of each field:

<dl>
<dt><strong>Time stamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>Columns: 1 - 27</p>
<p>The time of the log statement. The timestamp is defined up to the millisecond.</p>
</dd>

<dt><strong>Component</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Columns: 29 - 40</p>
<p>The component that produces logs. </p>
<p>Each component type is followed by a slash and a digit that indicates the application instance. 0 is the digit allocated to the first instance, 1 is the digit allocated to the second, and so on.</p>
<p>The following list outlines the different types of components:</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: The LGR component provides information about the Logging service.</dd>

<dt><strong>RTR</strong></dt>
<dd>Router: The RTR component provides information about HTTP requests to an application.</dd>

<dt><strong>STG</strong></dt>
<dd>Staging: The STG component provides information on how an application is staged or restaged.</dd>

<dt><strong>APP</strong></dt>
<dd>Application: The APP component provides information about an application.</dd>

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

<dt><strong>Stream</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Columns: 42 - 44</p>
<p>The stream that the log message is written to. <samp class="ph codeph">OUT</samp> refers to the <samp class="ph codeph">stdout</samp> stream and <samp class="ph codeph">ERR</samp> refers to the <samp class="ph codeph">stderr</samp> stream.</p>
</dd>

<dt><strong>Message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>Columns: 46 - end of line</p>
<p>The message that is issued by the component. The message varies depending on the context.</p>
</dd>
</dl>

The following figure shows the different components (log types) in a Cloud Foundry architecture that is based on the Droplet Execution Agent (DEA): 
![Log types in a DEA architecture.](images/logging_F1.png "Components (log types) in a Cloud Foundry architecture that is based on the Droplet Execution Agent (DEA).")


## Viewing logs
{: #viewing_logs}

You can view the logs for your Cloud Foundry apps in four places:

  * The {{site.data.keyword.Bluemix_notm}} Dashboard
  * The Kibana dashboard
  * The command line interface
  * External log hosts

### Viewing logs from the {{site.data.keyword.Bluemix_notm}} Dashboard
{: #viewing_logs_UI}

To see the deployment or runtime logs, complete the following steps:
1. Log in to {{site.data.keyword.Bluemix_notm}}, and then click the tile for your app. The app details page is displayed.
2. In the navigation bar, click **Logs**.

In the **Logs** console, you can view the recent logs for your app or tail logs in real time. In addition, you can filter logs by log type and channel.

**Note:** Logs are not persisted between app crashes and deployments.


### Viewing logs from the Kibana Dashboard
{: #viewing_logs_Kibana}

Create a custom dashboard to display, in a simple or creative manner, the logs for the apps that run in a space.

1. Open [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) to log in to the Kibana user interface.
2. Select the **Kibana 3** tab.
3. If you don't see any logs, adjust the time picker in the header.
4. Save the dashboard as a new dashboard.
  1. In the toolbar, click the **Save** icon.
  2. Enter a name for the dashboard.
  3. Next to the name field, click the **Save** icon.

For more information about customizing a Kibana dashboard, see [this blog post](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) or the [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) documentation.


### Viewing logs from the command line interface
{: #viewing_logs_cli}

Choose from the following options to view logs from the command line interface:

<ul>
<li>Tailing logs when you deploy apps.
<p>Use the **cf logs** command to display logs from your app and from the system components that interact with your app when you deploy apps to {{site.data.keyword.Bluemix_notm}}. You can type the following commands in the cf command line interface. For more information about cf logs, see <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target=" _blank">Log Types and Their Messages in Cloud Foundry <img src="../icons/launch-glyph.svg" alt="External link icon"></a> </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>Display logs from the recent past.</dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>Display logs that are generated from the moment that you run this
command.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Tip:</span> When you run the <span class="keyword cmdname">cf push</span> or <span class="keyword cmdname">cf
start</span> command in one command line window, you can enter <samp class="ph codeph">cf
logs appname --recent</samp> in another command line window to see
the logs in real time. </div>
</li>

<li>Viewing logs after the apps are deployed.

<p>If application logging is enabled, you can view the following application logs if you encounter problems with your app at run time. Application logs can help to determine the cause of the error.</p>

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>This log file records  fine-grained informational events for
debugging. You can  use this log to troubleshoot buildpack execution
problems.</p>
<p>To generate data to the <span class="ph filepath">buildpack.log</span> file, you must enable buildpack tracing by using the following command:
   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre></p>
<p>To view this log, enter the following command:
<pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>
<dt><strong>staging_task.log</strong></dt>
<dd><p>This log file records messages after the major steps of the
staging task. You can use this log to troubleshoot staging problems.</p>
<p>To view this log, enter the following command:
<pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Note:** For information about how to enable application logging, see [Debugging runtime errors](/docs/debug/index.html#debugging-runtime-errors).

### Viewing logs from external hosts
{: #viewing_logs_external}


When logs are generated, after a short delay you can view messages in your external log host that are similar to the messages that you view from the {{site.data.keyword.Bluemix_notm}} user interface or from the cf command line interface.  If you have multiple instances of your app, the logs are aggregated and you can see all the logs for your app. In addition, the logs are persisted between app crashes and deployments.

**Note:** Logs that you view in the command line interface are not in the syslog format, and might not exactly match the messages that are displayed in your external log host.




## Filtering logs from the command line interface
{: #filtering_logs}

To view logs that you are interested in or exclude the content that you don't want to view, you can use the **cf logs** command with filtering options such as **cut** and **grep** in the cf command line interface.

* To view a portion instead of the complete verbose logs, use the **cut** option. For example, to display the component and message information, use the following command:
```
cf logs appname --recent | cut -c 29-40,46-
```

For more information about the **grep** option, type cut --help.
* To display log entries that contain certain keywords, use the **grep** option. For example, to display log entries that contain the keyword `[APP`, you can use the follow command:

```
cf logs appname --recent | grep '\[App'
```
For more information about the **grep** option, type `grep --help`.



## Configuring external log hosts
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} keeps a limited amount of log information in memory. When information is logged, the old information is replaced by the newer information. To keep all the log information, you can save your logs to an external log host, such as a third-party log management service or other host.

To stream logs from your app and the system to an external log host, complete the following steps:

  1. Determine the logging endpoint.

	 You can send logs to a third-party log aggregator, such as Papertrail, Splunk, or Sumologic. You can also send logs to a syslog host, a syslog host that is encrypted with TLS (Transport Layer Security), or an HTTPS POST endpoint. The methods to obtain logging endpoints vary for different log hosts.

  2. Create a user-provided service instance.

	 Use the `cf create-user-provided-service` command (or `cups`, a short version of the command) to create a user-provided service instance:
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;

	 The name for the user-provided service instance.

	 &lt;logging_endpoint&gt;

	 The logging endpoint that {{site.data.keyword.Bluemix_notm}} sends logs to. Refer to the following table to replace *logging_endpoint* with your value:

	 <table>
	 <caption>Table 1. Logging endpoint values</caption>
     <thead>
     <tr>
     <th>Logging endpoint</th>
     <th>Command</th>
	 <th>Notes</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog host</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>For example, to enable logging to Papertrail, type `cf cups my-logs -l syslog://<papertrail-url>`. Replace `<papertrail-url>` with the URL of your logging endpoint from Papertrail.</td>
     </tr>
	 <tr>
     <td>syslog-tls host</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>The certificate must be trusted by a certificate authority. Don't use self-signed certificates.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>This endpoint must be on the public Internet and accessible by {{site.data.keyword.Bluemix_notm}}</td>
     </tr>
     </tbody>
     </table>
  3. Bind the service instance to your app.

	 Use the following command to bind the service instance to your app:

	 ```
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;

	 The name of your app.

	 &lt;service_name&gt;

	 The name for the user-provided service instance.

  4. Restage the app.
     Type `cf restage appname` for the changes to take effect.


### Example: Streaming Cloud Foundry application logs to Splunk
{: #splunk}

In this example, a developer named Jane creates a virtual server by using IBM Virtual Servers Beta and the Ubuntu image.  Jane tries to stream Cloud Foundry app logs from {{site.data.keyword.Bluemix_notm}} to Splunk.

  1. To begin, Jane sets up Splunk.

     a. Jane downloads Splunk Light from the [Download Splunk Light site ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window}, and then installs it by using the following command. The software is installed on */opt/splunk*.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane installs and patches the RFC5424 syslog technology add-on to integrate with {{site.data.keyword.Bluemix_notm}}. For more information about the instructions for installing the add-on, see the [Cloud Foundry guideline ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane installs the add-on by using the following commands:

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Then, Jane patches the add-on by replacing */opt/splunk/etc/apps/rfc5424/default/transforms.conf* with a new *transforms.conf* file that consists of the following text:

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. After Splunk is set up, Jane must open some ports on the Ubuntu machine to accept the incoming syslog drain (port 5140) and Splunk web UI (port 8000) because {{site.data.keyword.Bluemix_notm}} virtual server has the firewall set up by default.

	    **Note:** The iptable confiration is done here for Jane's evaluation purpose and is temporary. To configure the firewall setting in Bluemix virtual server in production, see the [Network Security Groups ![External link icon](../icons/launch-glyph.svg "External link icon")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} documentation for details.

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Then, Jane runs Splunk by using the following command:

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane configures the Splunk settings to accept the syslog drain from {{site.data.keyword.Bluemix_notm}}. She must create a data input for the syslog drain.

     a. From the Splunk web interface, Jane clicks **Data > Data inputs**. A list of input types that Splunk supports is displayed.

     b. She selects **TCP**, because the syslog drain uses the TCP protocol.

     c. In the **TCP** pane, she enters **5140** in the **Port** field, leaves the remaining fields blank, and then clicks **Next**.

     d. From the **Source Type** list, she selects **Uncategorized > rfc5424_syslog**.

     e. For the **Method** type, she selects **IP**.

     f. In the **Index** field, Jane clicks **Create a new index**. She names the new index "bluemix", and then clicks **Save**.

     g. Finally, in the **Review** window, Jane confirms that the setting is correct and then clicks **Submit** to enable this data input.

  3. In {{site.data.keyword.Bluemix_notm}}, Jane creates a syslog drain service and binds the service to an app.

     a. Jane creates a syslog drain service by using the following command from the cf cli:

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Note:** *dummyhost* is not the real name. It is used to hide the actual host name.

     b. Jane binds the syslog drain service to an app in her space, and then restages the app.

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane tries out her app, and then she types the following query string in the Splunk web interface:

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane sees a stream of logs in her Splunk web interface. Though the Splunk that Jane installs is Splunk Light, she can still retain 500MB logs a day.

## Logging for Cloud Foundry apps in {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}}
{: #hybrid_apps_logs_ov}


In {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}}, Cloud Foundry apps come with built-in logging. You can review the data that is collected from your apps on the {{site.data.keyword.Bluemix_notm}} console.
{:shortdesc}

Cloud Foundry apps use Cloud Foundry loggregator to monitor and forward logs from outside of the app. You don't need to install agents inside of the app.

### Hardware requirements


| **Requirement** |    **1 node**     | **3 nodes for high availability** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Memory | 80 GB | 240 GB |
| Local storage | 2.98 TB | 8.94 TB |
{: caption="Table 2. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

### Setup

In {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}}, logs are active for all apps by default. To view information about reading standard logs, see [Logging for apps running on Cloud Foundry](#logging_for_bluemix_apps). In addition, advanced logging can be enabled in {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}} environments.

* To confirm that advanced logging is enabled in your {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}} environments, follow the steps in [Viewing logs](#hybrid_apps_logs_dash). If you do not have the **Advanced View** button, then this feature is not enabled.

* To add advanced logging to your environment, follow the steps in the [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) or [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) documentation.

### Log retention

In {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}} Cloud Foundry apps, log data is stored for 30 days by default.

## Viewing logs for Cloud Foundry apps in {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}}
{: #hybrid_apps_logs_dash}

You can review logs for the apps that you are running on {{site.data.keyword.Bluemix_dedicated_notm}} and {{site.data.keyword.Bluemix_local_notm}}.
{:shortdesc}

To view your app logs, follow these steps.
1. Select a running app.
2. Click **Logs**. In the **Logs** view, you can view logs from your running app..
4. Click the **Advanced View** button. **Advanced View** shows a more detailed view of the logs by using Kibana, a visualization tool that uses logs and time-stamped data to create custom visualizations. For more information about using the advanced view, see the [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) documentation.

Next, you can customize a Kibana dashboard. See [Customizing log display in Kibana dashboard](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom) for more information.
