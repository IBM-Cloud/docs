---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# Start coding with Git
*Last updated: 2 March 2016*  

You can create a hosted Git repository that deploys to {{site.data.keyword.Bluemix}} automatically. Then, you can modify the code that runs in your app by pushing changes to the Git repository. 
{:shortdesc}

1. To get started, on the app's Overview page, click **Add Git Repo and Pipeline**, or in the {{site.data.keyword.Bluemix_notm}} Classic Experience, click **ADD GIT**. 
2. In the window that opens, make sure that the **Populate the repo with the starter app package and enable the Build & Deploy pipeline** check box is selected. The Git repository is created. If starter code is available, it is loaded into the repository. In addition, the application is deployed by the Delivery Pipeline service running in {{site.data.keyword.jazzhub}}.  
3. To update your app, you can use the command line or the Web IDE.  
   **If you use the command line:**  
   a. Clone your Git repository from the Git URL on the app's Overview page.  
   b. In your favorite editor, update the code.  
   c. From the Git command line interface, push your changes.  
	    
   **If you use the Web IDE:**  
   a. On the app's Overview page, click **Edit Code**. Your project opens in the Web IDE.  
   b. Make changes as needed, and then push by using the built-in Git support.  
		
The updated app is redeployed to {{site.data.keyword.Bluemix_notm}}.  

For step-by-step directions, see [Set up Git integration and auto-deploy in DevOps Services](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment).  

## Added Git? Try {{site.data.keyword.Bluemix_notm}} Live Sync  

If you are building a Node.js app, you can use {{site.data.keyword.Bluemix_notm}} Live Sync to quickly update the app instance on {{site.data.keyword.Bluemix_notm}} and develop as you would on the desktop.  

To learn more about {{site.data.keyword.Bluemix_notm}} Live Sync, see [{{site.data.keyword.Bluemix_notm}} Live Sync](../develop/bluemixlive.html). For more details on the commands, see the [{{site.data.keyword.Bluemix_notm}} Live Sync CLI doc](../cli/reference/bl/index.html). To use {{site.data.keyword.Bluemix_notm}} Live Sync with the Web IDE, see [Live Edit](../develop/bluemixlive.html).  

1. Download and install the {{site.data.keyword.Bluemix_notm}} Live Sync bl command line. 

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Download the Windows bl command line button" /> </a> 
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Download the Mac bl command line button" /> </a>
</p>

**Important:** The bl command line tool is available only for Windows 7 and 8 and Mac OS X version 10.9 or later. 

2. On a command line, log in using the following command. You will be prompted for your IBM® id and password. 
```
bl login
```

3. See the list of projects that are available for {{site.data.keyword.Bluemix_notm}} Live Sync synchronization by entering the following command: 
```
bl projects
```
Find the project name in the list that matches your application. The project name has the format of your *alias* | *your application name*. 

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}} by entering the following command. If you are the owner of the project, you only need to specify your-application-name for projectName. 
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync projectName -d localDirectory --verbose
```
This command continues to run (and synchronization continues) until you enter a "q". The --verbose option displays the logging and status information. If any of your arguments contain a space, you need to enclose the name in quotes. 

5. In another command line window, in your local directory, deploy the application to {{site.data.keyword.Bluemix_notm}} in Live Edit mode by entering the following command:
```
bl start
```  

When you change the files in your local directory, the changes are automatically propagated to both the application that is running on {{site.data.keyword.Bluemix_notm}} and the project cloud workspace. If you need to restart the Node application, then you can use the following command:
```
bl start --restart 
```
