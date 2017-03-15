---

copyright:
  years: 2017
lastupdated: "2017-02-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 開始使用 {{site.data.keyword.mqa}}（已淘汰）
{: #gettingstartedtemplate}

**{{site.data.keyword.mqafull}} 服務已淘汰。**如需狀態及日期的相關資訊，請參閱 [Retirement of Bluemix Mobile Quality Assurance 部落格文章 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}。
{:deprecated}

{{site.data.keyword.mqafull}} 讓團隊能夠擷取測試和實際使用者經驗，以持續建置與交付高品質的行動應用程式。
{: shortdesc}

若要快速開始使用 {{site.data.keyword.mqa}} 服務，請遵循下列步驟：

1. 建立 {{site.data.keyword.mqa}} 服務的實例之後，您可以在「{{site.data.keyword.Bluemix}} 儀表板」的**服務**區段中按一下您的磚，以存取「{{site.data.keyword.mqa}} 主控台」。

	{{site.data.keyword.mqa}} 服務會啟動。

2. 選取 **Add MQA App** 並提供應用程式的名稱，將行動應用程式新增至 {{site.data.keyword.mqa}} 實例。

3. 下載 {{site.data.keyword.mqa}} [Client SDK ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window}，並繼續下列其中一個程序以完成應用程式檢測：

	* [使用 Android 應用程式檢測 MQA](mqa_inst_app_android.html)
	* [使用 iOS 應用程式檢測 MQA](mqa_inst_app_ios.html)
	* [使用 Cordova 應用程式檢測 MQA](mqa_inst_app_cord.html)

	單一 SDK 用來檢測正式作業前及正式作業應用程式。您可以使用 `MODE:` 參數來指定 *QA*（代表正式作業前模式），或指定 *MARKET*（代表正式作業模式）。指定正式作業前模式，以便內部測試者能提供您應用程式所發生錯誤和當機的詳細資訊。指定正式作業模式，以便使用者能提供您的應用程式的相關詳細資訊。如果您的應用程式在正式作業中，{{site.data.keyword.mqa}} 有利於在應用程式內取得使用者的意見。

4. 檢測應用程式之後，您可以在 {{site.data.keyword.mqa}} 服務實例的介面上，選取下列其中一個選項，檢視它的詳細品質資訊：

	<dl>
		<dt><strong>Sessions</strong></dt>
		<dd>檢閱裝置在階段作業期間的當機、錯誤、意見和狀態等相關資訊。如需相關資訊，請參閱 IBM Knowledge Center 中的 [Viewing session details ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window}。</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>Crashes</strong></dt>
		<dd>檢閱當機起因的相關資訊。如需相關資訊，請參閱 IBM Knowledge Center 中的 [Crash reports ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window}。</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>Bugs</strong></dt>
		<dd>檢閱使用者報告的資訊，例如錯誤報告、畫面擷取及裝置詳細資料。如需相關資訊，請參閱 IBM Knowledge Center 中的 [Bug reports details ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window}。</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>Feedback</strong></dt>
		<dd>檢閱使用者意見回應，以查看誰撰寫了意見，以及撰寫的時間。如需相關資訊，請參閱 IBM Knowledge Center 中的 [User feedback ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window}。</dd>
		<dt><strong>Sentiment Score（如果已配置）</strong></dt>
		<dd>檢閱針對時間和版本的使用者觀感評分，以監視、測量和改善應用程式品質。如需相關資訊，請參閱 IBM Knowledge Center 中的 [User sentiment ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window}。</dd>
		<dt><strong>Registered Devices</strong></dt>
		<dd>檢閱在測試階段作業期間使用的裝置清單，以及這些裝置的相關資訊。如需相關資訊，請參閱 IBM Knowledge Center 中的 [Viewing device information ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window}。</dd>
	</dl>

	這些度量值包括下列資料：

	* 當機、錯誤、意見及階段作業的正式作業前資料。
	* 當機、意見、觀感及階段作業的正式作業資料。

	![介面的畫面擷取，您可以在這裡檢視應用程式的度量值。](images/quality_metrics_saas4.gif)

	藉由檢視應用程式的此資訊，您可以決定是否進一步調查特定的問題。例如，如果應用程式的當機比率驟升，您可以按一下當機比率以檢視該應用程式當機報告的更多詳細資訊。

5. 若要檢視應用程式的整體觀感評分，您必須配置觀感分析：

	1. 在 *Sentiment Score* 區段中，按一下鏈結以配置所選取應用程式的觀感分析。

	2. 在「應用程式詳細資料」頁面上，[配置觀感分析 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window} 並儲存您的變更。


# 相關鏈結
{: #rellinks notoc}

## 指導教學及範例
{: #samples notoc}

* [視訊：Getting Started with Mobile Quality Assurance in Bluemix ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [視訊：Sentiment Analysis in Mobile Quality Assurance ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks：Add IBM Mobile Quality Assurance to your mobile quality regimen ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks：Build mobile apps that work: Five tips from an expert panel ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks：Build a mobile app that isn't perfect ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks：DevOps for mobile apps challenges and best practices ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [Sample: bluelist-mqa ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
