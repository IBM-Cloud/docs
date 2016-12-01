---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---
{:new_window: target="_blank"}
{:codeblock:.codeblock}

# 起始設定 BMSClient
{: #sdk_BMSClient}

`BMSCore` 提供 HTTP 基礎架構，供其他 {{site.data.keyword.Bluemix}} Mobile 服務用戶端 SDK 用來與其對應的 {{site.data.keyword.Bluemix_notm}} 服務進行通訊。


## 起始設定 Android 應用程式
{: #init-BMSClient-android}

您可以下載及匯入 `BMSCore` 套件至 Android Studio 專案，或使用 Gradle。

1. 在專案檔開頭新增下列 `import` 陳述式，以匯入用戶端 SDK。

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. 在 Android 應用程式中主要活動的 `onCreate` 方法中或在最適合您專案的位置中新增起始設定碼，以在 Android 應用程式中起始設定 `BMSCore` SDK。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
	{: codeblock}

  您必須起始設定 `BMSClient` 與 **bluemixRegion** 參數。在起始設定程式中，**bluemixRegion** 值指定您所使用的 {{site.data.keyword.Bluemix_notm}} 部署（例如，`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`）。


## 起始設定 iOS 應用程式
{: #init-BMSClient-ios}

您可以使用 [CocoaPods](https://cocoapods.org){: new_window} 或 [Carthage](https://github.com/Carthage/Carthage){: new_window} 來取得 `BMSCore` 套件。

1. 若要使用 CocoaPods 來安裝 `BMSCore`，請將下列這幾行新增至 Podfile 中。如果您的專案還沒有 Podfile，請使用 `pod init` 指令。

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  然後，執行 `pod install` 指令，並且開啟產生的 `.xcworkspace` 檔案。若要更新至 `BMSCore` 的較新版次，請使用 `pod update BMSCore`。

  如需使用 CocoaPods 的相關資訊，請參閱 [CocoaPods Guides](https://guides.cocoapods.org/using/index.html){: new_window}。

2. 若要使用 Carthage 來安裝 `BMSCore`，請遵循這些[指示](https://github.com/Carthage/Carthage#getting-started){: new_window}。

  1. 將下列這一行新增至您的 Cartfile：

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. 執行 `carthage update` 指令。

  3. 建置完成之後，請遵循 Carthage 指示中的[步驟 3](https://github.com/Carthage/Carthage#getting-started)，將 `BMSCore.framework` 新增至專案中。

  若為使用 Swift 2.3 建置的應用程式，請使用 `carthage update --toolchain com.apple.dt.toolchain.Swift_2_3` 指令。否則，請使用 `carthage update` 指令。

3. 匯入模組。

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. 起始設定 `BMSClient` 類別，使用下列程式碼。

  將起始設定碼放在應用程式委派的 `application(_:didFinishLaunchingWithOptions:)` 方法中，或放在最適合您專案的位置中。

    ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
    ```
   {: codeblock}

    若要使用 {{site.data.keyword.mobileanalytics_short}} 用戶端 SDK，您必須起始設定 `BMSClient` 與 **bluemixRegion** 參數。在起始設定程式中，**bluemixRegion** 值指定您所使用的 {{site.data.keyword.Bluemix_notm}} 部署（例如，`BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom` 或 `BMSClient.Region.sydney`）。
