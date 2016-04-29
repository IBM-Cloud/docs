---

copyright:
  years: 2015, 2016

---
# Monitoring apps with {{site.data.keyword.mobileanalytics_short}}
{: #monitoringapps}
*Last updated: 25 April 2016*

The {{site.data.keyword.mobileanalytics_full}} provides monitoring and analytics for your mobile applications. You can record client logs and monitor data with the {{site.data.keyword.mobileanalytics_short}} Client SDK. Developers can control when to send this data to the {{site.data.keyword.mobileanalytics_short}} Service. When data is delivered to {{site.data.keyword.mobileanalytics_short}}, you can use the {{site.data.keyword.mobileanalytics_short}} dashboard to get analytics insights about your mobile applications, devices, and client logs.
{: shortdesc}

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report..
{: #shortdesc}

Learn more about monitoring and troubleshooting your app crashes.

### Creating custom charts for client logs
{: #custom-charts-client-logs}

You can create a custom chart for client logs that contain log information that is sent with the platform's Logger API. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use client log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

* Specific data
  * Log level
* Message data
  * Timestamp
* Device OS contextual data
  * Application name
  * Application version
  * Device OS
* Device contextual data
  * Device ID
  * Device model
  * Device OS version


1. Make sure that you have an application that is collecting device logs or gathering analytics.
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart.
4. Provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: Client Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab.
6. Provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your app name
7. Click **Save**

### Exporting custom data
{: #export-custom-data}

The data from each custom chart can be exported into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom}

You can import and export custom chart definitions programmatically or manually in the {{site.data.keyword.mobileanalytics_short}} Dashboard.

Ensure that you have at least one custom chart in the {{site.data.keyword.mobileanalytics_short}} Dashboard.
In this example, you manually export and import custom chart definitions.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab in the **Dashboard** page.
2. To export the custom chart definitions, click **Export Charts**. This action displays a dialog to save a `customChartsDefinition.json` file.
3. Choose a location to save the file.
4. Click the **Delete Chart** icon next to each custom chart to delete all custom charts.
5. To import a custom chart definition, click **Import Charts**. This action displays a dialog to choose a file.
6. Choose the `customChartsDefinition.json` file that you previously exported to open.

You can also export and import custom chart definitions programmatically by using your HTTP client of choice (for example, CURL or postman):
* The GET endpoint for export is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* The POST endpoint for import is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Note**: If you import a custom chart definition that exists, you end up with duplicate definitions, which also means that the {{site.data.keyword.mobileanalytics_short}} Dashboard shows duplicate custom charts.

## Setting alerts
{: #alerts}

You can set thresholds in alert definitions in the MobileFirst Analytics Console to better monitor your activities.
{: #shortdesc}

You can configure thresholds, which if exceeded, trigger alerts to notify the MobileFirst Analytics Console monitor. The triggered alerts can be visualized on the console, or the alerts can be handled by a custom webhook. This feature provides a proactive means of detecting client log errors, server log errors, extended periods of network latency, and authentication failures. Reactive thresholds and alerts keep you from having to sift through your data and set thresholds at a wide spectrum of granularity.

### Creating an alert definition for client logs
{: #alert-def-client-logs}

You can create an alert definition that is based on client logs.

In this example, you use client log data to create an alert definition. The alert monitors all client logs that were received in the last 5 minutes, and continues to check every 5 minutes, until the alert definition is disabled or deleted. An alert is triggered for each device that sent 3 or more client error logs with the same app name and version.

1. In the MobileFirst Analytics Console, click the bell icon to go to the **Alert Log** page.
2. Go to the **Alert Management** page and click Create **Alert**.
3. Provide the following values:
	* Alert Name: Alert for client logs
	* Message: Error Message Alert
	* Query Frequency: 5 minutes
	* Event Type: Client Logs
		* Property: Log Level
			* Value: Error
			* Threshold
				* Threshold Type: Total for Application Instance

					Note: If you choose the Average for Application option, the client logs are averaged by the number of devices. For example, if you have two devices, 					and one device sends six client logs while the other device sends three client logs, the average is 4.5 client logs.
				* Operator: is greater than or equals 3
	<!-- insert alert definition tab image? -->

4. Click **Next** or the **Distribution Method** tab, and provide the following value:
	* Method: Analytics Console Only

		Note: Choose the Analytics Console and Network Post option if you want to additionally send a POST message with a JSON payload to your customized URL. The following fields are available if you choose this option:
		* Network Post URL
        * Headers
        * Authentication Type
5. Click **Save**.

You created an alert definition to trigger an alert at the end of each 5 minute interval if the number of client logs reached your threshold of 3 or more error logs.

### Creating an alert definition for app crashes
{: #alert-def-app-crash}

You can create an alert definition based on app crashes.

In this example, you use app crash data to create an alert definition. The alert monitors all app crashes in the last 2 minutes, and continues to check every 2 minutes, until the alert definition is disabled or deleted. An alert is triggered for each app that crashed 5 or more times. For more information about app crashes, see [App crashes](app_crash/c_op_analytics_crashes.html).

1. In the MobileFirst Analytics Console, click the **Alerts** icon. This action brings up the Alert Log page.
2. Click the **Alert Management** tab and click **Create Alert**.
3. Provide the following values:
	* Alert Name: Alert for App Crashes
	* Message: App Crash Alert
	* Query Frequency: Application Crashes
		* Application Name: Any application
		* Application Version: Any version
    * Threshold
      * Threshold Type: Crash Count
      * Operator: is greater than or equals 5
4. Click the **Distribution Method** tab, and provide the following value:
  * Method: Analytics Console Only

    **Note**: Choose the **Analytics Console and Network Post** option if you want to additionally send a POST message with a JSON payload to your customized URL. The following fields are available if you choose this option:
      * Network Post URL (required)
      * Headers (optional)
      * Authentication Type (required)
5. Click **Save**.

### Managing Alert definitions
{: #managing-alert-definitions}

In this example, you manage your alert definitions from the Alert Management page.

1. In the MobileFirst Analytics Console, click the **Alerts** icon. This action opens the Alert Log page.
2. Click the **Alerts Management** tab.
3. Optional: Toggle the check-box under the **Enabled** column to enable or disable a specific alert definition.
4. Optional: Click the **Duplicate** icon if you want to create a copy of an alert definition and change some values.
5. Optional: Click the **Pencil** icon if you want to edit an alert definition.
6. Optional: Click the **Trash** icon if you want to delete an alert definition.

### Viewing alert details
{: #viewing-alert-details}

In this example, you view the details of your triggered alerts from the Alert Log page.

1. In the MobileFirst Analytics Console, click the **Alerts** icon. This action brings up the Alert Log page.
2. Click the **+** icon for any of the alerts. This action displays the **Alert Definition** and **Alert Instances** sections.

    **Note**: If the corresponding alert definition was not deleted or modified, you can edit the alert definition by clicking **Edit Alert**. Otherwise, the **Edit Alert** button is unavailable and the following message displays:

    `This alert definition has since been modified or deleted.`

3. Optional: Select an alert and click the **Trash** icon to delete the alert.

## App crashes
{: #monitor-app-crash}

You can view information about your app crashes in the MobileFirst Analytics Console to better monitor and troubleshoot your apps.
{: #shortdesc}

Learn more about monitoring and troubleshooting your app crashes.

### App crash monitoring
{: #app-crash}

You can quickly see information about your app crashes in the **Dashboard** section of the IBM MobileFirst™ Analytics Console.

In the **Overview** page of the **Dashboard** section, the **Crashes** bar graph shows a histogram of crashes over time.

You can display data in two ways:

1. Display crash rate: crash rate over time
2. Display total crashes: total crashes over time


### App crash troubleshooting
{: #app-crash-troubleshooting}

You can view the **Crashes** page in the **Applications** section of the IBM MobileFirst Analytics Console to better administer your apps.

The **Crash Overview** table shows the following data columns:

* App: app name
* Crashes: total number of crashes for that app
* Total Uses: total number of times a user opens and closes that app
* Crash Rate: percentage of crashes per use

The **Crash Summary** table is sortable and includes the following data columns:

* Crashes
* Devices
* Last Crash
* App
* OS
* Message

You can click on the + icon next to any entry to display the **Crash Details** table, which includes the following columns:

* Time Crashed
* App Version
* OS Version
* Device Model
* Device ID
* Download: link to download the logs that led up to the crash

You can expand any entry in the **Crash Details** table to get more details, including a stacktrace.

**Note**: The data for the **Crash Summary** table is populated by querying the fatal level client logs. If your app does not collect fatal client logs, no data is available.


# rellinks

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}

