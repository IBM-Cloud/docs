------

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 处理针对 iOS 的静默通知
{: #silent-notifications}
上次更新时间：2017 年 1 月 16 日
{: .last-updated}

静默通知不会显示在设备屏幕上。这些通知由应用程序在后台进行接收，这会将应用程序唤醒最多 30 秒来执行指定的后台任务。用户可能并不知道有通知到达。要针对 iOS 发送静默通知，请使用 [REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobile.{DomainName}/imfpush/ "外部链接图标 "){: new_window}。   

1. 要发送静默推送通知，请在项目的 `appDelegate.m` 文件中实施以下方法。在 Swift 中，服务器针对静默通知发送的 `contentAvailable` 值等于 1。
```
//For Swift
	 func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       let contentAPS = userInfo["aps"] as [NSObject : AnyObject]
       if let contentAvailable = contentAPS["content-available"] as? Int {
           //silent or mixed push
           if contentAvailable == 1 {
               completionHandler(UIBackgroundFetchResult.NewData)
           } else {
               completionHandler(UIBackgroundFetchResult.NoData)
           }
       } else {
   //Default notification
           completionHandler(UIBackgroundFetchResult.NoData)
       }
    }
```
	{: codeblock}

