{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Monitoring and logging
{: #monitoringandlogging}

*Last updated: 4 December 2015*

By monitoring your apps and reviewing logs, you can follow application execution and data flow to get a better understanding of your deployment. In addition, you can reduce the time and effort that is required to locate any issues and repair them.
{:shortdesc}

{{site.data.keyword.Bluemix}} applications can be widely distributed, multi-instance applications, and the execution of your application and its data can be shared across many services. In this complex environment, monitoring your apps and reviewing logs is important for you to manage your apps.

{{site.data.keyword.Bluemix_notm}} has a built-in logging mechanism to produce log files for your apps as they are running. In the logs, you can view the errors, warnings, and informational messages that are produced for your app. In addition, you can also configure your app to write log messages to the log file. For more information about log formats and how to view logs, see [Logging for {{site.data.keyword.Bluemix_notm}} apps](#logging_for_bluemix_apps).

Monitoring your app enables you to see and control your app deployment. With monitoring, you can accomplish the following tasks:

* Collect and monitor performance information for app instances, and check whether they are functional.
* Gain insight on application operations, for example, detect the potential bottlenecks or when upgrades are required.
* Estimate resource usage and charges.

For stable operations of your deployments on {{site.data.keyword.Bluemix_notm}} platform, you want to detect problems promptly and determine causes efficiently. To accomplish this objective, keep troubleshooting in mind when you design your apps, and use services or tools for monitoring and logging when your app is deployed to {{site.data.keyword.Bluemix_notm}}.

##Monitoring apps running on Cloud Foundry
{: #monitoring_bluemix_apps}

When you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}, you'll want to keep up with performance information such as health status, resource usage, and traffic metrics. With this performance information, you can then make decisions or take actions accordingly.

To monitor {{site.data.keyword.Bluemix_notm}} apps, use one of the following methods:

* {{site.data.keyword.Bluemix_notm}} services. Monitoring and Analytics offers a service that you can use to monitor your application performance. In addition, this service also provides analytic features such as log analysis. For more information, see [Monitoring and Analytics](../services/monana/index.html).
* Third-party options. For example, [New Relic](http://newrelic.com/){:new_window}.

##Logging for apps running on Cloud Foundry
{: #logging_for_bluemix_apps}

Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view the logs either from the {{site.data.keyword.Bluemix_notm}} Dashboard or from the cf command line interface. You can also filter the logs to see the parts that you are interested in.

###Log format
{: #log_format}

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
<dt><strong>Timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>Columns: 1 - 27</p>
<p>The time of the log statement. The timestamp is defined up to the millisecond.</p>
</dd>

<dt><strong>Component</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Columns: 29 - 40</p>
<p>The component that produces logs. The following list gives the definition for the all the components:</p>

<dl>
<dt><strong>APP</strong></dt>
<dd>Application. The component APP is followed by a slash and a digit that indicates the application instance. Where 0 is the first instance, 1 is the second, and so on.</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent.</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator.</dd>

<dt><strong>RTR</strong></dt>
<dd>Router.</dd>

<dt><strong>STG</strong></dt>
<dd>Staging.</dd>
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

###Viewing logs
{: #viewing_logs}

You can use either the {{site.data.keyword.Bluemix_notm}} Dashboard or the command line interface to view logs.

####VIEWING LOGS FROM THE {{site.data.keyword.Bluemix_notm}} DASHBOARD

To see the **Deployment** or **Runime** logs, complete the following steps:
1. Click the tile for your app. The app details page is displayed.
2. In the left navigation bar, click **Logs**.

####VIEWING LOGS FROM THE COMMAND LINE INTERFACE

Choose from the following options to view logs from the command line interface:

<ul>
<li>Tailing logs when you deploy apps.
<p>Use the **cf logs** command to display logs from your app and from the system components that interact with your app when you deploy apps to {{site.data.keyword.Bluemix_notm}}. You can type the following commands in the cf command line interface. For more information about cf logs, see [Log Types and Their Messages in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.</p>
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

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>This log file records  fine-grained informational events for
debugging. You can  use this log to troubleshoot buildpack execution
problems.</p>
<p>To generate data to the <span class="ph filepath">buildpack.log</span> file, you must enable buildpack tracing by using the following command:
   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
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


**Note:** For information about how to enable application logging, see [Debugging runtime errors](../troubleshoot/debugging.html#debug_runtime).

###Filtering logs
{: #filtering_logs}

To view logs that you are interested in or exclude the content that you don't want to view, you can use the **cf logs** command with filtering options such as **cut** and **grep** in the cf command line interface.

* To view a portion instead of the complete verbose logs, use the **cut** option. For example, to display the component and message information, use the following command:
```
cf logs appname --recent | cut -c 29-40,46- 
```
For more information about the **grep** option, type cut --help.
* To display log entries that contain certain keywords, use the **grep** option. For example, to display log entries that contain the keyword [APP, you can use the follow command:
```
cf logs appname --recent | grep '\[App'
```
For more information about the **grep** option, type `grep --help`.

###Configuring third-party logging
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} keeps a limited amount of log information in memory. When information is logged, the old information is replaced by the newer information. To keep all the log information, you can save your logs to a third-party log management service.

To stream logs from your application and the system to a third-party log management service, complete the following steps:

1. Register a third-party log management service.
    
    You can use any third-party log management service that supports the [syslog protocol](http://tools.ietf.org/html/rfc5424){:new_window}, such as Papertail, Splunk Storm, SumoLogic, and Logentries. Register a third-party log management service, then configure the service to provide a destination for your logs in {{site.data.keyword.Bluemix_notm}}. After you complete the configuration, the service typically provides you a syslog URL as the destination for your logs in {{site.data.keyword.Bluemix_notm}}. For information on how to configure third-party log management services, see [Configuring Selected Third-Party Log Management Services](http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html){:new_window}.

2. Create a user-provided service instance.
	
	To stream logs in {{site.data.keyword.Bluemix_notm}} to the third-party log management service, you must first create a user-provided service instance. Use the following command to create a user-provided service instance, where service_name is the name for the user-provided service instance, and syslog_URL is the URL that you get from your third-party logging service.
	
	```
	cf create-user-provided-service <service_name> -l <syslog_URL>
	```
	
3. Bind the service instance to your application.

	Use the following command to bind the service instance to your application, where appname is the name of your application, and service_name is the name for the user-provided service  instance.
	
	```
	cf bind-service appname <service_name>
	```
	
	After that, you will be prompted to restage the application by typing cf restage appname for the changes to take effect. When logs are generated, you can view similar messages in the third-party log management service after a short delay.

**Note:** Logs you view in the command line interface are not in the syslog format, and might not exactly match the messages that are displayed in the third-party log management services.