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

*前次更新：2016 年 5 月 19 日*

使用 {{site.data.keyword.weatherfull}}，可以將來自 The Weather Company (TWC) 的天氣資料納入 {{site.data.keyword.Bluemix}} 應用程式中。
{:shortdesc}

**附註：**目前無法在日本使用 Insights for Weather 服務。

在您開始之前，請先使用例如 Liberty for Java 的執行時期，在儀表板中建立一個 {{site.data.keyword.Bluemix_notm}} Web 應用程式。等待應用程式佈建，然後將 Insights for Weather 服務新增至您的應用程式。

當您將應用程式連結至 Insights for Weather 時，所佈建的服務實例即隨附唯一認證。您的應用程式會使用這些認證與
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} 來擷取天氣資料。

請遵循下列步驟以從 `VCAP_SERVICES` 擷取認證，並整合服務實例與您的應用程式。

1. 導覽至應用程式概觀頁面。
2. 跳至**環境變數**區段。即會顯示每一個服務的 `VCAP_SERVICES` 資訊。
3. 記下 Insights for Weather 服務的使用者名稱及密碼值。若要嘗試 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，則必須在系統提示您登入時輸入這些認證。您的 `VCAP_SERVICES` 類似於下列範例：

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

**附註：**每個區域各自獨立。您無法將在某個區域佈建給您的服務認證，在另一個區域中用來鑑別服務。若無法輸入適當的認證，則會導致回應內文中出現「未獲授權」訊息。 

# 相關鏈結
{: #rellinks}
## 範例
{: #samples}
* [Insights for Weather 展示](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [進行 Insights 上機實驗室](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [Bluemix 中的天氣如何？](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
{: #api}
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 相容的執行時期

{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 一般
{: #general}
* [將服務新增至您的應用程式](../reqnsi.html){: new_window}
* [端對端開發](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 定價單](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
