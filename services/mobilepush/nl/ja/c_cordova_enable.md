---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Cordova アプリケーションによるプッシュ通知受け取りの可能化
{: #cordova_enable}
最終更新日: 2016 年 11 月 06 日
{: .last-updated}

Cordova は、JavaScript、CSS、および HTML を使用したハイブリッド・アプリケーションの構築用プラットフォームです。
{{site.data.keyword.mobilepushshort}} サービスは、Cordova ベースの iOS アプリケーションおよび Android アプリケーションの開発をサポートします。

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

1. Cordova アプリケーションのルート・ディレクトリーで、コマンド **cordova plugin add bms-push** を入力して Cordova の Push プラグインをインストールします。追加したプラットフォームに応じて、以下のような内容が表示されます。
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. your-app-root-folder から、コマンド **cordova plugin list** を使用して、Cordova の Core および Push のプラグインが正常にインストールされたことを確認します。追加したプラットフォームに応じて、以下のような内容が表示されます。
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush"
```
	{: codeblock}

1. (iOS のみ) - iOS 開発環境を構成します。
2. Xcode を使用してアプリケーションをビルドおよび実行します。
1. (Android のみ)- コマンド **cordova build android** を使用して、Android プロジェクトをビルドします。

	**注**: Android Studio でプロジェクトを開く前に、Cordova CLI を使用して Cordova アプリケーションをビルドしてください。これは、ビルド・エラーの回避に有効です。

## Cordova プラグインの初期化
{: #cordova_initialize}

{{site.data.keyword.mobilepushshort}}サービスの Cordova プラグインを使用するには、事前に、アプリケーション経路とアプリケーション GUID を受け渡すことでプラグインを初期化しておく必要があります。プラグインを初期化したら、Bluemix ダッシュボードで作成したサーバー・アプリに接続することができます。Cordova プラグインは、Cordova アプリが Bluemix サービスと通信できるようにするための Android および iOS のクライアント SDK のラッパーです。

1. 以下のコード・スニペットをメイン JavaScript ファイル (通常、**www/js** ディレクトリーの下にある) にコピー・アンド・ペーストして、BMSClient を初期化します。

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
    }
```
	{: codeblock}

アプリケーションの地域を受け渡します。以下の定数が提供されています。

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

例えば、次のようにします。

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**注**: Cordova CLI (例えば、Cordova の create app-name コマンド) を使用して Cordova アプリを作成した場合、この Javascript コードを index.js ファイルの onDeviceReady: function() 関数内の app.receivedEvent 関数の後に置いて、`BMSClient` を初期化します。 


## デバイスの登録
{: #cordova_register}


デバイスを{{site.data.keyword.mobilepushshort}}サービスに登録するには、register メソッドを呼び出します。デバイスを登録するために、次のコード・スニペットを Cordova アプリケーションにコピーします。

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

以下の JavaScript コード・スニペットは、Bluemix Mobile Services クライアント SDK を初期化し、デバイスを{{site.data.keyword.mobilepushshort}}サービスに登録し、プッシュ通知を listen する方法を示しています。このコードを Javascript ファイルに組み込んでください。

コードは **onDeviceReady: function()** 内に置きます。

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification);
```
	{: codeblock}

### Objective-C
{: #cordova_register_objective}
アプリケーション代行クラスに次の Objective-C コード・スニペットを追加します。


```
// Register the device token with Bluemix Push Notification Service
	- (void)application:(UIApplication *)application
     didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken{
       [[CDVBMSPush sharedInstance] didRegisterForRemoteNotificationsWithDeviceToken:deviceToken];
}
// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
   [[CDVBMSPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
}
```
	{: codeblock}

###Swift
{: #cordova_register_swift}

アプリケーション代行クラスに次の Swift コード・スニペットを追加します。

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
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
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification);
```
	{: codeblock}

###Android 通知プロパティー

次のセクションに、Android の通知プロパティーをリストします。

* **message** - プッシュ通知メッセージ
* **payload** - 通知ペイロードを含む JSON オブジェクト


###iOS 通知プロパティー

次のセクションに、iOS の通知プロパティーをリストします。

* **message** - プッシュ通知メッセージ
* **payload** - 通知ペイロードを含む JSON オブジェクト。
action-loc-key - このストリングは、現行ローカリゼーションにおいて、`「View」`の代わりに該当ボタンのタイトルに使用されるローカライズされたストリングを取得するためのキーとして使用されます。
* **badge** - アプリ・アイコンのバッジとして表示する数。このプロパティーがないと、バッジは変更されません。バッジを削除するには、このプロパティーの値を 0 に設定します。
* **sound** - アプリ・バンドル内、またはアプリ・データ・コンテナーの Library/Sounds フォルダー内にある音声ファイルの名前。

###Objective-C

アプリケーション代行クラスに次の Objective-C コード・スニペットを追加します。

```
// Handle receiving a remote notification
 -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
  {
 [[CDVBMSPush sharedInstance] didReceiveRemoteNotificationWithNotification:userInfo];
}
```
	{: codeblock}



```
//Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {
  if (launchOptions != nil) {
   [[CDVBMSPush sharedInstance] didReceiveRemoteNotificationOnLaunchWithLaunchOptions:launchOptions];
     }
 }
```
	{: codeblock}

###Swift

アプリケーション代行クラスに次の Swift コード・スニペットを追加します。
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool
  {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
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
