---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# App details
{: #manageapps}

The Apps dashboard in the {{site.data.keyword.Bluemix}} console provides summary information for the applications that you created. The summary information includes the name, icon, URL, runtime, running status, and service instances that are bound to the app. 
{:shortdesc}

From the Apps dashboard, you can view the status of each application.

**Stopped or Unknown (gray)**

  Your app is stopped or the status is unknown. The gray icon indicates that the app is stopped or the status is unknown.

**Running (green)**

  Your app is running. The green icon indicates that the app is started and all instances are running.

*Number* **running (yellow)**

  The app is started, but not all instances are running. The yellow icon indicates that fewer than 100% of the instances are running. The number of instances that are running and the number of instances that failed are displayed.

**Not running (red)**

  Your app is not running. The red icon indicates that the app is started, but no instance is running.

To view more information about an app, click the name to open the app's Overview page.

When an app is deployed, you can start, stop, restart, or (in the case of web applications) modify the number of instances and the amount of memory that is used by the app. At this time, for web applications, {{site.data.keyword.Bluemix_notm}} does not automatically scale your appbased on its load, so you must manage this aspect yourself.

Applications can be redeployed if an update is made. The mechanism for updating the app is the same mechanism that is used to deploy it originally. {{site.data.keyword.Bluemix_notm}} stops all running instances and replaces them with new instances automatically.
