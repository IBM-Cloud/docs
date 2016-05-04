---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 Insights for Weather
{: #insights_weather_overview}

*前次更新：2016 年 4 月 6 日*

使用 {{site.data.keyword.weatherfull}}，可以將來自 The Weather Company (TWC) 的天氣資料納入 {{site.data.keyword.Bluemix}} 應用程式中。
{:shortdesc}

下列指示會引導您完成建立應用程式、將應用程式連結至 Insights for Weather 服務，以及擷取服務認證以與 [REST API](https://twcservice.{APPDomain}/rest-api/) 進行互動的處理程序。

### 建立應用程式
{: #create_an_app}

基於示範目的，您會使用 Liberty for Java 執行時期來建立應用程式，但是下列一般處理程序可套用到其他執行時期。

1. 如果沒有現有的應用程式，請在儀表板中按一下**建立應用程式**。
2. 當系統要求您選擇應用程式範本時，請按一下 **WEB**。
3. 當系統要求您選擇入門範本時，請按一下 **Liberty for Java**。
4. 按一下**繼續**。
5. 在**應用程式名稱**欄位中，輸入應用程式的名稱。
6. 按一下**完成**。請等待應用程式佈建。

### 新增 Insights for Weather 服務
{: #add_insights_for_weather_service}

遵循這些步驟，將 Insights for Weather 服務新增至您的應用程式。
1. 開啟**型錄**功能表。
2. 從**資料及分析**區段中，按一下 **Insights for Weather** 磚。
3. 在**應用程式**下拉清單中，選取您的應用程式。
4. 按一下**使用**。
5. 當系統提示時，請按一下**重新編譯打包**以重新啟動您的應用程式。

### 擷取 Insights for Weather 認證
{: #retrieve_weather_credentials}

當您將應用程式連結至 Insights for Weather 時，所佈建的服務實例即隨附唯一認證。這些認證會儲存在應用程式的 `VCAP_SERVICES` 中，而且對於支援服務之間的互動是必要的。

1. 導覽至應用程式概觀頁面。
2. 跳至**環境變數**區段。即會顯示每一個服務的 `VCAP_SERVICES` 資訊。
3. 請注意 Insights for Weather 服務的使用者名稱及密碼值。若要嘗試 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，則必須在系統提示您登入時輸入這些認證。您的 `VCAP_SERVICES` 類似於下列範例：

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

# 相關鏈結
## 範例
* [Insights for Weather 展示](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [進行 Insights 上機實驗室](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [Bluemix 中的天氣如何？](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 相容的執行時期
{:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 一般
* [關於 Insights for Weather](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [將服務新增至您的應用程式](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [端對端開發](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 定價單](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
