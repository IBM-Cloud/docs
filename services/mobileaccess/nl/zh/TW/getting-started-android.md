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

# 設定 Android SDK
{: #getting-started-android}

使用 {{site.data.keyword.amafull}} 用戶端 SDK 檢測 Android 應用程式、起始設定 SDK，以及對受保護資源及未受保護資源提出要求。
{: shortdesc}

## 開始之前
{: #before-you-begin}

您必須具有：

* {{site.data.keyword.Bluemix_notm}} 應用程式的實例。
* {{site.data.keyword.amafull}} 服務的實例。
* **承租戶 ID**。在 {{site.data.keyword.amafull}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* **應用程式路徑**。這是後端應用程式的 URL。在傳送要求至其受保護端點時，將需要此值。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`雪梨`或`英國`，並對應至程式碼中所需的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY` 或 `BMSClient.REGION_UK`。您需要此值來起始設定 {{site.data.keyword.amashort}} 用戶端。
* 設定成使用 Gradle 的 Android Studio 專案。如需如何設定 Android 開發環境的相關資訊，請參閱 [Google Developer Tools ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://developer.android.com/sdk/index.html){: new_window}。

## 安裝 {{site.data.keyword.amashort}} 用戶端 SDK
{: #install-mca-sdk}

{{site.data.keyword.amashort}} 用戶端 SDK 是使用 Gradle（Android 專案的相依關係管理程式）進行配送。Gradle 會從儲存庫中自動下載構件，並使它們可供 Android 應用程式使用。

1. 建立 Android Studio 專案，或開啟現有專案。

1. 開啟適用於您的應用程式的 `build.gradle` 檔案（**不是**專案 `build.gradle` 檔案）。

1. 尋找 `build.gradle` 檔案的 **dependencies** 區段。新增 {{site.data.keyword.amashort}} 用戶端 SDK 的編譯相依關係：

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

1. 將專案與 Gradle 同步化。按一下**工具 &gt; Android &gt; 將專案與 Gradle 檔案同步化**。

1. 開啟 Android 專案的 `AndroidManifest.xml` 檔案。在 `<manifest>` 元素下，新增網際網路存取權：

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

## 起始設定 {{site.data.keyword.amashort}} 用戶端 SDK
{: #initalize-mca-sdk}

將 **context** 及 **region** 參數傳遞給 `initialize` 方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 `onCreate` 方法。

```Java
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
					
  BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));
						
	```
{: codeblock}

* 將 `<applicationBluemixRegion>` 取代為管理 {{site.data.keyword.Bluemix_notm}} 服務的地區。
* 將 `<MCAServiceTenantId>` 取代為 **tenantId** 

。
如需這些值的相關資訊，請參閱[開始之前](#before-you-begin)。

## 對行動後端應用程式提出要求
{: #request}

起始設定 {{site.data.keyword.amashort}} 用戶端 SDK 之後，即可開始對行動後端應用程式提出要求。

1. 嘗試傳送要求至行動後端應用程式的受保護端點。在瀏覽器中，開啟下列 URL：`{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`）。   

	使用 MobileFirst Services Starter 樣板所建立之行動後端應用程式的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。在瀏覽器中會傳回 `Unauthorized` 訊息，因為只有使用 {{site.data.keyword.amashort}} 用戶端 SDK 所檢測的行動應用程式才能存取這個端點。



1. 使用 Android 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼：

	```Java
	Request request = new Request("http://my-mobile-backend.mybluemix.net/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
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

1. 當要求成功時，您會在 LogCat 公用程式中看到下列輸出：

	![影像](images/getting-started-android-success.png)

## 後續步驟
{: #next-steps}

當您連接至受保護端點時，不需要任何認證。若需要使用者登入應用程式，您必須配置 Facebook、Google 或自訂鑑別。

* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [自訂](custom-auth-android.html)
