------

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# iOS のサイレント通知の処理
{: #silent-notifications}
最終更新日: 2017 年 1 月 16 日
{: .last-updated}

サイレント通知は、デバイスの画面に表示されません。これらの通知は、アプリケーションがバックグラウンドで受け取ります。その結果、アプリケーションは最大で 30 秒までウェイク状態になり、指定されたバックグラウンド・タスクを実行します。ユーザーは、この通知の着信に気付かない可能性があります。iOS のサイレント通知を送信するには、[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を使用します。   

1. サイレント・プッシュ通知を送信するには、プロジェクトの `appDelegate.m` ファイルで以下のメソッドを実装します。Swift では、サーバーから送信される、サイレント通知の `contentAvailable` 値は 1 になります。
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

