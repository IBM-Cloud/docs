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


# 配置適用於 {{site.data.keyword.amashort}} Android 應用程式的自訂鑑別
{: #custom-android}


配置 Android 應用程式搭配自訂鑑別來使用 {{site.data.keyword.amashort}} 用戶端 SDK，並將您的應用程式連接至 {{site.data.keyword.Bluemix}}。

## 開始之前
{: #before-you-begin}
開始之前，您必須具有：

* 配置為使用自訂身分提供者之 {{site.data.keyword.amashort}} 服務實例所保護的資源（請參閱[配置自訂鑑別](custom-auth-config-mca.html)）。  
* **承租戶 ID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* **領域**名稱。這是您在 {{site.data.keyword.amashort}} 儀表板的**管理**標籤上，**自訂**區段內的**領域名稱**欄位中指定的值。
* 後端應用程式的 URL（**應用程式路徑**）。在傳送要求至後端應用程式的受保護端點時，將需要此值。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`雪梨`或`英國`，並對應至 WebView Javascript 程式碼中所需的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY` 或 `BMSClient.REGION_UK`。您需要此值來起始設定 {{site.data.keyword.amashort}} 用戶端。

如需相關資訊，請參閱下列資訊：
 * [開始使用 {{site.data.keyword.amashort}}](getting-started.html)
 * [設定 Android SDK](getting-started-android.html)
 * [使用自訂身分提供者](custom-auth.html)
 * [建立自訂身分提供者](custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 進行自訂鑑別](custom-auth-config-mca.html)



## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #custom-android-initialize}
如果您的 Android 應用程式已使用 {{site.data.keyword.amashort}} Android SDK 進行檢測，則可以跳過本節。
1. 在 Android Studio 的 Android 專案中，開啟應用程式模組的 `build.gradle` 檔案（不是專案 `build.gradle`）。

1. 在 `build.gradle` 檔案中，尋找 `dependencies` 區段，並檢查下列相依關係是否存在。

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. 將專案與 Gradle 同步化。按一下**工具 > Android > 將專案與 Gradle 檔案同步化**。

1. 開啟 Android 專案的 `AndroidManifest.xml` 檔案。
在 `<manifest>` 元素下，新增網際網路存取權：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

1. 起始設定 SDK。  
	放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 `onCreate` 方法。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
```
	{: codeblock}

將 `BMSClient.REGION_UK` 取代為 {{site.data.keyword.amashort}} 地區。如需取得這些值的相關資訊，請參閱[開始之前](#before-you-begin)。


## AuthenticationListener 介面
{: #custom-android-authlistener}

{{site.data.keyword.amashort}} 用戶端 SDK 提供 `AuthenticationListener` 介面，讓您可以實作自訂鑑別流程。`AuthenticationListener` 介面會公開在鑑別處理期間於不同階段所呼叫的三個方法。

### onAuthenticationChallengeReceived 方法
{: #custom-onAuth}
從 {{site.data.keyword.amashort}} 服務收到自訂鑑別盤查時，會呼叫此方法。

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
{: codeblock}


#### 引數
{: #custom-android-onAuth-arg}

* `AuthenticationContext`：由 {{site.data.keyword.amashort}} 用戶端 SDK 所提供，讓您可以在認證收集期間回報鑑別盤查回答或失敗。例如，使用者取消鑑別時。
* `JSONObject`：包含自訂身分提供者所傳回的自訂鑑別盤查。
* `Context`：傳送要求時所使用的「Android 環境定義」的參照。此引數通常代表「Android 活動」。

透過呼叫 `onAuthenticationChallengeReceived` 方法，{{site.data.keyword.amashort}} 用戶端 SDK 會將控制權委派給開發人員。服務會等待認證。開發人員必須收集認證，並使用其中一種 `AuthenticationContext` 介面方法將它們回報給 {{site.data.keyword.amashort}} 用戶端 SDK。

### onAuthenticationSuccess 方法
{: #custom-android-authlistener-onsuccess}
在成功鑑別之後，會呼叫此方法。引數包含「Android 環境定義」以及內含鑑別成功延伸資訊的選用 JSONObject。

```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```
{: codeblock}

### onAuthenticationFailure 方法
{: #custom-android-authlistener-onfail}
在鑑別失敗之後，會呼叫此方法。引數包括「Android 環境定義」以及選用的 `JSONObject`，其中包含鑑別失敗的延伸資訊。
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```
{: codeblock}

## AuthenticationContext 介面
{: #custom-android-authcontext}

`AuthenticationContext` 提供作為自訂 `AuthenticationListener` 的 `onAuthenticationChallengeReceived` 方法的引數。您必須收集認證，並使用 `AuthenticationContext` 方法將認證傳回給 {{site.data.keyword.amashort}} 用戶端 SDK 或報告失敗。請使用下列其中一種方法。

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
{: codeblock}

```Java
void submitAuthenticationFailure (JSONObject info);
```
{: codeblock}

## 自訂 AuthenticationListener 範例實作
{: #custom-android-samplecustom}

此 AuthenticationListener 範例設計成使用自訂身分提供者。您可以從 [Github 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "外部鏈結圖示"){: new_window} 下載此範例。

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationListener;
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
			// Access client SDK will remain in a waiting-for-credentials state
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
{: codeblock}

## 登錄自訂 AuthenticationListener
{: #custom-android-register}

建立自訂 AuthenticationListener 之後，請先向 `BMSClient` 登錄它，再開始使用接聽器。將下列程式碼新增至應用程式。必須在將任何要求傳送至受保護資源之前先呼叫此程式碼。

```Java
MCAAuthorizationManager mcaAuthorizationManager = 
      MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<MCAServiceTenantId>");
mcaAuthorizationManager.registerAuthenticationListener(realmName, new CustomAuthenticationListener());
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);

```
{: codeblock}


在程式碼中：
* 將 `MCAServiceTenantId` 取代為 **TenantId** 值（請參閱[開始之前](##before-you-begin)）。
* 使用您在 {{site.data.keyword.amashort}} 儀表板中指定的 `realmName`（請參閱[配置自訂鑑別](custom-auth-config-mca.html)）。


## 測試鑑別
{: #custom-android-testing}
起始設定用戶端 SDK 並登錄自訂 AuthenticationListener 之後，即可開始對行動後端應用程式提出要求。

### 測試之前
{: #custom-android-testing-before}
您必須具有資源位於 `/protected` 端點且受 {{site.data.keyword.amashort}} 所保護的應用程式。


1. 從瀏覽器中將要求傳送至行動後端應用程式的受保護端點 (`{applicationRoute}/protected`)，例如 `http://my-mobile-backend.mybluemix.net/protected`。如需取得 `{applicationRoute}` 值的相關資訊，請參閱[開始之前](#before-you-begin)。

1. 使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。因此，會在瀏覽器中顯示 `Unauthorized` 訊息。

1. 使用 Android 應用程式以對包含 `{applicationRoute}` 的相同受保護端點提出要求。起始設定 `BMSClient` 並登錄自訂 AuthenticationListener 之後，請新增下列程式碼。

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp",  MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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

1. 	當要求成功時，LogCat 工具中會有下列輸出：

	![影像](images/android-custom-login-success.png)

 您也可以新增下列程式碼，來新增登出功能：

 ```Java
 MCAAuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```
 {: codeblock}


 如果您在使用者登入之後呼叫此程式碼，則會將使用者登出。使用者嘗試再次登入時，必須再次回答從伺服器收到的盤查。

 傳遞給 logout 函數的 `listener` 值可以是 `null`。
