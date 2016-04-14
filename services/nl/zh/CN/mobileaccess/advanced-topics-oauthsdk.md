---

copyright:
  years: 2015, 2016
  
---

# 后端到后端通信
{: #backend-comm}

在某些高级场景中，可能需要将来自正在 {{site.data.keyword.Bluemix}} 上运行的后端应用程序的请求，发送到受 {{site.data.keyword.amashort}} 服务保护的其他后端服务，例如 {{site.data.keyword.cloudant}} 服务。在这些情况下，必须将 OAuth 令牌添加到请求。

使用 `bms-mca-oauth-sdk` npmjs 模块来获取 OAuth 令牌，并将其注入到请求中。

## 安装 bms-mca-oauth-sdk 模块
{: #sdk}

在命令行上，打开 Node.js 应用程序目录，并运行以下命令：

```Bash
npm install -save bms-mca-oauth-sdk
```

## 使用 bms-mca-oauth-sdk 模块
{: #using-sdk}

以下代码演示了如何使用 `bms-mca-oauth-sdk` 模块。


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {


	// You can cache tokens to avoid extra roundtrips on every request
	// This property defines the number of tokens to be cached

	cacheSize: 100,

	// All of the below properties are retrieved automatically when your Node.js
	// runs on {{site.data.keyword.Bluemix_notm}} and bound to an instance of {{site.data.keyword.amashort}} Service.
	// Alternatively you can get these properties values by clicking Show Credentials
	// on the {{site.data.keyword.amashort}} Service tile in your {{site.data.keyword.Bluemix_notm}} application dashboard

	appId: "appId",				// Bleumix applicationGUID，即 tenantId
	clientId: "clientId",			
	secret: "secret",
	serverUrl: "serverUrl"
};

oauthSDK.getAuthorizationHeader(options).then(function(authHeader){

	// In the request that you want to send to the protected resource, 
	// add the authHeader value.

	request.headers.Authorization = authHeader;

	// Send request

});

```
