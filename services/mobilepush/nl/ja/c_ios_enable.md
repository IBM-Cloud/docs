---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#iOS アプリケーションによる {{site.data.keyword.mobilepushshort}} の送信の可能化
{: #enable-push-ios-notifications}
最終更新日: 2017 年 2 月 14 日
{: .last-updated}

iOS アプリケーションによる、デバイスへの {{site.data.keyword.mobilepushshort}} の送信を可能にすることができます。


##CocoaPods のインストール
{: #enable-push-ios-notifications-install}

既存の Xcode プロジェクトでは、CocoaPods 依存関係管理ツールを使用して Bluemix Mobile サービス・クライアント SDK をセットアップできます。あるいは、手動で SDK をインストールすることもできます。

Swift の Push の README ファイルを表示するには、[README ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}を参照してください。



1. Mac ターミナルで以下のコマンドを使用して CocoaPods をインストールします。
```$ sudo gem install cocoapods
```
	{: codeblock}
2. ターミナルで `pod init` コマンドを入力して、CocoaPods を初期化します。このコマンドは、Xcode プロジェクトが位置するディレクトリーから必ず実行してください。`pod init` コマンドによって Podfile が作成されます。  
3. 生成された Podfile に、必要な SDK 依存関係を追加します。以下の Podfile をコピーします。
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
		//Copy the following list as is and remove the dependencies you do not need.
		use_frameworks!
		target 'MyApp' do
		platform :ios, '8.0'
		pod 'BMSCore'
		pod 'BMSPush'
		pod 'BMSAnalyticsAPI' end
	```
		{: codeblock}

3. ターミナルで、プロジェクト・フォルダーに移動し、`pod update` コマンドを使用して依存関係をインストールします。

このコマンドにより、依存関係がインストールされ、新規 Xcode ワークスペースが作成されます。  
**注**: 元の Xcode プロジェクト・ファイルではなく、次のように必ず新しい Xcode ワークスペースを開いてください。
```
  $ open App.xcworkspace
```
	{: codeblock}

このワークスペースには、元のプロジェクトと、依存関係が含まれている Pods プロジェクトが含まれています。Bluemix モバイル・サービスのソース・フォルダーを変更する場合は、Pods プロジェクト内の `Pods/yourImportedSourceFolder` の下にあります (例えば、`Pods/BMSPush`)。

##Carthage を使用したフレームワークの追加
{: #carthage}

[Carthage ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}を使用してプロジェクトにフレームワークを追加します。Xcode8 の Carthage はサポートされません。

1. `BMSPush` フレームワークを Cartfile に追加します。
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. `carthage update` コマンドを実行します。ビルドが完了したら、`BMSPush.framework`、 `BMSCore.framework`、および `BMSAnalyticsAPI.framework` をドラッグして、Xcode プロジェクトに入れます。
3. [Carthage ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}サイトの説明に従って統合を完了してください。

##iOS SDK のセットアップ
{: ios-sdk}

iOS SDK をセットアップするには、以下のコードをアプリケーション内の **AppDelegate.swift** ファイルに追加します。これによって APNs にも登録されることに注意してください。  
```
  func application(_ application: UIApplication,
  didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool
   {
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

##インポートされたフレームワークおよびソース・フォルダーの使用
{: using-imported-frameworks}

コードで SDK を参照します。以下の前提条件を満たしていることを確認してください。

- iOS 8.0 以降	
- Xcode 7

関連するヘッダーの `#import` ディレクティブを記述します。例えば、以下のようにします。
```
//swift
 import BMSCore
 import BMSPush
```
		{: codeblock}

Swift の Push の README ファイルを読むには、[README ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}を参照してください。

**注**: CocoaPods コマンド `pod install` または `pod update` を使用して Pods プロジェクトを更新すると、Bluemix モバイル・サービスのソース・フォルダーがオーバーライドされる可能性があります。元ファイルのカスタマイズしたバージョンを保持する場合は、これらのコマンドのいずれかを発行する前には、それらをバックアップしてください。


##ビルド設定
{: build-settings}

**「Xcode」>「ビルド設定」>「ビルド・オプション」に移動し、「Bitcode を使用可能に設定 (Set Enable Bitcode)」**を**「いいえ」**に設定します。

**重要**: iOS 9 現在では、App Transport Security (ATS) 機能に対する変更が、認証プロセスの処理方法に影響する可能性があります。次のブログ投稿にこれらの変更の詳細な情報が記載されています: [ATS and Bitcode in iOS 9 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window}および [Connect your iOS 9 app to Bluemix today ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}を参照してください。

## iOS アプリ用の Push SDK の初期化
{: #enable-push-ios-notifications-initialize}

初期化コードを配置する一般的な場所は、iOS アプリケーションのアプリケーション代行内です。Push ダッシュボード内の**「モバイル・オプション」**リンクをクリックして、アプリケーション経路と GUID を取得します。

###Core SDK の初期化
{: Initializing-the-core-sdk}


```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.")
```
	{: codeblock}

### 経路、GUID、および Bluemix の地域
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

Bluemix で作成したサーバー・アプリケーションに割り当てられた経路を指定します。

####GUID
{: ios-guid}

Bluemix で作成したアプリケーションに割り当てられた固有キーを指定します。この値では、大/小文字が区別されます。

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

アプリがホストされている場所を指定します。`bluemixRegion` パラメーターでは、使用する Bluemix デプロイメントを指定します。`BMSClient.REGION` 静的プロパティーを使用してこの値を設定し、次の 3 つの値のいずれかを使用できます。

- BMSClient.Region.usSouth 
- BMSClient.Region.unitedKingdom
- BMSClient.Region.sydney

####AppGUID
{: ios-AppGUID}

Bluemix で作成した{{site.data.keyword.mobilepushshort}}サービスに割り当てられた固有の AppGUID キーを指定します。

###クライアント Push SDK の初期化
{: initializing-the-client-Push-SDK}

```
	//Initialize client Push SDK for Swift
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


## iOS アプリケーションとデバイスの登録
{: #enable-push-ios-notifications-register}


アプリケーションでリモート通知を受け取るには、アプリケーションをデバイスにインストールした後、APNs に登録する必要があります。アプリは、APNs によって生成されたデバイス・トークンを受け取った後、それを{{site.data.keyword.mobilepushshort}}サービスに送り返す必要があります。

iOS のアプリケーションおよびデバイスを登録するには、以下を行う必要があります。

1. バックエンド・アプリケーションを作成します。
2. トークンを {{site.data.keyword.mobilepushshort}} に渡します。


###バックエンド・アプリケーションの作成
{: create-a-backend-app}

Bluemix® カタログの Boilerplates セクションでバックエンド・アプリケーションを作成します。これにより、{{site.data.keyword.mobilepushshort}} サービスはこのアプリケーションに自動的にバインドされます。バックエンド・アプリを既に作成済みの場合は、必ずそのアプリを {{site.data.keyword.mobilepushshort}} サービスにバインドしてください。


###{{site.data.keyword.mobilepushshort}}へのトークンの受け渡し
{: pass-token-push-notifications}

トークンを APNs から受け取った後で、`registerWithDeviceToken` メソッドの一部としてそのトークンを{{site.data.keyword.mobilepushshort}}に渡します。

トークンを APNs から受け取った後で、`didRegisterForRemoteNotificationsWithDeviceToken` メソッドの一部として、そのトークンをプッシュ通知に渡します。

```
  func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
           print( "status code during device registration : \(statusCode)")
      }
       else{
           print( "Error during device registration \(error) ")
           print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
       }
   }
  }
```
	{: codeblock}


## iOS デバイスでのプッシュ通知の受け取り
{: #enable-push-ios-notifications-receiving}


iOS デバイスでプッシュ通知を受け取るには、アプリケーションのアプリケーション代行に以下の Swift メソッドを追加します。

```
  // For Swift
  func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void)
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

## iOS デバイスでのプッシュ通知のモニター
{: ios-monitoring}

通知の現在の状況をモニターするには、アプリケーションのアプリケーション代行に以下の Swift メソッドを追加します。

```
	// Send notification status when app is opened by clicking the notifications
	func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
 	let push =  BMSPushClient.sharedInstance
 	let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 	let data = respJson.data(using: String.Encoding.utf8)
 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 	let messageId:String = jsonResponse.value(forKey: "nid") as! String
    push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
      print("Send message status to the Push server")
     }
}
```
	{: codeblock}

```
	// Send notification status when the app is in background mode.
	func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 	let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
 	self.showAlert(title: "Recieved Push notifications", message: payLoad)
 	let push =  BMSPushClient.sharedInstance
 	let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 	let data = respJson.data(using: String.Encoding.utf8)
 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 	let messageId:String = jsonResponse.value(forKey: "nid") as! String
 	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
   }
}
```
	{: codeblock}


## 基本プッシュ通知の送信
{: #send}

アプリケーションの開発が完了したら、基本プッシュ通知を送信できます。

基本プッシュ通知を送信するには、以下の手順を実行します。

1. **「通知の送信 (Send Notifications)」**を選択し、**「送信先 (Send To)」**オプションを選択することでメッセージを構成します。サポートされるオプションは、**「タグ指定によるデバイス (Device by Tag)」**、**「デバイス ID (Device Id)」**、**「ユーザー ID」**、**「Android デバイス (Android devices)」**、**「iOS デバイス (iOS devices)」**、**「Web 通知 (Web Notifications)」**、および**「すべてのデバイス」**です。  
**注**: **「すべてのデバイス」**オプションを選択すると、{{site.data.keyword.mobilepushshort}}をサブスクライブしているすべてのデバイスが通知を受け取ることになります。
![「通知」画面](images/tag_notification.jpg)

2. **「メッセージ」**フィールドで、メッセージを構成します。必要に応じてオプションの設定を構成してください。
3. **「送信」**をクリックします。
3. デバイスが通知を受信していることを確認します。

次のイメージは、iOS デバイス上で{{site.data.keyword.mobilepushshort}}を処理しているアラート・ボックスを示しています。

![iOS 上のフォアグラウンドのプッシュ通知](images/iOS_Screenshot.jpg) 

### 通知を送信するためのオプションの設定
{: #send_ios_otpional_setting}

iOS デバイスに通知を送信するための{{site.data.keyword.mobilepushshort}}設定をさらに詳細にカスタマイズできます。以下の任意指定のカスタマイズ・オプションがサポートされます。

- **バッジ**: アプリケーション・バッジに表示される数値を示します。デフォルト値はゼロ (0) で、この場合、バッジは表示されません。 
- **音 (Sound)**: 通知の受信時に音声クリップを再生するかどうかを示します。デフォルト、またはアプリにバンドルされている音声リソースの名前がサポートされます。
- **追加のペイロード (Additional payload)**: 通知用のカスタム・ペイロードの値を指定します。

##対話式通知の使用可能化

対話式通知を使用可能にすることにより、イメージ、マップ、応答ボタンを追加するなど、より詳細な機能を iOS 通知に持たせることができるようになりました。これによって、より多くのコンテキストをお客様に提供するとともに、現行コンテキストから離れることなく、即時にアクションを取ることができます。  

対話式通知を使用可能にするには、以下のコードを使用します。

```
	// This defines the button action.
	let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 	let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
	{: codeblock}
```
	// This defines category for the buttons
	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
```
	{: codeblock}
```
	// This updates the registration to include the buttonsPass the defined category into iOS BMSPushClientOptions
	let notificationOptions = BMSPushClientOptions(categoryName: [category])
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
```
	{: codeblock}

対話式通知を送信するには、以下の手順を実行します。

1. 「構成 (Compose)」セクションで、「送信先 (Send To)」ドロップダウン・リストに、**「iOS Devices (iOS デバイス)」**を選択します。
2. 送信する通知メッセージを入力します。
3. 「オプション設定 (Optional Settings)」セクションで、**「モバイル」**を選択して、**「iOS」** をクリックします。
4. 「タイプ」ドロップダウン・リストで、**「混合」**を選択します。
5. 「カテゴリー」フィールドに、アプリで定義した通知タイプを指定します。 

![iOS 用の対話式通知](images/push_ios_notification_interactive.jpg) 

## 次のステップ
{: #next_steps_tags}

基本通知を正常にセットアップしたら、タグ・ベースの通知および詳細オプションの構成を行うことができます。

以下の Push Notifications Service の機能をご使用のアプリに追加します。タグ・ベースの通知を使用する場合は、[タグ・ベースの通知](c_tag_basednotifications.html)を参照してください。拡張通知オプションを使用する場合は、[拡張プッシュ通知の使用可能化](t_advance_badge_sound_payload.html)を参照してください。
