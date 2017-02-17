---

copyright:
  years: 2015, 2017
lastupdated: "2015-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Managing applications
{: #manageapps}

You can use the Dashboard in the {{site.data.keyword.Bluemix}} user interface to view and manage your applications and services, and to monitor resource usage by using the quota gauges.
{:shortdesc}

The application section on the Dashboard provides summary information for the applications that you created. The summary information includes the name, icon, URL, runtime, and running status of the application, and service instances that are bound to the application. Different colors are used to indicate the running status of each application.

**Stopped or Unknown (gray)**

  Your app is stopped or the status is unknown. The gray icon indicates that the application is stopped, or the status is unknown.

**Running (green)**

  Your app is running. The green icon indicates that the application is started and all instances are running.

*Number* **running (yellow)**

  The app is started, but not all instances are running. The yellow icon indicates that fewer than 100% of the instances are running. The number of instances that are running and the number of instances that failed are displayed.

**Not running (red)**

  Your app is not running. The red icon indicates that the application is started, but no instance is running.

In the {{site.data.keyword.Bluemix_notm}} Catalog, you can view the available services and starters. You can select a starter to create an application, bind a service, and manage the application. After a service is bound to an application, you can manage existing service instances that are bound to the current application and create service instances for the application. You can also unbind or delete the service instance from an application, or you can choose a different service plan.

To view more information about an application, click the tile to open the app Overview page.

**Note:** You can view resources of only one organization at a time. If you are a member of multiple organizations, you can switch organizations by clicking the **CHANGE ORGANIZATION** icon next to the current organization that is displayed in the header of the dashboard.

When an application is deployed, you can start, stop, restart, or (in the case of web applications) modify the number of instances and the amount of memory that is used by the application. At this time, for web applications, {{site.data.keyword.Bluemix_notm}} does not automatically scale your application based on its load, so you must manage this aspect yourself.

Applications can be redeployed if an update is made. The mechanism for updating the application is the same mechanism that is used to deploy it originally. {{site.data.keyword.Bluemix_notm}} stops all running instances and replaces them with new instances automatically.
