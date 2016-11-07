---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# 關於 {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
前次更新：2016 年 8 月 29 日
{: .last-updated}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} 服務提供行動應用程式開發人員及應用程式擁有者的重要應用程式用法及效能見解。使用 {{site.data.keyword.mobileanalytics_short}}，應用程式擁有者及開發人員可以瞭解使用者端發生的情況，而且他們可以使用這項見解來建置與使用者最相關且行動應用程式真實領域內最顯著的較佳應用程式。 

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
		<dd>在 {{site.data.keyword.Bluemix}} 中建立服務實例、將 SDK 新增至專案、將兩行程式碼貼入應用程式，您就可以收集許多預先定義的度量值。</dd>
	<!--<dt>Collect any data you want</dt>-->
		<!--<dd>Instrument apps with custom events, discover how users are interacting with your app, track purchases, and monitor app activity.  
</dd>-->
<dt>概略查看所有應用程式的度量值</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} 主控台提供<!-- both -->現成<!--and custom-->圖表，而不需撰寫查詢。</dd>
<dt>聚焦於對您重要的事物</dt>
	<dd>依時間、配接器、應用程式、應用程式版本、OS、OS 版本或裝置模型來過濾度量值。</dd>
<dt>快速探索問題</dt>
	<dd>監視損毀狀態。設定重要度量值的警示觸發程式，並將警示遞送至任何 REST 端點。</dd>
<dt>疑難排解到主要原因</dt>
	<dd>在應用程式中使用自訂記載，並自動上傳日誌，以及從主控台中搜尋它們。往下探查到損毀事件，以查看堆疊追蹤。</dd>
</dl>
 

## 使用度量值及事件
{: #usingmetrics}

使用**預先定義的度量值**，您可以回答下列這類問題：

* 我有多少位新使用者？  
* 有多少人正在活躍地使用我的應用程式？  
* 他人使用我的應用程式的頻率為何？ 
* 他人在什麼時間使用我的應用程式？  
* 我的使用者喜歡哪些裝置模型？ 
* 我應該何時淘汰支援舊式作業系統？ 
* 哪些應用程式發生效能問題？  

<!--By adding your own **custom events** you can answer questions like:--> 

<!--* What features are used most and least?-->  
<!--* Where are users entering and leaving my app?-->  
<!--* What activities are users viewing most? --> 
<!--* Are users completing workflows in the app (for example, conversion funnels)? -->  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

## {{site.data.keyword.mobileanalytics_short}} 常見問題 
{: #faq}

<dl>
	<dt>何謂 {{site.data.keyword.mobileanalytics_full}}？</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} 是一種服務，可提供行動應用程式的效能及使用情形的即時及和歷程見解。利用 {{site.data.keyword.mobileanalytics_short}}，應用程式開發人員和應用程式擁有者可以透過監視作用中使用者、階段作業、行動平台及應用程式損毀的趨勢，進行以資料驅動的決策。您也可以對所選取的度量值設定警示，一旦觸發該警示，就會將訊息傳送至所有 REST 端點，包括推送服務或內部傳訊服務。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} 測試版有何用途？</dt>
		<dd>身為「行動應用程式產品管理員」，您可以查看有多少人使用您的應用程式（使用者度量值），以及他們在何時使用該應用程式（階段作業度量值）。此資訊將以時間序列呈現並即時更新，可讓您查看對應用程式所進行變更的效果。您可以過濾來查看特定的應用程式版本或作業系統，以進行淘汰和優先順序決策。</dd>
		<dd>身為「行動應用程式行銷人員」，您可以利用使用者及階段作業度量值，透過觀察某段時間內的變化並將您的事件日期產生關聯，來監視忠誠度、管理客戶流失，以及評估行動應用程式行銷結果的有效性。</dd>
		<dd>身為「行動應用程式開發人員」，您可以使用損毀度量值，在行動應用程式效能問題讓使用者感到挫敗並危及應用程式信譽之前，加以探索及解決。您可以從分析主控台同時監視損毀計數及損毀比率，也可以對影響大部分使用者的損毀設定優先順序。您可以設定警示，以在損毀次數超出給定的臨界值時傳送通知或自動化動作，也可以往下探查至損毀實例，以查看裝置日誌及應用程式堆疊追蹤資料來進行疑難排解。</dd>
	<dt>我需要有資料分析師技能，才能使用 Mobile Analytics 嗎？</dt>
		<dd>不需要，{{site.data.keyword.mobileanalytics_short}} 提供一個現成可用的分析主控台，供商業利害關係人及應用程式開發人員使用。不需要任何查詢技能。</dd>
	<dt>我可以對分析資料執行自訂查詢嗎？</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} 測試版不容許自訂查詢，但未來已考量納入此特性。</dd>
	<dt>如何將我的應用程式連接至 {{site.data.keyword.mobileanalytics_short}}？</dt>
		<dd>請[下載 iOS 或 Android 的開放程式碼 SDK](install-client-sdk.html)，或使用其他平台的 {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.stage1.ng.bluemix.net/analytics-service/)。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} 可在哪些 Bluemix 地區中使用？</dt>
		<dd>在撰寫本資訊時，Mobile Analytics 可在美國南部及英國使用。已計劃在其他地區提供，但時間範圍尚未決定。</dd>
	<dt>此服務需要多少成本？</dt>
		<dd>服務的測試版可免費使用。</dd>
	<dt>我的分析資料可保存多久？</dt>
		<dd>若為測試版，資料會保留至少 30 天。</dd>
	<dt>需要多長時間才能將資料顯示在 {{site.data.keyword.mobileanalytics_short}} 主控台中？</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} 主控台中的資料幾乎是即時，表示資料會在實際事件發生後的數秒內顯示。</dd>
	<dt>{{site.data.keyword.mobileanalytics_full}} 與 MobileFirst Platform Foundation 中的行動分析有何不同？</dt>
		<dd>這兩個主控台中的使用者及階段作業非常類似，但 MobileFirst Platform Foundation 隨附的分析包含其他度量值及設定，可容許用戶端管理自己的內部部署分析叢集。此外，MobileFirst Platform Foundation 分析主控台還會產生配接器及配接器程序的度量值，但在 {{site.data.keyword.mobileanalytics_short}} 服務中，我們正在規劃將這些度量值整合到 {{site.data.keyword.mobileanalytics_short}} 服務（後置測試版）中的網路要求圖表及表格。</dd>
	<dt>我正在使用內部部署的 MobileFirst Platform Foundation 來開發我的應用程式，但我不想要管理專屬的分析叢集。我可以改用 {{site.data.keyword.mobileanalytics_full}} 嗎？</dt>
		<dd>可以。您在此處有數個選項：如果您使用 MobileFirst Platform Foundation 7.x 或 8.0，而且您的應用程式是使用 MobileFirst Platform SDK 進行監控，則可以配置 MobileFirst 伺服器，以將分析資料報告給 {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}。如需詳細資料，請閱讀[配置 Mobile Analytics 及 Mobile Foundation Bluemix 服務](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/)部落格文章。另外，您也可以使用 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} SDK 來監控應用程式，並直接報告結 {{site.data.keyword.mobileanalytics_short}} 服務。</dd>
	<dt>我正在嘗試使用 {{site.data.keyword.mobileanalytics_short}}，但卻在應該顯示字元的位置看到空格。發生了什麼事？</dt>
		<dd>很可能是因為您使用了 {{site.data.keyword.Bluemix_notm}} 的「傳統」視圖介面。「傳統」視圖已淘汰，所以 {{site.data.keyword.mobileanalytics_short}} 測試版是在新的 {{site.data.keyword.Bluemix_notm}} 介面中執行。如果您是在「傳統」視圖中，則會在 {{site.data.keyword.Bluemix_notm}} 標頭中看到一個鏈結，指出「請嘗試新的 {{site.data.keyword.Bluemix_notm}}！」. 按一下該鏈結，即可使用新的介面。</dd>
</dl>


# 相關鏈結
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  

<!-- {:elementKind="article" id="rellinks"} -->
