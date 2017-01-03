---

copyright:
  years: 2016
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} (Beta) 入门

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} 帮助开发人员、IT 管理员和业务利益相关方深入了解移动应用程序的执行方式和使用方式。从台式机或图形输入板监视所有应用程序的性能和使用情况。快速识别趋势和异常，向下钻取以解决问题，并在关键度量值超过严重阈值时触发警报。
{: shortdesc}

要快速启动和运行 {{site.data.keyword.mobileanalytics_short}} 服务，请遵循下列步骤：

1. 在创建<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)--> {{site.data.keyword.mobileanalytics_short}} 服务的实例之后，即可访问 {{site.data.keyword.mobileanalytics_short}} Console，方法是单击 {{site.data.keyword.Bluemix}}“仪表板”**服务**部分中的磁贴。

 {{site.data.keyword.mobileanalytics_short}} 服务在启用**演示方式**的情况下启动。演示方式可在**应用程序数据**和**警报**页面填充图表，因此您可以查看数据的显示方式。当您具有自己的数据时，可以关闭演示方式。当处于演示方式时，{{site.data.keyword.mobileanalytics_short}} Console 是只读的，因此您无法创建新警报定义。

2. 安装 {{site.data.keyword.mobileanalytics_short}} [Client SDK](/docs/services/mobileanalytics/install-client-sdk.html)。可以选择使用 {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}。

3. 导入客户端 SDK，并使用下列代码片段对它们进行初始化，以记录使用情况分析：

	#### Android
	{: #android-import}

	将以下 `import` 语句添加到项目文件的开头：
	
    ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **注释：**iOS 和 watchOS 可以使用 Swift SDK。
	
 通过将以下 `import` 语句添加到 `AppDelegate.swift` 项目文件的开头，导入 `BMSCore` 和 `BMSAnalytics` 框架：

   ```Swift
  import BMSCore
  import BMSAnalytics
  ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 从 Cordova 应用程序根目录运行以下命令来添加 Cordova 插件：

 ```Javascript
 cordova plugin add bms-core
 ```
 {: codeblock}  

4. 使用 [API 密钥](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)值在应用程序代码内部初始化 {{site.data.keyword.mobileanalytics_short}} 客户端 SDK，以记录使用情况分析和应用程序会话。	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 **bluemixRegion** 参数指定您使用的是哪一个 {{site.data.keyword.Bluemix_notm}} 部署，例如 `BMSClient.REGION_US_SOUTH` 和 `BMSClient.REGION_UK`。 
    <!-- , or `BMSClient.Region.Sydney`.-->

 #### iOS
 {: #ios-initialize}
  
  使用 [API 密钥](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)值在应用程序代码内部初始化客户端 SDK，以记录使用情况分析和应用程序会话。
	
  ```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
		```
  {: codeblock}
			
   **bluemixRegion** 参数指定您使用的是哪一个 Bluemix 部署，例如 `BMSClient.Region.usSouth` 或 `BMSClient.Region.unitedKingdom`。
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
 #### Cordova
 {: #cordova-initialize}
	
 使用 [API 密钥](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)值在应用程序代码内部初始化客户端 SDK，以记录使用情况分析和应用程序会话。
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  **bluemixRegion** 参数指定您使用的是哪一个 {{site.data.keyword.Bluemix_notm}} 部署，例如 `BMSClient.REGION_US_SOUTH` 和 `BMSClient.REGION_UK`。
  
 **注：**您针对应用程序选择的名称 (`your_app_name_here`) 会在 {{site.data.keyword.mobileanalytics_short}} 控制台中显示为应用程序名称。应用程序名称用作过滤器，在仪表板中搜索应用程序日志。当您跨平台（例如 Android 和 iOS）使用相同的应用程序名称时，您可以在相同的名称下，查看该应用程序的所有日志，而无论日志发自哪个平台。

5. 将记录的使用情况分析发送到 Mobile Analytics 服务。一个简单的方法可测试您的分析，即在应用程序启动时，运行下列代码：

	#### Android
	{: #android-send}

	使用 `Analytics.send()` 方法，将分析数据发送到服务器。您可以在 Android 应用程序主要活动的 `onCreate` 方法的任何位置或最适合您项目的位置，放置 `Analytics.send()` 方法。 
	
	您可以在任何位置插入 `Analytics.send()`。

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	使用 `Analytics.send` 方法，将分析数据发送到服务器。您可以将 `Analytics.send` 方法置于应用程序代表的 `application(_:didFinishLaunchingWithOptions:)` 方法的任何位置，或者置于适合您项目的位置。 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	使用 `BMSAnalytics.send` 方法，将分析数据发送到服务器。将 `BMSAnalytics.send` 方法置于最适合您的项目的位置。
	
	```
	BMSAnalytics.send
	```
	{: codeblock}
	
	请阅读[检测您的应用程序](/docs/services/mobileanalytics/sdk.html)主题，以了解其他 {{site.data.keyword.mobileanalytics_short}} 功能，例如，[登录](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger)、[网络请求](/docs/services/mobileanalytics/sdk.html#network-requests)和[崩溃分析](/docs/services/mobileanalytics/sdk.html#report-crash-analytics)。
	
6. 在移动仿真器或设备上编译并运行应用程序。

7. 转到 {{site.data.keyword.mobileanalytics_short}} Console，以查看应用程序的使用情况分析。您还可以通过<!--[creating custom charts](app-monitoring.html#custom-charts),-->[设置警报](/docs/services/mobileanalytics/app-monitoring.html#alerts)和[监视应用程序崩溃](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash)来监视应用程序。


# 相关链接

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova 插件核心 SDK](https://www.npmjs.com/package/bms-core){: new_window}

## API 参考
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
