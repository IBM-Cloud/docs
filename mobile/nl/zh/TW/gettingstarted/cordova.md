---

copyright:
  years: 2015, 2016

---
<!-- Attribute definitions -->
{:codeblock: .codeblock}

# 開始使用 HelloWorld 範例
{: #gettingstarted-cordova}
*前次更新：2016 年 3 月 17 日*

如果您要開始使用新的 Cordova 應用程式，可以使用 HelloWorld 應用程式。這個應用程式會示範如何從行動式應用程式連接到 {{site.data.keyword.Bluemix}} 的行動式後端而不需鑑別。應用程式已安裝 SDK。當您準備好時，便可以取得想要在應用程式中使用的特定程式庫。

1. 在 {{site.data.keyword.Bluemix_notm}} 中建立行動式後端。

	1. 在 {{site.data.keyword.Bluemix_notm}} 型錄的「樣板」區段中，按一下 MobileFirst Services Starter。
	1. 輸入您應用程式的名稱及主機，然後按一下**建立**。
	1. 按一下**完成**。

2. 從 GitHub 取得專案。您可以使用 git clone 指令來取得專案。從您的電腦中，開啟終端機，然後輸入下列指令：

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. 從專案目錄執行下列指令，以新增 Android 及 iOS 平台環境：

	### Android

	```Bash
	cordova platform add android
	```

	### iOS

	```Bash
	cordova platform add ios
	```

4. 使用下列指令新增 Cordova 外掛程式：

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. 配置 HelloWorld 範例。

	* 切換至複製專案的目錄。
	* 開啟 *&lt;your_app_dir&gt;*/www/js/index.js 檔案，並將 *&lt;APPLICATION_ROUTE&gt;* 和 *&lt;APPLICATION_ID&gt;* 取代為 Bluemix 應用程式 ID 和路徑值。

		**附註：**請確定您的路徑安全地使用 https 通訊協定。

		```Javascript
		// Bluemix credentials
		route: "<APPLICATION_ROUTE>",
		GUID: "<APPLICATION_GUID>",
		```

6. 為 iOS 配置 Cordova 應用程式。Android 平台不需要其他配置。

	### iOS
  配置 Xcode 專案以避免發生建置錯誤，如下所示。

	1. 使用最新版的 Xcode 來開啟 *&lt;app_name&gt;*/platforms/ios 目錄中的 `xcode.proj` 檔案。

		**重要事項：**如果收到「轉換為最新 Swift 語法」的訊息，請按一下**取消**。

	2. 移至**建置設定 > Swift 編譯器 - 產生程式碼 > Objective-C 橋接器標頭**，並新增下列路徑：

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```

	3. 移至**建置設定 > 鏈結 > Runpath 搜尋路徑**，並新增下列 Frameworks 參數：

		```
		@executable_path/Frameworks
			```

7. 在行動式模擬器或裝置上建置並執行此範例。

  ### Android
	1. 使用下列指令建置 Cordova 應用程式：

    **重要事項：**在 Android Studio 中開啟專案之前，您必須先透過 Cordova 指令行介面 (CLI) 建置您的 Cordova 應用程式。否則，您會遇到建置錯誤。

	```Bash
	cordova build android
	```

	2. 在 Android Studio 中執行範例應用程式。

  ### iOS
  1. 在 Xcode 中建置 Cordova 應用程式。

    **提示：**在 Xcode 中建置可提供更多選項，例如除錯及專案配置。

  2. 在 Xcode 中執行範例應用程式。

即會顯示含有**連線測試 BLUEMIX** 按鈕的單一視圖應用程式。當您點選此按鈕時，應用程式會測試從用戶端連至後端 {{site.data.keyword.Bluemix_notm}} 應用程式的連線。此連線將使用您在 `index.js` 檔案中指定的應用程式路徑來進行測試。


![Hello World 應用程式順利連接 Bluemix](images/yayconnected.jpg "圖 1. Hello World 應用程式順利連接 Bluemix")


當您順利從行動式應用程式連接至 {{site.data.keyword.Bluemix_notm}} 時，即會顯示訊息「耶！您連上了」。


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

如果連線失敗，則會顯示錯誤訊息。訊息中包含了錯誤的相關資訊。您可以檢查下列項目來進行錯誤疑難排解：

- 驗證您已正確地貼上路徑及 GUID 值。
- 檢視 Xcode 或 Android 除錯日誌。
- 檢查 {{site.data.keyword.Bluemix_notm}} 中應用程式的狀態。

## 後續步驟：
{: #next}
如需如何取得 SDK 並整合到您的行動式應用程式的相關資訊，請參閱：
* [Mobile Client Access：設定 Cordova 外掛程式](../../services/mobileaccess/getting-started-cordova.html)
* [Push Notifications：設定 Cordova 外掛程式](../../services/mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# 相關鏈結

## 範例
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## SDK
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
