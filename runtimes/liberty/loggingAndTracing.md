---

copyright:
  years: 2015, 2017
lastupdated: "2016-12-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Logging and tracing
{: #logging_tracing}

## Log files
{: #log_files}

The standard Liberty logs, such as `messages.log` or the `ffdc` directory, are available in IBM Bluemix in the `logs` directory of each application instance. These logs can be accessed from the IBM Bluemix console or via the CF CLI. For example:

* To access recent logs for an app, run the following command:

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* To see the `messages.log` file of an app running on a DEA node, run the following command:

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* To see the `messages.log` file of an app running on a Diego cell, run the following command:

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

The log level and other trace options can be set through the Liberty configuration file. For more information, see [Liberty profile: Trace and logging](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). Tracing can also be adjusted on a running application instance by using the IBM Bluemix console.

## Using the trace and dump capabilities
{: #using_trace_and_dump}

The Liberty tracing configuration can be adjusted for a running application directly from the IBM Bluemix console. The console also provides capability for requesting and downloading thread and heap dumps. In order to adjust the tracing configuration or request a dump, select a Liberty application in the Bluemix console and choose the `Runtime` menu in the navigation. In the `Runtime` view, select an instance and press the *TRACE* or *DUMP* button. If adjusting the trace level, see [Liberty profile: Trace and logging](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) for the details of the syntax of the trace specification.

### Diego: triggering dumps via SSH

For an application running in a Diego cell, it is also possible to trigger a thread and heap dump via CF CLI using the SSH feature. For example:

```
$ cf ssh <appname> -c "pkill -3 java"
```
{: codeblock}

See the documentation below for details on downloading the generated dump files.

## Download dump files
{: #download_dumps}

By default, the various dump files are placed in the `dumps` directory of the application container.

### DEA application

For an application running in a DEA node, use the "cf files" functionality to view and download the dump files.

* To see the generated dumps, run the following command:

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* To download a dump file, run the following commands:
  
    1. Get application GUID

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Download dump file

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Diego application

For an application running in a Diego cell, use the "cf ssh" functionality to view and download the dump files.

* To see the generated dumps, run the following command:

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* To download a dump file, run the following command:

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

It is also possible to use `scp` and other similar tools to view and download the dump files. Refer to [Accessing Apps with SSH](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) for more information.

# rellinks
{: #rellinks}
## general
{: #general}
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

