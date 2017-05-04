---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 配置身份提供者
{: #setting-up-idp}

您可以配置 Facebook 和/或 Google 来为用户设置单点登录体验。通过使用身份提供者，用户就能够使用自己熟悉的凭证进行登录。
{:shortdesc}


## 配置 Facebook 认证
{: #facebook}

将 {{site.data.keyword.appid_short}} 服务配置为将 Facebook 用作身份提供者。

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### 从 Facebook 获取应用程序标识和私钥
{: #getting-facebook-appid}

要在移动或 Web 应用程序上将 Facebook 用作身份提供者，必须在 Facebook 应用程序上添加并配置 Web 站点平台。

1. 在 <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers 站点 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 上登录到您的帐户。
2. 记录 Facebook 应用程序标识和私钥。在服务仪表板中配置 Web 项目进行认证时，需要这些值。
3. 添加 Web 平台并输入站点 URL。
4. 从产品列表中，选择 **Facebook 登录**。
5. 在“有效的 OAuth 重定向 URL”字段中，输入授权服务器回调端点 URL。可以在配置 {{site.data.keyword.appid_short_notm}} 服务后，在随后的步骤中添加此值。
6. 单击**保存更改**。

### 配置 {{site.data.keyword.appid_short_notm}} 进行 Facebook 认证
{: #configuring-facebook-appid}

已拥有 Facebook 应用程序标识和私钥并且将 Facebook for Developers 应用程序配置为向 Web 客户端提供服务后，可以在服务仪表板中编辑 Facebook 认证。

1. 在服务仪表板的**管理**选项卡中，选择 **Facebook**，然后单击**编辑**。
2. 输入从 Facebook for Developers Web 站点获取的 Facebook 应用程序标识和私钥。
3. 复制 **Facebook for Developers 的重定向 URI** 字段中的 URI。将此 URI 粘贴到 Facebook 开发者门户网站上 **Facebook 登录**部分中的**有效的 OAuth 重定向 URI** 字段中。
4. 单击**保存**。
5. 可选：要配置 Web 应用程序的认证，请在“Web 应用程序重定向 URL”中输入重定向 URL。此值由开发者确定，并用于在完成授权过程之后访问该重定向 URL。


## 配置 Google 认证
{: #google}

将 {{site.data.keyword.appid_short_notm}} 服务配置为将 Google 用作身份提供者。

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### 从 Google 获取客户端标识和私钥
{: #google-client-id}

要将 Google 用作身份提供者，请获取 Google 客户端标识和私钥并在 Google 开发者控制台中创建项目。

1. 在 <a href="https://console.developers.google.com/apis/library" target="_blank">Google 开发者控制台 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 中打开 Google 应用程序。
2. 添加 Google+ API。
3. 使用 OAuth 创建凭证。在 **应用程序类型**字段中，选择 **Web 应用程序**。在**授权重定向 URI** 字段中，输入 App ID 重定向 URI。从服务仪表板的 Google 配置屏幕中获取 App ID 重定向授权 URI。
4. 保存更改。记录 Google 客户端标识和私钥。



### 配置 {{site.data.keyword.appid_short_notm}} 进行 Google 认证
{: #google-client-appid}

已拥有 Google 客户端和私钥并且将 Google 开发者控制台配置为向 Web 客户端提供服务后，可以在服务仪表板中编辑 Google 认证。

1. 在服务仪表板的**管理**选项卡中，选择 **Google**，然后单击**编辑**。
3. 输入从 Google 开发者控制台获取的 Google 客户端标识和私钥。
4. 复制 **Google for Developers 的重定向 URI** 字段中的 URI。将此 URI 粘贴到 Google 开发者门户网站上 **Web 应用程序的客户端标识**部分中**限制**下的**授权重定向 URI** 字段中。
5. 单击**保存**。
6. 可选：要配置 Web 应用程序的认证，请在“Web 应用程序重定向 URI”字段中输入重定向 URI。此值由开发者确定，并用于在完成授权过程之后访问该重定向 URI。



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
