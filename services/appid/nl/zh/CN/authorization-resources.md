---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 授权过滤器和头
{: #auth}

{{site.data.keyword.appid_short}} 服务器 SDK 提供了用于保护以下两种类型的资源的策略：API 和 Web 应用程序。
{:shortdesc}


## 授权过滤器
{: #auth-filter}

API 保护策略会返回 HTTP 401 响应，其中包含用于为未经认证的客户端获取授权的作用域列表。Web 应用程序保护策略会返回 HTTP 302 重定向。根据配置，重定向会将未经认证的客户端发送到 {{site.data.keyword.appid_short_notm}} 服务托管的登录页面，或者直接发送到身份提供者的登录页面。



### API 策略
{: #api}

API 策略期望请求包含带有有效访问令牌的授权头。响应还可以包含身份令牌，但这并不是必需的；请参阅[访问令牌和身份令牌](/docs/services/appid/access-identity.html#access-and-identity)。

如果令牌无效或到期，那么 API 策略会返回 HTTP 401 错误，其中包含以下信息：Www-Authenticate=Bearer scope="{scope}" error="{error}"。`error` 组成部分是可选的。

如果请求返回有效的令牌，那么控制权会传递到下一个中间件，并且 `appIdAuthorizationContext` 属性会注入请求对象中。此属性包含原始访问令牌和身份令牌，以及解码为纯 JSON 对象的有效内容信息。


### Web 应用程序策略
{: #web}

Web 应用程序策略类检测到对受保护资源的未经认证的访问尝试时，会自动将用户的浏览器重定向到认证页面。成功认证后，用户会返回到 Web 应用程序的回调 URL。服务使用 Web 应用程序策略类来获取访问令牌和身份令牌。获取这些令牌后，Web 应用程序策略类会将其存储在 `WebAppStrategy.AUTH_CONTEXT` 下的 HTTP 会话中。由用户决定是否将访问令牌和身份令牌存储在应用程序数据库中。

## 授权头
{: #auth-header}

入局请求中的授权头由三个部分组成：Bearer、访问令牌、身份令牌，这三部分之间用空格分隔。访问令牌是必需的组成部分，而身份令牌是可选的。期望的头结构为：Authorization=Bearer {access_token} [{id_token}]
