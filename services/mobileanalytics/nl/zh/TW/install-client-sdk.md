---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

# 安裝 {{site.data.keyword.mobileanalytics_short}} Client SDK
{: #mobileanalytics_sdk}

{{site.data.keyword.mobileanalytics_short}}
Client SDK 目前適用於 Android、iOS、WatchOS 及 Cordova。
{: #shortdesc}

## 安裝 Android Client SDK
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

{{site.data.keyword.mobileanalytics_short}} Client SDK 隨 Gradle（Android 專案的相依關係管理程式）一起配送。Gradle 會從儲存庫自動下載構件，並讓它們可供 Android 應用程式使用。

1. 建立 [Android Studio](http://developer.android.com/sdk/index.html) 專案，或開啟現有專案。

2. 開啟**應用程式模組**中的 `build.gradle` 檔案。

  **提示**：您的 Android 專案可能有兩個 `build.gradle` 檔案：一個適用於專案，一個適用於應用程式模組。請務必使用**應用程式模組**檔案。

3. 找到 `build.gradle` 檔案的 `Dependencies` 區段，並新增 {{site.data.keyword.mobileanalytics_short}} Client SDK 的編譯相依關係。您的儲存庫陳述式應該類似於下列程式碼範例：

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  ```
  {: codeblock}

4. 按一下**工具 &gt; Android &gt; 將專案與 Gradle 檔案同步化**，以將專案與 Gradle 同步化。

5. 開啟 Android 專案的 `AndroidManifest.xml` 檔案。您可以在**應用程式 > 資訊清單**中找到此檔案。在 `<manifest>` 元素下新增網際網路存取權：

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. 您現在已安裝 Android Client SDK。接下來，請[匯入並起始設定](sdk.html#initalize-ma-sdk) Analytics Client SDK。   

## 安裝 Swift SDK
{: #installing-sdk-ios}

![CocoaPods 相容](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

{{site.data.keyword.mobileanalytics_full}} SDK 可讓您檢測行動應用程式。Swift SDK 適用於 iOS 及 watchOS。

### 開始之前
{: #before-you-begin-ios}

請確定已正確設定 Xcode。若要瞭解如何設定 iOS 開發環境，請參閱 [Apple Developer 網站](https://developer.apple.com/support/xcode/)。請閱讀 Client SDK Swift Analytics 的 [Xcode 需求](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements)。

{{site.data.keyword.mobileanalytics_short}} SDK 隨 [CocoaPods](https://cocoapods.org/) 及 [Carthage](https://github.com/Carthage/Carthage#getting-started)（Cocoa 專案的相依關係管理程式）一起配送。CocoaPods 及 Carthage 會從儲存庫自動下載構件，並讓它們可供應用程式使用。選取 CocoaPods 或 Carthage：

#### CocoaPods
{: #cocoapods}

1. 遵循 GitHub 上的 [{{site.data.keyword.Bluemix_notm}} Mobile Services Swift SDK 指示](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods)，以使用 CocoaPods 來安裝 `BMSAnalytics`，並將它新增至 Podfile 中。 
	
2. 在安裝 iOS Client SDK 之後，請[匯入並起始設定](sdk.html#initalize-ma-sdk) Analytics Client SDK。   

#### Carthage
{: #carthage}

如果您不是使用 CocoaPods，則可以使用 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 將架構新增至專案中。

1. 遵循 GitHub 上的 [Carthage 安裝指示](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage)來安裝 `BMSAnalytics`。

2. 在安裝 iOS Client SDK 之後，請[匯入並起始設定](sdk.html#initalize-ma-sdk) Analytics Client SDK。

## 安裝 Cordova 外掛程式
{: #installing-sdk-cordova}

{{site.data.keyword.mobileanalytics_full}} Cordova 外掛程式<!--SDK-->可讓您檢測行動應用程式。 

1. 將 Android 及 iOS 平台新增至 Cordova 應用程式中。從指令行中，執行下列其中一或兩個執行：

	```Bash
	cordova platform add android
	```
	
	```Bash
	cordova platform add ios
	```
	
2. 如果您已新增 Android 平台，則必須將最低支援 API 層次新增至 Cordova 應用程式的 `config.xml` 檔案中。開啟 `config.xml` 檔案，並將下列這幾行新增至 `<platform name="android">` 元素：

	```XML
	<platform name="android">  
  	<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
  </platform>
```
*minSdkVersion* 值必須高於 `15`。請參閱 [Android 平台指南](https://cordova.apache.org/docs/en/latest/guide/platforms/android/)，以保持現行支援的 Android SDK *targetSdkVersion*。

3. 如果您已新增 iOS 作業系統，請使用目標宣告來更新 `<platform name="ios">` 元素：

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  </platform>
```

4. 安裝 {{site.data.keyword.mobileanalytics_short}} Cordova 外掛程式：

 	```Bash
	cordova plugin add bms-core
	```

5. 請執行下列指令來確認外掛程式已順利安裝：
	```Bash
	cordova plugin list
	```
	
6. 您現在已安裝 Cordova 外掛程式。接下來，請[匯入並起始設定](sdk.html#initalize-ma-sdk) Analytics Client SDK。

# 相關鏈結

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova 外掛程式核心 SDK](https://www.npmjs.com/package/bms-core){: new_window}

## API 參考資料
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
