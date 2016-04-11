---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Logging and tracing
{: #logging_tracing}

*Last Updated: 23 March 2016*

## Log files
{: #log_files}

The standard Liberty logs, such as messages.log or the ffdc directory, are available in IBM Bluemix in the logs directory of each application instance. These logs can be accessed from the IBM Bluemix console or by using the cf logs and cf files commands.
For example, to see the messages.log file, run the command:
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

The log level and other trace options can be set through the Liberty configuration file. For more information, see [Liberty profile: Trace and logging](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). Tracing can also be adjusted on a running application instance by using the IBM Bluemix console.

## Using the trace and dump capabilities
{: #using_trace_and_dump}

In the IBM Bluemix user interface, there are trace and dump capabilities.
* Use Trace to view and update the Liberty logging traceSpecification on running application instances.
* Use Dump to create and manipulate thread and heap dumps on running application instances.

To do this action, select a Liberty application in the user interface. Under Runtime in the navigation on the left, you can open the instance details. Select an instance or multiple instances. Under the Actions menu, you can choose TRACE or DUMP.

# rellinks
## general
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
