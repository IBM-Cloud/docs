---

copyright:
  year: 2016, 2017
lastupdated: "2017-04-06"

---

**重要信息：{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。**

# 启用 Web 应用程序的 Google 认证
{: #google-auth-web}

使用 Google 登录在 Web 应用程序上认证用户。


## 开始之前
{: #before-you-begin}

您必须具有：
* Web 应用程序。
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端的更多信息，请参阅[入门](index.html)。

## 针对 Web 站点配置 Google 应用程序
要开始将 Google 用作身份提供者，请在 [Google 开发者控制台](https://console.developers.google.com)中创建项目。创建项目的步骤之一是获取 Google 客户端标识和私钥。Google 客户端标识和私钥是 Google 认证针对您的应用程序使用的唯一标识，设置 {{site.data.keyword.Bluemix_notm}} 应用程序时需要这些标识。

1. 使用 Google+ API 创建项目。
1. 使用 **OAuth** 创建凭证。要创建凭证，您需要：
    * 选择 **Web 应用程序**应用程序类型。
    * 提供**授权重定向 URI** 值：

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. 完成凭证创建并记录 Google 客户端标识和私钥。


## 配置 Mobile Client Access 进行 Google 认证
在您已经有 Google 应用程序标识和私钥之后，可以在 {{site.data.keyword.amashort}} 仪表板中启用 Google 认证。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。
1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。
1. 单击 Google 磁贴。
1. 输入 Google 客户端标识和私钥，并保存。


## 使用 Mobile Client Access 进行 Google Web 认证
要启动授权过程：

1. 从 Web 应用程序重定向到以下授权服务器端点：  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  使用以下查询参数：
	```
response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri which you want to return to after getting a grant code>
   scope= ‘openid’
   state= <state>
	```

  `state` 参数目前暂不使用，可以保留为空。

  `redirect_uri` 参数是 URI，用于在使用 Google 成功认证或认证失败之后进行重定向。重定向之后获取的响应包含请求查询参数中的授权代码。
1. 向授权服务器令牌端点发出 `POST` 请求：

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  使用以下查询参数：

	```
  	grant_type=’authorization_code’
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
`redirect_uri` 参数必须与步骤 1 的 `redirect_uri` 相匹配，`<authorization code>` 值为从响应接收的值。
请确保在 10 分钟内发送此 `POST` 请求，因为授权代码有效的最长时间为 10 分钟。`POST` 响应主体应该包含以 Base64 编码的 `access_token` 和 `id_token`。

## 测试认证

现在，您可以开始向受保护资源发出请求。
对受保护资源的所有请求都应该在授权请求头字段中包含访问令牌。
