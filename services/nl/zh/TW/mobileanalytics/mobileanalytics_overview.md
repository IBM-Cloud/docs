---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# 關於 {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
*前次更新：2016 年 4 月 21 日*
{: .last-updated}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} 服務提供行動應用程式開發人員及應用程式擁有者的重要應用程式用法及效能見解。使用 {{site.data.keyword.mobileanalytics_short}}，應用程式擁有者及開發人員可以瞭解「使用者端」發生的情況，而且他們可以使用這項見解來建置與使用者最相關且行動應用程式真實領域內最顯著的較佳應用程式。 

{: #overview}  
此服務包括的「{{site.data.keyword.mobileanalytics_short}} 主控台」，可讓開發人員及應用程式擁有者監視行動應用程式效能、查看用法統計資料，以及搜尋裝置日誌。{{site.data.keyword.mobileanalytics_short}} 提供適用於 iOS 8+（僅限 Swift）及 Android 4+ 的 Client SDK。

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

使用 {{site.data.keyword.mobileanalytics_short}} 服務，您可以：
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>立即瞭解</dt>
		<dd>即時查看效能及用法度量值。</dd>
	<dt>快速實作</dt>
		<dd>在 {{site.data.keyword.Bluemix}} 中建立服務實例、將 SDK 新增至專案、將兩行程式碼貼入應用程式，而且您已備妥可收集許多預先定義的度量值。</dd>
	<dt>收集您要的任何資料</dt>
		<dd>使用自訂事件來檢測應用程式、探索使用者如何與應用程式互動、追蹤採購，以及監視應用程式活動。  
</dd>
<dt>概略查看所有應用程式的度量值</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} 主控台提供現成及自訂圖表，而不需撰寫查詢。</dd>
<dt>聚焦於對您重要的事物</dt>
	<dd>依時間、配接器、應用程式、應用程式版本、OS、OS 版本或裝置模型來過濾度量值。</dd>
<dt>快速探索問題</dt>
	<dd>監視損毀狀態。設定重要度量值的警示觸發程式，並將警示遞送至任何 REST 端點。</dd>
<dt>疑難排解到主要原因</dt>
	<dd>在應用程式中使用自訂用戶端記載，並自動上傳日誌，以及從主控台中搜尋它們。往下探查到損毀事件，以查看堆疊追蹤。</dd>
</dl>
 

## 使用度量值及事件
{: #usingmetrics}

使用**預先定義的度量值**，您可以回答下列這類問題：

*我有多少位新使用者？*  
*有多少人正在活躍地使用我的應用程式？*  
*他人使用我的應用程式的頻率為何？*  
*他人在什麼時間使用我的應用程式？*  
*我的使用者喜歡哪些裝置模型？*  
*我應該何時淘汰支援舊式作業系統？*  
*哪些應用程式發生效能問題？*  

自行新增**自訂事件**，您可以回答下列這類問題：  

*最常使用及最少使用的特性為何？*  
*使用者在哪裡進入及離開我的應用程式？*  
*使用者最常檢視的活動為何？*  
*使用者是否在應用程式中完成工作流程？（例如，轉換通道）*  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

>
# 相關鏈結 {:class="linklist"}
<!-->## 指導教學及範例 {:id="samples"}-->
<!-->* [Link1](https://github.com/)-->
>
># 相關鏈結 {:class="linklist"}
>## 相關鏈結 {:id="general"}
## SDK
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core )  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  
>
>{:elementKind="article" id="rellinks"}
