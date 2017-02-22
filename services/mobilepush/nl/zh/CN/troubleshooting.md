---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 故障诊断
{: #errors}
上次更新时间：2017 年 1 月 11 日
{: .last-updated}

使用本部分作为指南，对常见 {{site.data.keyword.mobilepushshort}} 问题进行故障诊断。


### 发生内部服务器错误。请联系管理员。（内部错误代码：PUSHD102E）

**说明**：如果您在 2015 年 11 月之前创建了推送实例，那么可能会发生此错误。  

**用户响应**：要解决此问题，请删除推送实例并创建新实例。请注意，删除推送实例时，不会保留标记。


### UnauthorizedRegistration

**说明**：Chrome Web 推送不使用 Firebase 云消息传递 (FCM) 密钥。如果您从 GCM 迁移到 FCM 之后无法在 Chrome 上接收 Web 推送通知，这是因为 Web 站点先前配置为与 GCM 项目一起运作，而现在 FCM 中创建了新项目。所生成的识别浏览器的标记在 Chrome 浏览器中缓存。

**用户响应**：您可以通过删除 cookie 并重置浏览器权限来解决此问题。这样将请求启用推送通知的权限。 


### 在此浏览器中不支持服务工作程序

**解释**：使用服务工作程序作为 `BMSPushSDK.js` 一部分包含的 SDK 不可用。 

**用户响应**：建议您切换至支持服务工作程序的浏览器。受支持的浏览器版本为 Firefox V49 或更高版本，以及 Chrome V53（64 位元）或更高版本。


### SecurityError：操作不安全

**解释**：当您在 Firefox 中启用 Web 控制台时，您可能会看到错误。Push Notification 服务中的 Web 推送支持需要使用 `https` 协议而非 `http` 访问 Web 站点。

**用户响应**：建议您尝试从浏览器使用 `https` 连接到 Web 站点。

