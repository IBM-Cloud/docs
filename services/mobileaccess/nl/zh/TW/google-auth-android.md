---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**重要事項：{{site.data.keyword.amafull}} 服務取代為 {{site.data.keyword.appid_full}} 服務。**

# 啟用 Android 應用程式的 Google 鑑別
{: #google-auth-android}

在 {{site.data.keyword.amafull}} Android 應用程式上使用 Google 來鑑別使用者。新增 {{site.data.keyword.amashort}} 安全功能。

## 開始之前
{: #before-you-begin}

您必須具有：

* {{site.data.keyword.amafull}} 服務實例和 {{site.data.keyword.Bluemix_notm}} 應用程式。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。
* 後端應用程式的 URL（**應用程式路徑**）。在傳送要求至後端應用程式的受保護端點時，將需要此值。
* **承租戶 ID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`雪梨`或`英國`，並對應至 WebView Javascript 程式碼中所需的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY` 或 `BMSClient.REGION_UK`。您需要此值來起始設定 {{site.data.keyword.amashort}} 用戶端。
* 配置成使用 Gradle 的 Android 專案。專案不需要使用 {{site.data.keyword.amashort}} 用戶端 SDK 進行檢測。  

設定 {{site.data.keyword.amashort}} Android 應用程式的 Google 鑑別將需要進一步配置：

* {{site.data.keyword.Bluemix_notm}} 應用程式
* Android Studio 專案

## 在 Google Developer Console 中建立專案
{: #create-google-project}

若要開始使用 Google 作為身分提供者，請在 [Google Developer Console ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.developers.google.com){: new_window} 中建立專案。建立專案的一部分是取得「Google 用戶端 ID」。「Google 用戶端 ID」是 Google 鑑別所使用之您的應用程式的唯一 ID，並且是設定 {{site.data.keyword.amashort}} 服務的必要項目。

從主控台中：

1. 使用 **Google+** API 建立專案。
2. 新增 **OAuth** 使用者存取權。
3. 在您新增認證之前，必須選擇平台 (Android)。
4. 新增認證。

若要完成認證建立作業，您需要新增**簽署憑證指紋**。


### 設定簽署憑證
{: #signing_cert}

為了讓 Google 驗證應用程式確實性，您必須指定簽署憑證指紋。

Android OS 需要使用開發人員憑證來簽署 Android 裝置上安裝的所有應用程式。Android 應用程式可以使用兩種模式建置：除錯及發行。通常建議針對除錯及發行模式使用不同的憑證。用於以除錯模式簽署 Android 應用程式的憑證會與 Android SDK 組合。Android Studio 通常會自動安裝 Android SDK。當您要將應用程式發行到 Google Play 時，必須使用另一個憑證來簽署應用程式（您通常會自行產生另一個憑證）。如需相關資訊，請參閱[簽署您的 Android 應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}。

包含開發環境憑證的金鑰儲存庫儲存在 `~/.android/debug.keystore` 檔案中。預設金鑰儲存庫密碼為 `android`。此憑證用來以除錯模式建置應用程式。

1. 從用戶端開發環境中擷取簽署憑證指紋：

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	{: codeblock}

	您也可以使用相同的語法來擷取發行模式憑證的金鑰雜湊。請取代指令中的別名及金鑰儲存庫路徑。

1. 在「Google 主控台認證」對話框的**憑證指紋**下，找到開頭為 `SHA1` 的那一行。將透過執行 **keytool** 指令所取得的指紋值複製到此文字框。

###套件名稱

1. 在「認證」對話框上，輸入 Android 應用程式的套件名稱。

	若要尋找 Android 應用程式的套件名稱，請在 Android Studio 中開啟 `AndroidManifest.xml` 檔案，並尋找：

	```
	<manifest package="{your-package-name}">
	```
	{: codeblock}

1. 完成時，請按一下**建立**。這會完成認證建立作業。

###Google 用戶端 ID
{: #google-client-id}

順利建立認證之後，認證頁面會顯示您的「Google 用戶端 ID」。請記下此值。您需要在 {{site.data.keyword.Bluemix}} 應用程式中登錄此值。


## 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
{: #google-auth-android-config}

現在，您有適用於 Android 的「Google 用戶端 ID」，可以在 {{site.data.keyword.amashort}} 儀表板中啟用 Google 鑑別。

1. 在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 展開 **Google** 區段。
1. 在**適用於 Android 的用戶端 ID** 中，指定適用於 Android 的「Google 用戶端 ID」，然後按一下**儲存**。

## 配置適用於 Android 的 {{site.data.keyword.amashort}} 用戶端 SDK
{: #google-auth-android-sdk}

從 Android Studio 專案。

1. 開啟應用程式模組的 `build.gradle` 檔案。

	Android 專案可能會有兩個 `build.gradle` 檔案：一個用於專案，另一個用於應用程式模組。請使用應用程式模組。

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

	**附註：**您可以移除對 `com.ibm.mobilefirstplatform.clientsdk.android` 群組的 `core` 模組的相依關係（如果已有的話）。`googleauthentication` 模組會為您自動下載它。`googleauthentication` 模組會下載 Google+ SDK，並將它安裝在 Android 專案中。

1. 按一下**工具 > Android > 將專案與 Gradle 檔案同步化**，以將專案與 Gradle 同步化。

1. 開啟 Android 專案的 `AndroidManifest.xml` 檔案。

1. 在 `<manifest>` 元素下，新增網際網路存取權：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```
	{: codeblock}

1. 若要使用 {{site.data.keyword.amashort}} 用戶端 SDK，您必須傳遞 **context** 及 **region** 參數來起始設定 SDK。

	放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 `onCreate` 方法。

1. 起始設定用戶端 SDK，並登錄 Google 鑑別管理程式。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
		MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	GoogleAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

	* 將 `BMSClient.REGION_UK` 取代為您的 {{site.data.keyword.Bluemix_notm}} **地區**。
	* 將 `<MCAServiceTenantId>` 取代為**承租戶 ID** 值。

	如需取得這些值的相關資訊，請參閱[開始之前](##before-you-begin)。

	**附註：**如果您的 Android 應用程式是以 Android 6.0 版（API 層次 23）或以上版本為目標，則必須確定應用程式先進行 `android.permission.GET_ACCOUNTS` 呼叫，再呼叫 `register`。如需相關資訊，請參閱[在 Android 上要求許可權 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.android.com/training/permissions/requesting.html){: new_window}。

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

## 測試鑑別
{: #google-auth-android-test}

起始設定用戶端 SDK 並登錄「Google 鑑別管理程式」之後，即可開始對後端應用程式提出要求。

開始測試之前，您必須具有使用 **MobileFirst Services Starter** 樣板所建立的行動後端應用程式，並且已具有 {{site.data.keyword.amashort}} `/protected` 端點所保護的資源。如需相關資訊，請參閱[保護資源](protecting-resources.html)。

1. 開啟 `{applicationRoute}/protected`（例如：`http://my-mobile-backend.mybluemix.net/protected`），嘗試在桌面瀏覽器中將要求傳送給行動後端應用程式的受保護端點。如需取得 `{applicationRoute}` 值的相關資訊，請參閱[開始之前](#before-you-begin)。

	使用「MobileFirst Services 樣板」所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。因此，只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取它。因此，您會在桌面瀏覽器中看到 `Unauthorized`。

1. 使用 Android 應用程式以對相同的受保護端點提出要求。起始設定 `BMSClient` 實例並登錄 `GoogleAuthenticationManager` 之後，請新增下列程式碼。

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", MCAAuthorizationManager.getInstance().getUserIdentity().toString());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```
	{: codeblock}

1. 執行您的應用程式。即會蹦現「Google 登入」畫面。登入之後，應用程式會要求資源的存取權：

	![影像](images/android-google-login.png)

	根據 Android 裝置以及目前是否已登入 Google，您可能會有不同的使用者介面。

	按一下**確定**，即會授權 {{site.data.keyword.amashort}} 使用 Google 使用者身分來進行鑑別。

1. 	要求成功之後，您會在 LogCat 工具中看到下列輸出：

	![影像](images/android-google-login-success.png)

	您也可以新增下列程式碼，來新增登出功能：

	```Java
	GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	如果您在使用者使用 Google 登入之後呼叫此程式碼，則會將使用者登出 Google。使用者嘗試再次登入時，他們必須選取 Google 帳戶才能再次登入。他們嘗試使用先前登入的 Google ID 進行登入時，不會提示使用者再次輸入其認證。若要讓系統再次提示輸入登入認證，使用者必須從 Android 裝置中移除其 Google 帳戶。

	傳遞給 logout 函數的 `listener` 值可以是 `null`。
