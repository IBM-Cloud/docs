---

copyright:
 years: 2015, 2016

---

# iOS アプリケーションによるプッシュ通知受け取りの可能化
{: #enable-push-ios-notifications}

iOS アプリケーションによるプッシュ通知の受け取りとデバイスへのプッシュ通知の送信を可能にします。



##CocoaPods のインストール
{: #enable-push-ios-notifications-install}

既存の Xcode プロジェクトでは、CocoaPods 依存関係管理ツールを使用して Bluemix Mobile Services クライアント SDK をセットアップできます。あるいは、手動で SDK をインストールすることもできます。

**注**: Swift の Push の readme ファイルを確認するには、 https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master にアクセスしてください。



1. Mac ターミナルで以下のコマンドを使用して CocoaPods をインストールします。```
$ sudo gem install cocoapods
```
2. ターミナルで以下のコマンドを入力して CocoaPods を初期化します。このコマンドを発行する際には、必ず、Xcode プロジェクトがあるディレクトリーで実行してください。`pod init` コマンドはファイルのタイトルを作成します。
```
$ pod init
```
3. 生成された Podfile に、必要な SDK 依存関係を追加します。以下の Podfile をコピーします。

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
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
このワークスペースには、元のプロジェクトと、依存関係が含まれている Pods プロジェクトが含まれています。Bluemix Mobile Services ソース・フォルダーを変更したい場合は、Pods プロジェクト内の `Pods/yourImportedSourceFolder` の下にあります (例えば、`Pods/IMFGoogleAuthentication`)。

##インポートされたフレームワークおよびソース・フォルダーの使用

コードで SDK を参照します。


### Objective-C

関連するヘッダーの #import ディレクティブを記述します。例えば、以下のようにします。

```
//Objective-C

#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**注**: CocoaPods コマンド `pod install` または `pod update` を使用して Pods プロジェクトを更新すると、Bluemix Mobile Services のソース・フォルダーがオーバーライドされる可能性があります。元ファイルのカスタマイズしたバージョンを保持する場合は、これらのコマンドのいずれかを発行する前には、それらをバックアップしてください。

###Swift

**前提条件**

- iOS 8.0 以降
- Xcode 7


関連するヘッダーの #import ディレクティブを記述します。例えば、以下のようにします。

```
//swift
import BMSCore
import BMSPush
```


##ビルド設定

**「Xcode」>「ビルド設定」>「ビルド・オプション」に移動し、「Bitcode を使用可能に設定 (Set Enable Bitcode)」**を**「いいえ」**に設定します。

**重要**: iOS 9 現在では、App Transport Security (ATS) 機能に対する変更が、認証プロセスの処理方法に影響する可能性があります。以下のブログ投稿に、変更に関する詳細情報が記載されています。 [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) および [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




## iOS アプリ用の Push SDK の初期化
{: #enable-push-ios-notifications-initialize}

初期化コードを配置する一般的な場所は、iOS アプリケーションのアプリケーション代行内です。
Bluemix アプリケーション・ダッシュボード内の**「モバイル・オプション」**リンクをクリックして、アプリケーション経路と GUID を取得します。


###Core SDK の初期化

####Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```


###クライアント Push SDK の初期化

####Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

####Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

### 経路、GUID、および Bluemix の地域

**appRoute**

Bluemix で作成したサーバー・アプリケーションに割り当てられた経路を指定します。

**GUID**

Bluemix で作成したアプリケーションに割り当てられた固有キーを指定します。この値では、大/小文字が区別されます。

**bluemixRegionSuffix**

アプリがホストされている場所を指定します。```bluemixRegion``` パラメーターは、使用する Bluemix デプロイメントを指定します。```BMSClient.REGION`` 静的プロパティーを使用してこの値を設定し、次の 3 つの値のいずれかを使用できます。

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY




## iOS アプリケーションとデバイスの登録
{: #enable-push-ios-notifications-register}


アプリケーション (アプリ) でリモート通知を受け取るには、そのアプリケーション (アプリ) を APNs に登録する必要があります。これは、通常アプリをデバイスにインストールした後で行われます。
アプリは、APNs によって生成されたデバイス・トークンを受け取った後、それを Push Notifications Service に送り返す必要があります。


iOS のアプリケーションおよびデバイスを登録するには、以下を行います。

1. バックエンド・アプリケーションの作成
2. プッシュ通知へのトークンの受け渡し


###バックエンド・アプリケーションの作成

Bluemix® カタログの Boilerplates セクションでバックエンド・アプリケーションを作成します。これにより、プッシュ・サービスはこのアプリケーションに自動的にバインドされます。バックエンド・アプリを既に作成済みの場合は、必ずアプリを Push Notification Service にバインドしてください。


####Objective-C

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

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

###プッシュ通知へのトークンの受け渡し

トークンを APNs から受け取った後で、```registerDevice:withDeviceToken``` メソッドの一部としてそのトークンをプッシュ通知に渡します。

####Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];


 [client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

####Swift

トークンを APNS から受け取った後で、```didRegisterForRemoteNotificationsWithDeviceToken``` メソッドの一部としてそのトークンをプッシュ通知に渡します。

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {print( "Response during device registration : \(response)")
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

###Objective-C
iOS デバイスでプッシュ通知を受け取るには、アプリケーションのアプリケーション代行に以下の Objective-C メソッドを追加します。

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

###Swift
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


基本プッシュ通知の送信を行います。

1. **「対象者の選択 (Choose the Audience)」**で、**「すべてのデバイス (All Devices)」**、またはプラットフォームに従って**「iOS デバイスのみ (Only iOS devices)」**または**「Android デバイスのみ (Only Anroid devices)」**のいずれかの対象者を選択します。 
	**注**: **「すべてのデバイス (All Devices)」**オプションを選択すると、プッシュ通知をサブスクライブしているすべてのデバイスが通知を受け取ることになります。


	![「通知」画面](images/tag_notification.jpg)

2. **「通知の作成 (Create your Notification)」**で、メッセージを入力して、**「送信」**をクリックします。
3. デバイスが通知を受信していることを確認します。

	次のスクリーン・ショットは、Android デバイスおよび iOS デバイス上のフォアグラウンドでプッシュ通知を処理しているアラート・ボックスを示しています。

	![Android 上のフォアグラウンドのプッシュ通知](images/Android_Screenshot.jpg)

	![iOS 上のフォアグラウンドのプッシュ通知](images/iOS_Screenshot.jpg)

	次のスクリーン・ショットは、Android のバックグラウンドでのプッシュ通知を示しています。
	![Android 上のバックグラウンドのプッシュ通知](images/background.jpg)




## 次のステップ
{: #next_steps_tags}

基本通知を正常にセットアップしたら、タグ・ベースの通知および詳細オプションの構成を行うことができます。


以下の Push Notifications Service の機能をご使用のアプリに追加します。タグ・ベースの通知を使用する場合は、[タグ・ベースの通知](c_tag_basednotifications.html)を参照してください。
拡張通知オプションを使用する場合は、[拡張プッシュ通知](t_advance_notifications.html)を参照してください。
