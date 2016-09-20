---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 關於 {{site.data.keyword.twittershort}}
{: #about_twitter}

*前次更新：2016 年 5 月 13 日*
{: .last-updated}

使用 {{site.data.keyword.twitterfull}}，將 Twitter 內容從 Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} 或 [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} 串流納入您的 {{site.data.keyword.Bluemix}} 應用程式中。
{:shortdesc}

會即時重新整理 Content Store 並對其編製索引，讓搜尋更為動態及快速。服務會根據來自 [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window} 的深入自然語言處理演算法，以使用多種語言的觀感及其他見解來強化推文。完整支援即時處理 Twitter 資料串流，並且可透過豐富的一組查詢參數及關鍵字進行配置。{{site.data.keyword.twittershort}} 包括可讓您自訂搜尋的	RESTful API，並傳回 JSON 格式的推文及強化。傳回遵循 Twitter 資料的 [Gnip Activity Stream](http://support.gnip.com/sources/twitter/data_format.html){: new_window} 格式的推文。

{{site.data.keyword.twittershort}} 服務會即時分析 Twitter Decahose 及 PowerTrack 串流，以提供每篇推文作者的下列強化：
* 性別
* 永久位置（依國家/地區、州/省及城市所定義）

下列強化也適用於推文內容：

* 觀感（正面、負面、矛盾或中性的英文、德文、法文及西班牙文推文）
* 推文中所含的正面/負面觀感詞組（適用於英文、德文、法文及西班牙文推文）

為了驗證 {{site.data.keyword.twittershort}} 搜尋結果，此服務會提供 REST API 方法，以確認是否仍可在 Twitter 上存取特定推文。 

## 意見及支援 
{: #feedback_support}

{{site.data.keyword.twitterfull}} 小組想要收到您的意見。

如果您使用此服務時遇到任何問題，請造訪
IBM [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} 討論區。搜尋先前所提交問題的回答，或提問。
請包含 **insights-twitter** 及 **bluemix** 標籤以加強回應時間。

如果您的問題未在 developerWorks Answers 中提出，請在
[Stack Overflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} 上張貼問題，並將您的問題標記 **twitter** 及 **bluemix**。

您也可以檢視 [Bluemix 平台](https://developer.ibm.com/bluemix/support/#status){: new.window}的狀態或[開啟支援問題單](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}。如需相關資訊，請參閱[疑難排解](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}。
