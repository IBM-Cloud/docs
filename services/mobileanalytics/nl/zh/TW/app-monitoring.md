---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使用 {{site.data.keyword.mobileanalytics_short}} 監視應用程式
{: #monitoringapps}

{{site.data.keyword.mobileanalytics_full}} 提供行動應用程式的監視及分析。您可以記錄應用程式日誌，以及使用 {{site.data.keyword.mobileanalytics_short}} Client SDK 來監視資料。開發人員可以控制何時將這項資料傳送至 {{site.data.keyword.mobileanalytics_short}} 服務。將資料遞送給 {{site.data.keyword.mobileanalytics_short}} 時，您可以使用 {{site.data.keyword.mobileanalytics_short}} 主控台來深入分析行動應用程式、裝置及應用程式日誌。
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for app logs
{: #custom-charts-client-logs}

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
{: #export-custom-data}

You can export the data from each custom chart into JSON, XML, or CSV format.

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

-->

## 設定警示
{: #alerts}

您可以在 {{site.data.keyword.mobileanalytics_short}} 主控台中設定警示定義的臨界值，以更適當地監視您的活動。

您可以配置臨界值，以在超出時，觸發警示來通知 {{site.data.keyword.mobileanalytics_short}} 主控台監視器。觸發的警示可以在主控台上進行視覺化，或者自訂 Webhook 可以處理警示。<!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.-->此特性提供主動的方法來偵測應用程式日誌錯誤和應用程式損毀的伺服器日誌錯誤。反應臨界值及警示讓您不需要篩選資料，並且用更廣的精度來設定臨界值。

### 建立應用程式日誌的警示定義
{: #alert-def-client-logs}

您可以根據應用程式日誌來建立警示定義。

在此範例中，您使用應用程式日誌資料來建立警示定義。此警示會監視過去 5 分鐘接收到的所有應用程式日誌，而且除非停用或刪除警示定義，否則會持續每 5 分鐘檢查一次。針對已對相同應用程式名稱及版本傳送 3 個以上應用程式錯誤日誌的每一個裝置，觸發警示。

1. 在 {{site.data.keyword.mobileanalytics_short}} 主控台中，按一下**定義**，以移至「警示定義」頁面。
2. 按一下**建立警示**，以建立警示。
3. 提供下列值：
	* 警示名稱：應用程式日誌的警示
	* 訊息：錯誤訊息警示
	* 查詢頻率：5 分鐘
	* 事件類型：應用程式日誌
		* 內容：記載層次
			* 值：錯誤
			* 臨界值
				* 臨界值類型：應用程式實例總計

					**附註**：如果您選擇「應用程式平均值」選項，則應用程式日誌會除以裝置數目來取得平均值。例如，如果您有兩個裝置，而且其中一個裝置傳送六個應用程式日誌，而另一個裝置傳送三個應用程式日誌，則平均值是 4.5 個應用程式日誌。
				* 運算子：大於或等於 3
	<!-- insert alert definition tab image? -->

4. 按**下一步**，然後提供下列值：
	* 方法：僅限 Analytics 主控台

		**附註**：如果您要將具有 JSON 有效負載的 POST 訊息額外傳送至自訂的 URL，請選擇 Analytics 主控台及 Network Post 選項。如果您選擇這個選項，則可以使用下列欄位：
		* Network Post URL
        * 標頭
        * 鑑別類型
5. 按一下**儲存**。

您已建立警示定義，以在應用程式日誌數目達到 3 個以上錯誤日誌的臨界值時，於每 5 分鐘間隔結束時觸發警示。

### 建立應用程式損毀的警示定義
{: #alert-def-app-crash}

您可以根據應用程式損毀來建立警示定義。

在此範例中，您使用應用程式損毀資料來建立警示定義。此警示會監視過去 2 分鐘的所有應用程式損毀，而且除非停用或刪除警示定義，否則會持續每 2 分鐘檢查一次。針對每一個損毀 5 次以上的應用程式，觸發警示。如需應用程式損毀的相關資訊，請參閱[應用程式損毀](#app_crash)。

1. 在 {{site.data.keyword.mobileanalytics_short}} 主控台中，按一下**定義**，以顯示「警示定義」頁面。
2. 按一下**建立警示**。
3. 提供下列值：
	* 警示名稱：應用程式損毀的警示
	* 訊息：應用程式損毀警示
	* 查詢頻率：應用程式損毀
		* 查詢頻率：2 分鐘
	* 事件類型：應用程式損毀
		* 應用程式名稱：任何應用程式
		* 應用程式版本：任何版本
    * 臨界值
      * 臨界值類型：損毀計數
      * 運算子：大於或等於 5
4. 按一下**分佈方法**標籤，然後提供下列值：
  * 方法：僅限 Analytics 主控台

    **附註**：如果您要將具有 JSON 有效負載的 POST 訊息額外傳送至自訂的 URL，請選擇 **Analytics 主控台及 Network Post** 選項。如果您選擇這個選項，則可以使用下列欄位：
      * Network Post URL（必要）
      * 標頭（選用）
      * 鑑別類型（必要）
5. 按一下**儲存**。

### 管理警示定義
{: #managing-alert-definitions}

在此範例中，您從「警示管理」頁面中管理警示定義。

1. 在 {{site.data.keyword.mobileanalytics_short}} 主控台中，按一下**日誌**。此動作會開啟「警示日誌」頁面。
2. 選用項目：切換**已啟用**直欄下方的勾選框，以啟用或停用特定警示定義。
3. 選用項目：如果您要建立警示定義的副本，並變更某些值，請按一下**複製**圖示。
4. 選用項目：如果您要編輯警示定義，請按一下**鉛筆**圖示。
5. 選用項目：如果您要刪除警示定義，請按一下**垃圾桶**圖示。

### 檢視警示詳細資料
{: #viewing-alert-details}

在此範例中，您從「警示日誌」頁面中檢視已觸發警示的詳細資料。

1. 在 {{site.data.keyword.mobileanalytics_short}} 主控台中，按一下**日誌**。此動作會啟動「警示日誌」頁面。
2. 按一下任何警示的 **+** 圖示。此動作會顯示**警示定義**及**警示實例**區段。

    **附註**：如果未刪除或修改對應的警示定義，您可以按一下**編輯警示**來編輯警示定義。否則，**編輯警示**按鈕無法使用，並且會顯示下列訊息：

    `已修改或刪除此警示定義。`

3. 選用項目：選取警示，然後按一下**垃圾桶**圖示來刪除警示。

## 監視應用程式損毀
{: #monitor-app-crash}

您可以在 {{site.data.keyword.mobileanalytics_short}} 主控台中檢視應用程式損毀的相關資訊，以更適當地監視應用程式並進行疑難排解。

### 應用程式損毀監視
{: #app-crash}

在**毀損**頁面上，**損毀概觀**表格會顯示下列資料直欄：

* 應用程式：應用程式名稱
* 損毀：該應用程式的損毀總數
* 使用總計：使用者開啟及關閉該應用程式的總次數
* 損毀比率：每次使用的損毀百分比

您可以在**損毀**表格中快速查看應用程式損毀的相關資訊。<!--In the **Overview** page of the **Dashboard** section,--> **損毀**長條圖會顯示一段時間內損毀的直方圖。

您可以使用兩種方式來顯示損毀資料：

1. 顯示損毀比率：一段時間的損毀比率
2. 顯示損毀總計：一段時間的損毀總計

### 應用程式損毀疑難排解
{: #app-crash-troubleshooting}

{{site.data.keyword.mobileanalytics_short}} 主控台中的**疑難排解**頁面會使用**損毀摘要**表格提供應用程式損毀的細微視圖。

**損毀摘要**表格可進行排序，而且包括下列資料直欄：

* 損毀
* 裝置
* 前次損毀
* 應用程式
* OS
* 訊息

按一下任何項目旁的 + 圖示來顯示**損毀詳細資料**表格，其中包括下列直欄：

* 損毀時間
* 應用程式版本
* OS 版本
* 裝置模型
* 裝置 ID
* 下載：下載已導致損毀的日誌的鏈結

展開**損毀詳細資料**表格中的任何項目來取得更多詳細資料（包括堆疊追蹤）。

**附註**：**損毀摘要**表格的資料是透過查詢嚴重層次應用程式日誌來移入。如果您的應用程式未收集嚴重應用程式日誌，則沒有可用的資料。

## 監視網路要求
{: #monitor-network-requests}


在 {{site.data.keyword.mobileanalytics_short}} 主控台中，針對您的應用程式檢視網路要求資料。 

資料可供下列測量使用：
	
* 往返時間 - 定義應用程式提出網路要求所需的時間長度（以毫秒為測量單位）。
* 要求計數 - 顯示應用程式提出網路要求的頻率。資料也顯示為平均值。

## 將資料匯出到 dashDB
{: #dashdb}

您在 {{site.data.keyword.mobileanalytics_short}} 主控台中看到的度量值只是您能從行動資料蒐集到的見解範例。您可以自動將行動資料以管道傳到 {{site.data.keyword.IBM}} dashDB 資料倉儲，您可以在這裡自訂分析、彙總資料與其他公用和專用資料來源，以及套用頂尖分析來衍生深入、詳細且準確的見解，協助您瞭解和推動業務。

在 {{site.data.keyword.mobileanalytics_short}} 主控台設定 dashDB，方法是按一下**匯出**頁面上的 **DashDB**。完成設定之後，傳送到 {{site.data.keyword.mobileanalytics_short}} 的新資料也會在 1-2 小時內轉遞給 dashDB。 

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

