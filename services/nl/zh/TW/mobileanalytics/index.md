---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 {{site.data.keyword.mobileanalytics_short}}（測試版）  

{: #gettingstartedtemplate}
*前次更新：2016 年 5 月 17 日*
{: .last-updated}

使用 {{site.data.keyword.mobileanalytics_full}} 服務來測量行動應用程式、行動使用者及行動裝置的狀態、行為及環境定義。
{: shortdesc}

若要快速啟動並執行 {{site.data.keyword.mobileanalytics_short}} 服務，請遵循下列步驟：

1. 為 {{site.data.keyword.mobileanalytics_short}} 服務[建立實例](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)之後，可以在「{{site.data.keyword.Bluemix}} 儀表板」的「服務」區段中按一下您的磚，以存取「{{site.data.keyword.mobileanalytics_short}} 主控台」。

  **重要事項：**當您一開始開啟新建立的 Mobile Analytics 服務時，會顯示一個視窗，確認您允許 {{site.data.keyword.Bluemix_notm}} 將有關您的必要資訊提供給服務，讓服務可以驗證您的身分。按一下**確認**，繼續移至 {{site.data.keyword.mobileanalytics_short}} 主控台。如果您取消，將不會開啟 {{site.data.keyword.mobileanalytics_short}} 主控台。

2. 安裝 {{site.data.keyword.mobileanalytics_short}} [Client SDK](install-client-sdk.html)。

3. 匯入 Client SDK，並使用下列程式碼 Snippet 起始設定它們，以記錄用法分析。

	#### Android
	{: #android-initialize}
	1. 匯入 Client SDK：

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
	2. 使用[用戶端金鑰](sdk.html#analytics-clientkey)值，以在應用程式碼內起始設定 Client SDK，來記錄用法分析及應用程式階段作業。

		```Java
			try {
			     BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
			}
			catch (MalformedURLException e) {
	            //The Bluemix region provided is invalid
	        }
				Analytics.init(getApplication(), your_app_name, your_client_key, Analytics.DeviceEvent.LIFECYCLE);
		```
    **bluemixRegion** 參數指定您所使用的 Bluemix 部署（例如，`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`）。

  #### iOS
  {: #ios-initialize}
  1. 匯入 `BMSCore` 及 `BMSAnalytics` 架構：
  ```
    import BMSCore
    import BMSAnalytics
    ```
  2. 使用[用戶端金鑰](sdk.html#analytics-clientkey)值，以在應用程式碼內起始設定 Client SDK，來記錄用法分析及應用程式階段作業。
 
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName(your_app_name, apiKey: your_client_key, deviceEvents: DeviceEvent.LIFECYCLE)
	```
  **bluemixRegion** 參數指定您所使用的 Bluemix 部署（例如，`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`）。
4. 將記錄的用法分析傳送至「Mobile Analytics 服務」。簡單的測試分析方式是在應用程式啟動時執行下列程式碼：

	#### Android
	{: #android-send}

	您可以在 Android 應用程式中主要活動的 `onCreate` 方法中或最適合您專案的位置中新增 `Analytics.send()` 方法。

	```
	Analytics.send();
	```

	#### iOS
	{: #ios-send}

	使用 `Analytics.send` 方法，將分析資料傳送至伺服器。將 `Analytics.send` 方法放在應用程式委派的 `application(_:didFinishLaunchingWithOptions:)` 方法中或最適合您專案的位置中。

	```
	Analytics.send()
	```

	請閱讀[檢測應用程式](sdk.html)主題。
5. 在模擬器或裝置上編譯並執行應用程式。

6. 移至 {{site.data.keyword.mobileanalytics_short}} **儀表板**以查看用法分析（例如，使用應用程式的新裝置及裝置總數）。您也可以[建立自訂圖表](app-monitoring.html#custom-charts)、[設定警示](app-monitoring.html#alerts)及[監視應用程式損毀](app-monitoring.html#monitor-app-crash)來監視應用程式。


# 相關鏈結

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
