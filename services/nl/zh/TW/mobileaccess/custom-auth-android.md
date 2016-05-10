---

copyright:
  years: 2015, 2016

---

# 配置 {{site.data.keyword.amashort}} Client SDK for Android
{: #custom-android}
配置 Android 應用程式，這個應用程式利用自訂鑑別來使用 {{site.data.keyword.amashort}} Client SDK，並將您的應用程式連接至 {{site.data.keyword.Bluemix}}。

## 開始之前
{: #before-you-begin}
您必須具有配置成使用自訂身分提供者的 {{site.data.keyword.amashort}} 服務實例所保護的資源。您的行動式應用程式也必須使用 {{site.data.keyword.amashort}} Client SDK 進行檢測。如需相關資訊，請參閱下列資訊：
 * [開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [設定 Android SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)
 * [使用自訂身分提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [建立自訂身分提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 進行自訂鑑別](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## 起始設定 {{site.data.keyword.amashort}} Client SDK
{: #custom-android-initialize}
1. 在 Android Studio 的 Android 專案中，開啟應用程式模組的 `build.gradle` 檔案。
<br/>**提示：**Android 專案可能會有兩個 `build.gradle` 檔案：用於專案和應用程式模組。請使用應用程式模組檔案。

1. 在 `build.gradle` 檔案中，尋找 `dependencies` 區段，並檢查下列編譯相依關係。請新增這個相依關係（如果尚未存在）。

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

1. 將專案與 Gradle 同步化。按一下**工具 > Android > 將專案與 Gradle 檔案同步化**。

1. 開啟 Android 專案的 `AndroidManifest.xml` 檔案。
在 `<manifest>` 元素下，新增網際網路存取權：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```

1. 起始設定 SDK。放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 `onCreate` 方法。將 *applicationRoute* 及 *applicationGUID* 取代為您在 {{site.data.keyword.Bluemix_notm}} 儀表板上按一下應用程式中的**行動式選項**時取得的**路徑**及**應用程式 GUID** 值。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");					
	```

## AuthenticationListener 介面
{: #custom-android-authlistener}

{{site.data.keyword.amashort}} Client SDK 提供 `AuthenticationListener` 介面，讓您可以實作自訂鑑別流程。`AuthenticationListener` 介面公開在鑑別處理程序不同階段所呼叫的三種方法。

### onAuthenticationChallengeReceived 方法
{: #custom-onAuth}
從 {{site.data.keyword.amashort}} 服務接收自訂鑑別盤查時，會呼叫此方法。

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
#### 引數
{: #custom-android-onAuth-arg}

* `AuthenticationContext`：由 {{site.data.keyword.amashort}} Client SDK 所提供，讓您可以在認證收集期間回報鑑別盤查回答或失敗。例如，使用者取消鑑別時。
* `JSONObject`：包含自訂身分提供者所傳回的自訂鑑別盤查。
* `Context`：傳送要求時所使用的「Android 環境定義」的參照。此引數通常代表「Android 活動」。

透過呼叫 `onAuthenticationChallengeReceived` 方法，{{site.data.keyword.amashort}} Client SDK 會將控制權委派給開發人員。服務會等待認證。開發人員必須收集認證，並使用其中一種 `AuthenticationContext` 介面方法將它們回報給 {{site.data.keyword.amashort}} Client SDK。

### onAuthenticationSuccess 方法
{: #custom-android-authlistener-onsuccess}
在成功鑑別之後，會呼叫此方法。引數包括「Android 環境定義」以及內含鑑別成功延伸資訊的選用 JSONObject。
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```

### onAuthenticationFailure 方法
{: #custom-android-authlistener-onfail}
在鑑別失敗之後，會呼叫此方法。引數包括「Android 環境定義」以及內含鑑別失敗延伸資訊的選用 JSONObject。
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```

## AuthenticationContext 介面
{: #custom-android-authcontext}

`AuthenticationContext` 提供作為自訂 `AuthenticationListener` 的 `onAuthenticationChallengeReceived` 方法的引數。您必須收集認證，並使用 `AuthenticationContext` 方法將認證傳回給 {{site.data.keyword.amashort}} Client SDK 或報告失敗。請使用下列其中一種方法。

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
```Java
void submitAuthenticationFailure (JSONObject info);
```

## 自訂 AuthenticationListener 範例實作
{: #custom-android-samplecustom}

此 AuthenticationListener 範例設計成使用自訂身分提供者。您可以從 [Github 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)下載此範例。

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {
	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// In this sample the AuthenticationListener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authContext.submitAuthenticationChallengeAnswer() API

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// In case there was a failure collecting credentials you need to report
			// it back to the AuthenticationContext. Otherwise Mobile Client
			// Access Client SDK will remain in a waiting-for-credentials state
			// forever

			log("This should never happen...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```

## 登錄自訂 AuthenticationListener
{: #custom-android-register}

建立自訂 AuthenticationListener 之後，請先向 `BMSClient` 登錄它，再開始使用接聽器。將下列程式碼新增至應用程式。必須先呼叫此程式碼，再將任何要求傳送至受保護資源。

```Java
BMSClient.getInstance().registerAuthenticationListener(realmName,
									new CustomAuthenticationListener());
```

使用 {{site.data.keyword.amashort}} 儀表板中所指定的 *realmName*。


## 測試鑑別
{: #custom-android-testing}
起始設定 Client SDK 並登錄自訂 AuthenticationListener 之後，即可開始對行動式後端提出要求。

### 開始之前
{: #custom-android-testing-before}
您必須具有使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立的應用程式，並在 `/protected` 端點具有 {{site.data.keyword.amashort}} 所保護的資源。


1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），以在瀏覽器中將要求傳送給行動式後端的受保護端點。

1. 使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才能存取這個端點。因此，會在瀏覽器中顯示 `Unauthorized` 訊息。

1. 使用 Android 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 並登錄自訂 AuthenticationListener 之後，請新增下列程式碼。

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

1. 	當要求成功時，LogCat 工具中會有下列輸出：

	![影像](images/android-custom-login-success.png)

1. 您也可以新增下列程式碼，來新增登出功能：

 ```Java
 AuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 如果您在使用者登入之後呼叫此程式碼，則會將使用者登出。使用者嘗試再次登入時，必須再次回答接收自伺服器的盤查。

 傳遞給 logout 函數的 `listener` 值可以是空值。
