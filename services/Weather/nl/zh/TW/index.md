---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 {{site.data.keyword.weather_short}}
{: #insights_weather_overview}

使用 {{site.data.keyword.weatherfull}}，可以將來自 The Weather Company (TWC) 的天氣資料納入 {{site.data.keyword.Bluemix}} 應用程式中。
{:shortdesc}

**注意：**目前在下列國家或地區**可能無法**購買或使用 {{site.data.keyword.weather_short}} 服務：
阿富汗、亞美尼亞、亞塞拜然、巴林、孟加拉、不丹、汶萊、柬埔寨、中國、塞普勒斯、
喬治亞、印尼、伊朗、伊拉克、日本、約旦、哈薩克、科威特、吉爾吉斯、寮國、
黎巴嫩、馬來西亞、馬爾地夫、蒙古、緬甸、尼泊爾、阿曼、巴基斯坦、菲律賓、卡達、
俄羅斯、沙烏地阿拉伯、新加坡、大韓民國、斯里蘭卡、敘利亞、塔吉克、
東帝汶、土耳其、土庫曼、阿拉伯聯合大公國、烏茲別克、越南、葉門。此清單會在有額外資訊時進行更新。

如果您現有的應用程式使用 [Insights for Weather 服務](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window}，您的應用程式將在引進
{{site.data.keyword.weather_short}} 之後，無須任何修改可繼續運作 90 天。若要利用新增的 API 和改良的定價模型，可以將應用程式移轉至新的服務。

在您開始之前，請先使用例如 Liberty for Java 的運行環境，在儀表板中建立一個 {{site.data.keyword.Bluemix_notm}} Web 應用程式。等待應用程式佈建，然後將
{{site.data.keyword.weather_short}} 服務新增至您的應用程式。

當您將應用程式連結至 {{site.data.keyword.weather_short}} 時，所佈建的服務實例即隨附唯一認證。您的應用程式會使用這些認證與
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} 來擷取天氣資料。

請遵循下列步驟以從 `VCAP_SERVICES` 擷取服務認證，並整合服務實例與您的應用程式。

1. 導覽至應用程式概觀頁面。
2. 跳至**環境變數**區段。即會顯示每一個服務的 `VCAP_SERVICES` 資訊。
3. 記下 {{site.data.keyword.weather_short}} 服務的使用者名稱及密碼值。若要嘗試 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，則必須在系統提示您登入時輸入這些認證。您的 `VCAP_SERVICES` 類似於下列範例：

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**附註：**每個區域各自獨立。您無法將在某個區域佈建給您的服務認證，在另一個區域中用來鑑別服務。若無法輸入適當的認證，則會導致回應內文中出現*未獲授權* 訊息。

# 相關鏈結
{: #rellinks}
## 範例
{: #samples}
* [{{site.data.keyword.weather_short}} 展示應用程式](http://weather-company-data-demo.{APPDomain}){: new_window}
* [{{site.data.keyword.weather_short}} Deep Dive 影片](https://youtu.be/pZHXIibziUo){: new_window}
* [Places Insights 上機實驗室](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [{{site.data.keyword.Bluemix_notm}} + Weather 範例應用程式](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Bare Metal, NYC Taxi Data, and Insights for Weather（YouTube 指導教學）](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

## API
{: #api}
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 相容的運行環境
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 一般
{: #general}
* [將服務新增至您的應用程式](/docs/services/reqnsi.html){: new_window}
* [端對端開發](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 定價單](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
