---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 啟用 Cordova 應用程式的 Google 鑑別
{: #google-auth-cordova}

若要整合 {{site.data.keyword.amafull}} Cordova 應用程式以進行 Google 鑑別，您必須在 Cordova 應用程式原生平台程式碼（Java 或 Objective-C）及 Cordova WebView (Javascript) 中進行變更。每一個平台都必須分別進行配置。使用原生開發環境，對原生程式碼進行變更（例如，在 Android Studio 或 Xcode 中）。


## 開始之前
{: #before-you-begin}

您必須具有：

* 使用 {{site.data.keyword.amashort}} 用戶端 SDK 進行檢測的 Cordova 專案。如需相關資訊，請參閱[設定 Cordova 外掛程式](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)。  
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端服務的相關資訊，請參閱[開始使用](index.html)。
* 應用程式路徑。這是後端應用程式的 URL。
* **承租戶 ID**。在 {{site.data.keyword.Bluemix_notm}} 儀表板中，開啟服務。按一下**行動選項**。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
*  尋找管理您 {{site.data.keyword.Bluemix_notm}} 應用程式的地區。您可以在標頭中找到您目前的 Bluemix 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。地區值應該是下列其中一項：**美國南部**、**雪梨**或**英國**。程式碼範例中會指出對應至這些名稱的確切 SDK 常數值。
* （選用）熟悉下列各節：
   * [啟用 Android 應用程式的 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [啟用 iOS 應用程式的 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)


## 配置 Android 平台
{: #google-auth-cordova-android}

配置 Cordova 應用程式的 Android 平台來進行 Google 鑑別時所需的步驟，與原生應用程式所需的步驟極為類似。請參閱[在 Android 應用程式中啟用 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)，並設定下列項目：

   * [在 Google Developer Console 中建立專案](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#create-google-project)。這會為您示範如何在 Google Developers 網站上設定鑑別服務。
   * [配置 MCA 以進行 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#google-auth-android-config)。這會為您示範如何設定 {{site.data.keyword.amashort}} 來使用 Google 授權。

### 配置適用於 Android Cordova 的 {{site.data.keyword.amashort}} 用戶端 SDK

1. 在 Android 專案資料夾中，開啟應用程式模組的 `build.gradle` 檔案（**不是**專案 `build.gradle` 檔案）。
尋找 dependencies 區段，並新增用戶端 SDK 的編譯相依關係：

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. 按一下**工具 > Android > 將專案與 Gradle 檔案同步化**，以將專案與 Gradle 同步化。

1. 仍然必須以原生程式碼登錄 `GoogleAuthenticationManager` API。將此程式碼新增至主要活動 `onCreate` 方法：

	```Java
	String tenantId = "<tenantId>";
	MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
	BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```
	{: codeblock}

1. 將下列程式碼新增至您的活動中：

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## 配置 iOS 平台
{: #google-auth-cordova-ios}

配置 Cordova 應用程式的 iOS 平台進行 Google 鑑別整合所需的步驟，與原生應用程式的步驟類似。主要差異是 Cordova CLI 目前不支援 CocoaPods 相依關係管理程式。您必須手動新增與 Google 鑑別整合所需的檔案。如需相關資訊，請參閱[啟用 iOS 應用程式的 Google 鑑別 (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)。請完成下列步驟：

   * [準備應用程式以進行 Google 登入](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-sign-in-ios)：準備「Google 登入」來鑑別 {{site.data.keyword.amashort}} iOS 應用程式。

   * [配置 MCA 以進行 Google 鑑別](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-config)：配置 {{site.data.keyword.amashort}} 服務以使用「Google 登入」。

   * [針對 iOS 配置 MCA 用戶端 SDK](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-sdk)：配置 {{site.data.keyword.amashort}} 用戶端以使用「Google 登入」。


### 針對 iOS 啟用金鑰鏈共用
{: #enable_keychain}

啟用 `Keychain Sharing`。移至 `Capabilities` 標籤，並將 Xcode 專案中的 `Keychain Sharing` 切換為 `On`。


### 在 iOS 程式碼中起始設定授權管理程式

在 `AppDelgate.m` 檔案的 Objective-C 中起始設定「{{site.data.keyword.amashort}} 授權管理程式」。

```
 #import "<your_module_name>-Swift.h" 
 
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{
	[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[GoogleAuthenticationManager sharedInstance] register];

    self.viewController = [[MainViewController alloc] init];

	    [[GoogleAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];

	return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		return [[GoogleAuthenticationManager sharedInstance] onOpenURLWithApplication:application url:url
	sourceApplication:sourceApplication annotation:annotation];
}
```
{: codeblock}

**附註：**

* 將 `<your_module_name>` 取代為您專案的模組名稱。例如，如果模組名稱為 `Cordova`，則匯入指令行應為 `#import "Cordova-Swift.h"`。若要尋找模組名稱，請移至 `Build Settings` 標籤、`Packaging` > `Product Module Name`。
* 將 `<tenantId>` 取代為您的承租戶 ID（請參閱[開始之前](#before-you-begin)）。


## 在 Cordova WebView 中起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #google-auth-cordova-initialize}

針對所有平台，在 Cordova 應用程式中使用下列 Javascript 程式碼，以起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

將 `<applicationBluemixRegion>` 取代為您的地區（請參閱[開始之前](#before-you-begin)）。

## 測試鑑別
{: #google-auth-cordova-test}

起始設定用戶端 SDK 之後，即可開始對行動後端應用程式提出要求。

### 開始之前
{: #google-auth-cordova-testing-before}

您必須在 `/protected` 端點具有 {{site.data.keyword.amashort}} 所保護的後端應用程式。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），嘗試在桌面瀏覽器中將要求傳送給行動後端應用程式的受保護端點。

1. 使用「MobileFirst Services 樣板」所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護，因此只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取它。因此，您會在桌面瀏覽器中看到 `Unauthorized`。

1. 使用 Cordova 應用程式來對相同的端點提出要求，並使用完整 URL（例如，`http://my-mobile-backend.mybluemix.net/protected`）。起始設定 `BMSClient` 之後，請新增下列程式碼。

	```JavaScript
	var success = function(data){
		console.log("success", data);
	}
	var failure = function(error){
		console.log("failure", error);
	}
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. 執行您的應用程式。即會顯示 Google 登入畫面。

	![Google 登入畫面](images/android-google-login.png)

	![Google 登入畫面](images/ios-google-login.png)

	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，即會授權 {{site.data.keyword.amashort}} 使用 Google 使用者身分來進行鑑別。

1. 您的要求應該會成功。視使用的平台而定，您會在 LogCat/Xcode 主控台中看到下列輸出：

	![Android 上的程式碼 Snippet](images/android-google-login-success.png)

	![iOS 上的程式碼 Snippet](images/ios-google-login-success.png)
