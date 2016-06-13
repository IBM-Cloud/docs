<!-- Attribute definitions -->
{:codeblock: .codeblock}

# 開始使用 HelloWorld 範例
{: #gettingstarted-cordova}

如果您要開始使用新的 Cordova 應用程式，可以使用 HelloWorld 應用程式。這個應用程式會示範如何從行動式應用程式連接到 Bluemix 後端而不需鑑別。應用程式已安裝 SDK。當您備妥時，即可取得想要在應用程式中使用的特定程式庫。

1. 在 Bluemix 中建立行動式後端。
<ol>
	<li>在 Bluemix 型錄的「樣板」區段中，按一下 MobileFirst Services Starter。</li>
    	<li>輸入您應用程式的名稱及主機，然後按一下**建立**。</li>
    	<li>按一下**完成**。</li>
</ol>
2. 從 GitHub 取得專案。您可以選擇性地使用 git clone 指令來取得專案。從您的電腦中，開啟終端機，然後輸入下列指令：
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. 從專案目錄中執行下列指令，以新增 Android 及 iOS 平台環境：

Android：
```
cordova platform add android
```

iOS：
```
cordova platform add ios
```

4. 使用下列指令，來新增 Cordova 外掛程式：
```
cordova plugin add ibm-mfp-core
```

5. 配置適用於 Android 及（或）iOS 的 Cordova 應用程式。

 * Android

	 在 Android Studio 中開啟專案之前，請透過指令行介面 (CLI) 建置及執行 Cordova 應用程式，以避免建置錯誤。

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 如下所示配置 Xcode 專案，以避免建置錯誤。

	    1. 使用最新版本的 Xcode，來開啟 &lt;app_name&gt;/platforms/ios 目錄中的 xcode.proj 檔案。

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

6. 配置 HelloWorld 範例
<ol>
	<li>切換至您已複製專案的目錄</li>
	<li>開啟 &lt;your_app_dir&gt;/www/js/index.js 檔案，並將 &lt;APPLICATION_ROUTE&gt; 及 &lt;APPLICATION_ID&gt; 取代為您的 Bluemix 應用程式 ID 及路徑值。</li>
</ol>

附註：請確定 &lt;APPLICATION_ROUTE&gt; 是使用 https 通訊協定進行保護。

```
// Bluemix credentials
route: "<APPLICATION_ROUTE>",
GUID: "<APPLICATION_GUID>",
```

7. 在行動式模擬器或裝置上執行範例。

   使用下列指令，來建置 Cordova 應用程式：
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   使用下列指令，來執行範例應用程式：
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


即會顯示具有 **PING BLUEMIX** 按鈕的單一視圖應用程式。當您點選此按鈕時，應用程式會測試從用戶端到後端 Bluemix 應用程式的連線。測試連線的方式是使用您在 index.js 檔案中指定的「應用程式路徑」。


![Hello World 應用程式順利連接至 Bluemix](images/yayconnected.jpg "圖 1. Hello World 應用程式順利連接至 Bluemix")

從行動式應用程式順利連接至 Bluemix 時，會顯示訊息：「耶！您連上了」。
8. 解決所有問題。

<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

如果連線失敗，則會顯示訊息：「糟糕，出問題了」。包括錯誤的相關資訊。
請檢查下列項目：
 * 驗證您已正確地貼上路徑及 GUID 值。
 * 檢視 Xcode 或 Android 除錯日誌。
 * 在 Bluemix 中檢查您應用程式的狀態。

## 後續步驟：
{: #next}
如需如何取得 SDK 並整合至行動式應用程式的相關資訊，請參閱「設定 Cordova Client SDK」。

# 相關鏈結

## 範例
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
