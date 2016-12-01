---

copyright:
 years: 2015, 2016

---

# Cordova アプリケーションによるプッシュ通知受け取りの可能化
{: #cordova_enable}
最終更新日: 2016 年 10 月 17 日
{: .last-updated}

Cordova は、JavaScript、CSS、および HTML を使用したハイブリッド・アプリケーションの構築用プラットフォームです。
{{site.data.keyword.mobilepushshort}} は、Cordova ベースの iOS アプリケーションおよび Android アプリケーションの開発をサポートします。

Cordova アプリケーションによる、デバイスでのプッシュ通知の受信を可能にすることができます。

## Cordova の Push プラグインのインストール
{: #cordova_install}

Cordova アプリケーションをさらに開発するために、クライアントの Push プラグインをインストールして使用します。これにより、Bluemix への接続を初期化する Cordova の Core プラグインもインストールされます。

### 始めに

1. 最新バージョンの Android Studio SDK と Xcode をダウンロードします。
1. エミュレーターをセットアップします。Android Studio では、Google Play API をサポートするエミュレーターを使用します。
1. Git のコマンド・ライン・ツールをインストールします。Windows では、必ず **「Windows コマンド・プロンプトから Git を実行する (Run Git from the Window Command Prompt)」**オプションを選択してください。このツールのダウンロードとインストールの方法については、[Git](https://git-scm.com/downloads) を参照してください。
1. Node.js と Node Package Manager (NPM) ツールをインストールします。NPM コマンド・ライン・ツールは Node.js とバンドルされています。Node.js のダウンロードとインストールの方法については、[Node.js](https://nodejs.org/en/download/) を参照してください。
1. コマンド・ラインから、**npm install -g cordova** コマンドを使用して、Cordova コマンド・ライン・ツールをインストールします。これは、Cordova の Push プラグインを使用するために必要です。Cordova のインストールと Cordova アプリのセットアップの方法については、[Cordova Apache](https://cordova.apache.org/#getstarted) を参照してください。詳しくは、Cordova プッシュ・プラグインの [Readme ファイル](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)を参照してください。
1. Cordova アプリを作成するフォルダーに移動し、次のコマンドを実行して Cordova アプリケーションを作成します。
既存の Cordova アプリがある場合は、ステップ 3 に進みます。

```
cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- オプション: **config.xml** ファイルを編集して、<name> エレメントのアプリケーション名を、デフォルトの HelloCordova という名前ではなく、自分で選択した名前に変更できます。

正しいバンドル ID を指定してください。誤ったバンドル ID を指定すると、Xcode で以下のエラー・メッセージが出されることがあります。

* 実行可能ファイルの署名に使用された資格が無効です (The executable was signed with invalid entitlements.) 
* アプリケーションのコード署名資格ファイルに指定された資格が、プロビジョニング・プロファイルに指定された資格と一致しません (The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile.)この問題を修正するには、Xcode または Cordova アプリ **config.xml** ファイルに正しいバンドル ID を指定します。

1. サポートされる最低レベルの API またはデプロイメント・ターゲット (Deployment Target) の宣言を、Cordova アプリケーションの config.xml ファイルに追加します。minSdkVersion の値は、15 より高くなければなりません。targetSdkVersion の値は、常に、Google から入手可能な最新の Android SDK を反映している必要があります。
	
	* Android - ご使用のエディターで config.xml ファイルを開き、`<platform name="android">` エレメントを最低レベルのターゲット SDK バージョンに更新し、

```
< !-- add deployment target declaration -->
デプロイメント・ターゲット宣言 <preference name="android-minSdkVersion" value="15" />
  <preference name="android-targetSdkVersion" value="23" />
</platform> を追加します。
```
    {: codeblock}

   * iOS - <platform name="ios"> エレメントを、以下のデプロイメント・ターゲット宣言を使用して更新します。

```
<platform name ="ios">
<preference name=deployment-target" value="8.0" /> <!-- other properties -->
</ platform>
```
	{: codeblock}

1. Cordova コマンド・ライン・インターフェース (CLI) から、以下のコマンドを使用して、プラットフォーム (iOS、Android、またはその両方) を追加します。
```
cordova platform add ios
cordova platform add android
```
	{: codeblock}

1. Cordova アプリケーションのルート・ディレクトリーで、コマンド **cordova plugin add ibm-mfp-push** を入力して Cordova の Push プラグインをインストールします。追加したプラットフォームに応じて、以下のような内容が表示されます。
```
Installing "ibm-mfp-push" for android
Installing "ibm-mfp-push" for ios
```
	{: codeblock}

1. *your-app-root-folder* から、コマンド **cordova plugin list** を使用して、Cordova の Core および Push のプラグインが正常にインストールされたことを確認します。追加したプラットフォームに応じて、以下のような内容が表示されます。
```
ibm-mfp-core 1.0.0 "MFPCore"
ibm-mfp-push 1.0.0 “MFPPush"
```
	{: codeblock}

1. (iOS のみ) - iOS 開発環境を構成します。
2. 以下のサブステップを実行します。

 a. Xcode を使用して、*your-app-name***/platforms/ios** ディレクトリーにある your-app-name.xcodeproj ファイルを開きます。

 b. ブリッジング・ヘッダーを追加します。**「ビルド設定」>「Swift コンパイラー - コード生成」>「 Objective-C ブリッジング・ヘッダー」**に移動し、パス *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h** を追加します。

 c. Frameworks パラメーターを追加します。**「ビルド設定」>「 リンク」>「実行パス検索パス (Runpath Search Paths)」**に移動し、`@executable_path/Frameworks` パラメーターを追加します。

 d. ブリッジング・ヘッダーの以下の Push インポート・ステートメントをアンコメントします。 *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h** に移動します。

```
//#import <IMFPush/IMFPush.h>
//#import <IMFPush/IMFPushClient.h>
//#import <IMFPush/IMFResponse+IMFPushCategory.h>
```
	{: codeblock}

 e. Xcode で、アプリケーションをビルドして実行します。

1. (Android のみ)- コマンド **cordova build android** を使用して、Android プロジェクトをビルドします。

	**注**: Android Studio でプロジェクトを開く前に、Cordova CLI を使用して Cordova アプリケーションをビルドしてください。これは、ビルド・エラーの回避に有効です。


## Cordova プラグインの初期化
{: #cordova_initialize}

{{site.data.keyword.mobilepushshort}}サービスの Cordova プラグインを使用するには、事前に、アプリケーション経路とアプリケーション GUID を受け渡すことでプラグインを初期化しておく必要があります。プラグインを初期化したら、Bluemix ダッシュボードで作成したサーバー・アプリに接続することができます。Cordova プラグインは、Cordova アプリが Bluemix サービスと通信できるようにするための Android および iOS のクライアント SDK のラッパーです。

1. 以下のコード・スニペットをメイン JavaScript ファイル (通常、**www/js** ディレクトリーの下にある) にコピー・アンド・ペーストして、BMSClient を初期化します。

```
BMSClient.initialize("https://myapp.mybluemix.net","App GUID");
```
	{: codeblock}

1. Bluemix の Route パラメーターと appGUID パラメーターを使用するように、コード・スニペットを変更します。Push ダッシュボード内の**「モバイル・オプション」**リンクをクリックして、アプリの経路、アプリ GUID、およびクライアント秘密鍵を取得します。この経路とアプリ GUID の値を、`BMSClient.initialize` コード・スニペットのパラメーターとして使用します。

	**注**: Cordova CLI (例えば、Cordova の create app-name コマンド) を使用して Cordova アプリを作成した場合、この Javascript コードを **index.js** ファイルの `onDeviceReady: function()` 関数内の `app.receivedEvent` 関数の後に置いて、BMS クライアントを初期化します。

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("https://myapp.mybluemix.net","App GUID");
    },
```
	{: codeblock}

## デバイスの登録
{: #cordova_register}


デバイスを{{site.data.keyword.mobilepushshort}}サービスに登録するには、register メソッドを呼び出します。デバイスを登録するために、次のコード・スニペットを Cordova アプリケーションにコピーします。

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
MFPPush.registerDevice({}, success, failure);
```
	{: codeblock}

### Android
{: #cordova_register_android}
Android では、settings パラメーターを使用しません。Android アプリのみをビルドする場合は、空のオブジェクトを渡します。例えば、次のようにします。

```
MFPPush.registerDevice({}, success, failure);
MFPPush.unregisterDevice(success, failure);
```
	{: codeblock}

### iOS
{: #cordova_register_ios}
アラート、バッジ、および音声のプロパティーをカスタマイズするには、次の JavaScript コード・スニペットを Cordova アプリケーションの Web パーツに追加します。

```
var settings = {
   ios: {
      alert: true,
      badge: true,
      sound: true
   }
}
MFPPush.registerDevice(settings, success, failure);
```
	{: codeblock}


### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```
	{: codeblock}

次のように JSON.parse を使用して、Javascript 内の成功した応答パラメーターの内容にアクセスできます。
**var token = JSON.parse(response).token**


使用可能なキーは、`token` および `deviceId` です。

以下の JavaScript コード・スニペットは、Bluemix Mobile Services クライアント SDK を初期化し、デバイスを{{site.data.keyword.mobilepushshort}}サービスに登録し、プッシュ通知を listen する方法を示しています。このコードを Javascript ファイルに組み込んでください。

```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```
	{: codeblock}

```
//Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```
	{: codeblock}
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
	{: codeblock}

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
	{: codeblock}

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
	{: codeblock}

##次のステップ

{: #cordova_register_next}

プロジェクトをビルドし、以下のコマンドを使用してプロジェクトを実行します。

####Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

####iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## デバイスでのプッシュ通知の受け取り
{: #cordova_receive}

デバイスでプッシュ通知を受け取るには、以下のコード・スニペットをコピーします。

###JavaScript

以下の JavaScript コード・スニペットを Cordova アプリケーションの Web パーツに追加します。

```
var notification = function(notification){
// notification is a JSON object.
alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```
	{: codeblock}

###Android 通知プロパティー

次のセクションに、Android の通知プロパティーをリストします。

* message - プッシュ通知メッセージ
* payload - 通知ペイロードを含む JSON オブジェクト


###iOS 通知プロパティー

次のセクションに、iOS の通知プロパティーをリストします。

* message - プッシュ通知メッセージ
* payload - 通知ペイロードを含む JSON オブジェクト。
action-loc-key - このストリングは、現行ローカリゼーションにおいて、`「View」`の代わりに該当ボタンのタイトルに使用されるローカライズされたストリングを取得するためのキーとして使用されます。
* badge - アプリ・アイコンのバッジとして表示する数。このプロパティーがないと、バッジは変更されません。バッジを削除するには、このプロパティーの値を 0 に設定します。
* sound - アプリ・バンドル内、またはアプリ・データ・コンテナーの Library/Sounds フォルダー内にある音声ファイルの名前。

###Objective-C

アプリケーション代行クラスに次の Objective-C コード・スニペットを追加します。

```
// Handle receiving a remote notification
 -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
  {
 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```
	{: codeblock}


```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
 [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
	}
```
	{: codeblock}

###Swift

アプリケーション代行クラスに次の Swift コード・スニペットを追加します。
```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){
  CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
	}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool
  {
  CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
	}
```
	{: codeblock}

## 基本プッシュ通知の送信
{: #push-send-notifications}

アプリケーションの開発が完了したら、基本プッシュ通知を送信できます。

基本プッシュ通知を送信するには、以下の手順を実行します。

1. **「通知の送信 (Send Notifications)」**を選択し、**「送信先 (Send To)」**オプションを選択することでメッセージを構成します。サポートされるオプションは、**「タグ指定によるデバイス (Device by Tag)」**、**「デバイス ID (Device Id)」**、**「ユーザー ID」**、**「Android デバイス (Android devices)」**、**「iOS デバイス (iOS devices)」**、**「Web 通知 (Web Notifications)」**、および**「すべてのデバイス」**です。
**注**: **「すべてのデバイス」**オプションを選択すると、{{site.data.keyword.mobilepushshort}}をサブスクライブしているすべてのデバイスが通知を受け取ることになります。![「通知」画面](images/tag_notification.jpg)

2. **「メッセージ」**フィールドで、メッセージを構成します。必要に応じてオプションの設定を構成してください。
3. **「送信」**をクリックします。
3. デバイスが通知を受信していることを確認します。

次のスクリーン・ショットは、Android デバイスおよび iOS デバイス上のフォアグラウンドで{{site.data.keyword.mobilepushshort}}を処理しているアラート・ボックスを示しています。

![Android 上のフォアグラウンドのプッシュ通知](images/Android_Screenshot.jpg)

![iOS 上のフォアグラウンドのプッシュ通知](images/iOS_Screenshot.jpg)

   以下のイメージは、Android のバックグラウンドでの{{site.data.keyword.mobilepushshort}}を示しています。
![Android 上のバックグラウンドのプッシュ通知](images/background.jpg)

## 次のステップ
{: #next_steps_tags}

基本通知を正常にセットアップしたら、タグ・ベースの通知および詳細オプションの構成を行うことができます。

{{site.data.keyword.mobilepushshort}}サービスの機能をアプリに追加します。
タグ・ベースの通知を使用する場合は、[タグ・ベースの通知](c_tag_basednotifications.html)を参照してください。
拡張通知オプションを使用する場合は、[拡張プッシュ通知の使用可能化](t_advance_badge_sound_payload.html)を参照してください。
