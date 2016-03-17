---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Managing Liberty and Node.js apps
{: #app_management}

*Last updated: 17 March 2016*

App Management is a set of development and debugging utilities that can be enabled for your Liberty and Node.js applications on {{site.data.keyword.Bluemix}}.
{:shortdesc}

##App Management utilities
{: #Utilities}

These utilities support both Liberty and Node.js.

  1. *proxy*: Minimal application management that serves as a proxy between your application and {{site.data.keyword.Bluemix_notm}}.

    When enabled, the buildpack starts a proxy agent that is located between your application's runtime and container. The *proxy* utility handles all requests that the application receives. Based on the type of request, it either performs an App Management action or forwards the request to your application. *proxy* allows enablement of most other App Management utilities. By enabling *proxy*, your application container continues to live even if the application crashes. The proxy agent also allows for incremental file updates, which enables the "Live Edit" mode for Node.js applications.
	
  2. *devconsole*: Enables the development console utility that is accessible at the following URL:
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/manage
    ```
	
    Using the development console, users can restart, stop, or suspend their applications. Users can also enable or access the shell and inspector utilities.

    The devconsole utility also starts *proxy*.
	
  3. *hc*: Health Center agent that enables your application to be monitored by the Health Center client.

    The Health Center supports analyzing the performance of your Liberty and Node.js applications by using the IBM Monitoring and Diagnostic Tools. For more information see [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>
	
  4. *shell*: Enables a web-based shell that is accessible from the devconsole utility or by accessing the following URL:
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/shell
    ```
	
    A terminal window is displayed with shell access into your application after you access the shell utility. You can do everything that is supported in a regular shell, such as editing files, checking memory usage or running diagnostic commands.
	
    The *shell* utility also starts *proxy*.

These utilities support Liberty only.

  1. *debug*: Turns the Liberty application into debug mode and enables clients such as the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} to establish a remote debugging session with the application.
  
   For more information, see [Remote Debug](../manageapps/eclipsetools/eclipsetools.html#remotedebug).
   
   The *debug* utility also starts *proxy*.
   
  2. *jmx*: Enables the JMX REST Connector to allow a remote JMX client to manage the application by using {{site.data.keyword.Bluemix_notm}} user credentials.
  
  For more information on configuring a JMX connector, see [Configuring secure JMX connection to the Liberty profile.](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.
  
  The *jmx* utility does not start proxy.

These utilities support Node.js only.

  1. *inspector*: Enables the node inspector debugger interface that is accessible from the *devconsole* utility or at *https://myApp.mybluemix.net/bluemix-debug/inspector.*
  
  The inspector process runs in your application container. Use this utility to create CPU usage profiles, add breakpoints, and debug code, all while your application is running on {{site.data.keyword.Bluemix_notm}}. For more information about the node inspector module, see [node-inspector on GitHub](https://github.com/node-inspector/node-inspector){:new_window}.
  
  The *inspector* utility also starts *proxy*.
  
  2. *strongpm*: Enables use of [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} to analyze your Node.js application with utilities such as [StrongLoop Metrics, Profiling and Tracing](https://strongloop.com/node-js/devops-tools/){:new_window}.
    
  The *strongpm* utility also starts *proxy*.
  
  Take the following steps to configure your Node.js application with [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window}.

    1. Configure the *strongpm* BlUEMIX_APP_MGMT_ENABLE environment variable and restage your application.
    
	```
    cf set-env <appname> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <appname>
    ```
	
    2. From the Cloud Foundry command line, add a route to your application where the route has "-pm" appended to the application name, such as, <appname>-pm.mybluemix.net.
    
	```
    cf map-route <appname> ng.bluemix.net -n <appname>-pm
    ```
	
    3. Install the [StrongLoop npm module](https://www.npmjs.com/package/strongloop){:new_window} on your local workstation.
    
	```
    npm install -g strongloop
    ```
	
    4. Create an account on [StrongLoop’s website](https://strongloop.com/register/){:new_window}.
    5. Launch Arc on your local workstation and login with the account you created.
    
	```
    slc arc
    ```
	
    6. Navigate to the Process Manager view within Arc. Input the newly created route with port 80 into the Process Manager. Press the Activate button. See [full documentation on using Arc](https://docs.strongloop.com/display){:new_window} for more details.
	
  3. *trace*: Dynamically sets trace levels if your application is using *log4js*, *ibmbluemix*, or *bunyan* logging modules.
  
  **Note:** Supported dependency versions:

    * log4js:(0.6.0 - 0.6.24)
    * bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
    * ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)
  
  Go to the Instance Details page in the {{site.data.keyword.Bluemix_notm}} web console and select **Actions** to see the UI.

  The *trace* utility does not start *proxy*.

##How to configure App Management
{: #configure}

To enable App Management utilities, set the *BLUEMIX_APP_MGMT_ENABLE* environment variable and restage your application. Multiple utilities can be enabled by separating them with a “+”.

For example, to enable devconsole and *shell* utilities, run the following command:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Don't forget to restage your application after you set the environment variable:

```
cf restage myApp
```

If you do not want the App Management utilities to be installed with your application, set the *BLUEMIX_APP_MGMT_INSTALL* environment variable to 'false' and restage your application.

For example:

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

##Restrictions
{: #restrictions}

* App Management supports only single-instance applications.
* Changes that you make to your application using App Management are transient, and are lost after exiting this mode. This mode is only for temporary development use, and is not intended to be used as a production environment due to performance.
* Most App Management utilities do not work if you set your start command in the manifest.yml file (command) or CF CLI (-c). Those methods are buildpack overrides, and are anti-patterns for starting Node.js applications. For best results, set the start command in the package.json file or Procfile.

##Development Mode for Eclipse Tools
{: #devmode}

Development mode is a feature of the [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) that gives developers the ability to work with their applications while they are running in the cloud.

While working with their applications on {{site.data.keyword.Bluemix_notm}}, developers might feel that they cannot perform normal development activities as they might on a local environment. To tackle this issue, development mode through Eclipse Tools provides a way for you to work in the cloud while in a temporary, secure workspace.

Development mode is supported for both Liberty and Node.js applications. With development mode enabled for your Liberty or Node.js application, you can update application files incrementally without having to push your application. You can also establish a debugging session with your application. Development mode for Liberty applications is equivalent to enabling the debug and jmx App Management utilities. For Node.js applications, it is equivalent to enabling the *devconsole*, *inspector*, and *shell* utilities.
