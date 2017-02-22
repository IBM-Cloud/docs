---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:codeblock:.codeblock}

# 初始化 BMSClient
{: #sdk_BMSClient}

`BMSCore` 提供了其他 {{site.data.keyword.Bluemix}} Mobile Services 客户机 SDK 用于与其对应的 {{site.data.keyword.Bluemix_notm}} 服务进行通信的 HTTP 基础架构。


## 初始化 Android 应用程序
{: #init-BMSClient-android}

您可以将 `BMSCore` 包下载并导入到 Android Studio 项目，或者使用 Gradle。

1. 通过在项目文件开始处添加以下 `import` 语句以导入客户机 SDK。

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. 通过在 Android 应用程序中主活动的 `onCreate` 方法中添加初始化代码，或在最适合运行项目的位置中添加初始化代码，以初始化 Android 应用程序中的 `BMSClient` SDK。

  ```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
  {: codeblock}

  必须使用 **bluemixRegion** 参数来初始化 `BMSClient`。在初始化程序中，**bluemixRegion** 值指定您使用的 {{site.data.keyword.Bluemix_notm}} 部署，例如 `BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。


## 初始化 iOS 应用程序
{: #init-BMSClient-ios}

可以使用 [CocoaPods](https://cocoapods.org){: new_window} 或 [Carthage](https://github.com/Carthage/Carthage){: new_window} 来获取 `BMSCore` 包。

1. 要使用 CocoaPods 安装 `BMSCore`，请将以下行添加到 Podfile。如果项目尚未具有 Podfile，请使用 `pod init` 命令。

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  然后运行 `pod install` 命令，并打开生成的 `.xcworkspace` 文件。要更新为较新的 `BMSCore` 发行版，请使用 `pod update BMSCore`。

  有关使用 CocoaPods 的更多信息，请参阅 [CocoaPods 指南 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://guides.cocoapods.org/using/index.html "外部链接图标"){: new_window}。

2. 要使用 Carthage 安装 `BMSCore`，请遵循以下 [指示 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/Carthage/Carthage#getting-started "外部链接图标"){: new_window}。

  1. 将以下行添加到 Cartfile：

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. 运行 `carthage update` 命令。

  3. 构建完成后，通过遵循 Carthage 指示信息中的[第 3 步 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/Carthage/Carthage#getting-started "外部链接图标")，将 `BMSCore.framework` 添加到项目。

      对于使用 Swift 2.3 构建的应用程序，请使用 `carthage update --toolchain com.apple.dt.toolchain.Swift_2_3` 命令。否则，请使用 `carthage update` 命令。

3. 导入模块。

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. 使用以下代码初始化 `BMSClient` 类。

  将初始化代码放入应用程序代表的 `application(_:didFinishLaunchingWithOptions:)` 方法中，或放入最适合运行项目的位置中。

  ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
    ```
  {: codeblock}

  必须使用 **bluemixRegion** 参数来初始化 `BMSClient`。在初始化程序中，**bluemixRegion** 值指定您使用的 {{site.data.keyword.Bluemix_notm}} 部署，例如 `BMSClient.Region.usSouth`、`BMSClient.Region.unitedKingdom` 或 `BMSClient.Region.sydney`。


## 初始化 Cordova 应用程序
{: #init-BMSClient-cordova}

1. 从 Cordova 应用程序根目录运行以下命令来添加 Cordova 插件：

  ```
  cordova plugin add bms-core
  ```
  {: codeblock}

2. 通过在主 JavaScript 文件中添加初始化代码，或在最适合运行项目的位置中添加初始化代码，以初始化 Cordova 应用程序中的 `BMSClient` 类。

  ```
  BMSClient.initialize(BMSClient.REGION_US_SOUTH);
  ```
  {: codeblock}
	
  必须使用 **bluemixRegion** 参数来初始化 `BMSClient`。在初始化程序中，**bluemixRegion** 值指定您使用的 {{site.data.keyword.Bluemix_notm}} 部署，例如 `BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。


# 相关链接
{: #rellinks}

## 相关链接
{: #general}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova 插件](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
