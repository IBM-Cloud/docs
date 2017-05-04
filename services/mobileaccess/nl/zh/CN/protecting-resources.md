---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

**重要信息：{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。**

# 使用 {{site.data.keyword.amashort}} 服务保护后端资源
{: #protecting-resources}


通过 {{site.data.keyword.amafull}} 服务，可以使用支持移动的 OAuth 安全性和监视功能来保护在 {{site.data.keyword.Bluemix_notm}} 上运行的 Node.js 和基于 Java 的后端应用程序。
{:shortdesc}

## 开始之前
{: #before-you-begin}
开始之前，请确保 {{site.data.keyword.Bluemix_notm}} 后端应用程序中存在 Node.js 服务。


## 授权过滤器
{: #auth-filter}
{{site.data.keyword.amashort}} 服务器 SDK 具有授权过滤器，可用于保护后端应用程序。授权过滤器会拦截传入请求，并验证是否存在 Authorization 头。如果 Authorization 头不存在或无效，那么过滤器将返回包含 HTTP 401 的响应。{{site.data.keyword.amashort}} 客户端 SDK 知道如何拦截 {{site.data.keyword.amashort}} 服务器 SDK 返回的 HTTP 401 响应，并会触发认证流程。
## Authorization 头
{: #auth-header}
传入请求中的 Authorization 头由三个部分组成：Bearer、Access Token 和 ID Token，这三部分之间用空格分隔。`Access Token` 是必需的组成部分，而 `ID Token` 是可选的。

传入的 Authorization 头由各自的授权过滤器进行处理。过滤器会验证访问令牌和标识令牌特征符、到期日期和结构完整性。验证通过后，会将安全上下文对象添加到请求对象。可以使用相关 API 来获取对安全上下文的引用。

安全上下文包含主体、用户、设备和应用程序信息，这些信息按以下结构存储：
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
{: codeblock}

* `imf.sub`：指定标识令牌的主体或客户机的唯一标识（如果不存在标识令牌）。
* `imf.user`：指定从标识令牌中抽取的用户身份。如果不存在标识令牌，此字段将保存空对象。
* `imf.device`：指定从标识令牌中抽取的设备身份。如果不存在标识令牌，此字段将保存空对象。
* `imf.application`：指定从标识令牌中抽取的应用程序身份。如果不存在标识令牌，此字段将保存空对象。

## 后续步骤
{: #next-steps}
* [保护 Node.js 资源](protecting-resources-nodejs.html)
* [保护 Liberty for Java&trade; 资源](protecting-resources-java.html)
* [本地开发](protecting-resources-local.html)
