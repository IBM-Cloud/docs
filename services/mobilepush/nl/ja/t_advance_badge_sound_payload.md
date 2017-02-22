---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#拡張プッシュ通知の使用可能化
最終更新日: 2017 年 1 月 11 日
{: .last-updated}

iOS バッジ、音声、追加の JSON ペイロード、アクション可能通知、および保留通知を構成します。

## 音声、ペイロード、および iOS バッジの構成
{: #badge-sound-payload}

iOS のバッジ、音声、および追加の JSON ペイロードを構成します。

1. {{site.data.keyword.mobilepushshort}}ダッシュボードで、**「通知」**タブに移動します。
2. **「オプション・フィールド」**セクションに移動して、{{site.data.keyword.mobilepushshort}}機能を構成します。 
	- **音声ファイル (Sound File)** - モバイル・アプリの音声ファイルを指定するストリングを入力します。ペイロードで、使用する音声ファイルのストリング名を指定します。
	- **iOS バッジ (iOS Badge)** - iOS デバイスにアプリ・アイコンのバッジとして表示する数。このプロパティーがないと、バッジは変更されません。バッジを削除するには、このプロパティーの値を 0 に設定します。
	
###Android

Android アプリケーションの `res/raw` ディレクトリーに音声ファイルを追加します。通知の送信中に、{{site.data.keyword.mobilepushshort}}の音声フィールドに音声ファイル名を追加します。

```
"settings":{
     "gcm":{
     "sound":"tt.wav",
  }
 }  
```
    {: codeblock}	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
      "sound": "tt.wav",
  }
}
``` 
	{: codeblock}
		
**追加のペイロード** - このペイロードは、任意のキーと値のペアにすることができますが、{{site.data.keyword.mobilepushshort}}で送信する JSON オブジェクトでなければなりません。 

```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## Android 通知の保留 
{: #hold-notifications-android}

アプリケーションがバックグラウンドになる場合に、アプリケーションに送信された通知を{{site.data.keyword.mobilepushshort}}に保留させたいことがあります。通知を保留するには、{{site.data.keyword.mobilepushshort}}を処理しているアクティビティーの onPause() メソッドで hold() メソッドを呼び出します。

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}
## iOS アクション可能通知の使用可能化  
{: #enable-actionable-notifications-ios}

従来の{{site.data.keyword.mobilepushshort}}とは異なり、アクション可能通知は、通知アラートを受け取る際にアプリを開くことなく選択を行うようにユーザーにプロンプトを出します。 

アプリケーションでアクション可能{{site.data.keyword.mobilepushshort}}を使用可能にするには、以下の手順を行います。

1. ユーザー応答アクションを作成します。
```
//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground
```
	{: codeblock}
```
//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
```
	{: codeblock}

2. 通知カテゴリーを作成し、アクションを設定します。**UIUserNotificationActionContextDefault** または **UIUserNotificationActionContextMinimal** が有効なコンテキストです。
```
// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. 通知設定を作成し、前のステップのカテゴリーを割り当てます。
```
// For Swift
	let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. ローカル通知またはリモート通知を作成し、その通知にカテゴリーの ID を割り当てます。
```
//For Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications()
```
	{: codeblock}
	
## アクション可能 iOS 通知の処理  
{: #actionable-notifications}

要アクション通知を受け取ると、選択した ID に基づいて制御が以下のメソッドに渡されます。

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
