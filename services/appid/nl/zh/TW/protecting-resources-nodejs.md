---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 保護 Node.js 資源
{: #protecting-resources-nodejs}

您可以使用 {{site.data.keyword.appid_short}} 伺服器 SDK 來保護 Node.js 應用程式中的資源。
{:shortdesc}

## 開始之前
{: #before-you-begin}

* 熟悉如何在 {{site.data.keyword.Bluemix_notm}} 上開發 Node.js 應用程式。
* {{site.data.keyword.appid_short_notm}} 伺服器 SDK 需要使用 <a href="http://expressjs.com/" target="_blank">Express 架構 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來實作 Node.js 伺服器。

**附註**：有其他架構使用 `Express` 架構（例如 LoopBack）。您可以搭配使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 與任何這些架構。

## 關於伺服器 SDK
{: #about}

{{site.data.keyword.appid_short_notm}} 伺服器 SDK 提供 {{site.data.keyword.Bluemix_notm}} 上所部署的後端應用程式中使用的 ApiStrategy 通行證策略。若要保護應用程式免於遭受未經授權的存取，您必須使用 ApiStrategy 來檢測 Node.js 伺服器。`appid-serversdk-nodejs npm 模組`提供 ApiStrategy 通行證策略及驗證方法，以驗證 {{site.data.keyword.appid_short_notm}} 所發出的存取記號及 ID 記號。

{{site.data.keyword.appid_short_notm}} 伺服器 SDK 使用 Passport 架構來強制執行授權，請參閱 <a href="http://passportjs.org/" target="_blank">Passport 架構 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。


## 安裝伺服器 SDK
{: #protecting-resources-serversdk}

1. 使用指令行，開啟具有 Node.js 應用程式的目錄。
2. 執行下列指令：

  ```
  npm install -save express
  npm install -save passport
  npm install -save appid-serversdk-nodejs
  ```
  {:pre}

## 保護 Node.js 中的資源
{: #protecting-resources-nodesdk}

下列 Snippet 示範如何在簡式 Express 應用程式中使用 `ApiStrategy` 來保護 `/protected` 端點 GET 方法。

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var ApiStrategy = require('appid-serversdk-nodejs').ApiStrategy;

  passport.use(new ApiStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('appid-api-strategy', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
```
  {:pre}

您可以使用 `WebAppStrategy` 來保護 Web 應用程式資源：

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var ApiStrategy = require('appid-serversdk-nodejs').WebStrategy;
  ```
  {:pre}

如需相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">GitHub 儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
