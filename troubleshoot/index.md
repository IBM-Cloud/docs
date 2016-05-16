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

# Troubleshooting for accessing {{site.data.keyword.Bluemix_notm}} 
{: #accessing}

*Last updated: 16 May 2016*

General problems with accessing {{site.data.keyword.Bluemix}} might include a user that is unable to log in to {{site.data.keyword.Bluemix_notm}}, an account that is stuck in a pending state, and so on. However, in many cases, you can recover from these problems by following a few easy steps. 
{:shortdesc}

## Unable to log in to {{site.data.keyword.Bluemix_notm}}
{: #ts_logintobm}

You must have a valid IBM ID and password to log in to {{site.data.keyword.Bluemix_notm}}.


When you try to sign in to {{site.data.keyword.Bluemix_notm}}, you see the following error message: 
{: tsSymptoms} 

`The IBM id and/or password entered below is incorrect. Please try again.`


The IBM ID and password that you use to sign in to {{site.data.keyword.Bluemix_notm}} is invalid.
{: tsCauses} 
 

To get a valid IBM ID and password, go to the My IBM profile page, and then complete one of the following steps:
{: tsResolve}
  * If you have already registered an IBM ID and you want to check whether your ID and password are valid, click **Sign in** and enter your IBM ID and password on the Sign in page. If you have forgotten your password, click **Forgot your password** on the right side of the Sign in page to reset your password. If you have forgotten your IBM ID or continue to have problems with your password, contact the Worldwide IBM Registration Help Desk for help. 
  * If you don't have an IBM ID, click **Register** to register an IBM ID and password. 
  
**Note:** For IBM employees, the IBM ID might be different from the intranet login ID. 





## You have unsaved changes
{: #ts_unsaved_changes}


When you navigate on the app details page, you might be unable to perform any actions and might be prompted to save changes before you can proceed. 


When you try to check your app or services on the app details page, you keep getting the following error message:
{: tsSymptoms} 

`You have unsaved changes in page app_name. Save or cancel the changes.`


When you scroll your mouse over the **INSTANCES** or **MEMORY QUOTA** field on the runtime pane, the values change. This behavior is by design; however, the error message prompts you to save the memory or instance settings before you navigate away from the page. 
{: tsCauses}


Close the message window, and then click the **RESET** button in your runtime pane. 
{: tsResolve} 




    
    
## Automatic failover between {{site.data.keyword.Bluemix_notm}} regions is not available
{: #ts_failover}

You are unable to use automatic failover between {{site.data.keyword.Bluemix_notm}} regions. However, you can use a DNS provider that supports failover among multiple IP addresses as a workaround.
 

When a {{site.data.keyword.Bluemix_notm}} region becomes unavailable, the apps that are running in that region are also unavailable, even if the same apps are running in another {{site.data.keyword.Bluemix_notm}} region.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}} does not yet provide automatic failover from one region to another.
{: tsCauses}

 
You can use a DNS provider that supports intelligent failover among multiple ID addresses, and manually configure your DNS settings to enable the automatic failover between {{site.data.keyword.Bluemix_notm}} regions. DNS providers with this capability include NSONE, Akamai, Dyn.
{: tsResolve}

When you configure your DNS settings, you must specify the public IP addresses of the {{site.data.keyword.Bluemix_notm}} regions that your apps are running in. To get the public IP address of a {{site.data.keyword.Bluemix_notm}} region, use the `nslookup` command. For example, you can type the following command in a command line window:
```
nslookup mybluemix.net
```



## Account is pending
{: #ts_accntpding}

If your account is pending, you cannot log in to {{site.data.keyword.Bluemix_notm}}.

 
After you register for a {{site.data.keyword.Bluemix_notm}} trial account, you might not be able to log in to {{site.data.keyword.Bluemix_notm}}. Instead, you see the following message:
{: tsSymptoms}

<code>Your account is pending. Please wait up to 24 hours for email confirmation and also check your spam folder. If you still have not received your email confirmation, contact <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix Support</a>.</code>


After you register for a {{site.data.keyword.Bluemix_notm}} trial account, you receive a confirmation email. You must click the link that is in the confirmation email to complete the registration process.
{: tsCauses} 

The confirmation email is sent to the email address that you provided. Check your inbox and your junk mail folder. If you haven't received the confirmation email, contact [{{site.data.keyword.Bluemix_notm}} Support](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



## Unable to add users to an organization
{: #ts_adduser}

You can invite more than one user to work under the same organization. You can invite users to your organization only if you are the account owner, or if you are both a manager and a member of the organization.
 

You cannot see the **Invite a New User** link in your **Manage Organizations** section. 
{: tsSymptoms}

 

Only the following {{site.data.keyword.Bluemix_notm}} users can invite users to an organization:
{: tsCauses}
  * The account owner of the organization
  * Organization managers who are also members, not collaborators, of the organization
  
In {{site.data.keyword.Bluemix_notm}}, you can be either a member or a collaborator of an organization:

<dl><dt>Collaborator</dt>
<dd>You are a collaborator of an organization if you already have a {{site.data.keyword.Bluemix_notm}} account, and someone else invites you to the organization.</dd>
<dt>Member</dt>
<dd>You are a member of an organization if you don't have a {{site.data.keyword.Bluemix_notm}} account, but then someone invites you to the organization and you sign up for {{site.data.keyword.Bluemix_notm}} from the invitation.</dd>
</dl>


You cannot invite users to your organization if you are a collaborator of the organization, even if you have been assigned as an organization manager.

**Note:** All organization managers, including those who are collaborators of an organization, can add, modify, and remove users that are already in the organization.

 

If you are unable to invite users to your organization and need a different role to do so, contact your organization manager to change your role. To identify your organization manager, complete the following steps:
{: tsResolve}

  1. Go to the {{site.data.keyword.Bluemix_notm}} Dashboard, click the **Account and Support** icon ![Account and Support](images/account_support.svg) in the top menu bar, and select **Manage Organizations**.
  2. Go to your organization, and view the information of organization manager on the **USERS** tab.  
  
If you are unable to invite users because you are a collaborator and not a member, you must delete your previous {{site.data.keyword.Bluemix_notm}} account and then be invited to join the account as a member of the organization. To delete your previous account and join the account as a member, complete the following steps: 

  1. Contact [{{site.data.keyword.Bluemix_notm}} Support](http://ibm.biz/bluemixsupport){: new_window} to open a support ticket and request that your account be deleted. If you have data that is associated with your old account that you want to save and move to the new account, include this information in your email. 
  2. After your account is deleted, have a user with the organization manager role invite you to the organization as an organization manager. Then, sign up for {{site.data.keyword.Bluemix_notm}} from the invitation. 




## Batch registration of users is not supported
{: #ts_batchregistration}

When you register users for {{site.data.keyword.Bluemix_notm}}, you must register each user individually.
 

{{site.data.keyword.Bluemix_notm}} does not provide the capability to register multiple users at the same time.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} doesn't support batch registration of users. To register users for {{site.data.keyword.Bluemix_notm}}, you must register each user individually.
{: tsCauses}
 

To register multiple users for {{site.data.keyword.Bluemix_notm}}, you must complete the following steps for each user:
{: tsResolve}

  1. Click **SIGN UP** in the upper-right corner of the {{site.data.keyword.Bluemix_notm}} user interface.
  2. Complete the steps by following the wizard.

    

## A {{site.data.keyword.Bluemix_notm}} page cannot be loaded
{: #ts_err}

When you use the {{site.data.keyword.Bluemix_notm}} user interface, you might not be able to load a {{site.data.keyword.Bluemix_notm}} page. Instead, you might see error messages BXNUI0001E or BXNUI0016E.
 

You might see one of the following error messages when you use the {{site.data.keyword.Bluemix_notm}} user interface:
{: tsSymptoms}

`BXNUI0001E: The page wasn't loaded because Bluemix didn't detect whether a session exists.`


`BXNUI0016E: The apps and services weren't retrieved because a Bluemix page didn't load.`

 

You can complete one or more of the following actions as necessary:
{: tsResolve}

  * Refresh or restart your browser.
  * Log out of {{site.data.keyword.Bluemix_notm}} and log in again.
  * Use the private browsing mode of your browser. 
  * Clear the cookies and the cache of the browser.
  * Use a different browser. For information about the versions of the browsers that are supported by {{site.data.keyword.Bluemix_notm}}, see [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * If you have installed the cf command line interface, enter the `cf apps` command to see whether your application is running.
  
  
  
  
  
## {{site.data.keyword.Bluemix_notm}} top menu bar disappears
{: #ts_topmenubar}

You might be unable to see the {{site.data.keyword.Bluemix_notm}} top menu bar when you resize your browser window, or when you use a mobile device.


When you decrease the size of your browser window, or when you use a mobile device, the {{site.data.keyword.Bluemix_notm}} top menu bar disappears. When the top menu bar disappears, the side drawer menu that displays as a stacked line icon appears in the upper left corner. 
{: tsSymptoms}

 

The {{site.data.keyword.Bluemix_notm}} user interface has a responsive design. When the viewing environment changes, the layout of the {{site.data.keyword.Bluemix_notm}} user interface might also change. 
{: tsCauses}
 

Use the side drawer menu in the upper left corner instead.
{: tsResolve}








# Troubleshooting for managing apps
{: #managingapps}

General problems with managing applications might include applications can't be updated, double-byte characters aren't displayed. However, in many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}





## Unable to switch apps into debug mode
{: #ts_debug}

You might not be able to enable the debug mode if the Java virtual machine (JVM) version is 8 or lower. 


After you select **Enable application debug**, the tools attempt to switch the application into the debug mode. Then, the Eclipse workbench begins a debug session. When the tools successfully enable debug mode, the web application status displays `Updating mode`, `Developing`, and `Debugging`. 
{: tsSymptoms}

However, when the tools fail to enable the debug mode, the web application status displays `Updating mode` and `Developing` only, and does not display `Debugging`. The tools might also display the following error message in the Console view:

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```
 

The following Java virtual machine (JVM) versions cannot establish a debug session: IBM JVM 7, IBM JVM 8, and previous versions of Oracle JVM 8.
{: tsCauses}

If your workbench JVM is one of these versions, then you might have issues when you create a debug session. Your workbench JVM version is typically the system JVM of your local computer. Your system JVM is not the same as the JVM of your running Bluemix Java application. The Bluemix Java application almost always runs on IBM JVM, and sometimes runs on OpenJDK JVM.
  

To check the version of Java that IBM Eclipse Tools for Bluemix runs, complete the following steps:
{: tsResolve}

  1. In IBM Eclipse Tools for Bluemix, select **Help** > **About Eclipse** > **Installation Details** > **Configuration**.
  2. Find the `eclipse.vm` property from the list. The following line is an example of an `eclipse.vm` property:
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. At the command line, enter `java -version` from the `bin` directory of your Java installation. Your IBM JVM version information is displayed.

If your workbench JVM is IBM JVM 7 or 8, or a previous version of Oracle JVM 8, complete the following steps to switch to Oracle JVM 8:

  1. Download and then install Oracle JVM 8, see [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} for details.
  2. Restart Eclipse.
  3. Check whether the `eclipse.vm` property points to your new installation of Oracle JVM 8.







## Unable to perform requested actions
{: #ts_authority}

You might not be able to complete actions without appropriate access authority.

 

When you try to perform actions for a service instance or an app instance, you can't complete the requested actions and see one of the following error messages: 
{: tsSymptoms}

`BXNUI0514E: You are not a developer for any of the spaces in the <orgName> organization.`


`Server error, status code: 403, error code: 10003, message: You are not authorized to perform the requested action.`

 

You do not have the appropriate level of authority that is required to perform the actions. 
{: tsCauses}

  

To obtain the appropriate authority level, use one of the following methods: 
{: tsResolve}
 * Select another organization and space for which you have the developer role. 
 * Ask the org manager to change your role to developer or to create a space and then assign you a developer role. See [Managing your organizations](../admin/orgs_spaces.html) for details.
 

 


## Unable to access {{site.data.keyword.Bluemix_notm}} services because of authorization errors
{: #ts_vcap}

Authorization errors might occur when your app accesses a {{site.data.keyword.Bluemix_notm}} service if the service credentials are hardcoded in your app. 

After you configure your app to communicate with a {{site.data.keyword.Bluemix_notm}} service, you deploy the app to {{site.data.keyword.Bluemix_notm}}. However, you can't use the app to access the {{site.data.keyword.Bluemix_notm}} service and receive an authorization error.
{: tsSymptoms}

The hardcoded credentials in the app might not be correct. Every time that the service is recreated, the credentials to access it change.
{: tsCauses}


Instead of hardcoding the credentials in your app, use connection parameters from the VCAP_SERVICES environment variable. The methods to use connection parameters from the VCAP_SERVICES environment variable vary depending on program languages. For example, for Node.js apps, you can use the following command: 
{: tsResolve}

```
process.env.VCAP_SERVICES
```
For more information about the commands that you can use in other program languages, see [Java](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} and [Ruby](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}. 
 

 
 




## Unable to deploy apps by using IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}
{: #ts_bm_tools_facet}

When an unsupported facet is applied to your Eclipse project, you might not be able to deploy your apps to {{site.data.keyword.Bluemix_notm}} by using the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}. 

 

You can successfully deploy your app to {{site.data.keyword.Bluemix_notm}} by using the Cloud Foundry CLI. However, you cannot deploy the app to {{site.data.keyword.Bluemix_notm}} by using the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, and you see the error message: `Project facet <facet_name> is not supported.` For example, `Project facet Cloud Foundry Standalone Application version 1.0 is not supported.`
{: tsSymptoms}

 

The IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} map projects to {{site.data.keyword.Bluemix_notm}} runtimes by project facets. Facets define the requirements for Java EE projects in Eclipse, and are used as part of the runtime configuration so that different runtimes are associated with different projects. If the facet that is applied to the project is not supported by the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, you might not be able to deploy your app by using the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}


You must remove the facet from the Eclipse project so that you can deploy your app by using the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsResolve} 

To remove the facet, in the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, click **Project > Properties > Project Facets** for the project. Then, clear the check box for the unsupported facet. 



## 502 Bad Gateway errors are received
{: #ts_502_error}

If you receive 502 Bad Gateway errors when you interact with apps on {{site.data.keyword.Bluemix_notm}}, check the {{site.data.keyword.Bluemix_notm}} status page, and then take actions accordingly.

 

You receive error messages that start with 502 Bad Gateway. For example, you might see `502 Bad Gateway: Registered endpoint failed to handle the request.`
{: tsSymptoms}

 

A Bad Gateway error usually happens when you visit a website that uses a proxy server to store and relay the data from the main server that hosts the site. The main server and the proxy server might not properly connect, therefore you see the HTTP status code 502 in your browser window. This status code indicates that the site's main server did not receive the HTTP implementation that it expected from the proxy server.
{: tsCauses}

Other less common causes of a Bad Gateway error are Internet service provider (ISP) dropouts, bad firewall configurations, and browser cache errors. 

 

If you suspect that a {{site.data.keyword.Bluemix_notm}} service is down, first check the [{{site.data.keyword.Bluemix_notm}} status](https://developer.ibm.com/bluemix/support/#status){: new_window} page. You might want to use the service in another {{site.data.keyword.Bluemix_notm}} region as a workaround. Detailed information is available in [Using services in another region](../services/reqnsi.html#cross_region_service){: new_window}. If the service status is normal, try the following steps to solve the problem: 
{: tsResolve}

  * Retry the action:
    * Reload the page by pressing F5 on your keyboard, or by clicking the refresh button. If this step does not work, clear your browser's cache and cookies, and then reload again.
	* Use a different browser.
	* Reboot your router, your modem, and your computer. Rebooting these devices can clear up various errors that lead to the error 502. 
  * Wait and try again later. In some instances, temporary problems might occur with your Internet service provider or the {{site.data.keyword.Bluemix_notm}} services. You can wait until the temporary problems are solved.
  * If the problem still exists, contact {{site.data.keyword.Bluemix_notm}} support. See [Contacting {{site.data.keyword.Bluemix_notm}} Support](../support/index.html#contacting-bluemix-support){: new_window} for more information. 




## Disk quota is exceeded
{: #ts_disk_quota}

If you run out of disk space, you can manually modify the disk quota to get more disk space.

  

When you run out of disk space, you might see a message that states that the disk quota is exceeded. To resolve the problem, you might have tried scaling up your app instance to get more disk space. For example, you might scale from 256 MB to 1256 MB by changing the memory quota on the app details page. However, because the disk quota remained the same, you did not get more disk space. 
{: tsSymptoms}


The default disk quota that is allocated for an app is 1 GB. If you need more disk space, you must manually specify the disk quota. 
{: tsCauses}

 
Use one of the following methods to specify your disk quota. The maximum disk quota that you can specify is 2 GB. If 2 GB is still not enough, try an external service such as [Object Store](../services/ObjectStorage/index.html){: new_window}.
{: tsResolve}

  * In the manifest.yml file, add the following item:
    ```
	disk_quota: <disk_quota>
	```
  * Use the **-k** option with the `cf push` command when you push your app to {{site.data.keyword.Bluemix_notm}}:
    ```
	cf push appname -p app_path -k <disk_quota>
	```

	
	
## Cannot add Git repository
{: #ts_cannot_addgit}

After you create an app on the Dashboard, you click ADD GIT to create a Git repository, but you cannot proceed.



When you click **ADD GIT**, a window opens and one of these issues occur:
{: tsSymptoms} 

  * The window hangs with a blank screen.
  * A message states that a problem exists with 3rd party cookies.



Your browser might be configured to prevent a cookie from being set. That cookie must be set from the IBM® Bluemix DevOps Services site in the hub.jazz.net internet domain from within the context of the {{site.data.keyword.Bluemix_notm}} console.
{: tsCauses}  

 

You can fix this problem in one of the following ways:
{: tsResolve}

  * Follow the instructions that are in the window that opens from the {{site.data.keyword.Bluemix_notm}} console. Click the button. Another browser window opens temporarily. In that window, DevOps Services sets the authentication cookie.
  * In another browser tab, go to https://hub.jazz.net and log in. Return to the {{site.data.keyword.Bluemix_notm}} console and refresh the page. Click **ADD GIT** again.
  * Change your browser settings to enable 3rd party cookies and click ADD GIT again. For details about configuring the settings, see the documentation for your browser:
    * [Mozilla Firefox](https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences#w_how-do-i-change-cookie-settings){: new_window}
	* [Google Chrome](https://support.google.com/chrome/answer/95647){: new_window}
	* [Apple Safari](https://support.apple.com/kb/PH17191){: new_window}
	* [Microsoft Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies#ie=ie-11){: new_window}
If those workarounds do not fix the problem, send an email to idslogin@jazz.net.



## Android apps can't receive push notifications
{: #ts_push}

Android apps in certain regions where Google is not accessible can't receive notifications that you send out through the IBM Push service. In this case, you can use third-party services as a workaround.

 

You bind a Push service for your Bluemix app and send a message to the registered devices. However, apps that are developed on the Android platform can't receive your notifications in certain regions. 
{: tsSymptoms}

 
IBM Push service uses the Google Cloud Messaging (GCM) service to dispatch notifications to mobile apps that are developed on the Android platform. To enable the Android apps to receive notifications, Google Cloud Messaging (GCM) service must be accessible by the mobile apps. In regions where the GCM service can't be reached by the Android apps, the Android apps are not able to receive push notifications.
{: tsCauses}

 
Use third-party services that do not rely on the GCM service as a workaround, for example, [Pushy](https://pushy.me){: new_window}, [igetui](http://www.getui.com/){: new_window}, and [jpush](https://www.jpush.cn/){: new_window}.
{: tsResolve}



## Organization's services limit is exceeded
{: #ts_servicelimit}

If you are a trial account user, you might be unable to create an application in {{site.data.keyword.Bluemix_notm}} if you have exceeded your organization's services limit.
 

When you try to create an application in {{site.data.keyword.Bluemix_notm}}, you see the following error message: 
{: tsSymptoms}

`BXNUI2032E: The <service_instances> resource wasn't created. While Cloud Foundry was being contacted to create the resource, an error occurred. Cloud Foundry message: "You have exceeded your organization's services limit."`



This error occurs when you have exceeded the limit on the number of service instances that you can have for your account. The maximum number of services instances for a trial account is 10.
{: tsCauses} 

 

Delete any services instances that are not needed, or remove the limit on the number of service instances that you can have.
{: tsResolve}
 
  * To delete a services instance, you can use the {{site.data.keyword.Bluemix_notm}} user interface or the command line interface.
    To use the {{site.data.keyword.Bluemix_notm}} user interface to delete a service instance, complete the following steps:
	  1. On the {{site.data.keyword.Bluemix_notm}} Dashboard, click **SERVICES** in the left pane. The services tiles display. 
	  2. On the service tile that you want to delete, click the **Menu** icon.
	  3. Click **Delete Service**. After you delete the service instance, you will be prompted to restage the application that the service instance was bound to. 
    To use the command line interface to delete a service instance, complete the following steps:
	  1. Unbind the service instance from an application by typing `cf unbind-service <appname> <service_instance_name>`.
	  2. Delete the service instance by typing `cf delete-service <service_instance_name>`.
	  3. After you delete the service instance, you might want to restage your application that the service instance was bound to by typing `cf restage <appname>`.
  * To remove the limit on the number of service instances that you can have, convert your trial account to a pay account. For information about how to convert your trial account to a pay account, see [How to change your plan](../pricing/index.html#changing){: new_window}.

  
  
## Executables can't be run on {{site.data.keyword.Bluemix_notm}}
{: #ts_executable}

You might be unable to run executables on {{site.data.keyword.Bluemix_notm}} when those executables were developed and built in a different environment. 

 

You are unable to run executables on {{site.data.keyword.Bluemix_notm}} when those executables were developed and built in a different environment.
{: tsSymptoms}

 

If the content that you want to push to {{site.data.keyword.Bluemix_notm}} is already an executable, the content was previously built and doesn't need to be built on {{site.data.keyword.Bluemix_notm}}. In this case, no buildpack is required for the executable to be run on {{site.data.keyword.Bluemix_notm}}. However, you must explicitly indicate to {{site.data.keyword.Bluemix_notm}} that no buildpack is required.
{: tsCauses}

 

When you push the executable to {{site.data.keyword.Bluemix_notm}}, you must specify a null-buildpack, which indicates that no buildpack is required. Specify a null-buildpack by using the **-b** option with the `cf push` command:
{: tsResolve}

```
cf push appname -p <app_path> -c <start_command> -b <null-buildpack>
```
For example:
```
cf push appname -p <app_path> -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## Organization's memory limit is exceeded
{: #ts_outofmemory}

If you are a trial account user, you might be unable to deploy an app to {{site.data.keyword.Bluemix_notm}} if you have exceeded the memory limit of your organization. You can either reduce the memory that your apps use or increase the memory quota of your account. 



When you deploy an app to {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms} 

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

 

This error occurs when the amount of memory that is remaining for your organization is less than the amount of memory that is required by the app that you want to deploy. The maximum memory quota for a trial account is 2 GB.
{: tsCauses}



You can either increase the memory quota of your account, or reduce the memory that your apps use.
{: tsResolve} 

  * To increase the memory quota of your account, convert your trial account to a pay account. For information about how to convert your trial account to a pay account, see [Pay accounts](../pricing/index.html#pay-accounts){: new_window}. 
  * To reduce the memory that your apps use, use either the {{site.data.keyword.Bluemix_notm}} user interface or the cf command line interface.
    If you use the {{site.data.keyword.Bluemix_notm}} user interface, complete the following steps:
	  1. On the {{site.data.keyword.Bluemix_notm}} Dashboard, select your application. The app details page opens.
	  2. In the runtime pane, you can reduce the maximum memory limit or the numbers of app instances, or both, for your app. 
	If you use the cf command line interface, complete the following steps:
	  1. Check how much memory is being used for your apps:
	  ```
	  cf apps
	  ```
	     The cf apps command lists all the apps that you deployed in your current space. The status of each app is also displayed.
      2. To reduce the amount of memory that is used by your app, reduce the number of app instances or the maximum memory limit, or both:
	  ```
	  cf push <appname> -p <app_path> -i <instance_number> -m <memory_limit>
      ```
	  3. Restart your app for the changes to take effect.



	  
## Apps are not automatically restarted
{: #ts_apps_not_auto_restarted}


An app is not automatically restarted when a service that you bind to the app stops working.	  
	  
 

When a service that you bind to an app crashes, problems such as outages, exceptions, and connection failures might occur on the app. {{site.data.keyword.Bluemix_notm}} does not automatically restart the app to recover from these problems.
{: tsSymptoms}



This behavior is by design of Cloud Foundry.
{: tsCauses} 

 

You can manually restart the app by typing the following command in the command line interface:
{: tsResolve}

```
cf push <appname> -p <app_path>
```
In addition, you can code the app to identify and recover from problems such as outages, exceptions, and connection failures. 

	  

## User-defined variables are lost when an application is pushed
{: #ts_varsnotretained}

When you push an app to {{site.data.keyword.Bluemix_notm}} from IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, the variables that you specified are reset unless you save the variables to the manifest file.



The variables that you specified are lost after you push an app to {{site.data.keyword.Bluemix_notm}} from IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms} 


The variables that you specified are saved only if you save them to the manifest file.
{: tsCauses} 

 

When you push an app to {{site.data.keyword.Bluemix_notm}} from IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, select the **Save to the manifest file** check box in the Application details page of the Application wizard. Then, the variables that you specified in the wizard are saved to the manifest file for your application. The next time you open the wizard, the variables are displayed automatically.
{: tsResolve}



## {{site.data.keyword.Bluemix_notm}} Live Sync icons are not shown
{: #ts_llz_lkb_3r}

You created an app in IBM Bluemix DevOps Services, but the IBM Bluemix Live Sync icons are not shown in the Web IDE.

 

When you edit a Node.js app in the DevOps Services Web IDE, the {{site.data.keyword.Bluemix_notm}} live edit, quick restart, and debug icons are not shown.
{: tsSymptoms}

 

The icons are not available in these circumstances:
{: tsCauses}

  * The `manifest.yml` file is not stored at the top level of your project.
  * Your app is stored in a subdirectory rather than the top level of your project, but the path to the subdirectory is not specified in the `manifest.yml` file.
  * The app does not contain a `package.json` file.


Use one of the following methods to solve the problem: 
{: tsResolve} 

  * If the `manifest.yml` file is not stored at the top level of your project, store it there.
  * If your app is stored in a subdirectory, specify the path to the subdirectory in the `manifest.yml` file.
  ```
   path: path_to_application
   ```
  * Create a `package.json` file that is in the same directory as your app.

  
  
  

  
  

  
  
## Organizations cannot be found on {{site.data.keyword.Bluemix_notm}}
{: #ts_orgs}

You might not be able to locate your organization on {{site.data.keyword.Bluemix_notm}} when working on a {{site.data.keyword.Bluemix_notm}} region.
  
 

You can log in to the {{site.data.keyword.Bluemix_notm}} user interface successfully, but you cannot push apps by using the cf command line interface or the Eclipse plug-in.
{: tsSymptoms}

When you try to push an application to {{site.data.keyword.Bluemix_notm}} by using the cf command line interface, you see one of the following error messages with the organization name specified in the message: 

`Error finding org`

`Organization not found`


When you try to push an application to {{site.data.keyword.Bluemix_notm}} by using the Cloud Foundry Eclipse Plugin, you see the following error message:

`cloudspace not found.`



This problem occurs because the API endpoint of the region that you want to work with is not specified, and the organization you're looking for might be in a different region.
{: tsCauses} 

   
  
If you are pushing your application to {{site.data.keyword.Bluemix_notm}} by using the cf command line interface, enter the cf api command and specify the API endpoint of the region. For example, enter the following command to connect to the {{site.data.keyword.Bluemix_notm}} Europe United Kingdom region:
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
If you are pushing your application to {{site.data.keyword.Bluemix_notm}} by using the Eclipse tools, you must first create a {{site.data.keyword.Bluemix_notm}} server and specify the API endpoint of the {{site.data.keyword.Bluemix_notm}} region that your organization was created in. For more information about using the Eclipse tools, see [Deploying apps with IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html){: new_window}.  
  
  


## An app route cannot be created
{: #ts_hostistaken}

When you deploy an app to {{site.data.keyword.Bluemix_notm}}, the route of the app can't be created if the host name that you specified is already being used.



When you deploy an app to {{site.data.keyword.Bluemix_notm}}, you see the following error message: 
{: tsSymptoms} 

`Creating route hostname.domainname ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken: hostname`



This problem occurs if the host name that you specified is already being used.
{: tsCauses} 


  
The host name that you specify must be unique within the domain that you are using. To specify a different host name, use one of the following methods:
{: tsResolve} 

  * If you deploy your application by using the `manifest.yml` file, specify the host name in the host option.	 
    ```
    host: <hostname>	
	```
  * If you deploy your application from the command prompt, use the `cf push` command with the **-n** option. 
    ```
    cf push <appname> -p <app_path> -n <hostname>
    ```


## A WAR app cannot be pushed by using the cf push command
{: #ts_cf_war}

You might not be able to use the cf push command to deploy an archived web app to {{site.data.keyword.Bluemix_notm}} if the app location is not specified correctly.
	


When you upload a WAR app to {{site.data.keyword.Bluemix_notm}} by using the `cf push` command, you see the error message, `Staging error: cannot get instances since staging failed.`
{: tsSymptoms} 

 

This problem might happen if the WAR file is not specified, or if the path to the WAR file is not specified. 
{: tsCauses}

 	
	
Use the **-p** option to specify a WAR file or add the path to the WAR file. For example:
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
For more information about the `cf push` command, enter `cf push -h`. 	





## Double-byte characters are not displayed properly when Liberty applications are pushed to {{site.data.keyword.Bluemix_notm}}
{: #ts_doublebytes}

Double-byte characters might not be displayed properly if Unicode support is not configured properly for the servlet or JSP files.

 

When a Liberty application is pushed to the {{site.data.keyword.Bluemix_notm}}, the double-byte characters that are specified within the app are not displayed properly.
{: tsSymptoms}

 

The problem might occur if Unicode support is not configured properly for the servlet or JSP files.
{: tsCauses}


You can use the following code within your servlet or JSP file:
{: tsResolve} 

  * In the servlet source file 
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * In the JSP 
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## Node.js apps can't be deployed
{: #ts_nodejs_deploy}

You might run into problems when you update a Node.js app or deploy a Node.js app to {{site.data.keyword.Bluemix_notm}}.



When you update a Node.js app or deploy your Node.js app to {{site.data.keyword.Bluemix_notm}}, you might see one of the following error messages:
{: tsSymptoms} 

`An app was not successfully detected by any available buildpack.`


`Instance (index 0) failed to start accepting connections.`


`Cannot get instances since staging failed.`


 

The following reasons are possible causes of the problem:
{: tsCauses}
 
  * The start command is not specified.
  * Files that are required to deploy a Node.js app are either missing from the app or placed in a folder other than the root directory.
  


	
Take the following actions based on the cause that leads to the problem:
{: tsResolve} 

  * Specify the start command by one of the following methods: 
      * Use the cf command line interface. For example: 
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * Use the [package.json](https://docs.npmjs.com/json){: new_window} file. For example:
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
	  * Use the `manifest.yml` file. For example: 
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Ensure that a `package.json` file exists in your Node.js app to enable the Node.js buildpack to recognize the app. In addition, you must put this file in the root directory of your app.	
    The following example shows a simple `package.json` file:  
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
For more tips about Node.js apps, see [Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}.	




## Configuration errors appear in the `server.xml` file after you import a {{site.data.keyword.Bluemix_notm}} Liberty app from Bluemix DevOps Services to Eclipse
{: #ts_eclipse}

If you see configuration errors in the `server.xml` file after you import a {{site.data.keyword.Bluemix_notm}} Liberty app from IBM Bluemix DevOps Services to Eclipse, you might need to remove the `server.xml` file from the project. 

 

After you import a {{site.data.keyword.Bluemix_notm}} Liberty app from {{site.data.keyword.Bluemix_notm}} DevOps Services into the Eclipse, you see configuration errors within the `server.xml` file from Eclipse Problems view. 
{: tsSymptoms}

 

Liberty buildpack uses the `server.xml` file to configure the app and generates a `runtime-vars.xml` file when the Liberty app is pushed to {{site.data.keyword.Bluemix_notm}}. When you import the app to Eclipse, the `runtime-vars.xml` file doesn't exist in your local environment.
{: tsCauses}

 

You can resolve this problem by removing the server.xml file from the project. The buildpack creates the `server.xml` file dynamically when you push the app as a WAR app. For more information, see [Liberty for Java](../runtimes/liberty/index.html){: new_window}.
{: tsResolve}
	
	
## An app cannot be staged by using a custom buildpack
{: #ts_bp_compilation}

You might not be able to deploy an app to {{site.data.keyword.Bluemix_notm}} by using a custom buildpack if the scripts within the buildpack are not executable.



When you deploy an app to {{site.data.keyword.Bluemix_notm}} by using a custom buildpack, you see the error message, `The application failed to stage, so there are no instances to display.`
{: tsSymptoms} 


This problem might happen if scripts, such as the detect script, the compile script, and the release script, are not executable.
{: tsCauses}

 

You can use the [git update](http://git-scm.com/docs/git-update-index){: new_window} command to change the permission of each script to executable. For example, you can type `git update --chmod=+x script.sh`.
{: tsResolve}
	
	
	
## An app can't be deployed from DevOps Services to {{site.data.keyword.Bluemix_notm}}
{: #ts_devops_to_bm}

You might not be able to push your app from IBM Bluemix DevOps Services to {{site.data.keyword.Bluemix_notm}} if the `manifest.yml` file is not present within your app.

 

When you deploy an app from DevOps Services to {{site.data.keyword.Bluemix_notm}}, an error message `Unable to detect a supported application type` might display.
{: tsSymptoms}

 

This problem might happen because DevOps Services requires a `manifest.yml` file to deploy an app to {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

 

To resolve this problem, you must create a `manifest.yml` file. For more information about how to create a `manifest.yml` file, see [Application manifest](../manageapps/depapps.html#appmanifest){: new_window}.
{: tsResolve}	
	




## Meteor apps can't be pushed
{: #ts_meteor}

You might not be able to push a Meteor application to {{site.data.keyword.Bluemix_notm}} if the buildpack is not specified correctly.

 

When you deploy a Meteor app to {{site.data.keyword.Bluemix_notm}}, you might see the error message, `The application failed to stage, so there are no instances to display.`
{: tsSymptoms}


This problem occurs because no built-in buildpack is provided for Meteor apps. You must use a custom buildpack.
{: tsCauses} 


 

To use a custom buildpack for Meteor apps, use one of the following methods:
{: tsResolve}

  * If you deploy your app by using the `manifest.yml` file, specify the URL or the name of your custom buildpack by using the buildpack option. For example:
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * If you deploy your application from the command prompt, use the `cf push` command and specify your custom buildpack by using the **-b** option. For example:
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor 
	```
	
  

    
## Deploy to {{site.data.keyword.Bluemix_notm}} button doesn't deploy an app
{: #deploytobluemixbuttondoesntdeployanapp}

If you click the Deploy to {{site.data.keyword.Bluemix_notm}} button and find that either the Git repository is not cloned or the app is not deployed, try the troubleshooting methods for the following issues.
  * [The Bluemix DevOps Services project cannot be created](#project-cannot-be-created)
  * [The Git repository is not found and cannot be cloned in DevOps Services](#repo-not-found)
  * [The Git repository is cloned in DevOps Services, but the app is not deployed to {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed)
For more information about how to create the button, see Creating a Deploy to {{site.data.keyword.Bluemix_notm}} button.

### The Bluemix DevOps Services project cannot be created
{: #project-cannot-be-created}

If you find that the DevOps Services project cannot be created, your IBM {{site.data.keyword.Bluemix_notm}} account might have expired.



You click the **Deploy to Bluemix** button, but the "Creating project" step does not complete successfully.
{: tsSymptoms} 


Your {{site.data.keyword.Bluemix_notm}} account might have expired.
{: tsCauses} 

Use one of the following methods to fix the problem:
{: tsResolve}

  * Log in to {{site.data.keyword.Bluemix_notm}} and update your account information.
  * Click the **Deploy to Bluemix** button again.


### The Git repository is not found and cannot be cloned in DevOps Services
{: #repo-not-found}

If you find that the Git repository is not cloned, an issue might exist with the repository or with the button snippet.



You click the **Deploy to Bluemix** button, but the Git repository is not found and cannot be cloned in DevOps Services. The "Cloning repository" step does not complete successfully. Therefore, the app cannot be deployed to {{site.data.keyword.Bluemix_notm}}. 
{: tsSymptoms} 

This problem might occur because of the following reasons:
{: tsCauses} 

  * The Git repository might not exist or be accessible.
  * An issue might exist in the HTML or markdown for the button snippet.
  * An issue might exist where special characters, query parameters, or fragments in the URL are preventing the Git repository from being accessed properly.

Use one of the following methods to fix the problem:
{: tsResolve}

  * Verify that your Git repository exists, is publicly accessible, and that the URL is correct.
  * Verify that the snippet does not contain any HTML or markdown errors.
  * If special characters, query parameters, or fragments cause an issue with the Git repository URL, encode the URL in the button snippet.
  

  
  
### The Git repository is cloned in DevOps Services, but the app is not deployed to {{site.data.keyword.Bluemix_notm}}
{: #repo-cloned-app-not-deployed}

If you find that the app is not deployed, issues might exist with the code in the repository.
     


You click the **Deploy to Bluemix** button and the Git repository is cloned in DevOps Services, but the app is not deployed to {{site.data.keyword.Bluemix_notm}}. The "Deploying to Bluemix" step does not complete successfully.
{: tsSymptoms} 

This problem might occur because of the following reasons:
{: tsCauses}  

  * There might not be enough space in your {{site.data.keyword.Bluemix_notm}} space to deploy an app. 
  * A required service might not be declared in the `manifest.yml` file.
  * A required service might be declared in the `manifest.yml` file, but the service is already in the target space.
  * An issue might exist with the code in the repository.
To diagnose the issue, review the build and deploy logs from the deployment:
  1. When the "Deploying to Bluemix" step does not complete successfully, click the link in the previous "Configuring pipeline" step to open the Delivery Pipeline.
  2. Identify the failed build or deploy stage.
  3. In the failed stage, click **View logs and history**.
  4. Locate the error message.
   
Use one of the following methods to fix the problem:
{: tsResolve}

  * If the error message indicates that there is not enough space in the {{site.data.keyword.Bluemix_notm}} space to deploy the app, target another space.
  * If the error message indicates that a required service is not declared in the `manifest.yml` file, notify the repository owner that the required service must be added.
  * If the error message indicates that a required service already exists in the target space, select a different space to use.
  * If the error message indicates that an issue exists with the build, fix any issues with the code that are preventing the app from being built. To verify that the code does not contain any issues, build the code by using Git commands:
    1. Clone the Git repository:
    ```
    git clone <git_repository_URL>
    ```
	2. Open the app directory:
	```
	cd <appname>
	```
	3. Create the app:
	```
	<appname> create
	```
	4. If necessary, provision add-ons.
	5. Add any configuration variables that are required.
	6. Push the code:
	```
	git push <appname> master
	```
	7. Verify that the app builds correctly.
	8. If necessary, run the post deployment command:
	```
	<appname> run
	```
	9. Open the app and verify that it is working correctly:
	```
	<appname> open
	```
	



# Troubleshooting for managing accounts
{: #managingaccounts}

You might experience problems when you manage your account, such as different apps share the same domain name, administrators can't view all organizations. However, in many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}


## Account is inactive
{: #ts_accnt_inactive}

You are unable to create an app in {{site.data.keyword.Bluemix_notm}} if your account is inactive. You must contact the support team to fix this problem.



When you try to create an app in {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms} 

`BXNUI0096E: The app wasn't created. Your account is inactive because it was canceled or suspended.`


The status of your {{site.data.keyword.Bluemix_notm}} account becomes inactive when the account is cancelled or suspended.
{: tsCauses}

 

To reactivate your account, contact [{{site.data.keyword.Bluemix_notm}} Support](http://ibm.biz/bluemixsupport.com){: new_window}. In the email, you must include the following information:
{: tsResolve}

  * The IBM ID that you use to log in to {{site.data.keyword.Bluemix_notm}}.
  * The name of the organization in which your app is being created. This information can help the support team determine whether you are assigned the correct roles or membership within your organization.



## No space is associated with the current organization
{: #ts_no_space}

You are unable to create an application if no space is associated with your current organization.



When you try to create an app in {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms} 


`BXNUI0097E: Before you can add an app, at least one space must be associated with your organization and region. On the Dashboard, click **Create a Space**. When the space is created, try again.`



Apps in {{site.data.keyword.Bluemix_notm}} must be created within a space under your organization.
{: tsCauses} 

 

To create a space, use one of the following methods: 
{: tsResolve}
 
  * On the {{site.data.keyword.Bluemix_notm}} Dashboard, select the organization in which you want to create the space, then click **Create a Space**.
  * In the cf command line interface, type ```cf create-space <space_name> -o <organization_name>```.
  
  
  
  
## The domain names for different applications are the same
{: #ts_domain_diff}

You might notice that several applications share the same URL in {{site.data.keyword.Bluemix_notm}}.

 

This problem might happen when you assign the same URL route for different applications within a space.
{: tsCauses}

For example, you push the myApp1 application to {{site.data.keyword.Bluemix_notm}} and set the domain to "mynewapp.mybluemix.net". Then, you push another myApp2 application to the same space and set one of its URL routes to "mynewapp.mybluemix.net". The route is now mapped to both applications.

 

This is supported behavior of the {{site.data.keyword.Bluemix_notm}} and you can use this practice to achieve zero downtime for your application upgrade. For more information, see Blue-green deployments.
{: tsResolve}
  
	
	





## Credit card can't be added
{: #ts_addcc}

You cannot submit your credit card information to convert your trial account to a Pay As You Go account.

 

The Submit button on the Add credit card page is disabled.
{: tsSymptoms}

 

This problem happens when your information is not filled in correctly in the Add credit card page.
{: tsCauses}

 

Complete the following steps to solve this problem:
{: tsResolve}

  1. On the Add credit card page, fill in all of the required fields that are in the contact information, contact address, and billing address sections.
  2. Select **I have read and agree to IBM's Terms and Conditions**, then click **Submit**. The **Select a payment method** section is displayed.
  3. Enter your credit card number, the expiration date of your card, and the security code that is on your card. Then, click **Submit**.





# Troubleshooting for runtimes
{: #runtimes}

You might experience problems when you use IBM® Bluemix™ runtimes. However, in many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}


## Obsolete buildpack is loaded from cache when an app is pushed
{: #ts_loading_bp}


You might not be able to use the latest buildpack components when you push an app. You can use buildpacks that have built-in mechanisms to prevent loading obsolete components, or you can delete the contents in your app's cache directory before you push or restage the app. 

 

When you push or restage an app after the buildpack is updated, the latest buildpack components are not loaded automatically. As a result, your app uses the obsolete buildpack components. Updates that have been applied to the buildpack since the last time you pushed the app are not implemented. 
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
	
	


