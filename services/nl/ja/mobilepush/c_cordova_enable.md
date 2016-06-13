---

copyright:
 years: 2015, 2016

---

# Cordova アプリケーションによるプッシュ通知受け取りの可能化
{: #cordova_enable}

Cordova は、JavaScript、CSS、および HTML を使用したハイブリッド・アプリケーションの構築用プラットフォームです。
{{site.data.keyword.mobilepushshort}} は、Cordova ベースの iOS アプリケーションおよび Android アプリケーションの開発をサポートします。

Cordova アプリケーションによるプッシュ通知の受け取りとデバイスへのプッシュ通知の送信を可能にします。





## Cordova の Push プラグインのインストール
{: #cordova_install}

Cordova アプリケーションをさらに開発するために、クライアントの Push プラグインをインストールして使用します。これにより、Cordova Core のプラグインもインストールされます。これは、Bluemix への接続を初期化するものです。


### 始めに

1. 最新バージョンの Android Studio SDK と Xcode をダウンロードします。
1. エミュレーターをセットアップします。Android Studio では、Google Play API をサポートするエミュレーターを使用します。
1. Git のコマンド・ライン・ツールをインストールします。Windows では、必ず **「Windows コマンド・プロンプトから Git を実行する (Run Git from the Window Command Prompt)」**オプションを選択してください。このツールのダウンロードとインストールの方法については、[Git](https://git-scm.com/downloads) を参照してください。

1. Node.js と Node Package Manager (NPM) ツールをインストールします。NPM コマンド・ライン・ツールは Node.js とバンドルされています。Node.js のダウンロードとインストールの方法については、[Node.js](https://nodejs.org/en/download/) を参照してください。
1. コマンド・ラインから、**npm install -g cordova** コマンドを使用して、Cordova コマンド・ライン・ツールをインストールします。これは、Cordova の Push プラグインを使用するために必要です。
Cordova のインストールと Cordova アプリのセットアップの方法については、[Cordova Apache](https://cordova.apache.org/#getstarted) を参照してください。

 **注**: Cordova の Push プラグインの readme ファイルを確認する場合は、[https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push) にアクセスしてください。

1. Cordova アプリを作成するフォルダーに移動し、次のコマンドを実行して Cordova アプリケーションを作成します。
既存の Cordova アプリがある場合は、ステップ 3 に進みます。


 ```
cordova create your_app_name
	cd your_app_name
	```
1. オプション: (オプション) **config.xml** ファイルを編集し、<name> エレメント内のアプリケーション名を、デフォルトの HelloCordova という名前ではなく、自分で選択した名前に変更します。

	**注**: 正しいバンドル ID を指定してください。正しいバンドル ID を指定しないと、Xcode に次のエラー・メッセージが表示されます。
	* 実行可能ファイルの署名に使用された資格が無効です (The executable was signed with invalid entitlements.) 
	* アプリケーションのコード署名資格ファイルに指定された資格が、プロビジョニング・プロファイルに指定された資格と一致しません (The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile.)

	この問題を修正するには、Xcode または Cordova アプリ **config.xml** ファイルに正しいバンドル ID を指定します。

1. サポートされる最低レベルの API またはデプロイメント・ターゲット (Deployment Target) の宣言を、Cordova アプリケーションの config.xml ファイルに追加します。minSdkVersion の値は、15 より高くなければなりません。targetSdkVersion の値は、常に、Google から入手可能な最新の Android SDK を反映している必要があります。
	* **Android** - ご使用のエディターで config.xml ファイルを開き、```<platform name="android">``` エレメントを最低レベルのターゲット SDK バージョンに更新します。

	```
	<!-- add deployment target declaration -->
	<platform name="android">    
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - <platform name="ios"> エレメントを、デプロイメント・ターゲット (Deployment Target) の宣言で更新します。

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Cordova コマンド・ライン・インターフェース (CLI) から、以下のコマンドを使用して、プラットフォーム (iOS、Android、またはその両方) を追加します。

	```
	cordova platform add ios@3.9.0
	cordova platform add android
	```
1. Cordova アプリケーションのルート・ディレクトリーで、以下のコマンドを入力して Cordova の Push プラグイン **cordova plugin add ibm-mfp-push** をインストールします。

	追加したプラットフォームに応じて、以下のような内容が表示されます。


	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. *your-app-root-folder* から、コマンド **cordova plugin list** を使用して、Cordova の Core および Push のプラグインが正常にインストールされたことを確認します。

	追加したプラットフォームに応じて、以下のような内容が表示されます。


	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (iOS のみ) - iOS 開発環境を構成します。a. Xcode を使用して、*your-app-name***/platforms/ios** ディレクトリーにある your-app-name.xcodeproj ファイルを開きます。

	b. ブリッジング・ヘッダーを追加します。**「ビルド設定」>「Swift コンパイラー - コード生成」>「 Objective-C ブリッジング・ヘッダー」**に移動し、パス *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h** を追加します。

	c. Frameworks パラメーターを追加します。**「ビルド設定」>「 リンク」>「実行パス検索パス (Runpath Search Paths)」**に移動し、以下のパラメーターを追加します。```
	@executable_path/Frameworks
	```
	d. ブリッジング・ヘッダーの以下の Push インポート・ステートメントをアンコメントします。 *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h** に移動します。

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Xcode で、アプリケーションをビルドして実行します。
1. (Android のみ)- コマンド **cordova build android** を使用して、Android プロジェクトをビルドします。

	**注**: Android Studio でプロジェクトを開く前に、最初に Cordova CLI を使用して Cordova アプリケーションをビルドする必要があります。そうしないと、ビルド・エラーが発生します。


## Cordova プラグインの初期化
{: #cordova_initialize}

Push Notification Service の Cordova プラグインを使用するには、事前に、アプリケーション経路とアプリケーション GUID を受け渡すことでプラグインを初期化しておく必要があります。
プラグインを初期化したら、Bluemix ダッシュボードで作成したサーバー・アプリに接続することができます。Cordova プラグインは、Cordova アプリが Bluemix サービスと通信できるようにするための Android および iOS のクライアント SDK のラッパーです。

1. 以下のコード・スニペットをメイン JavaScript ファイル (通常、**www/js** ディレクトリーの下にある) にコピー・アンド・ペーストして、BMSClient を初期化します。

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");```
1. Bluemix の Route パラメーターと appGUID パラメーターを使用するように、コード・スニペットを変更します。Bluemix アプリケーション・ダッシュボード内の**「モバイル・オプション」**リンクをクリックして、アプリケーション経路とアプリ GUID を取得します。この経路とアプリ GUID の値を、```BMSClient.initialize``` コード・スニペットのパラメーターとして使用します。

	**注**: Cordova CLI (例えば、Cordova の create app-name コマンド) を使用して Cordova アプリを作成した場合、この Javascript コードを **index.js** ファイルの ```nDeviceReady: function()``` 機能内の ```app.receivedEvent`` 機能の後に置いて、BMS クライアントを初期化します。

```
onDeviceReady: function() {
    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```

## デバイスの登録
{: #cordova_register}

デバイスを Push Notification Service に登録するには、登録メソッドを呼び出します。

デバイスを登録するには、次のコード・スニペットを Cordova アプリケーションにコピーして貼り付けます。


```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

### Android
{: #cordova_register_android}
Android では、settings パラメーターを使用しません。Android アプリのみをビルドする場合は、空のオブジェクトを受け渡します。例えば、次のようにします。

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

### iOS
{: #cordova_register_ios}
アラート、バッジ、および音声のプロパティーをカスタマイズする場合は、次の JavaScript コード・スニペットを Cordova アプリケーションの Web パーツに追加します。


```
	var settings = {
	   ios: {
             alert: true,
             badge: true,
             sound: true
         }}
	MFPPush.registerDevice(settings, success, failure);
```



### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);```

次のように JSON.parse を使用して、Javascript 内の成功した応答パラメーターの内容にアクセスできます。
**var token = JSON.parse(response).token**


使用可能なキーは、```token```、```userId``、および ```deviceId`` です。

以下の JavaScript コード・スニペットは、Bluemix Mobile Services クライアント SDK を初期化し、デバイスを Push Notification Service に登録し、プッシュ通知を listen する方法を示しています。このコードを Javascript ファイルに置きます。



```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```

```
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

コードは **onDeviceReady: function()** 内に置きます。

```
onDeviceReady: function() {
     app.receivedEvent('deviceready');
     BMSClient.initialize("https://http://myroute_mybluemix.net","my_appGuid");
     var success = function(message) { console.log("Success: " + message); };
     var failure = function(message) { console.log("Error: " + message); };
     var settings = {
         ios: {
             alert: true,
             badge: true,
             sound: true
         }   
     };
     MFPPush.registerDevice(settings, success, failure);
     var notification = function(notif){
         alert (notif.message);
     };
     MFPPush.registerNotificationsCallback(notification);

 }
```

### Objective-C
{: #cordova_register_objective}
アプリケーション代行クラスに次の Objective-C コード・スニペットを追加します。

```
	// Register the device token with Bluemix Push Notification Service

	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

###Swift
{: #cordova_register_swift}
アプリケーション代行クラスに次の Swift コード・スニペットを追加します。

```     
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
// Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
   CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

##次のステップ

{: #cordova_register_next}

プロジェクトをビルドし、以下のコマンドを使用してプロジェクトを実行します。

	* Android - **cordova build android** および **cordova run android**

	* iOS - **cordova build ios** および **cordova run ios**



## デバイスでのプッシュ通知の受け取り
{: #cordova_receive}

デバイスでプッシュ通知を受け取るには、以下のコード・スニペットをコピーして貼り付けます。


###JavaScript

以下の JavaScript コード・スニペットを Cordova アプリケーションの Web パーツに追加します。



```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

###Android 通知プロパティー

次のセクションに、Android の通知プロパティーをリストします。

* message - プッシュ通知メッセージ
* payload - 通知ペイロードを含む JSON オブジェクト


###iOS 通知プロパティー

次のセクションに、iOS の通知プロパティーをリストします。

* message - プッシュ通知メッセージ
* payload - 通知ペイロードを含む JSON オブジェクト。
action-loc-key - このストリングは、現行ローカリゼーションにおいて、「View」の代わりに右ボタンのタイトルに使用されるローカライズされたストリングを取得するためのキーとして使用されます。
* badge - アプリ・アイコンのバッジとして表示する数。このプロパティーがないと、バッジは変更されません。
バッジを削除するには、このプロパティーの値を 0 に設定します。

* sound - アプリ・バンドル内、またはアプリ・データ・コンテナーの Library/Sounds フォルダー内にある音声ファイルの名前。


###Objective-C

アプリケーション代行クラスに次の Objective-C コード・スニペットを追加します。

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

###Swift

アプリケーション代行クラスに次の Swift コード・スニペットを追加します。

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```


{: #push-send-notifications}
## 基本プッシュ通知の送信


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
