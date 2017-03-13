---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 Cordova 應用程式檢測 MQA（已淘汰）
{: #instrumentcord}

若要使用 {{site.data.keyword.mqafull}} 搭配 Cordova 應用程式，您必須下載 SDK 並使用指令行介面進行一些變更來加以檢測。
{: shortdesc}

使用 {{site.data.keyword.mqa}} 檢測應用程式之前，您必須有 {{site.data.keyword.Bluemix}} 帳戶，以及適合要檢測之應用程式平台的正確安裝開發環境版本。

若要檢測 {{site.data.keyword.mqa}} 以便搭配 Cordova 應用程式使用，請完成下列作業：

1. 將必要的許可權和已下載的 SDK 新增至您的 Cordova 專案。

	1. 開啟命令提示字元，並導覽至包含專案檔案的目錄。

	2. 視您的環境而定，完成下列步驟以將 {{site.data.keyword.mqa}} 外掛程式新增至 Cordova 專案：

		**重要事項**：如果您在 iOS 9 上使用 Xcode 7.x，您必須在 Xcode Build Settings 中將 Enable Bitcode 設定設為 No。您可以使用 Cordova 專案檔 .xcodeproj 開啟 Xcode，以變更此設定。該檔案位於 platform\iPhone 資料夾。

		* IBM MobileFirst™ Platform Foundation 7.1 版：

			1. 輸入下列指令，以安裝 {{site.data.keyword.mqa}} 外掛程式：

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			其中 *plugin_location* 是擷取出來的已下載 {{site.data.keyword.mqa}} 外掛程式的目錄路徑。

			2. 如果您的應用程式在 Android 上執行，請將 `project_name/app_name/platforms/android/custom_rules.xml` 檔案重新命名為 `custom_rules.xml.bak`。

		* 4.0 版以前的 Apache Cordova：
			1. 輸入下列指令，以安裝 {{site.data.keyword.mqa}} 外掛程式：

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			其中 *plugin_location* 是擷取出來的已下載 {{site.data.keyword.mqa}} 外掛程式的目錄路徑。

			2. 輸入下列指令，以新增其他必要外掛程式：

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. 如果您的應用程式在 Android 上執行，請將 `project_name/app_name/platforms/android/custom_rules.xml` 檔案重新命名為 `custom_rules_bak.xml`。

		* 4.0 版或更新版本的 Apache Cordova：

			1. 輸入下列指令：

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			其中 *plugin_location* 是擷取出來的已下載 {{site.data.keyword.mqa}} Cordova 外掛程式的目錄路徑。

			2. 輸入下列指令，以新增其他必要外掛程式：

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. 啟動新的 {{site.data.keyword.mqa}} 階段作業，以開始進行每個登入。

	1. 開啟下列目錄中的 `index.js` 檔案：`your_project_name\www\js`。

	2. 在 `index.js` 檔案的 `onDeviceReady()` 函數內，新增下列函數及參數。將函數放在函數的結束大括弧之前。

	限制：對於已經針對 Mobile Quality Assurance 使用舊版 Cordova 外掛程式進行檢測的應用程式，若要使用 Mobile Quality Assurance Cordova 外掛程式 3.0.18 以及更新版本所包含的特性，您必須重新產生並更換應用程式索引鍵。如需如何重新產生應用程式索引鍵的相關資訊，請參閱「管理應用程式設定」。在 2016 年二月以前產生的應用程式索引鍵，可持續搭配較舊的外掛程式運作，但您將外掛程式升級到 3.0.18 版或更新版本之後，便無法再運作。

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// or mode: "MARKET" for production mode.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. 繼續執行[開始使用 {{site.data.keyword.mqa}}](index.html) 中的步驟。



# 相關鏈結
{: #rellinks notoc}

## 相關鏈結
{: #general notoc}
* [開始使用 {{site.data.keyword.mqa}}](index.html){:new_window}
