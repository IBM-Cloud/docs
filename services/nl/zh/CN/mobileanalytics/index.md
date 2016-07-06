---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} (Beta) 入门  

{: #gettingstartedtemplate}
*上次更新时间：2016 年 5 月 17 日*
{: .last-updated}

使用 {{site.data.keyword.mobileanalytics_full}} 服务，可测量移动应用程序、移动用户和移动设备的状态、行为和上下文信息。
{: shortdesc}

要快速启动和运行 {{site.data.keyword.mobileanalytics_short}} 服务，请遵循下列步骤：

1. 在您[创建 {{site.data.keyword.mobileanalytics_short}} 服务的实例](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)之后，可以通过单击 {{site.data.keyword.Bluemix}} 仪表板“服务”部分的磁贴，来访问 {{site.data.keyword.mobileanalytics_short}} 控制台。

  **重要信息：**在您最初打开新创建的 Mobile Analytics 服务时，会显示一个窗口，确认您允许 {{site.data.keyword.Bluemix_notm}} 向服务提供有关您的必要信息，以便服务可以验证您的身份。单击**确认**，继续访问 {{site.data.keyword.mobileanalytics_short}} 控制台。如果取消，{{site.data.keyword.mobileanalytics_short}} 控制台将不会打开。

2. 安装 {{site.data.keyword.mobileanalytics_short}} [客户端 SDK](install-client-sdk.html)。

3. 导入客户端 SDK，并使用下列代码片段对它们进行初始化，以记录使用情况分析。

	#### Android
	{: #android-initialize}
	1. 导入客户端 SDK：

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
	2. 使用[客户端密钥](sdk.html#analytics-clientkey)值，在应用程序代码中初始化客户端 SDK，以记录使用情况分析和应用程序会话。

		```Java
			try {
			     BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
			}
			catch (MalformedURLException e) {
	            //The Bluemix region provided is invalid
	        }
				Analytics.init(getApplication(), your_app_name, your_client_key, Analytics.DeviceEvent.LIFECYCLE);
		```
    **bluemixRegion** 参数指定您使用的是哪一个 Bluemix 部署，例如 `BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。

  #### iOS
  {: #ios-initialize}
  1. 导入 `BMSCore` 和 `BMSAnalytics` 框架：
```
    import BMSCore
    import BMSAnalytics
    ```
  2. 使用[客户端密钥](sdk.html#analytics-clientkey)值，在应用程序代码中初始化客户端 SDK，以记录使用情况分析和应用程序会话。
 
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName(your_app_name, apiKey: your_client_key, deviceEvents: DeviceEvent.LIFECYCLE)
	```
  **bluemixRegion** 参数指定您使用的是哪一个 Bluemix 部署，例如 `BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。

4. 将记录的使用情况分析发送到 Mobile Analytics 服务。一个简单的方法可测试您的分析，即在应用程序启动时，运行下列代码：

	#### Android
	{: #android-send}

	您可以在 Android 应用程序主要活动的 `onCreate` 方法中或最适合您项目的位置，添加 `Analytics.send()` 方法。

	```
	Analytics.send();
	```

	#### iOS
	{: #ios-send}

	使用 `Analytics.send` 方法，将分析数据发送到服务器。将 `Analytics.send` 方法置于应用程序代表的 `application(_:didFinishLaunchingWithOptions:)` 方法中，或者置于适合您项目的位置。

	```
	Analytics.send()
	```

	阅读[检测应用程序](sdk.html)主题。
5. 在移动仿真器或设备上编译并运行应用程序。

6. 转到 {{site.data.keyword.mobileanalytics_short}} **仪表板**，以查看使用情况分析，如使用该应用程序的新设备和设备总数。您还可以通过[创建定制图表](app-monitoring.html#custom-charts)、[设置警报](app-monitoring.html#alerts)和[监视应用程序崩溃](app-monitoring.html#monitor-app-crash)，来监视应用程序。


# 相关链接

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
