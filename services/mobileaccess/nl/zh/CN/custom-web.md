---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-08"

---

# Web 应用程序定制认证
{: #custom-web}

将定制认证添加到 Web 应用程序：

## 开始之前
{: #before-you-begin}

您必须具有：
* 采用 `/apps/:Guid/<RealmName>/handleChallengeAnswer` 端点的 Web 应用程序，其在认证成功时返回用户身份。
用户身份 JSON 结构应该如下所示：

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端的更多信息，请参阅[入门](index.html)。



## 配置 {{site.data.keyword.amashort}} 应用程序进行定制认证


1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。
1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。
1. 单击“定制”磁贴。
1. 输入**定制域**、**定制身份提供者 URL** 和 **redirect_uri**。单击“保存”。 

## 使用 {{site.data.keyword.amashort}} 进行定制 Web 认证

要启动授权过程：

1. 从 Web 应用程序重定向到以下授权服务器端点：

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization


  使用以下查询参数：
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri for the redirect after getting an authorization code>
   scope= ‘openid’
   state= <state>
   ```

    `state` 参数目前暂不使用，可以保留为空。

    `redirect_uri` 参数会确定定制身份提供者的认证成功或失败之后的重定向。

1. 重定向到授权端点之后，您将获取登录表单。输入用户名和密码，以启动针对身份提供者的认证，并重定向到 `redirect_uri`。
成功认证之后返回的响应包含请求查询参数中的授权代码。

4. 向授权服务器令牌端点发出 `POST` 请求：

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 使用以下查询参数：
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
`redirect_uri` 参数必须与步骤 1 的 `redirect_uri` 相匹配。授权代码由步骤 2 中的请求返回。
  请确保在 10 分钟内发送此 `POST` 请求，因为授权代码有效的最长时间为 10 分钟。

`POST` 响应主体包含以 Base64 编码的 *access_token* 和 *id_token*。



## 测试认证


现在，您可以开始向受保护资源发出请求。
对受保护资源的所有请求都应该包含 `access_token`。在 `the-Authorization-request` 头字段中发送访问令牌。
