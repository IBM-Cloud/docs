---

copyright:
  years: 2015, 2016

---



{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}


# Debugging
{: #debugging}

*Last updated: 25 May 2016*

If you experience problems with {{site.data.keyword.Bluemix}}, you can view the log files to investigate the problems and debug the errors. 
{:shortdesc}

Logs provide information such as whether a job runs successfully, or whether it fails. They also provide relevant information that can be used to debug and determine the cause of a problem.

Logs are in a fixed format. For verbose logs, you can filter the logs or use external logging hosts to store and process the logs. For more information about log formats, viewing and filtering logs, and configuring external logging, see [Logging for apps running on Cloud Foundry](../monitor_log/monitoringandlogging.html#logging_for_bluemix_apps){: new_window}.


## Debugging staging errors
{: #debugging-staging-errors}
You might experience problems when you stage your applications on {{site.data.keyword.Bluemix_notm}}. If your app fails to stage, you can search and review staging (STG) logs to determine what has happened during the app deployment and to recover from the problem. For more information about the methods of viewing logs for Bluemix apps, see [viewing logs](../monitor_log/monitoringandlogging.html#viewing_logs){: new_window}.  

To understand why your app might be failing on {{site.data.keyword.Bluemix_notm}}, you need to know how an app is deployed to {{site.data.keyword.Bluemix_notm}} and runs on it. For detailed information, see [Application deployment](../manageapps/depapps.html#appdeploy){: new_window}.


The following procedure shows how you can use the `cf logs` command to debug staging errors. Before you take the following steps, ensure that you have installed the cf command line interface. For more information about installing the cf command line interface, see [Installing the cf command line interface](../starters/install_cli.html){: new_window}.

  1. Connect to {{site.data.keyword.Bluemix_notm}} by entering the following code in the cf command line interface:
     ```
	 cf api https://api.ng.bluemix.net
	 ```
	 
  2. Log in to {{site.data.keyword.Bluemix_notm}} by entering `cf login`.
  
  3. Retrieve recent logs by entering `cf logs appname --recent`. If you want to filter a verbose log, use the `grep` option. For example, you can enter the following code to display only the [STG] logs:
    ```
	cf logs appname --recent | grep '\[STG\]'
	```
  4. View the first error that is displayed in the log.
  
If you use the IBM Eclipse tools for {{site.data.keyword.Bluemix_notm}} plug-in to deploy applications, in the **Console** tab of the Eclipse tool, you can see logs that are similar to the cf logs output. You can also open a separate Eclipse window to track `the logs` when you deploy the application.

In addition to the `cf logs` command, in {{site.data.keyword.Bluemix_notm}} you can also use the Monitoring and Analytics service to collect the log details. In addition, the Monitoring and Analytics service monitors the performance, health, and availability of your applications. It also provides log analytics for Node.js and Liberty runtime applications.  

### Debugging staging errors for a Node.js application

The following example shows a log that is displayed after you enter `cf logs appname --recent`. The example assumes that staging errors occurred for a Node.js application:
```
2014-08-11T14:19:36.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({name"=>"SampleExpressApp"}
2014-08-11T14:20:44.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STOPPED"})
2014-08-11T14:20:44.19+0100 [App/0]   ERR
2014-08-11T14:20:44.43+0100 [DEA]     OUT Stopping app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:44.44+0100 [DEA]     OUT Stopped app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:48.97+0100 [DEA]     OUT Got staging request for app with id 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:50.94+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STARTED"})
2014-08-11T14:20:51.66+0100 [STG]     OUT -----> Download app package (4.1M)
2014-08-11T14:20:51.90+0100 [STG]     OUT -----> Download app buildpack cache (1.1M)
2014-08-11T14:20:52.78+0100 [STG]     OUT -----> Buildpack Version: v1.1-20140717-1447
2014-08-11T14:20:52.78+0100 [STG]     ERR parse error: Expected another key-value pair at line 18, column 3
2014-08-11T14:20:52.79+0100 [STG]     OUT 0 info it worked if it ends with ok
```
{: screen}


The first error in the log shows the reason why the staging fails. In the example, the first error is an output from the DEA component during the staging phase.
```
2014-08-11T14:20:52.78+0100 [STG]   ERR parse error: expected another key-value pair at line 18, column 3
```
{: screen}


For a Node.js application, the DEA uses the information in the `package.json` file to download the modules. From this error, you can see that error occurs for the module. Therefore, you might need to review the 18th line of the `package.json` file. 

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*",
18   }
```
{: screen}


You can see that a comma is placed at the end of line 17, therefore, a key-value pair on line 18 is expected. To fix the problem, remove the comma:

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*"
18   }
```
{: screen}


## Debugging runtime errors
{: #debugging-runtime-errors}
If you experience problems with your application at run time, application logs can help to pinpoint the cause of the error and recover from that problem. 

Specifically, logging to stdout and stderr can be enabled. For more information about how to configure the log files for applications that are deployed by using the {{site.data.keyword.Bluemix_notm}} built-in buildpacks, see the following list:

  * For Liberty for Java™ applications, see [Liberty Profile: Logging and Trace](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}.
  * For Node.js applications, see [How to log in node.js](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}. 
  * For PHP applications, see [error_log](http://php.net/manual/en/function.error-log.php){: new_window}.
  * For Python applications, see [Logging HOWTO](https://docs.python.org/2/howto/logging.html){: new_window}.
  * For Ruby on Rails applications, see [The Logger](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}.
  * For Ruby Sinatra applications, see [Logging](http://www.sinatrarb.com/intro.html#Logging){: new_window}.
  
When you enter `cf logs appname --recent` in the cf command line interface, only the most recent logs are displayed. To view the logs for errors that occurred earlier, you must retrieve all the logs and search for the errors. To retrieve all the logs for your application, use one of the following methods:
<dl> 
<dt><strong>{{site.data.keyword.Bluemix_notm}} Monitoring and Analytics Service</strong></dt> 
<dd>The integrated log file search and analysis capabilities of the Monitoring and Analytics Service can help you to quickly identify errors. For more information, see <a href="../services/monana/index.html#gettingstartedtemplate" target="_blank">Monitoring and Analytics</a>.</dd> 
<dt><strong>Third-party tools</strong></dt> 
<dd>You can collect and export the logs from your application to an external log host. For more information, see <a href="../monitor_log/monitoringandlogging.html#thirdparty_logging" target="_blank">Configuring external logging</a>.</dd> 
<dt><strong>Scripts to collect and export the logs </strong></dt> 
<dd>To use a script to automatically collect and export the logs to an external file, you must connect to the {{site.data.keyword.Bluemix_notm}} server from your computer, and you must have enough space on your computer to download the logs. For more information, see <a href="../support/index.html#collecting-diagnostic-information" target="_blank">Collecting diagnostic information</a>. </dd>
</dl>

The `stdout.log` and `stderr.log` files were previously accessible, by default, through the application view in the {{site.data.keyword.Bluemix_notm}} Dashboard under **Files** > **logs**. However, that application logging is no longer available with the current version of Cloud Foundry where {{site.data.keyword.Bluemix_notm}} is hosted. To keep the stdout and stderr application logging accessible through the {{site.data.keyword.Bluemix_notm}} Dashboard under **Files** > **logs**, you can redirect the logging to other files in the {{site.data.keyword.Bluemix_notm}} file system, depending on the runtime that you are using. 

  * For Liberty for Java applications, output directed to stdout and stderr is already contained in the `messages.log` file in the logs directory. Look for entries prefixed with SystemOut and SystemErr respectively.
  * For Node.js applications, you can override the console.log function to explicitly write to a file in the logs directory.
  * For PHP applications, you can use the error_log function write to a file in the logs directory.
  * For Python applications, you can have the logger write to a file in the logs directory: logging.basicConfig(filename='../../logs/example.log',level=logging.DEBUG)
  * For Ruby applications, you can have the logger write to a file in the logs directory.
 
 
### Debugging code changes
{: #debug_code_changes}

If you are making code changes to an app that is already deployed and working, yet your code changes aren't being reflected in {{site.data.keyword.Bluemix_notm}}, you can debug by using the logs. Whether or not your app is running, you can check the logs that are generated during the app deployment or runtime to debug why the new code isn't working.

Depending on the way the new code is deployed, choose one of the following methods to debug the code changes: 

  * For new code that is deployed from the cf command line, check the output from the *cf push* command. In addition, you can use the *cf logs* command to find more clues for solving the problem. For more information about how to use the *cf logs* command, see [viewing logs from the command line interface](../monitor_log/monitoringandlogging.html#viewing_logs_cli){: new_window}. 

  * For new code that is deployed from a GUI such as the {{site.data.keyword.Bluemix_notm}} user interface, DevOps Delivery Pipeline, or Travis-CI, you can check the logs from the interface. For example, if you deploy the new code from {{site.data.keyword.Bluemix_notm}} user interface, you can go to Dashboard, find your app, and then view logs for clues.   For more information about how to view logs from the {{site.data.keyword.Bluemix_notm}} user interface, see [Viewing logs from Bluemix Dashboard](../monitor_log/monitoringandlogging.html#viewing_logs_UI){: new_window}.  
 

# rellinks
{: #rellinks}

## general
{: #general}

  * [Droplet Execution Agent (DEA)](http://docs.cloudfoundry.org/concepts/architecture/execution-agent.html){: new_window}
  * [Getting started with IBM Monitoring and Analytics for Bluemix service](../services/monana/index.html#gettingstartedtemplate){: new_window}
  * [How Bluemix works](../public/index.html#howwork){: new_window}
  * [Installing the cf command tool](../starters/install_cli.html){: new_window}
  * [Viewing logs](../monitor_log/monitoringandlogging.html#viewing_logs){: new_window}
  
  
 









