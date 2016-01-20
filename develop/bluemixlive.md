{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} Live Sync {: #live-sync}

*Last Updated: 8 December 2015*  

If you are building a Node.js application, you can use {{site.data.keyword.Bluemix}} Live Sync to quickly update the application instance on {{site.data.keyword.Bluemix_notm}} and develop as you would on the desktop without redeploying.   
{: shortdesc} 

When you make a change, you can see that change in your running {{site.data.keyword.Bluemix_notm}} application immediately. {{site.data.keyword.Bluemix_notm}} Live Sync works from both the command line and in the Web IDE. You can debug applications written in Node.js by using {{site.data.keyword.Bluemix_notm}} Live Sync.  

{{site.data.keyword.Bluemix_notm}} Live Sync consists of three features. 

**Desktop Sync**  
    You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
	
**Live Edit**	
    You can make changes to a Node.js application running in {{site.data.keyword.Bluemix_notm}} and test them in your browser right away. Any changes that you make in a synchronized desktop directory or in the Web IDE are propagated to the application’s file system immediately.  
	
**Debug**  
    While a Node.js application is in Live Edit mode, you can shell into it and debug it. You can edit code dynamically, insert breakpoints, step through code, restart the runtime, and more using the Node Inspector debugger.  

You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. You can use Live Edit to propagate changes in your cloud-based project workspace to your running application. You can use one or both of these features. And if you use Desktop Sync or Live Edit to put your application into Live Edit mode, you can debug your running application.

The Bluemix Live Sync process is illustrated in the following diagram.	

*Figure 1. The Bluemix Live Sync process* 
![Image of the Bluemix Live Sync process](images/bluemix-live-sync.png)
 
If you are developing a Java application that is running on Liberty, you can debug remotely by using the [Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html#eclipsetools).

##Desktop Sync {: #desktop-sync} 

You can use the Desktop Sync feature of Bluemix Live Sync to quickly update the application instance on {{site.data.keyword.Bluemix_notm}} and develop as you would on your desktop. 

Desktop Sync has the following considerations: 
* Desktop Sync runs on these operating systems: 
  * Windows 7 or 8
  * Mac OS X version 10.9 or later   
      **Note:** Windows requires .NET Framework version 4.5. If you do not have .NET installed, you are prompted to install it when you install the {{site.data.keyword.Bluemix_notm}} Live Sync command line interface (CLI).  
* You do not need to clone your Git repository. 
* No matter what type of application you are developing, you can synchronize your desktop project with the cloud workspace. 
* If your application is written in Node.js, you can propagate changes to running applications.

For more details on the commands, see the [Bluemix Live Sync CLI doc](../cli/reference/bl/index.html). 

<ol>
<li>Download and install the {{site.data.keyword.Bluemix_notm}} Live Sync bl command line.   
<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Download the Windows bl command line button" /> </a> 
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Download the Mac bl command line button" /> </a>
</p>  

<strong>Important:</strong> The bl command line tool is available only for Windows 7 and 8 and Mac OS X version 10.9 or later. </li>
<li>On a command line, log in using the following command. You will be prompted for your IBM id and password.  
<pre class="codeblock">bl login</pre>
</li>

<li>See the list of projects that are available for {{site.data.keyword.Bluemix_notm}} Live Sync synchronization by entering the following command: 
<pre class="codeblock">bl projects</pre>
<p>Find the project name in the list that matches your application. The project name has the format of your <i>alias</i> | <i>your application name</i>. </p>
</li>
<li>Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}} by entering the following command. If you are the owner of the project, you only need to specify your-application-name for projectName. 
<pre class="codeblock">bl sync projectName -d localDirectory --verbose</pre>
<p>This command continues to run (and synchronization continues) until you enter a "q". The --verbose option displays the logging and status information. If any of your arguments contain a space, you need to enclose the name in quotes. </p></li>
<li>In another command line window, in your local directory, deploy the application to {{site.data.keyword.Bluemix_notm}} in Live Edit mode by entering the following command:
<pre class="codeblock">bl start</pre>
</li>
</ol>

When you change the files in your local directory, the changes are automatically propagated to both the application that is running on {{site.data.keyword.Bluemix_notm}} and the project cloud workspace. If you need to restart the Node application, then you can use the following command:
```
bl start --restart 
```

##Live Edit {: #live-edit} 

If you are building a Node.js application, when you make changes to your project using the Web IDE, the Live Edit feature of the {{site.data.keyword.Bluemix_notm}} Live Sync can quickly update the application instance running on {{site.data.keyword.Bluemix_notm}}. Live Edit allows you to develop as you would on the desktop without redeploying. 

Live Edit is supported for Node.js applications only. 

In the Web IDE, in the run bar, click **Live Edit**. 

![Image of Run bar with live edit](images/run-bar-live-edit.png) 

Live Edit allows you to quickly preview changes to Node.js applications running on {{site.data.keyword.Bluemix_notm}}. When you update your code with Live Edit turned on, you can refresh your web application's browser window to see those changes reflected seconds after you make them. 

For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync).

When you change the files in your Web IDE, they are automatically redeployed to your application running on {{site.data.keyword.Bluemix_notm}}. If you need to restart the Node application, then you can use the **Restart** button in the run bar.

##{{site.data.keyword.Bluemix_notm}} Live Debug {: #live-debug}

You can access {{site.data.keyword.Bluemix_notm}} Live Sync Debug feature when {{site.data.keyword.Bluemix_notm}} Live Sync is enabled for your Node.js app. 

With debug, you can dynamically edit code, insert breakpoints, step through code, restart the runtime and more, all while your app is being served by {{site.data.keyword.Bluemix_notm}}. You can incrementally develop your app with agility while choosing from the large list of {{site.data.keyword.Bluemix_notm}} services. 

{{site.data.keyword.Bluemix_notm}} Live Debug includes the following features:

* Application runtime control
* Debug by using [node-inspector](https://github.com/node-inspector/node-inspector)
* Shell access 

###Application runtime control {: #app-runtime} 

With the application runtime control, you can use Debug to inspect the app's state at start time. This capability is useful when you are troubleshooting an app that crashes on start.

While you are developing your app, you can select from the following actions:

* Perform a quick restart of the app
* Suspend the app before any app code runs

###Debug {: #debug} 

Debug includes the following capabilities:

**Restriction:** Google Chrome is required.

* Set breakpoints in the app code to pause execution at a specific line.
* Edit breakpoint conditions to pause execution only when certain criteria are met. 
* Inspect the state of local variables and fields. 
* View debug output from `console.log()` calls immediately. This action is faster than monitoring cf logs.
* Use the built-in source code editor to make immediate, yet temporary, changes to the running app code.

###Shell {: #shell} 

This tool gives you shell access to the container in which your app is running. By using this terminal, you can remotely run diagnostic shell commands to administer your app. 

Monitor memory and CPU usage within the instance that uses standard Linux commands, such as **top**, **ps**, and **kill**. 

###Configuring an app to enable {{site.data.keyword.Bluemix_notm}} Live Debug {: #configure_app_debug} 

The app must use the IBM SDK for Node.js buildpack. Custom buildpacks are not supported. 

1. Allow the buildpack to detect the app start command. The start command must be auto-detected by the buildpack, not set in the `manifest.yml` file.  
    
    a. Ensure that the `package.json` file contains a start script that includes a start command for the app.  
    b. If the app `manifest.yml` file contains a command, set it to null.  

2. Set the environment variable.  
    
    a. In the `manifest.yml` file, add this variable: 
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true" 
	```

3. Increase the memory.  
    
    a. In the app `manifest.yml` file, add 128M or more to the value that is specified for the memory attribute. 
	
After the {{site.data.keyword.Bluemix_notm}} Live Debug is installed, you can use the debug tools.

Push the app then browse to `https://app-host.mybluemix.net/bluemix-debug/manage` to access the {{site.data.keyword.Bluemix_notm}} debug user interface. When you are prompted, enter your IBM ID and password to authenticate. 

###Restoring app configurations and disabling Bluemix Live Debug {: #restore_live_debug} 

1. Remove the ENABLE_BLUEMIX_DEV_MODE environment variable from the app `manifest.yml` file.

2. Restore the app's original start command and memory value. 

3. Push the app.


># Related Links {:class="linklist"}
>## Tutorials and samples {:id="samples"}
>* [Test and debug a Node.js app with Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync)
>
># Related Links {:class="linklist"}
>## Related links {:id="general"}
>* [bl commands](https://www.ng.bluemix.net/docs/cli/bl_cli.html)   
>
>{:elementKind="article" id="rellinks"}
