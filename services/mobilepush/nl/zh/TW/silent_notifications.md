------

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 處理 iOS 的無聲自動通知
{: #silent-notifications}
前次更新：2017 年 1 月 16 日
{: .last-updated}

無聲自動通知不會出現在裝置畫面上。這些通知由應用程式在背景接收，此情況會喚醒應用程式最多達 30 秒，以執行指定的背景作業。使用者可能不知道有通知送達。若要傳送 iOS 的無聲自動通知，請使用 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/){: new_window}。   

1. 在專案中，若要傳送無聲自動推送通知，請在 `appDelegate.m` 檔案中實作下列方法。在 Swift 中，伺服器針對無聲自動通知而傳送的 `contentAvailable` 值等於 1。
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

