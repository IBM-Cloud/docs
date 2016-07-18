---

copyright:
  years: 2015, 2016

---

# 安裝 {{site.data.keyword.mobileanalytics_short}}
Client SDK
{: #mobileanalytics_sdk}
*前次更新：2016 年 4 月 21 日*
{: .last-updated}

{{site.data.keyword.mobileanalytics_short}}
Client SDK 目前適用於 Android、iOS 及 WatchOS。
{: #shortdesc}

## 安裝 Android Client SDK
{: #install-sdk-android}

{{site.data.keyword.mobileanalytics_short}} Client SDK 隨 Gradle（Android 專案的相依關係管理程式）一起配送。Gradle 會從儲存庫自動下載構件，並讓它們可供 Android 應用程式使用。

1. 建立 [Android Studio](http://developer.android.com/sdk/index.html) 專案，或開啟現有專案。

2. 開啟應用程式模組中的 `build.gradle` 檔案。

  **提示**：您的 Android 專案可能有兩個 `build.gradle` 檔案：一個適用於專案，一個適用於應用程式模組。請務必使用**應用程式模組**檔案。

3. 找到 `build.gradle` 檔案的 `Dependencies` 區段，並新增 {{site.data.keyword.mobileanalytics_short}} Client SDK 的編譯相依關係，如下所示：

  ```Gradle
compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  您的儲存庫陳述式應該類似於下列程式碼範例：

	```Gradle
      dependencies {
        compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
          name:'analytics',
          version: '1.+',
          ext: 'aar',
          transitive: true
    	// other dependencies  
      }
  ```
  {: screen}

4. 按一下**工具 &gt; Android &gt; 將專案與 Gradle 檔案同步化**，以將專案與 Gradle 同步化。

5. 開啟 Android 專案的 `AndroidManifest.xml` 檔案，並在 `<manifest>` 元素下新增網際網路存取許可權：

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## 安裝 Swift SDK
{: #installing-sdk-ios}

{{site.data.keyword.mobileanalytics_full}} SDK 可讓您檢測行動應用程式。Swift SDK 適用於 iOS 及 watchOS。

### 開始之前
{: #before-you-begin-ios}

請確定已正確設定 Xcode。若要瞭解如何設定 iOS 開發環境，請參閱 [Apple Developer 網站](https://developer.apple.com/support/xcode/)。

{{site.data.keyword.mobileanalytics_short}} SDK 隨 [Cocoapods](https://cocoapods.org/) 及 [Carthage](https://github.com/Carthage/Carthage#getting-started)（Cocoa 專案的相依關係管理程式）一起配送。CocoaPods 及 Carthage 會從儲存庫自動下載構件，並讓它們可供應用程式使用。

#### Cocoapods
{: #cocoapods}
1. 如果未安裝 CocoaPods，請執行：

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. 如果您尚未針對 CocoaPods 起始設定工作區，請在您專案的根目錄中執行 `pod init` 指令。CocoaPods 會為您建立 `Podfile` 檔案，您可以在其中定義 Xcode 專案的相依關係。

3. 將 `BMSAnalytics` pod 新增至 Podfile 中的目標，例如：

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. 儲存 `Podfile` 檔案，並從指令行執行 `pod install`。

5. 使用 CocoaPods 已產生的 `.xcworkspace` 檔案，來開啟 Xcode 專案工作區。

#### Carthage
{: #carthage}

使用 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)，來新增您專案的架構。

1. 將 `BMSAnalytics` 架構新增至 Cartfile：
  ```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. 執行 `carthage update` 指令。建置完成時，請將 `BMSAnalytics.framework`、`BMSCore.framework` 及 `BMSAnalyticsAPI.framework` 拖曳至 Xcode 專案。
3. 遵循 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 網站上的指示，來完成整合。

# 相關鏈結

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API 參考資料
{: #api}
* [REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
