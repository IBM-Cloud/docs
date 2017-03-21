---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 対話式通知
{: #interactive-notifications}
最終更新日: 2017 年 1 月 23 日
{: .last-updated}

対話式通知により、ユーザーはアプリケーションを開かずに通知に応答することができます。対話式通知が到着すると、デバイスは通知メッセージとともにアクション・ボタンを表示します。対話式通知は、バージョン 8 以降の iOS デバイスでサポートされています。バージョン 8 より前の iOS デバイスに送信された対話式通知については、通知アクションは表示されません。

##対話式{{site.data.keyword.mobilepushshort}}の送信


対話式通知は、Push ダッシュボードを使用するか、[REST API 資料](t_restapi.html)を参照して、送信できます。

{{site.data.keyword.mobilepushshort}} コンソールから以下を実行します。 

1. Push ダッシュボードの通知タブで、**「通知の送信」**をクリックします。 
2. 通知の受信側を選択して、**「次へ」**をクリックします。 
3. 「通知の作成」ページで、「タイプ」を「デフォルト」または「混合」のいずれかに設定し、「詳細オプション」タブの下で「カテゴリー」値を指定することで、対話式プッシュを送信できます。クライアント上でカテゴリー値を構成するには、ネイティブ iOS アプリケーション・セクションで**「対話式{{site.data.keyword.mobilepushshort}}の処理 (Handling interactive {{site.data.keyword.mobilepushshort}})」**にチェック・マークを付けます。

## iOS アプリケーションでの対話式{{site.data.keyword.mobilepushshort}}の処理


### Swift

対話式通知を受け取るには、以下の手順を行います。

1. リモート通知の受信時にバックグラウンド・タスクを実行するアプリケーション機能を使用可能にします。 
1. アクション・カテゴリーで `BMSPush` SDK を初期化します。
	```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: BMSClient.Region.usSouth)
	let push =  BMSPushClient.sharedInstance
    let actionOne = BMSPushNotificationAction(identifierName: "FIRST", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let actionTwo = BMSPushNotificationAction(identifierName: "SECOND", buttonTitle: "Reject", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
   	let notifOptions = BMSPushClientOptions(categoryName: [category])
	push.initializeWithAppGUID(appGUID: "YOUR_APP_GUID", clientSecret:"YOUR_APP_CLIENT_SECRET", options: notifOptions)
	```
		{: codeblock}

1. 以下のように、AppDelegate に新しいコールバック・メソッドを実装します。
	```
	 func userNotificationCenter(_ center: UNUserNotificationCenter,
       didReceive response: UNNotificationResponse,
       withCompletionHandler completionHandler: @escaping () -> Void) {
            switch response.actionIdentifier {
		    case "FIRST":
		      print("FIRST")
		    case "SECOND":
		      print("SECOND")  
		    default:
		      print("Unknown action")
		    }
		completionHandler
	}
	```
	{: codeblock} 
5. ユーザーがアクション・ボタンをクリックすると、この新しいコールバック・メソッドが呼び出されます。このメソッドの実装では、指定の ID に関連付けられたタスクを行い、`completionHandler` パラメーター内のブロックを実行する必要があります。


### Cordova

Cordova iOS アプリケーションで要アクション通知を取得するには、以下のステップを実行します。

1. `BMSPush.initialize` メソッド内にカテゴリー・フィールドを追加します。
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. AppDelegate に新しいコールバック・メソッドを実装します。
3. ユーザーがアクション・ボタンをクリックすると、この新しいコールバック・メソッドが呼び出されます。このメソッドの実装は、指定された ID に関連付けられたタスクを実行し、completionHandler パラメーターでブロックを実行する必要があります。
