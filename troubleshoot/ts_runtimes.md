---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Troubleshooting for runtimes
{: #runtimes}

You might experience problems when you use {{site.data.keyword.Bluemix}} runtimes. In many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}


## Obsolete buildpack used when an app is pushed
{: #ts_loading_bp}

You might not be able to use the latest buildpack components when you push an app. You can use buildpacks that have built-in mechanisms to prevent loading obsolete components, or you can delete the contents in your app's cache directory before you push or restage the app. 

When you push or restage an app after the buildpack is updated, the latest buildpack components aren't loaded automatically. As a result, your app uses the obsolete buildpack components from the cache. Updates that were applied to the buildpack since the last time you pushed the app aren't implemented. 
{: tsSymptoms}

Some buildpacks aren't configured to automatically download all updated components from the internet to ensure that you always use the latest version.
{: tsCauses} 

You can use buildpacks that have built-in mechanisms to avoid loading obsolete components, for example, the following buildpacks: 
{: tsResolve}

  * [Cloud Foundry Java buildpack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/java-buildpack){: new_window}. This buildpack has a built-in mechanism to ensure that the latest version of the buildpack is used. For more information about how this mechanism works, see [extending-caches.md ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Cloud Foundry Node.js buildpack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. This buildpack provides similar functionality by using environment variables. To enable the Node.js buildpack to download node modules from the internet every time, type the following command in the cf command line interface: 	
  ```
  set NODE_MODULES_CACHE=false
  ```

If the buildpack that you are using doesn't provide a mechanism to load the latest components automatically, you can manually delete the contents in the cache directory and push your app again. Use the following steps:

 1. Check out a branch of a null buildpack, for example, https://github.com/ryandotsmith/null-buildpack. For information about how to check out a branch, see [Git Basics - Getting a Git Repository ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
 2. Add the following line to the `null-buildpack/bin/compile` file and commit the changes. For information about how to commit changes, see [Git Basics - Recording Changes to the Repository ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
 3. Push your app with the null buildpack that was modified to delete the cache by using the following command. After you complete this step, all contents in the cache directory of your app are deleted.
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
 4. Push your app with the latest buildpack that you want to use by using the following command: 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
 
## NOTICE messages from the PHP buildpack
{: #ts_phplog}

You might see messages that contain NOTICE from the logs. You can stop the logging of these messages by changing the logging level.	

When you push an app to {{site.data.keyword.Bluemix_notm}} by using a PHP buildpack, you might see messages that contain `NOTICE`:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```
In the PHP buildpack, the error_log parameter defines the logging level. By default, the value of the `error_log` parameter is **stderr notice**. The following example shows the default logging level configuration in the `nginx-defaults.conf` file of the PHP buildpack that Cloud Foundry provides. For more information, see [cloudfoundry/php-buildpack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```
	
The `NOTICE` messages are for information and might not indicate a problem. You can stop the logging of these messages by changing the logging level from `stderr notice` to `stderr error` in the nginx-defaults.conf file of your buildpack. For example: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
For more information about how to change the default logging configuration, see [error_log ![External link icon](../icons/launch-glyph.svg "External link icon")](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Can't import a third-party Python library into {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

You might not be able to import a third-party Python library into {{site.data.keyword.Bluemix_notm}}. To resolve the problem, add configuration files to the root directory of your python app.

When you try to import a third-party Python library, such as the `web.py` library, the `cf push` command fails.
{: tsSymptoms}

Configuration information for the Python app is missing.
{: tsCauses}

Add a `requirements.txt` file and a `Procfile` file to the root directory of your Python app. The following information assumes that you are importing the `web.py` library:
{: tsResolve}

 1. Add a `requirements.txt` file to the root directory of your Python app.
 
 The `requirements.txt` file specifies the library packages that are required for your Python app and the version of the packages. The following example shows the content of the `requirements.txt` file, where `web.py==0.37` indicates the version of the `web.py` library that will be downloaded is 0.37, and `wsgiref==0.1.2` indicates the version of the web server gateway interface that is required by the web.py library is 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	 For more information about how to configure the `requirements.txt` file, see [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
 2. Add a `Procfile` file to the root directory of your Python app.
 The `Procfile` file must contain the start command for your Python app. In the following command, *yourappname* is the name of your Python app, and *PORT* is the port number that your Python app must use to receive requests from users of the app. *$PORT* is optional. If you don't specify PORT in the start command, the port number under the `VCAP_APP_PORT` environment variable that is inside the app is used. 
	```
	web: python <yourappname>.py $PORT
	```

You can now import the third-party Python library into {{site.data.keyword.Bluemix_notm}}.	


## The Actions button on the Instance Details page is disabled
{: #ts_actionsbutton}

The Actions button on the Instance Details page is disabled.
{: tsSymptoms} 

This problem occurs for the following reasons:
{: tsCauses}

 * The app isn't a Java&trade; web app. Runtime Management Utilities (RMU) supports only web apps that are deployed with Liberty buildpacks.
 * The app isn't deployed with the embedded Liberty buildpack.
 * The app was deployed with an early version of Liberty buildpack.

If the problem is caused by an early version of Liberty buildpack, redeploy the app in {{site.data.keyword.Bluemix_notm}}. Otherwise, you can provide the following client application log files to the support team:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
 
  
## Credentials are required to open a trace or dump window
{: #ts_username}

A user name and password are required to open the trace or dump window.
{: tsSymptoms}

This problem occurs because of the login session timeout.
{: tsCauses}

Enter the user name and password again.
{: tsResolve}


## Error occurs when trace or dump operations are running
{: #ts_target}

An error message is displayed while the trace or dump operations are running. The message indicates that a target instance for an app isn't in the running state:	
{: tsSymptoms}

```
Instance 0: Trace specification is set successfully
Instance 2: Trace specification is set successfully
Instance 1: Target instance 1 for app abcd is not in the running state.
Instance 3: Trace specification is set successfully
Instance 4: Trace specification is set successfully
```

This problem occurs for the following reasons:
{: tsCauses} 

  * The trace or dump management capabilities are only for app instances that are running. Trace or dump operations can't be used on app instances that are stopped, starting, or crashed.
  * The status of the app instance is changing when the trace or dump dialog is opened. 

Close the window, then open it again.
{: tsResolve} 


## Instances have different traceSpecification configurations
{: #ts_different_config}

For different instances of one app, you might see different traceSpecification configurations.
{: tsSymptoms}

This behavior occurs for the following reasons:
{: tsCauses}

  * You changed the configuration for one or more instances previously. If you change the traceSpecification configuration for one instance, the change doesn't apply to other instances of the same app. For example, your app uses log4j and you have 2 instances for this app. You can change the log level of instance 0 from info to debug, but the log level of instance 1 remains as info.
  
  * The app scales out and has new instances. RMU doesn't apply the traceSpecification configuration of the existing instance to the new, scaled out, instance. The new instance uses the default configuration. For example, your app uses log4j and it has one instance. You can change the log level of this instance from info to debug. After you make this change, if you scale out your app to two instances, the log level of the new instance is info, rather than debug.

No action is required. This behavior is expected.
{: tsResolve} 


## Disk quota exceeded
{: #ts_diskquota}

You might see, in your app log, that your disk quota is exceeded.

You see the `Disk quota exceeded` error message in the log of your app.
{: tsSymptoms}

This problem occurs for one of the following reasons: 
{: tsCauses} 

  * The dump files are generated with the running app instances, and the files use up the allocated disk quota. By default, the disk quota for one app instance is 1 GB. You can check your disk usage by clicking **Dashboard > Application > App Runtime**. The following example shows the runtime information, including disk usage, for two instances of an app:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * The disk quota is limited by the current organization quota.

Use one of the following methods:
{: tsResolve} 

  * Delete dump files after they are downloaded.
  * Redeploy the app with a bigger disk quota by including the following entry in the deployment manifest:
    ```
	disk_quota: 2048
	```
	
