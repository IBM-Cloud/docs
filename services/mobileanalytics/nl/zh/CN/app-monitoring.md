---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使用 {{site.data.keyword.mobileanalytics_short}} 监视应用程序
{: #monitoringapps}

{{site.data.keyword.mobileanalytics_full}} 可监视和分析移动应用程序。您可以使用 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK 来记录应用程序日志并监视数据。开发者可以控制何时将这些数据发送到 {{site.data.keyword.mobileanalytics_short}} 服务。数据传递到 {{site.data.keyword.mobileanalytics_short}} 后，可以使用 {{site.data.keyword.mobileanalytics_short}} 控制台，来获取有关移动应用程序、设备和应用程序日志的分析洞察。
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

## 设置警报
{: #alerts}

您可以在 {{site.data.keyword.mobileanalytics_short}} 控制台中的警报定义内设置阈值，以更好地监视活动。

您可以配置阈值，当超过阈值时，触发器便会触发警报以向 {{site.data.keyword.mobileanalytics_short}} 控制台监视器通知此情况。已触发的警报可以显示在控制台中，也可以由定制 webhook 进行处理。<!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.--> 此功能能够主动检测应用程序日志错误和应用程序崩溃服务器日志错误。响应式阈值和警报使您不必筛查数据，或者设置大范围的阈值。

### 为应用程序日志创建警报定义
{: #alert-def-client-logs notoc}

您可以基于应用程序日志创建警报定义。

在此示例中，您将使用应用程序日志数据来创建警报定义。该警报会监控在过去 5 分钟内收到的所有应用程序日志，并且每 5 分钟继续检查一次，直到该警报定义被禁用或删除。如果设备发送了 3 个或更多个具有相同应用程序名称和版本的应用程序错误日志，那么将会触发警报。

1. 在 {{site.data.keyword.mobileanalytics_short}} 控制台中，单击**定义**以转至“警报定义”页面。
2. 单击**创建警报**以创建警报。
3. 提供以下值：
	* 警报名称：应用程序日志的警报
	* 消息：错误消息警报
	* 查询频率：5 分钟
	* 事件类型：应用程序日志
		* 属性：日志级别
			* 值：错误
			* 阈值
				* 阈值类型：应用程序实例的总计

					**注**：如果您选择“应用程序的平均值”选项，那么会按设备数来计算应用程序日志平均值。例如，如果您有两个设备，其中一个设备发送六个应用程序日志，而另一个设备发送三个应用程序日志，那么平均值为 4.5 个应用程序日志。
				* 运算符：大于或等于 3
	
	<!-- insert alert definition tab image? -->

4. 单击**下一步**，然后提供以下值：
	* 方法：仅限分析控制台

		**注**：如果您想要额外发送具有 JSON 有效内容的 POST 消息到您定制的 URL，请选择“分析控制台和网络 Post”选项。如果选择此选项，那么以下字段可用：
		* 网络 Post URL
        * 标头
        * 认证类型
5. 单击**保存**。

您已创建警报定义，在应用程序日志数达到您的阈值，即 3 个或更多错误日志时，每 5 分钟触发一次警报。

### 为应用程序崩溃创建警报定义
{: #alert-def-app-crash notoc}

您可以基于应用程序崩溃来创建警报定义。

在此示例中，您将使用应用程序崩溃数据来创建警报定义。该警报会监控在过去 2 分钟内出现的所有应用程序崩溃，并且每 2 分钟继续检查一次，直到该警报定义被禁用或删除。对于出现 5 次或以上崩溃事件的应用程序，将触发警报。
有关应用程序崩溃的更多信息，请参阅[应用程序崩溃](#app_crash)。

1. 在 {{site.data.keyword.mobileanalytics_short}} 控制台中，单击**定义**以显示“警报定义”页面。
2. 单击**创建警报**。 
3. 提供以下值：
	* 警报名称：应用程序崩溃的警报
	* 消息：应用程序崩溃警报
	* 查询频率：应用程序崩溃
		* 查询频率：2 分钟
	* 事件类型：应用程序崩溃
		* 应用程序名称：任何应用程序
		* 应用程序版本：任何版本
    * 阈值
      * 阈值类型：崩溃计数
      * 运算符：大于或等于 5
4. 单击**分发方法**选项卡并提供以下值：
  * 方法：仅限分析控制台

    **注**：如果您想要额外发送具有 JSON 有效内容的 POST 消息到您定制的 URL，请选择**分析控制台和网络 Post** 选项。如果选择此选项，那么以下字段可用：
      * 网络 Post URL（必需）
      * 标头（可选）
      * 认证类型（必需）
5. 单击**保存**。

### 管理警报定义
{: #managing-alert-definitions notoc}

在此示例中，您将通过“警报管理”页面来管理警报定义。

1. 在 {{site.data.keyword.mobileanalytics_short}} 控制台中，单击**日志**。此操作会打开“警报日志”页面。
2. 可选：切换**启用**列下的复选框，以启用或禁用特定警报定义。
3. 可选：如果您想要创建警报定义的副本并更改一些值，请单击**复制**图标。
4. 可选：如果您想要编辑警报定义，请单击**画笔**图标。
5. 可选：如果您想要删除警报定义，请单击**废纸篓**图标。

### 查看警报详细信息
{: #viewing-alert-details notoc}

在此示例中，您将在“警报日志”页面中查看已触发警报的详细信息。

1. 在 {{site.data.keyword.mobileanalytics_short}} 控制台中，单击**日志**。此操作会打开“警报日志”页面。
2. 单击任意警报的 **+** 图标。该操作会显示**警报定义**和**警报实例**部分。

    **注**：如果未删除或修改相应的警报定义，那么您可以通过单击**编辑警报**，来编辑警报定义。否则，无法使用**编辑警报**按钮，且会显示下列消息：

    `此警报定义已修改或删除。`

3. 可选：选择警报并单击**废纸篓**图标，以删除警报。

## 监视应用程序崩溃
{: #monitor-app-crash}

您可以在 {{site.data.keyword.mobileanalytics_short}} 控制台中查看应用程序崩溃的相关信息，以更好地监视应用程序和进行故障诊断。

### 应用程序崩溃监视
{: #app-crash notoc}

在**崩溃**页面上，**崩溃概述**表显示以下数据列：

* 应用程序：应用程序名称
* 崩溃：应用程序的总崩溃次数
* 使用总数：用户打开和关闭该应用程序的总次数
* 崩溃率：崩溃次数占使用次数的百分比

您可以快速查看应用程序使**崩溃**表崩溃的相关信息。<!--In the **Overview** page of the **Dashboard** section,-->**崩溃**条形图显示崩溃次数随时间变化的直方图。

您可以使用两种方式来显示崩溃数据：

1. 显示崩溃率：随时间变化的崩溃率
2. 显示总崩溃次数：随时间变化的总崩溃次数

### 应用程序崩溃故障诊断
{: #app-crash-troubleshooting notoc}

{{site.data.keyword.mobileanalytics_short}} 控制台中的**故障诊断**页面<!-- **Applications** section of the -->使用**崩溃摘要**表提供应用程序崩溃的详细视图。

**崩溃摘要**表可进行排序，且包含下列数据列：

* 崩溃
* 设备
* 上次崩溃
* 应用程序
* 操作系统
* 消息

单击任意条目旁的 + 图标，以显示包含以下各列的**崩溃详细信息**表：

* 崩溃时间
* 应用程序版本
* 操作系统版本
* 设备模型
* 设备标识
* 下载：用于下载一直到发生此崩溃时的日志的链接

展开**崩溃详细信息**表中的任何条目，以获取包含堆栈跟踪在内的更多详细信息。

**注**：通过查询致命级别应用程序日志，可以填充**崩溃摘要**表的数据。如果您的应用程序未收集致命应用程序日志，那么没有可用的数据。

## 监视网络请求
{: #monitor-network-requests}


在 {{site.data.keyword.mobileanalytics_short}} 控制台中查看应用程序的网络请求数据。 

数据可用于以下度量：
	
* 往返时间 - 定义应用程序发出网络请求花费的时间长度，以毫秒为单位。
* 请求计数 - 显示应用程序发出网络请求的频率。数据还作为平均值显示。

## 将数据导出到 dashDB
{: #dashdb}

{{site.data.keyword.mobileanalytics_short}} 控制台中显示的度量仅为样本洞察，您可从移动数据进行收集。您可以将移动数据自动传递到 {{site.data.keyword.IBM}} dashDB 数据仓库，在其中定制分析、将您的数据与其他公共和专用数据源聚集以及应用前沿分析来获取深入、详细且复杂的洞察，以帮助您了解和推动业务发展。

在 {{site.data.keyword.mobileanalytics_short}} 控制台中，通过单击**导出**页面上的 **DashDB**，对 dashDB 进行设置。完成设置之后，发送到 {{site.data.keyword.mobileanalytics_short}} 的新数据也会在 1-2 小时内转发给 dashDB。 

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

