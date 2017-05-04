---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

**重要信息：{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。**

# 通过 {{site.data.keyword.amashort}} 保护 Node.js 资源
{: #protecting-resources-nodejs}


您可以使用 {{site.data.keyword.amashort}} 服务器 SDK 来保护 Node.js 应用程序中的资源。

## 开始之前
{: #before-you-begin}

* 您必须熟悉如何在 {{site.data.keyword.Bluemix_notm}} 上开发 Node.js 应用程序。有关更多信息，请参阅[使用 Node.js 的 SDK 创建应用程序](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime)。
* {{site.data.keyword.amashort}} 服务器 SDK 要求 Node.js 服务器通过 `Express` 框架进行实施。请注意，有其他框架使用 `Express` 框架，例如 LoopBack。可以将 {{site.data.keyword.amashort}} 服务器 SDK 与其中任意框架一起使用。有关 Express 框架的更多信息，请参阅 [Expressjs.com ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://expressjs.com/){: new_window}。

## 关于服务器 SDK
{: #about}

{{site.data.keyword.amashort}} 服务器 SDK 提供了要在 IBM {{site.data.keyword.Bluemix_notm}} 上部署的后端应用程序中使用的 `MCABackendStrategy` 通行证策略。要保护应用程序不受未经授权的访问，并获取监视信息，您必须在 Node.js 服务器中安装 `MCABackendStrategy`。`bms-mca-token-validation-strategy` npm 模块提供了 `MCABackendStrategy` 通行证策略和验证方法，以验证 {{site.data.keyword.amashort}} 发出的访问令牌和标识令牌。此模块还会自动提供有关安全事件的监视信息。

{{site.data.keyword.amashort}} 服务器 SDK 使用 `Passport` 框架来实施授权功能。有关更多信息，请参阅 [Passportjs.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://passportjs.org/){: new_window}。

## 安装服务器 SDK
{: #protecting-resources-serversdk}

在命令行上打开 Node.js 应用程序的目录，并运行以下命令：

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## 在 Node.js 中保护资源
{: #protecting-resources-nodesdk}

以下片段演示了如何在简单 Express 应用程序中使用 `MCABackendStrategy` 来保护 `/protected` 端点 GET 方法。

```JavaScript
var express = require('express');
var passport = require('passport');
var MCABackendStrategy = require('bms-mca-token-validation-strategy').MCABackendStrategy;

passport.use(new MCABackendStrategy());var app = express();
app.use(passport.initialize());app.get('/protected', passport.authenticate('mca-backend-strategy', {session: false }),
    function(request, response){
		console.log("Securty context", request.securityContext)    
		response.send(200, "Success!");
    }
);

app.listen(process.env.PORT);
```
{: codeblock}
