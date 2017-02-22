---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-27"

---

{:shortdesc: .shortdesc} 
{:codeblock:.codeblock}

# 使用 {{site.data.keyword.amashort}} 保護 Node.js 資源
{: #protecting-resources-nodejs}


您可以使用 {{site.data.keyword.amashort}} 伺服器 SDK 來保護 Node.js 應用程式中的資源。

## 開始之前
{: #before-you-begin}

* 您必須熟悉如何在 {{site.data.keyword.Bluemix_notm}} 上開發 Node.js 應用程式。如需相關資訊，請參閱[使用 SDK for Node.js 建立應用程式](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime)。
* {{site.data.keyword.amashort}} 伺服器 SDK 需要使用 `Express` 架構來實作 Node.js 伺服器。請注意，有其他架構使用 `Express` 架構（例如 LoopBack）。您可以搭配使用 {{site.data.keyword.amashort}} 伺服器 SDK 與任何這些架構。如需 Express 架構的相關資訊，請參閱 [Expressjs.com ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://expressjs.com/ "外部鏈結圖示"){: new_window}。

## 關於伺服器 SDK
{: #about}

{{site.data.keyword.amashort}} 伺服器 SDK 提供 `MCABackendStrategy` 通行證策略，以用於在 IBM {{site.data.keyword.Bluemix_notm}} 上部署的後端應用程式。若要保護應用程式免於遭受未經授權的存取，並取得監視資訊，則必須使用 `MCABackendStrategy` 來檢測 Node.js 伺服器。`bms-mca-token-validation-strategy` npm 模組提供 `MCABackendStrategy` 通行證策略及驗證方法，來驗證 {{site.data.keyword.amashort}} 所發出的存取記號及 ID 記號。此模組也會自動提供安全事件的監視資訊。

{{site.data.keyword.amashort}} 伺服器 SDK 使用 `Passport` 架構來施行授權。如需相關資訊，請參閱 [Passportjs.org ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://passportjs.org/ "外部鏈結圖示"){: new_window}。

## 安裝伺服器 SDK
{: #protecting-resources-serversdk}

在指令行上開啟含 Node.js 應用程式的目錄，並執行下列指令：

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## 保護 Node.js 中的資源
{: #protecting-resources-nodesdk}

下列 Snippet 示範如何在簡單 Express 應用程式中使用 `MCABackendStrategy` 來保護 `/protected` 端點 GET 方法。

```JavaScript
var express = require('express');
var passport = require('passport');
var MCABackendStrategy = require('bms-mca-token-validation-strategy').MCABackendStrategy;

passport.use(new MCABackendStrategy());

var app = express();
app.use(passport.initialize());

app.get('/protected', passport.authenticate('mca-backend-strategy', {session: false }),
    function(request, response){
		console.log("Securty context", request.securityContext)    
		response.send(200, "Success!");
    }
);

app.listen(process.env.PORT);
```
{: codeblock}
