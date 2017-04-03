---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} 服務取代為 {{site.data.keyword.appid_full}} 服務。

# 設定 Cordova 外掛程式
{: #getting-started-cordova}

使用 {{site.data.keyword.amafull}} 用戶端 SDK 來檢測 Cordova 用戶端應用程式。在 Android (Java) 或 iOS 程式碼（使用 Swift SDK 及相關標頭檔的 Objective C）中起始設定「授權管理程式」。起始設定用戶端，並從 WebView 對受保護及未受保護的資源提出要求。

{:shortdesc}

## 開始之前
{: #before-you-begin}
您必須具有：

* {{site.data.keyword.Bluemix_notm}} 應用程式的實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。
* {{site.data.keyword.amafull}} 服務的實例。
* 後端應用程式的 URL（**應用程式路徑**）。在傳送要求至後端應用程式的受保護端點時，將需要此值。
* **承租戶 ID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`雪梨`或`英國`，並對應至 WebView Javascript 程式碼中所需的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY` 或 `BMSClient.REGION_UK`。您需要此值來起始設定 {{site.data.keyword.amashort}} 用戶端。
* Cordova 應用程式或現有專案。如需如何設定 Cordova 應用程式的相關資訊，請參閱 [Cordova 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cordova.apache.org/){: new_window}。

## 安裝 {{site.data.keyword.amashort}} Cordova 外掛程式
{: #getting-started-cordova-plugin}

適用於 Cordova 的 {{site.data.keyword.amashort}} 用戶端 SDK 是包裝原生 {{site.data.keyword.amashort}} 用戶端 SDK 的 Cordova 外掛程式。它是使用「Cordova 指令行介面 (CLI)」及 `npmjs`（Cordova 專案的外掛程式儲存庫）進行配送。Cordova CLI 會從儲存庫中自動下載外掛程式，並使它們可供 Cordova 應用程式使用。

1. 將 Android 及/或 iOS 平台新增至 Cordova 應用程式。從指令行中，執行下列一個或兩個指令：

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

2. 如果您已新增 Android 平台，則必須將最低支援的 API 層次新增至 Cordova 應用程式的 `config.xml` 檔案。開啟 `config.xml` 檔案，並將下行新增至 `<platform name="android">` 元素：

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	{: codeblock}

	*minSdkVersion* 值必須是 `15` 或更高。請參閱 [Android 平台手冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window}，讓 Android SDK 支援的 *targetSdkVersion* 保持最新。

3. 如果您已新增 iOS 作業系統，請使用目標宣告來更新 `<platform name="ios">` 元素：

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. 安裝 {{site.data.keyword.amashort}} Cordova 外掛程式：

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. 為 Andro為 Android 或 iOS 配置您的平台，或兩者都配置。

	####Android
	{: #cordova-android}

	在 Android Studio 開啟您的專案之前，請透過指令行介面 (CLI) 建置您的 Cordova 應用程式，以避免發生建置錯誤。

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	依照下列方式來配置您的 Xcode 專案。

	1. 使用最新版的 Xcode，開啟 `<app_name>/platforms/ios` 目錄中的 `xcode.proj` 檔案。

		**重要事項：**如果您收到要轉換為最新 Swift 語法的訊息，請按一下**取消**。

	2. 使用 Xcode 建置並執行您的應用程式。

	**附註**：您在執行 `cordova build ios` 時，可能會收到下列錯誤。這個問題是[問題 12 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12){: new_window} 中追蹤的相依外掛程式錯誤所引起。您還是可以透過模擬器或裝置在 XCode 中執行 iOS 專案。

	```
	xcodebuild: error: Unable to find a destination matching the provided destination specifier:
			{ platform:iOS Simulator }

		Missing required device specifier option.
		The device type "iOS Simulator" requires that either "name" or "id" be specified.
		Please supply either "name" or "id".
	```

6. 執行下列指令，驗證已順利安裝外掛程式：

	```Bash
	cordova plugin list
	```
	{: codeblock}

7. 在 **Capabilities** 標籤中將 **Keychain Sharing** 切換為 `On`，以針對 iOS 啟用「金鑰鏈共用」。

8. 在 **Build Settings** > **Packaging** 標籤中，將 **Defines Module** 切換為 `YES`，以針對 iOS 啟用 **Defines Module**。


## 在 Cordova WebView 中起始設定 {{site.data.keyword.amashort}} 用戶端 (Javascript)
{: #getting-started-cordova-initialize}

若要使用 {{site.data.keyword.amashort}} 用戶端 SDK，您必須傳遞 `applicationBluemixRegion`，以起始設定 SDK。

新增下列呼叫到 `index.js` 檔案，以起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**注意：**請將 `<applicationBluemixRegion>` 取代為管理 {{site.data.keyword.Bluemix_notm}} 服務的地區，請參閱[開始之前](#before-you-begin)。

##從原生程式碼起始設定 {{site.data.keyword.amashort}} 授權管理程式
{: #initializing-auth-manager}

您需要新增下列程式碼 Snippet，才能使用 `BMSAuthorizationManager`。下列原生程式碼會使用 {{site.data.keyword.amashort}} 服務 `tenantId` 來起始設定 `BMSAuthorizationManager`（請參閱[開始之前](#before-you-begin)）。

### Android (Java)

在 `MainActivity.java` 檔案的 `OnCreate` 方法中，將程式碼新增在 `loadUrl` 之前。
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS (Objective C)
根據您的 Xcode 版本，在 `AppDelegate.m` 中新增「授權管理程式」起始設定。

```Objective-C
  #import "<your_module_name>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**附註：**匯入的標頭檔名稱為模組名稱連結 `-Swift.h` 字串的組合，例如，如果您的模組名稱為 `Cordova`，則匯入指令行為 `#import "Cordova-Swift.h"`。若要尋找模組名稱，請移至 `Build Settings` > `Packaging` > `Product Module Name`。將 `<tenantId>` 取代為您的承租戶 ID（請參閱[開始之前](#before-you-begin)）。


## 對行動後端服務提出要求
{: #getting-started-request}

起始設定 {{site.data.keyword.amashort}} 用戶端 SDK 之後，即可開始對行動後端服務提出要求。

1. 嘗試傳送要求至行動後端應用程式的受保護端點。在瀏覽器中，開啟下列 URL：`{applicationRoute}/protected`（例如：`http://my-mobile-backend.mybluemix.net/protected`）。

	使用 MobileFirst Services Starter 樣板所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才會存取這個端點。



2. 使用 Cordova 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼：

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. 當要求成功時，您會在 LogCat 或 Xcode 主控台中看到下列輸出（視使用的平台而定）：

	![成功訊息](images/getting-started-android-success.png)

	## 後續步驟
	{: #next-steps}

	當您連接至受保護端點時，不需要任何認證。若需要使用者登入應用程式，您必須配置 Facebook、Google 或自訂鑑別。
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [自訂](custom-auth-cordova.html)
