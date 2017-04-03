---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。

# 启用 Web 应用程序的 Facebook 认证
{: #facebook_web}

使用 Facebook 在 Web 应用程序上认证用户。

## 开始之前
{: #facebook-auth-android-before}
您必须具有：
* Web 应用程序。  
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端的更多信息，请参阅[入门](index.html)。
* Facebook 应用程序标识和应用程序私钥。有关更多信息，请参阅[从 Facebook 开发者门户网站获取 Facebook 应用程序标识](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。


## 针对 Web 站点配置 Facebook 应用程序
要在 Web 站点上将 Facebook 用作身份提供者，必须在 Facebook 应用程序上添加并配置 Web 站点平台。

1. 在 Facebook 开发者门户网站中打开 Facebook 应用程序。
1. 记录应用程序的应用程序标识和应用程序私钥。配置 Web 项目以进行 Facebook 认证时需要此值。
1. 从**设置**页面中，单击**添加平台**并选择 **Web 站点**。
1. 保存更改。
1. 在侧边栏中单击 **Facebook 登录**。
1. 在**有效的 OAuth 重定向 URI** 框中输入授权服务器回调端点：https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback。保存更改。




# 配置 {{site.data.keyword.amashort}} 进行 Facebook 认证
已拥有 Facebook 应用程序标识和应用程序私钥并且将 Facebook 应用程序配置为向 Web 客户端提供服务后，可以在 {{site.data.keyword.Bluemix_notm}} 仪表板中启用 Facebook 认证。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。
1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。
1. 单击 Facebook 磁贴。
1. 输入 Facebook 应用程序标识和应用程序私钥，并保存。




## 使用 Mobile Client Access 进行 Facebook Web 认证

要启动授权过程：

1. 从 Web 应用程序重定向到以下授权服务器端点：https://imf-newauthserver.bluemix.net/oauth/v2/authorization。

1. 添加以下查询参数：
   
   ```
response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri for redirecting after receiving the authorization code>
    scope= 'openid'
    state= <state>
    ```


  `state` 参数目前暂不使用，可以保留为空。`redirect_uri` 参数是 URI，用于在使用 Facebook 成功认证或认证失败之后进行重定向。

1. 重定向到授权端点之后，您将从 Facebook 获取登录表单。  输入用户名和密码，以重定向到 `redirect_uri`。
重定向之后获取的响应包含请求查询参数中的授权代码。

1. 向授权服务器的令牌端点发出 `POST` 请求：

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  使用以下查询参数：
  ```
grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
`redirect_uri` 参数必须与步骤 2 的 `redirect_uri` 相匹配。
`code` 值是步骤 3 结束时响应中接收的授权代码。
请确保在 10 分钟内发送此 `POST` 请求，因为授权代码有效的最长时间为 10 分钟。  `POST` 响应主体应该包含以 Base64 编码的 `access_token` 和 `id_token`。

## 测试认证
现在，您可以开始向受保护资源发出请求。
对受保护资源的所有请求都应该在授权请求头字段中包含 `access_token`。
