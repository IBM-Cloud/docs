---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# リッチ・メディア通知の使用可能化
{: #interactive-notifications}
最終更新日: 2017 年 1 月 11 日
{: .last-updated}


iOS 10 以上でリッチ・メディアの{{site.data.keyword.mobilepushshort}}を有効にすることができます。プッシュ通知は、音声、ビデオ、GIF、およびイメージとともに送信できます。 

iOS 10 でリッチ・プッシュを受信するようにアプリケーションをセットアップするには、以下を実行します。  

1. Xcode で、**「File」** > **「New」** > **「Target」** > **「Notification Service Extension」**を選択します。
2. `UNNotificationServiceExtension` 内のメソッド `didReceive()` に以下のコードを追加します。
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
リッチ・メディアの{{site.data.keyword.mobilepushshort}}を Push ダッシュボードから送信するには、メッセージ、タイトル、サブタイトル、および attachmentURL の各フィールドを指定するようにしてください。
