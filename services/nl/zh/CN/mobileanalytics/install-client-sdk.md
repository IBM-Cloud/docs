---

copyright:
  years: 2015, 2016

---

# 安装 {{site.data.keyword.mobileanalytics_short}}
客户端 SDK
{: #mobileanalytics_sdk}
*上次更新时间：2016 年 4 月 21 日*
{: .last-updated}

目前，Android、iOS 和 WatchOS 可以使用 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK。
{: #shortdesc}

## 安装 Android 客户端 SDK
{: #install-sdk-android}

{{site.data.keyword.mobileanalytics_short}} 客户端 SDK 通过 Gradle 进行分发；Gradle 是用于 Android 项目的依赖关系管理器。Gradle 会自动从存储库下载工件，并将其提供给 Android 应用程序。

1. 创建 [Android Studio](http://developer.android.com/sdk/index.html) 项目或打开现有项目。

2. 打开应用程序模块中的 `build.gradle` 文件。

  **提示**：Android 项目可能具有两个 `build.gradle` 文件：一个用于项目，另一个用于应用程序模块。请确保使用**应用程序模块**文件。

3. 找到 `build.gradle` 文件的 `Dependencies` 部分，并添加 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK 的编译依赖关系，如下所示：

  ```Gradle
compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  您的存储库语句应该类似下列代码示例：

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

4. 通过单击**工具 &gt; Android &gt; 使用 Gradle 文件同步项目**来使用 Gradle 同步项目。

5. 打开 Android 项目的 `AndroidManifest.xml` 文件，并在 `<manifest>` 元素下添加因特网访问许可权：

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## 安装 Swift SDK
{: #installing-sdk-ios}

使用 {{site.data.keyword.mobileanalytics_full}} SDK，您可以检测移动应用程序。iOS 和 watchOS 可以使用 Swift SDK。

### 开始之前
{: #before-you-begin-ios}

确保正确设置 Xcode。要了解如何设置 iOS 开发环境，请参阅 [Apple 开发人员 Web 站点](https://developer.apple.com/support/xcode/)。

{{site.data.keyword.mobileanalytics_short}} SDK 通过 [Cocoapods](https://cocoapods.org/) 和[Carthage](https://github.com/Carthage/Carthage#getting-started) 进行分发，它们是用于 Cocoa 项目的依赖关系管理器。CocoaPods 和 Carthage 会自动从存储库下载工件，并将其提供给您的应用程序。

#### Cocoapods
{: #cocoapods}
1. 如果未安装 CocoaPods，请运行：

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. 如果您未针对 CocoaPods 初始化您的工作空间，请在项目的根目录中，运行 `pod init` 命令。CocoaPods 会为您创建 `Podfile` 文件，您可以在该文件中定义 Xcode 项目的依赖关系。

3. 将 `BMSAnalytics` pod 添加到 Podfile 中的 target 部分，例如：

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. 保存 `Podfile` 文件，然后在命令行中运行 `pod install`。

5. 使用 CocoaPods 生成的 `.xcworkspace` 文件，打开 Xcode 项目工作空间。

#### Carthage
{: #carthage}

使用 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)，将框架添加到项目。

1. 将 `BMSAnalytics` 框架添加到 Cartfile：
```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. 运行 `carthage update` 命令。构建完成时，将 `BMSAnalytics.framework`、`BMSCore.framework` 和 `BMSAnalyticsAPI.framework` 拖到 Xcode 项目中。
3. 遵循 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 站点上的指示，完成集成。

# 相关链接

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API 参考
{: #api}
* [REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
