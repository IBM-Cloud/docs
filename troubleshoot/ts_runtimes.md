---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# Troubleshooting for runtimes
{: #runtimes}

Last updated: 18 August 2016
{: .last-updated}


You might experience problems when you use IBM® Bluemix™ runtimes. However, in many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}


## Obsolete buildpack used when an app is pushed
{: #ts_loading_bp}


You might not be able to use the latest buildpack components when you push an app. You can use buildpacks that have built-in mechanisms to prevent loading obsolete components, or you can delete the contents in your app's cache directory before you push or restage the app. 

 

When you push or restage an app after the buildpack is updated, the latest buildpack components are not loaded automatically. As a result, your app uses the obsolete buildpack components from the cache. Updates that have been applied to the buildpack since the last time you pushed the app are not implemented. 
{: tsSymptoms}



Some buildpacks are not configured to automatically download all updated components from the internet to ensure that you always use the latest version.
{: tsCauses} 

 

You can use buildpacks that have built-in mechanisms to avoid loading obsolete components. The following buildpacks are two examples: 
{: tsResolve}

  * [Cloud Foundry Java buildpack](https://github.com/cloudfoundry/java-buildpack){: new_window}. This buildpack has a built-in mechanism to ensure that the latest version of the buildpack is used. For more information about how this mechanism works, see [extending-caches.md](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Cloud Foundry Node.js buildpack](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. This buildpack has similar functionality by using environment variables. To enable the Node.js buildpack to download node modules from the internet every time, type the following command in the cf command line interface: 	
  ```
  set NODE_MODULES_CACHE=false
  ```
If the buildpack that you are using does not provide a mechanism to load the latest components automatically, you can manually delete the contents in the cache directory and push your app again by taking the following steps:
  1. Check out a branch of a null buildpack, for example, https://github.com/ryandotsmith/null-buildpack. For information about how to check out a branch, see [Git Basics - Getting a Git Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
  2. Add the following line to the `null-buildpack/bin/compile` file and commit the changes. For information about how to commit changes, see [Git Basics - Recording Changes to the Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
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
	
 

When you push an application to Bluemix by using a PHP buildpack, you might see messages that contain `NOTICE`:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



In the PHP buildpack, the error_log parameter is used to define the logging level. By default, the value of the `error_log` parameter is **stderr notice**. The following example shows the default logging level configuration in the `nginx-defaults.conf` file of the PHP buildpack that is provided by Cloud Foundry. For more information, see [cloudfoundry/php-buildpack](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
The `NOTICE` messages are informational and do not necessarily indicate that a problem has occurred. You can stop the logging of these messages by changing the logging level from stderr notice to stderr error in the nginx-defaults.conf file of your buildpack. For example: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
For more information about how to change the default logging configuration, see [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Unable to import a third-party Python library into {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

You might not be able to import a third-party Python library into {{site.data.keyword.Bluemix_notm}}. You can solve the problem by adding configuration files into the root directory of your python application.


When you try to import a third-party Python library, such as the `web.py` library, the `cf push` command fails.
{: tsSymptoms}


 

This problem occurs when configuration information for the Python application is missing.
{: tsCauses}


 

To solve the problem, add a `requirements.txt` file and a `Procfile` file into the root directory of your Python app. The following information assumes that you are importing the web.py library:
{: tsResolve}

  1. Add a `requirements.txt` file into the root directory of your Python app.
     The `requirements.txt` file specifies the library packages that are required for your Python application and the version of the packages. The following example shows the content of the `requirements.txt` file, where `web.py==0.37` indicates the version of the `web.py` library that will be downloaded is 0.37, and `wsgiref==0.1.2` indicates the version of the web server gateway interface that is required by the web.py library is 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	For more information about how to configure the `requirements.txt` file, see [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
  2. Add a `Procfile` file into the root directory of your Python application.
	The `Procfile` file must contain the start command for your Python application. In the following command, *yourappname* is the name of your Python application, and *PORT* is the port number that your Python application must use to receive requests from users of the app. *$PORT* is optional. If you do not specify PORT in the start command, the port number under the `VCAP_APP_PORT` environment variable that is inside the app is used instead. 
	```
	web: python <yourappname>.py $PORT
	```
You are now able to import the third-party Python library into {{site.data.keyword.Bluemix_notm}}.	



## The Actions button on the Instance Details page is disabled
{: #ts_actionsbutton}



The Actions button on the Instance Details page is disabled.
{: tsSymptoms} 

 

This problem occurs because of the following reasons:
{: tsCauses}

  * The application is not a Java™ web application. Runtime Management Utilities (RMU) supports only web applications that are deployed with Liberty buildpacks.
  * The application is not deployed with the embedded Liberty buildpack.
  * The application was deployed with an early version of Liberty buildpack.



If the problem is caused by an early version of Liberty buildpack, redeploy the application in {{site.data.keyword.Bluemix_notm}}. Otherwise, you can provide the following client application log files to the support team:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## Credentials are required when opening trace or dump window
{: #ts_username}


 

A user name and password are required when opening the trace and dump window.
{: tsSymptoms}

 

This problem occurs because of the login session timeout.
{: tsCauses}

 

The solution is to reenter the user name and password.
{: tsResolve}




## Error occurs when trace or dump operations are running
{: #ts_target}

 

An error message is displayed while the trace or dump operations are running. The message indicates that a target instance for an app is not in the running state:	
{: tsSymptoms}

```
Instance 0: Trace specification is set successfully
Instance 2: Trace specification is set successfully
Instance 1: Target instance 1 for app abcd is not in the running state.
Instance 3: Trace specification is set successfully
Instance 4: Trace specification is set successfully
```



This problem occurs because of the following reasons:
{: tsCauses} 

  * The trace or dump management capabilities are only for application instances that are running. Trace or dump operations cannot be used on application instances that are stopped, starting, or crashed.
  * The status of the application instance is changing when the trace or dump dialog is opened. 
  


The solution is to close the window, and then reopen it again.
{: tsResolve} 



## Instances have different traceSpecification configuration
{: #ts_different_config}

 

For different instances of one application, you might see different traceSpecification configuration.
{: tsSymptoms}

 

This problem occurs because of the following reasons:
{: tsCauses}

  * You might have changed the configuration for one or more instances previously. If you change the traceSpecification configuration for one instance, it does not apply to other instances of the same application. For example, you application uses log4j and you have 2 instances for this application. You can change the log level of instance 0 from info to debug, but the log level of instance 1 remains info. 
  * The application scales out and has new instances. RMU does not apply the traceSpecification configuration of the existing instance to the new, scaled out instance. The new instance uses the default configuration. For example, your application uses log4j and it has one instance. You can change the log level of this instance from info to debug. After you make this change, if you scale out your application into two instances, the log level of the new instance is info, rather than debug.
  


This behavior is expected.
{: tsResolve} 





## Disk quota exceeded
{: #ts_diskquota}

You might see, in your app log, that your disk quota is exceeded.

 

You see the `Disk quota exceeded` error message in the log of your app.
{: tsSymptoms}



This problem is caused by one of the following reasons: 
{: tsCauses} 

  * The dump files are generated with the running application instances, and the files use up the allocated disk quota. By default, the disk quota for one application instance is 1 GB. You can check your disk usage by clicking **Dashboard > Application > App Runtime**. The following example shows the runtime information, including disk usage, for two instances of an application:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * The disk quota is limited by the current organization quota.
  
  


You can resolve this issue by using one of the following methods:
{: tsResolve} 

  * Delete dump files after they are downloaded.
  * Redeploy the application with a bigger disk quota by including the following entry in the deployment manifest:
    ```
	disk_quota: 2048
	```
	
	
<!-- begin STAGING ONLY --> 

	
## Log4js logger objects are not displayed in the Node.js Trace pop-up window
{: #ts_logger}

The log4js logger objects are not displayed in the Node.js Trace pop-up window when both the log4js and ibmbluemix modules are used in your app. 	

 
The log4js logger objects are not displayed in the Node.js Trace pop-up window when both the log4js, winston, and ibmbluemix modules are used in your app.
{: tsSymptoms}


Because the ibmbluemix module provides a unified API for log operations that use the log4js and winston modules, only the ibmbluemix logger objects are displayed in the Node.js Trace pop-up window. This is to stop the log level settings for the ibmbluemix, log4js, and winston logger objects from overwriting each other.
{: tsCauses}


This behavior is expected.
{: tsResolve}

<!-- end STAGING ONLY -->




<!-- begin STAGING ONLY -->


## Apply trace setting to all instances of the application check box is disabled
{: #ts_bunyan}

The **Apply trace setting to all instances of the application** check box is unchecked and disabled in the Node.js Trace pop-up window when the Bunyan logger levels are modified.



When you change the levels of the Bunyan logger objects, the **Apply trace setting to all instances of the application** check box is unchecked and disabled in the Node.js Trace pop-up window.
{: tsSymptoms} 

 

When Bunyan log levels are modified, the trace setting cannot be applied to all instances of an application. This is because the Bunyan library does not require the names or identifiers of Bunyan logger objects to be unique. More than one of the Bunyan logger objects that are used to specify levels in the log messages for your application can have the same name or identifier. Therefore, if the trace setting is enabled for an application, the log levels that are specified in the log messages of your application might be inaccurate.
{: tsCauses}




This behavior is expected.
{: tsResolve} 

<!-- end STAGING ONLY -->

