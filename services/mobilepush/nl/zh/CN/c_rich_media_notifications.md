---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 启用富媒体通知
{: #interactive-notifications}
上次更新时间：2017 年 1 月 11 日
{: .last-updated}


您可以在 iOS 10 和以上版本中启用富媒体 {{site.data.keyword.mobilepushshort}}。推送通知可随音频、视频、GIF 和图像一起发送。 

要设置应用程序在 iOS 10 上接收富媒体推送，请完成以下步骤：  

1. 在 Xcode 中，选择**文件** > **新建** > **目标** > **通知服务扩展**。
2. 在 `UNNotificationServiceExtension` 的方法 `didReceive()` 上，添加代码。
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
要从“推送”仪表板发送富媒体 {{site.data.keyword.mobilepushshort}}，请确保您指定消息、标题、子标题和附件 URL 字段。
