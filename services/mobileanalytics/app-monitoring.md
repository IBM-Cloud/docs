---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Monitoring applications with {{site.data.keyword.mobileanalytics_short}}
{: #monitoringapps}

The {{site.data.keyword.mobileanalytics_full}} provides monitoring and analytics for your mobile applications. You can record application logs and monitor data with the {{site.data.keyword.mobileanalytics_short}} Client SDK. Developers can control when to send this data to the {{site.data.keyword.mobileanalytics_short}} Service. When data is delivered to {{site.data.keyword.mobileanalytics_short}}, you can use the {{site.data.keyword.mobileanalytics_short}} console to get analytics insights about your mobile applications, devices, and application logs.
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts notoc}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for app logs
{: #custom-charts-client-logs notoc}

You can create a custom chart for app logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use app log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

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
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart that is based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart and provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: App Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your application name
7. Click **Save**

### Exporting custom data
{: #export-custom-data notoc}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom notoc}

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

-->

## Setting alerts
{: #alerts}

You can set thresholds in alert definitions in the {{site.data.keyword.mobileanalytics_short}} console to better monitor your activities.

You can configure thresholds, which if exceeded, trigger alerts to notify the {{site.data.keyword.mobileanalytics_short}} console monitor. The triggered alerts can be visualized on the console, or the alerts can be handled by a custom webhook. <!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.--> This feature provides a proactive means of detecting application log errors and application crashes server log errors. Reactive thresholds and alerts keep you from having to sift through your data and set thresholds at a wide spectrum of granularity.

### Creating an alert definition for application logs
{: #alert-def-client-logs notoc}

You can create an alert definition that is based on application logs.

In this example, you use application log data to create an alert definition. The alert monitors all application logs that were received in the last 5 minutes, and continues to check every 5 minutes, until the alert definition is disabled or deleted. An alert is triggered for each device that sent 3 or more application error logs with the same application name and version.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click **Definitions** to go to the Alert Definitions page.
2. Click **Create Alert** to create an alert.
3. Provide the following values:
	* Alert Name: Alert for app logs
	* Message: Error Message Alert
	* Query Frequency: 5 minutes
	* Event Type: App Logs
		* Property: Log Level
			* Value: Error
			* Threshold
				* Threshold Type: Total for Application Instance

					**Note**: If you choose the Average for Application option, the app logs are averaged by the number of devices. For example, if you have two devices, and one device sends six app logs while the other device sends three app logs, the average is 4.5 app logs.
				* Operator: is greater than or equals 3
	<!-- insert alert definition tab image? -->

4. Click **Next** and provide the following value:
	* Method: Analytics Console Only

		**Note**: Choose the Analytics Console and Network Post option if you want to additionally send a POST message with a JSON payload to your customized URL. The following fields are available if you choose this option:
		* Network Post URL
        * Headers
        * Authentication Type
5. Click **Save**.

You created an alert definition to trigger an alert at the end of each 5 minute interval if the number of app logs reached your threshold of 3 or more error logs.

### Creating an alert definition for application crashes
{: #alert-def-app-crash notoc}

You can create an alert definition based on application crashes.

In this example, you use application crash data to create an alert definition. The alert monitors all application crashes in the last 2 minutes, and continues to check every 2 minutes, until the alert definition is disabled or deleted. An alert is triggered for each application that crashed 5 or more times. For more information about application crashes, see [Application crashes](#app_crash).

1. In the {{site.data.keyword.mobileanalytics_short}} console, click **Definitions** to display the Alerts Definitions page.
2. Click **Create Alert**.
3. Provide the following values:
	* Alert Name: Alert for Application Crashes
	* Message: App Crash Alert
	* Query Frequency: Application Crashes
		* Query Frequency: 2 minutes
	* Event Type: Application Crashes
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

### Managing alert definitions
{: #managing-alert-definitions notoc}

In this example, you manage your alert definitions from the Alert Management page.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click **Logs**. This action opens the Alert Logs page.
2. Optional: Toggle the check-box under the **Enabled** column to enable or disable a specific alert definition.
3. Optional: Click the **Duplicate** icon if you want to create a copy of an alert definition and change some values.
4. Optional: Click the **Pencil** icon if you want to edit an alert definition.
5. Optional: Click the **Trash** icon if you want to delete an alert definition.

### Viewing alert details
{: #viewing-alert-details notoc}

In this example, you view the details of your triggered alerts from the Alert Log page.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click **Logs**. This action brings up the Alert Log page.
2. Click the **+** icon for any of the alerts. This action displays the **Alert Definition** and **Alert Instances** sections.

    **Note**: If the corresponding alert definition was not deleted or modified, you can edit the alert definition by clicking **Edit Alert**. Otherwise, the **Edit Alert** button is unavailable and the following message displays:

    `This alert definition has since been modified or deleted.`

3. Optional: Select an alert and click the **Trash** icon to delete the alert.

## Monitoring application crashes
{: #monitor-app-crash}

You can view information about your application crashes in the {{site.data.keyword.mobileanalytics_short}} console to better monitor and troubleshoot your applications.

### Application crash monitoring
{: #app-crash notoc}

On the **Crashes** page, The **Crash Overview** table shows the following data columns:

* Application: application name
* Crashes: total number of crashes for that app
* Total Uses: total number of times a user opens and closes that app
* Crash Rate: percentage of crashes per use

You can quickly see information about your application crashes the **Crashes** table. <!--In the **Overview** page of the **Dashboard** section,--> The **Crashes** bar graph shows a histogram of crashes over time.

You can display crash data in two ways:

1. Display crash rate: crash rate over time
2. Display total crashes: total crashes over time

### App crash troubleshooting
{: #app-crash-troubleshooting notoc}

The **Troubleshooting** page in the <!-- **Applications** section of the --> {{site.data.keyword.mobileanalytics_short}} console offers a granular view of your app crashes, using the **Crash Summary** table.

The **Crash Summary** table is sortable and includes the following data columns:

* Crashes
* Devices
* Last Crash
* Application
* OS
* Message

Click the + icon next to any entry to display the **Crash Details** table, which includes the following columns:

* Time Crashed
* Application Version
* OS Version
* Device Model
* Device ID
* Download: link to download the logs that led up to the crash

Expand any entry in the **Crash Details** table to get more details, including a stacktrace.

**Note**: The data for the **Crash Summary** table is populated by querying the fatal level app logs. If your application does not collect fatal application logs, no data is available.

## Monitoring network requests
{: #monitor-network-requests}


View network request data for your applications in the {{site.data.keyword.mobileanalytics_short}} console. 

Data is available for the following measurements:
	
* Round Trip Time - defines the length of time, measured in ms, that it takes for your app to make network requests.
* Request Count - displays how often an app makes network requests. Data also displays as an average.

## Exporting data to dashDB
{: #dashdb}

The metrics you see in the {{site.data.keyword.mobileanalytics_short}} console are just a sample of the insights that you can glean from your mobile data. You can automatically pipe your mobile data to the {{site.data.keyword.IBM}} dashDB data warehouse, where you can customize your analyses, aggregate your data with other public and private data sources, and apply leading-edge analytics to derive deep, detailed, and sophisticated insights to help you understand and drive your business.

Set up dashDB in the {{site.data.keyword.mobileanalytics_short}} console by clicking **DashDB** on the **Export** page. After you complete the setup, new data that is sent to {{site.data.keyword.mobileanalytics_short}} is also forwarded to dashDB within 1-2 hours. 

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

