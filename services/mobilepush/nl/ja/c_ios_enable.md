---

copyright:
 years: 2015, 2016

---

# iOS アプリケーションによるプッシュ通知受け取りの可能化
{: #enable-push-ios-notifications}
最終更新日: 2016 年 8 月 16 日
{: .last-updated}

iOS アプリケーションでプッシュ通知を受け取り、デバイスにプッシュ通知を送信できるようにすることができます。


##CocoaPods のインストール
{: #enable-push-ios-notifications-install}

既存の Xcode プロジェクトでは、CocoaPods 依存関係管理ツールを使用して Bluemix Mobile Services クライアント SDK をセットアップできます。あるいは、手動で SDK をインストールすることもできます。

**注**: Swift の Push の readme ファイルを確認するには、https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master にアクセスしてください。



1. Mac ターミナルで以下のコマンドを使用して CocoaPods をインストールします。
```
$ sudo gem install cocoapods
```
2. ターミナルで以下のコマンドを入力して CocoaPods を初期化します。このコマンドは、Xcode プロジェクトが位置するディレクトリーから必ず実行してください。`pod init` コマンドはファイルのタイトルを作成します。  
```
$ pod init
```
3. 生成された Podfile に、必要な SDK 依存関係を追加します。設定に応じて、以下のいずれかの Podfile をコピーします。

###Objective-C
   {: objc-sdkdependencies}

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

####Swift
   {: swift-sdkdependencies}

	```
	source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
3. ターミナルで、プロジェクト・フォルダーに移動し、以下のコマンドを使用して依存関係をインストールします。
```
$ pod update
```
このコマンドにより、依存関係がインストールされ、新しい Xcode ワークスペースが作成されます。**注**: 元の Xcode プロジェクト・ファイルではなく、次のように必ず新しい Xcode ワークスペースを開いてください。

 ```
	$ open App.xcworkspace
	```
このワークスペースには、元のプロジェクトと、依存関係が含まれている Pods プロジェクトが含まれています。Bluemix Mobile Services ソース・フォルダーを変更したい場合は、Pods プロジェクト内の `Pods/yourImportedSourceFolder` の下にあります (例えば、`Pods/BMSPush`)。

##Carthage
{: #carthage}

[Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) を使用して、プロジェクトにフレームワークを追加します。 (https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos%29.)

1. `BMSPush` フレームワークを Cartfile に追加します。
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
2. `carthage update` コマンドを実行します。ビルドが完了したら、`BMSPush.framework`、 `BMSCore.framework`、および `BMSAnalyticsAPI.framework` をドラッグして、Xcode プロジェクトに入れます。
3. [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) サイトにある手順に従って、統合を完了します。

##インポートされたフレームワークおよびソース・フォルダーの使用
{: using-imported-frameworks}

コードで SDK を参照します。


####Objective-C
{: objc-import-directives}

関連するヘッダーの #import ディレクティブを記述します。例えば、以下のようにします。

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**注**: CocoaPods コマンド `pod install` または `pod update` を使用して Pods プロジェクトを更新すると、Bluemix Mobile Services のソース・フォルダーがオーバーライドされる可能性があります。元ファイルのカスタマイズしたバージョンを保持する場合は、これらのコマンドのいずれかを発行する前には、それらをバックアップしてください。

####Swift
{: swift-import-directives}

####前提条件
{: prerequisites}

- iOS 8.0 以降
- Xcode 7


関連するヘッダーの #import ディレクティブを記述します。例えば、以下のようにします。

```
//swift
import BMSCore
import BMSPush
```
**重要**: Swift の Push の readme ファイルを確認するには、[Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master) にアクセスしてください。

##ビルド設定
{: build-settings}

**「Xcode」>「ビルド設定」>「ビルド・オプション」に移動し、「Bitcode を使用可能に設定 (Set Enable Bitcode)」**を**「いいえ」**に設定します。

**重要**: iOS 9 現在では、App Transport Security (ATS) 機能に対する変更が、認証プロセスの処理方法に影響する可能性があります。以下のブログ投稿に、変更に関する詳細情報が記載されています。 [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) および [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




## iOS アプリ用の Push SDK の初期化
{: #enable-push-ios-notifications-initialize}

初期化コードを配置する一般的な場所は、iOS アプリケーションのアプリケーション代行内です。Push ダッシュボード内の**「モバイル・オプション」**リンクをクリックして、アプリケーション経路と GUID を取得します。

###Core SDK の初期化
{: Initializing-the-core-sdk}

####Objective-C
{: objc-initialize-core-sdk}

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift
{: swift-initialize-core-sdk}

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

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

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

####AppGUID
{: ios-AppGUID}

Bluemix で作成したプッシュ通知サービスに割り当てられた固有の AppGUID キーを指定します。

###クライアント Push SDK の初期化
{: initializing-the-client-Push-SDK}

####Objective-C
{: objc-initialize-push-sdk}

```
//Initialize client Push SDK for Objective-C
IMFPushClient *push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID"];

```

####Swift
{: swift-initialize-push-sdk}

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID")

```



## iOS アプリケーションとデバイスの登録
{: #enable-push-ios-notifications-register}


アプリケーション (アプリ) でリモート通知を受け取るには、そのアプリケーション (アプリ) をデバイスにインストールした後、APNs に登録する必要があります。アプリは、APNs によって生成されたデバイス・トークンを受け取った後、それを{{site.data.keyword.mobilepushshort}}サービスに送り返す必要があります。

iOS のアプリケーションおよびデバイスを登録するには、以下を行います。

1. バックエンド・アプリケーションの作成
2. {{site.data.keyword.mobilepushshort}}へのトークンの受け渡し


###バックエンド・アプリケーションの作成
{: create-a-backend-app}

Bluemix® カタログの Boilerplates セクションでバックエンド・アプリケーションを作成します。これにより、{{site.data.keyword.mobilepushshort}}サービスはこのアプリケーションに自動的にバインドされます。バックエンド・アプリを既に作成済みの場合は、必ずアプリを{{site.data.keyword.mobilepushshort}}サービスにバインドしてください。

####Objective-C
{: objc-backendapp-code}

```
	//For Objective-C
	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
	    [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
	    [[UIApplication sharedApplication] registerForRemoteNotifications];
	    }
	    else{
	    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
	    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
	    }
	    return YES;
	}
```

####Swift
{: swift-backendapp-code}

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil) UIApplication.sharedApplication().registerUserNotificationSettings(settings) UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```

###{{site.data.keyword.mobilepushshort}}へのトークンの受け渡し
{: pass-token-push-notifications}

トークンを APNs から受け取った後で、`registerWithDeviceToken` メソッドの一部としてそのトークンを{{site.data.keyword.mobilepushshort}}に渡します。

####Objective-C
{: objc-token}

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID"];
[push registerWithDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     NSLog(@"%@",error.description);
  }  else {
    NSLog(@"%@",response.responseJson.description);
}
}];
```

####Swift
{: swift-token}

トークンを APNS から受け取った後で、`didRegisterForRemoteNotificationsWithDeviceToken` メソッドの一部として、そのトークンをプッシュ通知に渡します。

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
  push.initializeWithAppGUID("appGUID")
  push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
  push.initializeWithPushAppGUID("pushAppGUID")
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



## iOS デバイスでのプッシュ通知の受け取り
{: #enable-push-ios-notifications-receiving}

iOS デバイスでプッシュ通知を受け取ります。

####Objective-C
{: objc-receive-push-notifications}

iOS デバイスでプッシュ通知を受け取るには、アプリケーションのアプリケーション代行に以下の Objective-C メソッドを追加します。

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

####Swift
{: swift-receive-push-notifications}
iOS デバイスでプッシュ通知を受け取るには、アプリケーションのアプリケーション代行に以下の Swift メソッドを追加します。

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }

```



## 基本プッシュ通知の送信
{: #send}

アプリケーションを開発したら、(タグ、バッジ、追加のペイロード、音声ファイルを使用することなく) 基本プッシュ通知を送信できます。


1. **「対象者の選択 (Choose the Audience)」**で、**「すべてのデバイス (All Devices)」**、またはプラットフォームに従って**「iOS デバイスのみ (Only iOS devices)」**または**「Android デバイスのみ (Only Anroid devices)」**のいずれかの対象者を選択します。 

	**注**: **「すべてのデバイス (All Devices)」**オプションを選択すると、プッシュ通知をサブスクライブしているすべてのデバイスが通知を受け取ることになります。

![「通知」画面](images/tag_notification.jpg)

2. **「通知の作成 (Create your Notification)」**で、メッセージを入力して、**「送信」**をクリックします。
3. デバイスが通知を受信していることを確認します。次のイメージは、iOS デバイス上のフォアグラウンドおよびバックグラウンドで{{site.data.keyword.mobilepushshort}}を処理しているアラート・ボックスを示しています。

	![Android 上のフォアグラウンドのプッシュ通知](images/iOS_Foreground.jpg)

![iOS 上のフォアグラウンドのプッシュ通知](images/iOS_Screenshot.jpg)




## 次のステップ
{: #next_steps_tags}

基本通知を正常にセットアップしたら、タグ・ベースの通知および詳細オプションの構成を行うことができます。

以下の Push Notifications Service の機能をご使用のアプリに追加します。タグ・ベースの通知を使用する場合は、[タグ・ベースの通知](c_tag_basednotifications.html)を参照してください。拡張通知オプションを使用する場合は、[拡張プッシュ通知](t_advance_notifications.html)を参照してください。
