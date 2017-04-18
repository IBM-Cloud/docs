---

copyright:
  years: 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 Insights for Twitter {: #insights_twitter_overview}

使用 {{site.data.keyword.twitterfull}}，將 Twitter 內容從 Twitter [Decahose](http://support.gnip.com/gnip2.0/){: new_window} 或 [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} 串流納入您的 {{site.data.keyword.Bluemix}} 應用程式中。
{:shortdesc}

若要開始使用 {{site.data.keyword.twittershort}}，請先使用像是 Liberty for Java 的運行環境建立 Bluemix Web 應用程式，然後將 {{site.data.keyword.twittershort}} 服務新增到您的應用程式。{{site.data.keyword.twittershort}} 服務連結至您的應用程式之後，會使用唯一認證來佈建服務實例。您的應用程式使用這些認證搭配 REST API，來搜尋及耗用 Twitter 內容。請遵循下列步驟，從 VCAP_SERVICES 擷取認證，並將服務實例與您的應用程式整合。

1. 導覽至應用程式概觀頁面。
2. 跳至**環境變數**區段。即會顯示每一個服務的 ` 資訊。
3. 請記下來自 {{site.data.keyword.twittershort}} 服務的 username 及 password 值。若要測試 REST API 參考文件中的作業，您將需要輸入這些認證。例如，您的 `VCAP_SERVICES` 將類似下列 Snippet：

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

# 相關鏈結
{: #rellinks}
## 範例
{: #samples}
* [互動式 decahose 搜尋展示](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks：decahose 搜尋展示的指導教學及原始碼](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [分析 "American Sniper" 票房資料 (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Places Insights 上機實驗](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## API
{: #api}
* [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## 相容的運行環境 
{: #buildpacks}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## 一般
{: #general}
* [{{site.data.keyword.Bluemix_notm}} 服務的新增內容](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [將服務新增至您的應用程式](../reqnsi.html){: new_window}
* [端對端開發](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 定價單](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

