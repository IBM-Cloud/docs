---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 關於 {{site.data.keyword.weather_short}}
{: #about_weather}

使用 {{site.data.keyword.weatherfull}}，可以將來自 The Weather Company (TWC) 的天氣資料納入 {{site.data.keyword.Bluemix}} 應用程式中。
{:shortdesc}

您可以使用 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，將天氣觀測資料和預測新增至 {{site.data.keyword.Bluemix_notm}} 應用程式，以及顯示地理定位所指定區域的天氣資料。The Weather Company 提供最詳盡的歷史及預測天氣資料。將會擷取所有天氣型態（包括降雨、氣壓、風及雷雨）的資料。

您可以使用 REST API 來擷取下列資訊：

* 所指定地理定位從目前時間開始的未來 48 小時的每小時天氣預測。
* 從現行日開始接下來 3、5、7 或 10 天的每日預測，包括指定地理定位的白天及夜晚區段的預測。這項預測包括最多 256 個字元的預測敘述性字串，內含適用於所在位置的度量單位並使用所要求的語言。
* 從現行日開始接下來 3、5、7 或 10 天的每日預測（將每一個每日預測分成早上、下午、晚上及午夜區段）。
* 所指定地理定位目前觀測到的天氣資料。這項天氣資料包含溫度、降雨、風向及風速、濕度、氣壓、露點、能見度及紫外線 (UV)。
* 過去 24 小時內（含），指定地理定位觀測到的天氣資料。這項資料是來自實際觀測站。
* 政府發出的天氣警示，包括由 National Weather Service（美國）、Environment Canada 及 MeteoAlarm（歐洲）所發出的天氣監視、警告、聲明及建議。
* 年鑑服務，提供歷史每日或每月天氣資料，資料來源是 National Weather Service（美國國家氣象局）觀測站，時間則跨越 10 到 30 年以上。
* 位置對映服務，提供查閱位置名稱或地理編碼（經緯度）以擷取符合您要求之位置集的功能。

## 定價模型
{: #pricing_models}

定價模型是根據對 REST API 的每分鐘呼叫數。每月會向客戶收費。「免費」及「基本」方案讓您能進行每分鐘最多 10 次 API 呼叫。「標準」和「高階」方案能讓您分別進行每分鐘 150 和 375 次 API 呼叫。每個方案都有容許的 API 呼叫數目上限。

只要限制呼叫數目，就可以針對任何地理定位區域、預測類型或時間序列觀測資料，在應用程式中測試天氣資料。「免費」、「基本」、「標準」和「高階」方案在購買時不需要合約。「免費」方案可讓您的應用程式進行最多 10,000 次呼叫。剩餘的方案可讓您的應用程式分別進行每個月 150,000 次、2 百萬次，或 5 百萬次 API 呼叫。

也可以針對在計費期間部署的每個服務實例購買多個付費方案。如果您的應用程式使用超過 10,000 次呼叫，則必須與 IBM 簽訂合約以持續佈建這些服務。

當您的應用程式到達根據所選方案允許進行的每分鐘 API 呼叫限制時，下次進行的 API 呼叫將不會成功，直到您的應用程式能夠要求更多 API 呼叫為止。

例如，如果您使用「標準」方案，則您的應用程式*可以* 在一分鐘內進行 500 次 API 呼叫，即使是這超過了方案的限制也允許，不過必須等到
5 分鐘之後才會再允許下次 API 呼叫。因此，使用者可能會發現在您的應用程式中，天氣資料的重新整理會有延遲現象。
您必須確定開發應用程式時已處理這些限制，而不會要求激增的 API 呼叫。相反地，您可以監視應用程式的 API 呼叫使用情形。您可以藉由檢查
API 呼叫傳回的項目數，來驗證應用程式是否到達方案的限制。

當您的應用程式到達根據所選方案允許進行的每月 API 呼叫限制時，接下來進行的 API 呼叫將會依平均每 10,000 次 API 呼叫 $1.70 的費率收費。

## 意見與支援
{: #feedback_support}

您可以搜尋資訊或透過討論區提問來取得協助。您也可以開啟支援問題單。

使用討論區提問時，請標記您的問題，以便 {{site.data.keyword.Bluemix_notm}} 開發團隊能看到它。

* 如果您有使用 {{site.data.keyword.weather_short}} 開發或部署應用程式的相關技術問題，請將問題張貼在 [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window}，並使用 **ibm-bluemix** 和 **weather** 來標記您的問題。
* 如果遇到服務或開始使用指示的相關問題，請使用 [IBM developerWorks Answers 討論區](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}。請包含 **bluemix** 及 **weather** 標籤。
* 如果您對於從 Insights for Weather 移轉應用程式到 {{site.data.keyword.weather_short}}
有問題，請到 [IBM developerWorks](http://www.ibm.com/developerworks){:new_window} 與我們聯絡。

如需使用討論區的詳細資料，請參閱[取得協助](https://console.{DomainName}/docs/support/index.html#getting-help){: new_window}。

如需開啟 IBM 支援問題單的相關資訊，或支援層次與問題單嚴重性的相關資訊，請參閱[與支援中心聯絡](https://console.{DomainName}/docs/support/index.html#contacting-support){: new_window}。
