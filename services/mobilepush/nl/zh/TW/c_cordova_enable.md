---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 讓 Cordova 應用程式可接收推送通知
{: #cordova_enable}
前次更新：2017 年 1 月 18 日
{: .last-updated}

Cordova 是一個平台，可使用 JavaScript、CSS 及 HTML 來建置混合式應用程式。{{site.data.keyword.mobilepushshort}} 服務支援開發 Cordova 型 iOS 及 Android 應用程式。

您可以啟用 Cordova 應用程式來接收傳送至您裝置的推送通知。

## 安裝 Cordova Push 外掛程式
{: #cordova_install}

安裝及使用 Client Push 外掛程式來進一步開發 Cordova 應用程式。這也會安裝起始設定您的 Bluemix 連線的 Cordova Core 外掛程式。

### 開始之前

1. 下載最新的 Android Studio SDK 及 Xcode 版本。
1. 設定您的模擬器。若為 Android Studio，請使用支援 Google Play API 的模擬器。
1. 安裝 Git 指令行工具。若為 Windows，請確保選取**從 Windows 命令提示字元執行 Git** 選項。如需如何下載及安裝此工具的相關資訊，請參閱 [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads "外部鏈結圖示"){: new_window}。
1. 安裝 Node.js 及「Node 套件管理程式 (NPM)」工具。NPM 指令行工具與 Node.js 組合在一起。如需如何下載及安裝 Node.js 的相關資訊，請參閱 [Node.js ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://nodejs.org/en/download/ "外部鏈結圖示"){: new_window}。
1. 從指令行中，使用 **npm install -g cordova** 指令來安裝 Cordova 指令行工具。若要使用 Cordova Push 外掛程式，這是必要動作。如需如何安裝 Cordova 以及設定 Cordova 應用程式的相關資訊，請參閱 [Cordova Apache ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cordova.apache.org/#getstarted "外部鏈結圖示"){: new_window}。如需相關資訊，請參閱 Cordova Push 外掛程式 [Readme 檔 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push "外部鏈結圖示"){: new_window}。
1. 切換至您要在其中建立 Cordova 應用程式的資料夾，並執行下列指令來建立 Cordova 應用程式。如果您有現存的 Cordova 應用程式，請移至步驟 3。
```cordova create your_app_name
cd your_app_name
```
	{: codeblock}
- 選用項目：您可以編輯 **config.xml** 檔案，並將 <name> 元素中的應用程式名稱變更為您選擇的名稱，而不是預設 HelloCordova 名稱。

請確定您指定正確的「軟體組 ID」。如果指定不正確的「軟體組 ID」，則下列錯誤訊息可能會導致 Xcode。

* 以無效的授權簽署執行檔。
* 應用程式的「程式碼簽署授權」檔案中指定的授權，不符合佈建設定檔中指定的授權。若要修正此問題，請在 Xcode 或 Cordova 應用程式 **config.xml** 檔案中指定正確的「軟體組 ID」。

1. 將最低支援的 API 或部署目標宣告新增至 Cordova 應用程式的 config.xml 檔案。minSdkVersion 值必須高於 15。targetSdkVersion 值必須一律反映可從 Google 取得的最新 Android SDK。
	
	* Android - 使用編輯器來開啟 **config.xml** 檔案，並將
`<platform name="android">` 元素更新為最小及目標 SDK 版本：

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - 使用部署目標宣告更新 <platform name="ios"> 元素：

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. 從 Cordova 指令行介面 (CLI) 中，使用下列指令新增平台：iOS 及（或）Android：
```
cordova platform add ios
cordova platform add android
```
	{: codeblock}

1. 從 Cordova 應用程式根目錄中，輸入下列指令來安裝 Cordova Push 外掛程式：**cordova plugin add bms-push**。根據您新增的平台，您可能會看到：
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. 從 your-app-root-folder 中，使用下列指令，驗證已順利安裝 Cordova Core 及 Push 外掛程式：**cordova plugin list**。根據您新增的平台，您可能會看到：
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. 配置您的 iOS 開發環境。
2. 使用 Xcode 建置並執行應用程式。
1. 下載針對 Android 使用的 Firebase `google-services.json`，並且將他們放置在 Cordova 專案的根資料夾：[your-app-name]/platforms/android。
	1. 請移至 `[your-app-name]/platforms/android`。
	2. 開啟 `build.gradle` 檔案（路徑：platform > android > build.gradle）。
	3. 在 `build.gradle` 檔案中尋找 `buildscript` 文字。
	4. 在類別路徑行之後，新增此行：classpath 'com.google.gms:google-services:3.0.0'
	5. 然後，尋找 "dependencies"。選取 `compile` 文字的相依關係以及選取要於何處結束該相依關係，在此之後，新增此行 :apply plugin: 'com.google.gms.google-services'。
	6. 準備及建置您的 Cordova Android 專案。
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**附註**：在 Android Studio 中開啟專案之前，請先透過 Cordova CLI 建置 Cordova 應用程式。這將有助於避免建置錯誤。

## 起始設定 Cordova 外掛程式
{: #cordova_initialize}

您需要透過傳遞應用程式路徑及應用程式 GUID 來起始設定 {{site.data.keyword.mobilepushshort}} Service Cordova 外掛程式，才能使用該外掛程式。在起始設定外掛程式之後，您可以連接至在 Bluemix 儀表板中所建立的伺服器應用程式。Cordova 外掛程式是 Android 及 iOS Client SDK 的封套，可讓 Cordova 應用程式與 Bluemix 服務通訊。

1. 複製下列程式碼 Snippet，並將其貼入您的主要 JavaScript 檔案（通常位於 **www/js** 目錄下），以起始設定 BMSClient。

```
onDeviceReady: function() {
	app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

傳入應用程式的地區。會提供以下常數：

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

例如：

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**附註**：如果您已使用 Cordova CLI（例如，Cordova create app-name 指令）建立 Cordova 應用程式，請將此 JavaScript 程式碼放置在 index.js 檔案中 onDeviceReady: function() 函數內的 app.receivedEvent 函數後面，以起始設定 `BMSClient`。 


## 登錄裝置
{: #cordova_register}


若要向 {{site.data.keyword.mobilepushshort}} Service 登錄裝置，請呼叫 register 方法。將下列程式碼 Snippet 複製至 Cordova 應用程式，以登錄裝置。

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

下列 JavaScript 程式碼 Snippet 顯示如何起始設定 Bluemix Mobile Services Push Client SDK、向 {{site.data.keyword.mobilepushshort}} Service 登錄裝置，以及接聽推送通知。請在 Javascript 檔案中包含此程式碼。

在 **onDeviceReady: function()** 內。

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

將下列 Swift 程式碼 Snippet 新增至應用程式委派類別。

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

##後續步驟

{: #cordova_register_next}

使用下列指令建置專案，然後執行專案：

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

## 在裝置上接收推送通知
{: #cordova_receive}

複製下列程式碼 Snippet，以在裝置上接收推送通知。

###JavaScript

將下列 JavaScript 程式碼 Snippet 新增至 Cordova 應用程式的 Web 組件。
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

###Android 通知內容

下節列出 Android 通知內容：

* **message** - 推送通知訊息
* **payload** - 包含通知有效負載的 JSON 物件


###iOS 通知內容

下節列出 iOS 通知內容：

* **message** - 推送通知訊息
* **payload** - 包含通知有效負載的 JSON 物件
* **action-loc-key** - 此字串用來作為索引鍵，在現行本地化中取得一個本地化字串，以用於適當的按鈕標題，而取代 `View`。
* **badge** - 顯示為應用程式圖示徽章的號碼。如果沒有此內容，則不會變更徽章。若要移除徽章，請將此內容的值設為 0。
* **sound** - 應用程式組合或者應用程式資料容器之 Library/Sounds 資料夾中的音效檔名稱。


將下列 Swift 程式碼 Snippet 新增至應用程式委派類別。
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

## 傳送基本推送通知
{: #push-send-notifications}

開發應用程式之後，您可以傳送基本推送通知。

若要傳送基本推送通知，請完成下列步驟：

1. 選取**傳送通知**，然後選擇**傳送至**選項來編寫訊息。支援的選項是**依標籤的裝置**、**裝置 ID**、**使用者 ID**、**Android 裝置**、**iOS 裝置**、**Web 通知**及**所有裝置**。
**附註**：當您選取**所有裝置**選項時，所有已訂閱 {{site.data.keyword.mobilepushshort}} 的裝置都會接收到通知。![通知畫面](images/tag_notification.jpg)

2. 在**訊息**欄位中，編寫訊息。視需要選擇配置選用設定。
3. 按一下**傳送**。
3. 驗證您的裝置已接收到通知。

下列擷取畫面顯示在 Android 及 iOS 裝置的前景中處理 {{site.data.keyword.mobilepushshort}} 的警示框。

![Android 上的前景推送通知](images/Android_Screenshot.jpg)

![iOS 上的前景推送通知](images/iOS_Screenshot.jpg)

   下列影像在 Android 的背景中顯示 {{site.data.keyword.mobilepushshort}}。  
![Android 上的背景推送通知](images/background.jpg)

## 後續步驟
{: #next_steps_tags}

順利設定基本通知之後，您就可以配置標籤型通知及進階選項。

將 {{site.data.keyword.mobilepushshort}} Service 特性新增至您的應用程式。若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。
若要使用進階通知選項，請參閱[啟用進階推送通知](t_advance_badge_sound_payload.html)。
