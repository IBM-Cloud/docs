---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 保护 Node.js 资源
{: #protecting-resources-nodejs}

您可以使用 {{site.data.keyword.appid_short}} 服务器 SDK 来保护 Node.js 应用程序中的资源。{:shortdesc}

## 开始之前
{: #before-you-begin}

* 熟悉如何在 {{site.data.keyword.Bluemix_notm}} 上开发 Node.js 应用程序。
* {{site.data.keyword.appid_short_notm}} 服务器 SDK 要求 Node.js 服务器通过 <a href="http://expressjs.com/" target="_blank">Express 框架 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 进行实施。

**注**：有其他框架使用 `Express` 框架，例如 LoopBack。可以将 {{site.data.keyword.appid_short_notm}} 服务器 SDK 与其中任意框架一起使用。

## 关于服务器 SDK
{: #about}

{{site.data.keyword.appid_short_notm}} 服务器 SDK 提供了用于 {{site.data.keyword.Bluemix_notm}} 上部署的后端应用程序的 ApiStrategy 通行证策略。要保护应用程序不受未经授权的访问，您必须使用 ApiStrategy 检测 Node.js 服务器。`appid-serversdk-nodejs npm 模块`提供了 ApiStrategy 通行证策略和验证方法，以验证 {{site.data.keyword.appid_short_notm}} 发出的访问令牌和身份令牌。

{{site.data.keyword.appid_short_notm}} 服务器 SDK 使用 Passport 框架来实施授权功能，请参阅 <a href="http://passportjs.org/" target="_blank">Passport 框架 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。


## 安装服务器 SDK
{: #protecting-resources-serversdk}

1. 使用命令行打开包含 Node.js 应用程序的目录。
2. 运行以下命令：

  ```
  npm install -save express
  npm install -save passport
  npm install -save appid-serversdk-nodejs
  ```
  {:pre}

## 在 Node.js 中保护资源
{: #protecting-resources-nodesdk}

以下片段演示了如何在简单 Express 应用程序中使用 `ApiStrategy` 来保护 `/protected` 端点 GET 方法。

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

可以使用 `WebAppStrategy` 来保护 Web 应用程序资源：

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var ApiStrategy = require('appid-serversdk-nodejs').WebStrategy;
  ```
  {:pre}

有关更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">GitHub 存储库 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
