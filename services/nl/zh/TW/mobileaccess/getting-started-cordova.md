---

copyright:
  years: 2015, 2016
  
---

# 設定 Cordova 外掛程式
{: #getting-started-cordova}

使用 {{site.data.keyword.amashort}} Client SDK 檢測 Cordova 應用程式、起始設定 SDK，以及對受保護資源及未受保護資源提出要求。

## 開始之前
{: #before-you-begin}

- 您必須具有 {{site.data.keyword.amashort}} 服務所保護之行動式後端的實例。如需如何建立行動式後端的相關資訊，請參閱[開始使用](getting-started.html)。

- 建立 Cordova 應用程式，或使用現有專案。如需如何設定 Cordova 應用程式的相關資訊，請參閱 [Cordova 網站](https://cordova.apache.org/)。

## 安裝 {{site.data.keyword.amashort}} Cordova 外掛程式
{: #getting-started-cordova-plugin}

{{site.data.keyword.amashort}} Client SDK for Cordova 是包裝原生 {{site.data.keyword.amashort}} Client SDK 的 Cordova 外掛程式。它是使用「Cordova 指令行介面 (CLI)」及 `npmjs`（Cordova 專案的外掛程式儲存庫）進行配送。Cordova CLI 會從儲存庫中自動下載外掛程式，並使它們可供 Cordova 應用程式使用。

1. 將 Android 及 iOS 平台新增至 Cordova 應用程式。從指令行中，執行下列一個或兩個指令：

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. 如果您已新增 Android 平台，則必須將最低支援的 API 層次新增至 Cordova 應用程式的 `config.xml` 檔案。開啟 `config.xml` 檔案，並將下行新增至 `<platform name="android">` 元素：

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	*minSdkVersion* 值必須高於 `15`。*targetSdkVersion* 值必須是可從 Google 取得的最新 Android SDK。



1. 如果您已新增 iOS 作業系統，請使用目標宣告來更新 `<platform name="ios">` 元素：

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
	</platform>
	```

1. 安裝 {{site.data.keyword.amashort}} Cordova 外掛程式：

 	```Bash
	cordova plugin add ibm-mfp-core
	```

1. 為 Android、iOS 或兩者配置您的平台。

	* **Android**

		在 Android Studio 開啟您的專案之前，請透過指令行介面 (CLI) 建置您的 Cordova 應用程式，以避免發生建置錯誤。

		```
		cordova build android
		```

	* **iOS**

		如下所示配置 Xcode 專案，以避免發生建置錯誤。

		1. 使用最新版的 Xcode，開啟 &lt;*app_name*&gt;/platforms/ios 目錄中的 xcode.proj 檔案。

		**重要事項：**如果您收到一則訊息指出「轉換為最新 Swift 語法」，請按一下「取消」。

		2. 移至**建置設定 > Swift 編譯器 - 產生程式碼 > Objective-C 橋接標頭**，並新增下列路徑：

			```
			<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. 移至**建置設定 > 鏈結 > Runpath 搜尋路徑**，並新增下列 Frameworks 參數：

			```
			@executable_path/Frameworks
			```

		4. 使用 Xcode 建置並執行您的應用程式。

1. 執行下列指令，驗證已順利安裝外掛程式：
    

	```Bash
	cordova plugin list
	```

## 起始設定 {{site.data.keyword.amashort}} Client 外掛程式
{: #getting-started-cordova-initialize}

若要使用 {{site.data.keyword.amashort}} Client SDK，您必須傳遞 *applicationGUID* 及 *applicationRoute* 參數來起始設定 SDK。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板的主頁面上，尋找路徑及應用程式 GUID 值。依序按一下應用程式名稱及**行動式選項**，以顯示**應用程式路徑**及**應用程式 GUID** 值來起始設定 SDK。

3. 新增下列呼叫到 `index.js` 檔案，以起始設定 {{site.data.keyword.amashort}} Client SDK。將 *applicationRoute* 及 *applicationGUID* 取代為 {{site.data.keyword.Bluemix_notm}} 儀表板中**行動式選項**的值。

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

## 對行動式後端提出要求
{: #getting-started-request}

起始設定 {{site.data.keyword.amashort}} Client SDK 之後，即可開始對行動式後端提出要求。

1. 嘗試將要求傳送給新行動式後端的受保護端點。在瀏覽器中，開啟下列 URL：`{applicationRoute}/protected`。例如：

	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	使用 MobileFirst Services Starter 樣板所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。瀏覽器中會傳回 `Unauthorized` 訊息。傳回此訊息的原因是只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才會存取這個端點。



1. 使用 Cordova 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 之後，請新增下列程式碼：

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
		console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

1. 當要求成功時，您會在 LogCat 或 Xcode 主控台中看到下列輸出（視使用的平台而定）：

	![影像](images/getting-started-android-success.png)

	## 後續步驟
	{: #next-steps}

	當您連接至受保護端點時，不需要任何認證。若需要使用者登入應用程式，您必須配置 Facebook、Google 或自訂鑑別。
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [自訂](custom-auth-cordova.html)
