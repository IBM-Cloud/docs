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


# 啟用 Cordova 應用程式的 Facebook 鑑別
{: #facebook-auth-cordova}

若要配置 {{site.data.keyword.amafull}} Cordova 應用程式來進行 Facebook 鑑別整合，請個別配置每個平台。Cordova 應用程式必須已使用 {{site.data.keyword.amashort}} SDK 進行檢測。

您的原生平台和 Cordova WebView Javascript 程式碼都需要變更，才能啟用 Facebook 鑑別。

使用原生開發環境，對原生程式碼進行變更（例如，在 Android Studio 或 Xcode 中）。
{:shortdesc}

## 開始之前
{: #facebook-auth-before}

您必須具有：
* 使用 {{site.data.keyword.amashort}} 用戶端 SDK 來檢測的 Cordova 專案（Android 或 iOS），請參閱[設定 Cordova 外掛程式](getting-started-cordova.html#getting-started-cordova-plugin)。
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端服務的相關資訊，請參閱[開始使用](index.html)。
* 應用程式路徑。這是後端應用程式的 URL。
* `tenantId` 值。開啟 {{site.data.keyword.amashort}} 服務儀表板。按一下**行動選項**。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。在起始設定 SDK 以及傳送要求至後端服務時，將需要這些值。
*  尋找管理 {{site.data.keyword.Bluemix_notm}} 服務的地區。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在功能表列**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。地區值應該是下列其中一項：**美國南部**、**雪梨**或**英國**。程式碼範例中會指出對應至這些名稱的確切 SDK 常數值。
* Facebook 應用程式及應用程式 ID。如需相關資訊，請參閱[從 Facebook 開發人員入口網站取得 Facebook 應用程式 ID](facebook-auth-overview.html#facebook-appID)。



## 配置 Android 平台
{: #facebook-auth-cordova-android}

配置 Cordova 應用程式的 Android 平台來進行 Facebook 鑑別整合所需的步驟，與原生 Android 應用程式所需的步驟極為類似。如需相關資訊，請參閱[在 Android 應用程式中啟用 Facebook 鑑別](facebook-auth-android.html)。請完成下列步驟：

* [針對 Android 平台配置 Facebook 應用程式](facebook-auth-android.html#facebook-auth-android-config)。這會在 Facebook Developers 網站上，針對 Android 應用程式來設定 Facebook 鑑別。
* [配置 MCA 以進行 Facebook 鑑別](facebook-auth-android.html#facebook-auth-android-mca)。這會在 {{site.data.keyword.Bluemix}} 伺服器上配置 {{site.data.keyword.amashort}} 服務，以進行 Android Facebook 鑑別。


### 針對 Android 平台配置 {{site.data.keyword.amashort}} Facebook 用戶端 SDK
{: #configure_android}

{{site.data.keyword.amashort}} Facebook 用戶端 SDK 必須以原生 Android 應用程式專案內的 Gradle 來新增。

1. 在 Android 專案資料夾中，開啟應用程式模組的 `build.gradle` 檔案（**不是**專案 `build.gradle` 檔案）。尋找 dependencies 區段，並新增用戶端 SDK 的編譯相依關係：

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
```
	{: codeblock}

2. 按一下**工具 > Android > 將專案與 Gradle 檔案同步化**，使專案與 Gradle 同步化。

3. 開啟 `android/res/values/strings.xml` 檔案，並新增包含「Facebook 應用程式 ID」的 `<facebook_app_id>` 字串。

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

4. 在 Android 專案的 `AndroidManifest.xml` 檔案 (`android/manifests/AndroidManifest.xml`) 中：

	* 將 Facebook SDK 的必要 meta 資料新增至 <application> 元素：

    ```XML
    <application .......>
    <meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
    <activity ...../>
    </application>
    ```
    {: codeblock}

   * 在現有活動下，新增「Facebook 活動」元素：

    ```XML
    <application .....>
        <activity ...../>
		<activity ...../>
	<activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name" 
			    />
    </application>
    ```
    {: codeblock}

5. 將下列程式碼新增至您的活動 Java 程式碼。

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### 在原生 Android 程式碼中起始設定授權管理程式
{: #initialize_android}

仍然必須以原生程式碼登錄 `FacebookAuthenticationManager` API。使用 `<tenantId>` 將此程式碼新增至主要活動 `onCreate` 方法（請參閱[開始之前](#before-you-begin)）。

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## 配置 iOS 平台
{: #facebook-auth-cordova-ios}

配置 Cordova 應用程式的 iOS 平台來進行 Facebook 鑑別整合所需的步驟，與原生 iOS Swift 應用程式所需的步驟類似（若要使用 Objective-C 程式碼與 Swift SDK 搭配，需要標頭檔）。主要差異是 Cordova CLI 目前不支援 CocoaPods 相依關係管理程式。您必須手動新增 {{site.data.keyword.amashort}} 用戶端與 Facebook 鑑別整合所需的檔案。如需相關資訊，請參閱[啟用 iOS 應用程式的 Facebook 鑑別 (Swift SDK)](facebook-auth-ios-swift-sdk.html)。請完成下列步驟：

* [針對 iOS 平台配置 Facebook 應用程式](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config)。這會在 Facebook Developers 網站上設定 Facebook 鑑別服務。
* [配置 MCA 以進行 Facebook 鑑別](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca)。這會在 {{site.data.keyword.Bluemix}} 伺服器上配置 {{site.data.keyword.amashort}} 服務。
* [針對 iOS 配置 MCA Facebook 用戶端 SDK](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk)。這會使用 CocoaPods 來安裝用於 Facebook 授權的 {{site.data.keyword.amashort}} iOS Swift SDK。


### 針對 iOS 啟用金鑰鏈共用
{: #enable_keychain}

啟用 `Keychain Sharing`。移至 `Capabilities` 標籤，並將 Xcode 專案中的 `Keychain Sharing` 切換為 `On`。

### 在 Objective-C 中起始設定 {{site.data.keyword.amashort}} 授權管理程式
{: #initialize_objc}

必須根據您的 Xcode 版本，在 `app-delegate.m` 檔案的原生 Objective-C 程式碼中起始設定「授權管理程式」。

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

	{

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}
	

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**附註：**匯入的標頭檔名稱為模組名稱連結 `-Swift.h` 字串的組合，例如，如果您的模組名稱為 `Cordova`，則匯入指令行為 `#import "Cordova-Swift.h"`。若要尋找模組名稱，請移至 `Build Settings` > `Packaging` > `Product Module Name`。

將 `<tenantId>` 取代為您的承租戶 ID（請參閱[開始之前](#facebook-auth-before)）。


##在 Cordova WebView 中起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #initialize_webview}

針對所有平台，在 Cordova Javascript WebView 中使用下列 JavaScript 程式碼，以起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

將 `<applicationBluemixRegion>` 取代為您的地區（請參閱[開始之前](#facebook-auth-before)）。

## 測試鑑別
{: #facebook-auth-cordova-test}

起始設定用戶端 SDK 並登錄 Facebook 鑑別管理程式之後，即可開始對行動後端服務提出要求。

### 開始之前
{: #testing_auth_before}

您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如需相關資訊，請參閱[保護資源](protecting-resources.html)。

1. 嘗試從瀏覽器傳送要求至行動後端應用程式的受保護端點。開啟下列 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`。

	`/protected` 端點值應為行動後端服務中，使用 MobileFirst Services Starter 樣板建立，並透過 {{site.data.keyword.amashort}} 保護的任何受保護端點。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。



1. 使用 Cordova 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼：

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. 執行您的應用程式。即會蹦現 Facebook 登入畫面：

	![影像](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![影像](images/ios-facebook-login.png)

	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，以授權 {{site.data.keyword.amashort}} 使用您的 Facebook 使用者身分來進行鑑別。

1. 	當要求成功時，在 LogCat 公用程式或 Xcode 主控台中會有下列輸出：

	![Android 的 Facebook 鑑別成功訊息](images/android-facebook-login-success.png)

	![iOS 的 Facebook 鑑別成功訊息](images/ios-facebook-login-success.png)
