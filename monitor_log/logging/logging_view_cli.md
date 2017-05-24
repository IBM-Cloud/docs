---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyzing logs from the CLI
{: #analyzing_logs_cli}

In {{site.data.keyword.Bluemix}}, you can view, filter, and analyze logs through the command line interface. Use the command line to manage logs programmatically. 
{:shortdesc}

To analyze Cloud Foundry (CF) application logs, use the following command: `cf logs`
For more information, see [Analyzing CF app logs from the CLI](logging_view_cli.html#analyzing_cf_logs_cli).

To analyze Docker container logs, use the following command: `cf ic logs`
For more information, see [Analyzing Docker container logs from the CLI](logging_view_cli.html#analyzing_container_logs_cli). This feature applies only to containers that are deployed in the {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure.


## Analyzing CF app logs from the CLI
{: #analyzing_cf_logs_cli}

Use the **cf logs** command to display logs from a Cloud Foundry app and from the system components that interact with it when you deploy the app in {{site.data.keyword.Bluemix_notm}}. The **cf logs** command displays the STDOUT and STDERR log streams of a Cloud Foundry application.

To view logs that you are interested in or exclude the content that you don't want to view, you can use the **cf logs** command with filtering options such as **cut** and **grep** in the cf command line interface:

* To view the logs for a Cloud Foundry app, see [Viewing the log for a Cloud Foundry app](logging_view_cli.html#full_log_cli).
* To view the most recent log records for a Cloud Foundry app, see [Viewing the latest log entries for a Cloud Foundry app](logging_view_cli.html#tailing_log_cli).
* To view the log records for a Cloud Foundry app in a specific time range, see [Viewing a section of the logs](logging_view_cli.html#partial_log_cli).
* To view entries in the logs for a Cloud Foundry app that contain specific keywords, see [Viewing log entries that contain certain keywords](logging_view_cli.html#partial_by_keyword_log_cli).


### Viewing the log for a Cloud Foundry app
{: #full_log_cli}

To see all the logs available for a Cloud Foundry app, complete the following steps:

1. Open a terminal and log in to {{site.data.keyword.Bluemix}}.

2. From the command line, run the following command to display all the logs:

   <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var></code></pre>
   
   
### Viewing the latest log entries for a Cloud Foundry app
{: #tailing_log_cli}

To see the most recent logs that are available for a Cloud Foundry app, complete the following steps:

1. Open a terminal and log in to {{site.data.keyword.Bluemix}}.

2. From the command line, run the following command to display all the logs:

     <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">Tip:</span> When you run the <span class="keyword cmdname">cf push</span> or <span class="keyword cmdname">cf start</span> command in one command line window, you can enter <samp class="ph codeph">cf
logs appname --recent</samp> in another command line window to see the logs in real time. </div>


### Viewing a section of a Cloud Foundry log
{: #partial_log_cli}

To view a portion of the logs that are available for a Cloud Foundry app within a time range, complete the following steps:

1. Open a terminal and log in to {{site.data.keyword.Bluemix}}.

2. From the command line, run the following command to display all the logs:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent  | cut -c 29-40,46-</code></pre>
    
    For more information about the **cut** option, enter **cut --help**.


### Viewing log entries that contain certain keywords
{: #partial_by_keyword_log_cli}

To display log entries that contain certain keywords for a Cloud Foundry app, complete the following steps:

1. Open a terminal and log in to {{site.data.keyword.Bluemix}}.

2. From the command line, run the following command to display all the logs:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent | grep '<var class="keyword varname">keyword</var>'</code></pre>
    

For example, to display log entries that contain the keyword **APP**, you can use the follow command:

<pre class="pre screen"><code>cf logs appname --recent | grep '\[App'</code></pre>

For more information about the **grep** option, type **grep --help**.


### Cloud Foundry application logs
{: #cf_app_logs_cli}

The following logs are available for a Cloud Foundry application after you deploy it in {{site.data.keyword.Bluemix}}:

**buildpack.log**

This log file records fine-grained informational events for debugging. You can  use this log to troubleshoot buildpack execution problems.

To generate data to the *buildpack.log* file, you must enable buildpack tracing by using the following command: `cf set-env appname JBP_LOG_LEVEL DEBUG`
   
To view this log, enter the following command: `cf files appname app/.buildpack-diagnostics/buildpack.log`


**staging_task.log**

This log file records messages after the major steps of the staging task. You can use this log to troubleshoot staging problems.

To view this log, enter the following command: `cf files appname logs/staging_task.log`


**Note:** For information about how to enable application logging, see [Debugging runtime errors](/docs/debug/index.html#debugging-runtime-errors).

## Analyzing Docker container logs from the CLI
{: #analyzing_container_logs_cli}

**Note:** This feature applies only to containers that are deployed in the {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure.

Use the `cf ic logs` command to display logs from a container in {{site.data.keyword.Bluemix_notm}}. For example, you can use the logs to analyze why a container has stopped or for reviewing the container output. 

To see application errors for the app that runs in a container through the `cf ic logs` command, the application must write its logs to the standard output (STDOUT) and standard error (STDERR) output streams. If you design your application to write to these standard output streams, you can view the logs via the command line even if the container shuts down or crashes.

For more information about the `cf ic logs` command, see [cf ic logs command](/docs/containers/container_cli_reference_cfic.html#container_cli_reference_cfic__logs).


