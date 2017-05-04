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

# 啟用 Android 應用程式的 Facebook 鑑別
{: #facebook-auth-android}

若要在 {{site.data.keyword.amafull}} Android 用戶端應用程式中，使用 Facebook 作為身分提供者，請新增並配置 Android 用戶端，以在 Facebook for Developers 網站上存取您的 Facebook 應用程式。
{:shortdesc}

## 開始之前
{: #before-you-begin}

您必須具有：

* {{site.data.keyword.amafull}} 服務實例和 {{site.data.keyword.Bluemix_notm}} 應用程式。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。
* 後端應用程式的 URL（**應用程式路徑**）。在傳送要求至後端應用程式的受保護端點時，將需要此值。
* **承租戶 ID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`雪梨`或`英國`，並對應至 WebView Javascript 程式碼中所需的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY` 或 `BMSClient.REGION_UK`。您需要此值來起始設定 {{site.data.keyword.amashort}} 用戶端。
* 配置成使用 Gradle 的 Android 專案。專案不需要使用 {{site.data.keyword.amashort}} 用戶端 SDK 進行檢測。  
* [Facebook for Developers 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.facebook.com/){: new_window} 上搭配 Android 平台的 Facebook 應用程式。

**重要事項：**您不需要個別安裝 Facebook SDK (`com.facebook.FacebookSdk`)。當您新增 {{site.data.keyword.amashort}} Facebook 用戶端 SDK 時，Gradle 會自動安裝 Facebook SDK。在 Facebook for Developers 網站中新增 Android 平台時，可以跳過此步驟。

## 在 Facebook for Developers 網站上配置應用程式
{: #facebook-auth-android-config}

從 Facebook for Developers 網站：

1. 在 [Facebook for Developers 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developers.facebook.com){: new_window} 上登入您的帳戶。

1. 從**產品清單**中，選擇 **Facebook 登入**。

1. 新增或配置 Android 平台。

1. 在「Google Play 套件名稱」提示中，指定 Android 應用程式的套件名稱。若要尋找 Android 應用程式的套件名稱，請在 Android Studio 專案的 `AndroidManifest.xml` 檔案中尋找 `<manifest ..... package="{your-package-name}">`。

1. 在**類別名稱**提示中，指定主要活動的類別名稱。類別名稱是活動附件中 `android:name` 內容的值。如果 `AndroidManifest.xml` 檔案中有多個活動，請尋找包含 `<intent-filter>` 的活動：

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```
	{: codeblock}

1. 為了讓 Facebook 確保應用程式確實性，您必須指定開發人員憑證 SHA1 的雜湊。

	**進一步瞭解 Android 安全：**Android OS 需要使用開發人員憑證來簽署 Android 裝置上安裝的所有應用程式。Android 應用程式可以使用兩種模式建置：除錯及發行。

	請針對除錯及發行模式使用不同的憑證。用於以除錯模式簽署 Android 應用程式的憑證會與 Android SDK（通常是由 Android Studio 自動安裝）組合。當您要將應用程式發行到 Google Play 商店時，必須使用另一個憑證來簽署應用程式（您通常會自行產生另一個憑證）。

	您可以使用 Facebook 輸入兩組金鑰雜湊：一個金鑰雜湊是針對使用除錯憑證以除錯模式所建置的應用程式，另一個金鑰雜湊則是針對使用發行憑證以發行模式所建置的應用程式。如需相關資訊，請參閱[簽署您的 Android 應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}。

1. 包含您用於開發環境之憑證的金鑰儲存庫，會儲存在 `~/.android/debug.keystore` 檔案中。預設金鑰儲存庫密碼為：`android`。請使用此憑證，以除錯模式建置應用程式。

1. 擷取除錯模式憑證的金鑰雜湊：

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```
	{: codeblock}

	**提示**：您可以使用相同的語法來擷取發行模式憑證的金鑰雜湊。請取代指令中的別名及金鑰儲存庫路徑。

1. 複製透過 **keytool** 指令所取得的金鑰雜湊，並將其貼入 Facebook for Developers 網站中的「開發/發行金鑰雜湊」提示。

	**提示**：如果您計劃使用單一登入，請考慮啟用此特性。

1. 按一下**儲存設定**。

## 配置 {{site.data.keyword.amashort}} 服務以進行 Facebook 鑑別
{: #facebook-auth-android-mca}

具有「Facebook 應用程式 ID」並配置「Facebook 應用程式」來服務 Android 用戶端之後，即可利用 {{site.data.keyword.amashort}} 儀表板啟用 Facebook 鑑別。

1. 在儀表板中開啟 {{site.data.keyword.amashort}} 服務。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 展開 **Facebook** 區段。
1. 新增 **Facebook 應用程式 ID**。
1. 按一下**儲存**。

## 配置 {{site.data.keyword.amashort}} 用戶端 Android SDK 以進行 Facebook 鑑別
{: #facebook-auth-android-sdk}

若要配置適用於 Android 的用戶端 SDK，請使用 Android Studio 中的 Gradle 相依關係管理程式。

1.  開啟應用程式模組的 `build.gradle` 檔案。您的 Android 專案可能會有兩個 `build.gradle` 檔案：一個用於專案，另一個用於應用程式模組。請使用應用程式模組的檔案。

1. 尋找 `build.gradle` 檔案的 dependencies 區段，並新增用戶端 SDK 的編譯相依關係：

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

	**附註：**您可以移除對 `com.ibm.mobilefirstplatform.clientsdk.android` 群組的 `core` 模組的相依關係（如果它在您的檔案中）。`facebookauthentication` 模組會自動下載 `core` 模組及 Facebook 自己的 SDK。

	儲存更新之後，`facebookauthentication` 模組會下載所有必要的 SDK，並將其安裝在 Android 專案中。

1. 按一下**工具 > Android > 將專案與 Gradle 檔案同步化**，以將專案與 Gradle 同步化。

1. 開啟 `res/values/strings.xml` 檔案，並新增包含「Facebook 應用程式 ID」的 `facebook_app_id` 字串：

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```
	{: codeblock}

1. 在 Android 專案的 `AndroidManifest.xml` 檔案中：
	* 在 `<manifest>` 元素下，新增網際網路存取權：

		```XML
		<uses-permission android:name="android.permission.INTERNET" />
		```
		{: codeblock}

	* 將 Facebook SDK 的必要 meta 資料新增至 `<application>` 元素：

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
	<activity android:name="com.facebook.FacebookActivity"
				android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
				android:theme="@android:style/Theme.Translucent.NoTitleBar"
				android:label="@string/app_name" />
		</application>
		```
		{: codeblock}

1. 起始設定用戶端 SDK，並登錄鑑別管理程式。傳遞 **context** 及 **region**，以起始設定 {{site.data.keyword.amashort}} 用戶端 SDK。

	放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 `onCreate` 方法。<br/>

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	FacebookAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

   * 將 `BMSClient.REGION_UK` 取代為適當的地區。
   * 將 `<MCAServiceTenantId>` 取代為 `tenantId` 值。

	如需取得這些值的相關資訊，請參閱[開始之前](#before-you-begin)。

	**附註：**如果您的 Android 應用程式是以 Android 6.0 版（API 層次 23）或以上版本為目標，則必須確定應用程式先進行 `android.permission.GET_ACCOUNTS` 呼叫，再呼叫 `register`。如需相關資訊，請參閱 Android Developers 網站上的[這個主題 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.android.com/training/permissions/requesting.html){: new_window}。

1. 將下列程式碼新增至您的活動中：

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}


## 測試鑑別
{: #testing_auth}

起始設定用戶端 SDK 並登錄「Facebook 鑑別管理程式」之後，即可開始對行動後端提出要求。

### 開始測試之前
{: #facebook-auth-android-testing-before}

您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有受 {{site.data.keyword.amashort}} 保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](protecting-resources.html)。

1. 嘗試在瀏覽器中將要求傳送給新建的行動後端應用程式的受保護端點。開啟下列 URL：

	`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`。  

	使用 MobileFirst Services Starter 樣板所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。

1. 使用 Android 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 並登錄 `FacebookAuthenticationManager` 之後，請新增下列程式碼。

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

1. 執行您的應用程式。即會顯示 Facebook 登入畫面。

	![影像](images/android-facebook-login.png)

	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，以授權 {{site.data.keyword.amashort}} 使用您的 Facebook 使用者身分來進行鑑別。

1. 當要求成功時，LogCat 公用程式中會有下列輸出：

	![影像](images/android-facebook-login-success.png)

	您也可以新增下列程式碼，來新增登出功能：

	```
	FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```
	{: codeblock}

	如果您在使用者使用 Facebook 登入之後呼叫此程式碼，則會將使用者登出 Facebook。使用者嘗試再次登入時，系統會提示輸入其 Facebook 認證。

	傳遞給 logout 函數的 `listener` 值可以是 `null`。
