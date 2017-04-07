---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Runtime application logging through CF apps
{: #logging_writing_to_log_from_cf_app}

In {{site.data.keyword.Bluemix}}, to persist log data for a Cloud Foundry app and its runtime, you must write your logs to STDOUT and STDERR. 
{:shortdesc}

In {{site.data.keyword.Bluemix}}, STDOUT and STDERR log records are collected automatically:

* STDOUT (standard output) provides general information.  
* STDERR (standard error) provides information that includes error messages and other diagnostic warnings. 

Loggregator automatically picks up standard output and standard error data. The Loggregator is the component that forwards logs from inside of Cloud Foundry. 

For example, 

For a **Liberty Cloud Foundry app**, the default console.log for the liberty server is automatically picked up by loggregator. 

* The console.log contains the redirected STDOUT and STDERR from the JVM process. The console output contains major events and errors if you use the default consoleLogLevel configuration. The console output also contains any messages that are written to the system.out and system.err streams if you use the default copySystemStreams configuration. The console output always contains messages that are written directly by the JVM process, such as -verbose:gc output. You can adjust the logging level of liberty via the server.xml.
* The consoleLogLevel sets the filter level of the console.log handler. When you set the consoleLogLevel to INFO, you configure all INFO, AUDIT, WARNING, and ERROR messages to be written to the console.log file. **Note:** FINE, FINER, FINEST log entries are only written to the trace.log file.

For more information about Liberty for Java™ applications, see [Liberty Profile: Logging and Trace ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}.

For a **Node.js Cloud Foundry app**, you can use the built in console logging module to configure logging for the runtime in {{site.data.keyword.Bluemix}}. You can put messages on both the stdout and stderr:

* console.log('message') will send the msg to the STDOUT stream
* console.error('error_message') will send the error to the STDERR stream

For more information about Node.js applications, see [How to log in node.js ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}.


For more information about **Ruby on Rails applications**, see [The Logger ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}.

The following table lists the mapping between some application runtimes logs and the logs that are picked automatically by Loggregator:

| **Runtime** |    **STDOUT**     | **STDERR** |
|-----------------|-------------------|-------------------|
| Liberty | system.out | system.err |
| Node.js | console.log, console.info | console.error, console.warn |
| Ruby | stdout| stderr |
{: caption="Table 1. Mapping between some application runtimes logs and the logs that are picked automatically by Loggregator" caption-side="top"}

