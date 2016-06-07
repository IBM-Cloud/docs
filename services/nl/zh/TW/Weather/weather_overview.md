---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 關於 Insights for Weather
{: #about_weather}

*前次更新：2016 年 5 月 19 日*

使用 {{site.data.keyword.weatherfull}}，可以將來自 The Weather Company (TWC) 的天氣資料納入 {{site.data.keyword.Bluemix}} 應用程式中。
{:shortdesc}

您可以使用 [Insights for Weather REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，將天氣觀測資料和預測新增至 {{site.data.keyword.Bluemix_notm}} 應用程式，以及顯示地理定位所指定區域的天氣資料。The Weather Company 提供最詳盡的歷史及預測天氣資料。將會擷取所有天氣型態（包括降雨、氣壓、風及雷雨）的資料。

您可以使用 REST API 來擷取下列資訊：

* 所指定地理定位從目前時間開始的未來 24 小時的每小時天氣預測。
* 所指定地理定位未來 10 天的每日天氣預測，其中包含白天及夜晚區段的預測。這項預測包括最多 256 個字元的預測敘述性字串，內含適用於所在位置的度量單位並使用所要求的語言。
* 所指定地理定位目前觀測到的天氣資料。這項天氣資料包含溫度、降雨、風向及風速、濕度、氣壓、露點、能見度及紫外線 (UV)。
* 所指定地理定位及所指定時間範圍觀測到的天氣資料。這項資料是來自實際觀測站。這個 API 會傳回目前狀況的天氣觀測資料，以及最多前 24 小時（含）的過去觀測資料。

如需 The Weather Company 的天氣詞彙和圖示的相關資訊，請參閱 [Icon Code, Phrases and Images](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}。
您也可以[下載一組圖示](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}以便用於您的應用程式。

## 定價模型
{: #pricing_models}

定價模型是根據 Insights for Weather API 的每日呼叫，而這些 API 會每月向用戶端收取費用。只要限制呼叫數目，就可以針對任何地理定位區域、預測類型或時間序列觀測資料，在應用程式中測試天氣資料。「免費」、「基本」和「高階」方案在購買時不需要合約。這些方案容許您的應用程式每天進行分別
500、5,000 或 50,000 次 API 呼叫。

也可以針對在計費期間部署的每個服務實例購買多個「高階」方案。如果應用程式所使用的呼叫數目每天超過 50,000 個呼叫或每分鐘超過 1,000 個呼叫，則必須與 IBM 簽訂合約以持續佈建這些服務。

當您的應用程式到達根據所選方案允許進行的 API 呼叫限制時，下一個進行的 API 呼叫將不會成功，直到您的應用程式能夠要求更多
API 呼叫為止。

例如，如果您使用「基本」方案，則您的應用程式可以在一分鐘內進行 500 個 API 呼叫，即使是這超過了方案的限制也允許，不過必須等到
5 分鐘之後才會再允許下個 API 呼叫。因此，使用者可能會發現在您的應用程式中，天氣資料的重新整理會有延遲現象。
您必須確定開發應用程式時已處理這些限制，而不會要求激增的 API 呼叫。相反地，您可以監視應用程式的 API 呼叫使用情形。您可以藉由檢查
API 呼叫傳回的項目數，來驗證應用程式是否到達方案的限制。

## 意見與支援
{: #feedback_support}

如果您具有使用 Insights for Weather 建立應用程式的技術問題，請在 [Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window} 上張貼問題，並以 **bluemix** 和 **weather** 來標記您的問題。

如果遇到此服務的任何問題，請使用 [IBM developerWorks Answers 討論區](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}。
請包含 **insights-weather** 及 **bluemix** 標籤，以讓 IBM 為您提供更完善的支援。

如需疑難排解 Bluemix 問題的相關資訊，請參閱[疑難排解](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}。如需關於透過論壇搜尋資訊及發問，以及關於與支援中心聯絡的詳細資料，請參閱[取得客戶支援](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}。
