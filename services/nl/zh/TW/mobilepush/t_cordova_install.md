---

copyright:
 years: 2015, 2016

---

# 安裝 Cordova Push 外掛程式
{: #cordova_install}

安裝及使用 Client Push 外掛程式來進一步開發 Cordova 應用程式。這也會安裝起始設定您的 Bluemix 連線的 Cordova Core 外掛程式。

### 開始之前

1. 下載最新的 Android Studio SDK 及 Xcode 版本。
1. 設定您的模擬器。若為 Android Studio，請使用支援 Google Play API 的模擬器。
1. 安裝 Git 指令行工具。若為 Windows，請確保選取**從 Windows 命令提示字元執行 Git** 選項。如需如何下載並安裝此工具的相關資訊，請參閱 [Git](https://git-scm.com/downloads)。

1. 安裝 Node.js 及「Node 套件管理程式 (NPM)」工具。NPM 指令行工具與 Node.js 組合在一起。如需如何下載並安裝 Node.js 的相關資訊，請參閱 [Node.js](https://nodejs.org/en/download/)。
1. 從指令行中，使用 **npm install -g cordova** 指令來安裝 Cordova 指令行工具。若要使用 Cordova Push 外掛程式，這是必要動作。如需如何安裝 Cordova 以及設定 Cordova 應用程式的相關資訊，請參閱 [Cordova Apache](https://cordova.apache.org/#getstarted)。

	**附註**：若要檢視 Cordova Push 外掛程式 Readme 檔，請移至 [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)。


## 安裝 Cordova Push 外掛程式
1. 切換至您要在其中建立 Cordova 應用程式的資料夾，並執行下列指令來建立 Cordova 應用程式。如果您有現存的 Cordova 應用程式，請移至步驟 3。


	cordova create your_app_name
	cd your_app_name
	```
1. 選用項目：（選用）編輯 **config.xml** 檔案，並將 <name> 元素中的應用程式名稱變更為您選擇的名稱，而不是預設 HelloCordova 名稱。

	**附註**：請確定指定正確的軟體組 ID。如果您未指定，則會在 Xcode 中顯示錯誤訊息。
	* 以無效的授權簽署執行檔。
	* 應用程式的「程式碼簽署授權」檔案中指定的授權，不符合佈建設定檔中指定的授權。

	若要修正此問題，請在 Xcode 或 Cordova 應用程式 **config.xml** 檔案中指定正確的「軟體組 ID」。

1. 將最低支援的 API 或部署目標宣告新增至 Cordova 應用程式的 config.xml 檔案。minSdkVersion 值必須高於 15。targetSdkVersion 值必須一律反映可從 Google 取得的最新 Android SDK。
	* **Android** - 使用編輯器開啟 config.xml 檔案，然後使用最低及目標 SDK 版本更新
```<platform name="android">``` 元素：

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - 使用部署目標宣告更新 <platform name="ios"> 元素：

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. 從 Cordova 指令行介面 (CLI) 中，使用下列指令新增平台：iOS 及（或）Android。

	```
	cordova platform add ios
	cordova platform add android
	```
1. 從 Cordova 應用程式根目錄中，輸入下列指令來安裝 Cordova Push 外掛程式：**cordova plugin add ibm-mfp-push**。

	根據您新增的平台，您會看到與下列類似的內容：

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. 從 *your-app-root-folder* 中，使用下列指令，驗證已順利安裝 Cordova Core 及 Push 外掛程式：**cordova plugin list**。

	根據您新增的平台，您會看到與下列類似的內容：

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 "MFPPush"
	```
1. （僅限 iOS）- 配置 iOS 開發環境。
	a. 使用 Xcode 開啟 *your-app-name***/platforms/ios** 目錄中的 your-app-name.xcodeproj 檔案。

	b. 新增橋接標頭。移至**建置設定 > Swift 編譯器 - 產生程式碼 > Objective-C 橋接標頭**，然後新增下列路徑：*your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. 新增 Frameworks 參數。移至**建置設定 > 鏈結 > Runpath 搜尋路徑**，然後新增下列參數：
	```
	@executable_path/Frameworks
	```
	d. 解除註解橋接標頭中的下列 Push import 陳述式。移至 *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. 使用 Xcode 建置並執行應用程式。
1. （僅限 Android）- 使用下列指令建置 Android 專案：**cordova build android**。

	**附註**：在 Android Studio 中開啟專案之前，必須先透過 Cordova CLI 建置 Cordova 應用程式。否則，將發生建置錯誤。

1. 後續步驟。[起始設定 Cordova 外掛程式](t_cordova_initalize.html)。
