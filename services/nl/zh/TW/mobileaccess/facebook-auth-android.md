---

copyright:
  years: 2015, 2016

---

# 在 Android 應用程式中啟用 Facebook 鑑別
{: #facebook-auth-android}
若要使用 Facebook 作為 Android 應用程式中的身分提供者，請針對 Facebook 應用程式新增及配置 Android 平台。

## 開始之前
{: #facebook-auth-android-before}
 * 您必須具有 {{site.data.keyword.amashort}} 所保護的資源，以及使用 {{site.data.keyword.amashort}} Client SDK 所檢測的 Android 專案。如需相關資訊，請參閱[開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 及[設定 Android SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)。  
 * 使用 {{site.data.keyword.amashort}} Server SDK，手動保護後端應用程式。如需相關資訊，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。
 * 建立「Facebook 應用程式 ID」。如需相關資訊，請參閱[從 Facebook 開發人員入口網站取得 Facebook 應用程式 ID](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。


## 配置 Android 平台的 Facebook 應用程式
{: #facebook-auth-android-config}
若要使用 Facebook 作為 Android 應用程式中的身分提供者，您必須針對 Facebook 應用程式新增及配置 Android 平台。

1. 在「Facebook 開發人員入口網站」中，開啟 Facebook 應用程式。

1. 按一下**設定 &gt; 新增平台 &gt; Android**。

1. 在「Google Play 套件名稱」提示中，指定 Android 應用程式的套件名稱。若要尋找 Android 應用程式的套件名稱，請在 Android Studio 中開啟 `AndroidManifest.xml` 檔案，並尋找 `<manifest ..... package="{your-package-name}">`。

1. 在**類別名稱**提示中，指定主要活動的類別名稱。若要尋找 Android 應用程式的主要活動類別名稱，請開啟 `AndroidManifest.xml` 檔案，並使用與下列程式碼 Snippet 類似的目的過濾器來尋找活動宣告：

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

1. 為了讓 Facebook 確保應用程式確實性，您必須指定開發人員憑證 SHA1 的雜湊。

	**進一步瞭解 Android 安全：**Android OS 需要使用開發人員憑證來簽署 Android 裝置上安裝的所有應用程式。Android 應用程式可以使用兩種模式建置：除錯及發行。<br/>請針對除錯及發行模式使用不同的憑證。用於以除錯模式簽署 Android 應用程式的憑證會與 Android SDK（通常是由 Android Studio 自動安裝）組合。當您要將應用程式發行到 Google Play 商店時，必須使用通常自行產生的另一個憑證來簽署應用程式。<br/>您可以使用 Facebook 輸入兩組金鑰雜湊：一個金鑰雜湊是針對使用除錯憑證以除錯模式所建置的應用程式，另一個金鑰雜湊則是針對使用發行憑證以發行模式所建置的應用程式。如需相關資訊，請參閱[簽署 Android 應用程式](http://developer.android.com/tools/publishing/app-signing.html)。

1. 包含用於開發環境之憑證的金鑰儲存庫儲存在 `~/.android/debug.keystore` 檔案中。預設金鑰儲存庫密碼為：`android`。請使用此憑證，以除錯模式建置應用程式。

1. 擷取除錯模式憑證的金鑰雜湊：

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```

	**提示**：您可以使用相同的語法來擷取發行模式憑證的金鑰雜湊。請取代指令中的別名及金鑰儲存庫路徑。

1. 複製透過 **keytool** 指令所取得的金鑰雜湊，並將其貼入「Facebook 開發人員入口網站」中的「開發/發行金鑰雜湊」提示。

	**提示**：如果您計劃使用此特性，請考慮啟用單一登入。

1. 按一下**儲存設定**。

## 配置 {{site.data.keyword.amashort}} 進行 Facebook 鑑別
{: #facebook-auth-android-mca}
具有「Facebook 應用程式 ID」並配置「Facebook 應用程式」來服務 Android 用戶端之後，即可在 {{site.data.keyword.amashort}} 儀表板中啟用 Facebook 鑑別。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。

1. 按一下**行動式選項**，並記下您的**路徑** (`applicationRoute`) 及 **應用程式 GUID** (`applicationGUID`)。起始設定 SDK 時，您需要這些值。

1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。

1. 按一下 **Facebook** 磚。

1. 指定「Facebook 應用程式 ID」，然後按一下**儲存**。

## 配置 {{site.data.keyword.amashort}} Client SDK for Android
{: #facebook-auth-android-sdk}
若要配置 Client SDK for Android，請使用 Android Studio 中的 Gradle 相依關係管理程式。

1.  開啟應用程式模組的 `build.gradle` 檔案。
Android 專案可能會有兩個 `build.gradle` 檔案：用於專案和應用程式模組。請使用應用程式模組檔案。

1. 尋找 `build.gradle` 檔案的 dependencies 區段，並新增 Client SDK 的編譯相依關係：

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

	您可以移除對 `com.ibm.mobilefirstplatform.clientsdk.android` 群組的 `core` 模組的相依關係（如果它在您的檔案中）。`facebookauthentication` 模組會自動下載 `core` 模組。

  儲存更新之後，`facebookauthentication` 模組會下載 Facebook SDK，並將它安裝在 Android 專案中。


1. 將專案與 Gradle 同步化。按一下**工具 > Android > 將專案與 Gradle 檔案同步化**。

1. 開啟 `res/values/strings.xml` 檔案，並新增包含「Facebook 應用程式 ID」的 `facebook_app_id` 字串：

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```

1. 在 Android 專案的 `AndroidManifest.xml` 檔案中：
   1. 在 `<manifest>` 元素下，新增網際網路存取權：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```
  2. 將 Facebook SDK 的必要 meta 資料新增至 `<application>` 元素：

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
```

   1. 在現有活動下，新增「Facebook 活動」元素：

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>

		<activity 	android:name="com.facebook.FacebookActivity"
					android:configChanges=
						"keyboard|keyboardHidden|screenLayout|screenSize|orientation"
					android:theme="@android:style/Theme.Translucent.NoTitleBar"
					android:label="@string/app_name" />

	</application>
```

1. 起始設定 Client SDK，並登錄 Facebook 鑑別管理程式。透過傳遞環境定義、應用程式 GUID (`applicationGUID`) 及路徑 (`applicationRoute`) 參數，來起始設定 {{site.data.keyword.amashort}} Client SDK。<br/>
 放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 `onCreate` 方法。<br/>
 將 *applicationRoute* 及 *applicationGUID* 取代為 Bluemix 儀表板中應用程式主頁面上的**行動式選項**功能表中的**路徑**及**應用程式 GUID** 值。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	FacebookAuthenticationManager.getInstance().register(this);
```


1. 將下列程式碼新增至「活動」：

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## 測試鑑別
起始設定 Client SDK 並登錄「Facebook 鑑別管理程式」之後，即可開始對行動式後端提出要求。

### 開始之前
{: #facebook-auth-android-testing-before}
您必須使用 {{site.data.keyword.mobilefirstbp}} 樣板，並且在 `/protected` 端點已具有 {{site.data.keyword.amashort}} 所保護的資源。如果您需要設定 `/protected` 端點，請參閱[保護資源](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)。

1. 嘗試在瀏覽器中將要求傳送給新建行動式後端的受保護端點。開啟下列 URL：`{applicationRoute}/protected`。例如：`http://my-mobile-backend.mybluemix.net/protected`。
<br/>使用 MobileFirst Services Starter 樣板所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才能存取這個端點。

1. 使用 Android 應用程式以對相同的端點提出要求。在起始設定 `BMSClient` 並登錄 `FacebookAuthenticationManager` 之後，請新增下列程式碼。

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
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

1. 執行您的應用程式。即會顯示 Facebook 登入畫面。

	![影像](images/android-facebook-login.png)

	如果您未在裝置上安裝 Facebook 應用程式，或目前未登入 Facebook，則此畫面可能會稍微不同。

1. 按一下**確定**，以授權 {{site.data.keyword.amashort}} 使用 Facebook 使用者身分來進行鑑別。

1. 	當要求成功時，LogCat 公用程式中會有下列輸出：

	![影像](images/android-facebook-login-success.png)

1. 您也可以新增下列程式碼，來新增登出功能：

 ```
FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 如果您在使用者使用 Facebook 登入之後呼叫此程式碼，則會將使用者登出 Facebook。使用者嘗試再次登入時，系統會提示輸入其 Facebook 認證。

 傳遞給 logout 函數的 `listener` 值可以是空值。
