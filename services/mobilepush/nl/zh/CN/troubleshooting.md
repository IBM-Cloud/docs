---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 故障诊断
{: #errors}
上次更新时间：2016 年 12 月 7 日
{: .last-updated}

使用本部分作为指南，对常见 {{site.data.keyword.mobilepushshort}} 问题进行故障诊断。


### 发生内部服务器错误。请联系管理员。（内部错误代码：PUSHD102E）

**说明**：如果您在 2015 年 11 月之前创建了推送实例，那么可能会发生此错误。  

**用户响应**：要解决此问题，请删除推送实例并创建新实例。请注意，删除推送实例时，不会保留标记。


### UnauthorizedRegistration

**说明**：Chrome Web 推送不使用 Firebase 云消息传递 (FCM) 密钥。如果您从 GCM 迁移到 FCM 之后无法在 Chrome 上接收 Web 推送通知，这是因为 Web 站点先前配置为与 GCM 项目一起运作，而现在 FCM 中创建了新项目。所生成的识别浏览器的标记在 Chrome 浏览器中缓存。

**用户响应**：您可以通过删除 cookie 并重置浏览器权限来解决此问题。这样将请求启用推送通知的权限。 

