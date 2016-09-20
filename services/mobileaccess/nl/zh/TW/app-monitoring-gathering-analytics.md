---

copyright:
  years: 2015, 2016

---

# 收集用量分析
{: #usage-analytics}
前次更新：2016 年 5 月 6 日
{: .last-updated}

您可以配置 {{site.data.keyword.amashort}} 用戶端 SDK 來記錄用量分析，以及將記錄的資料傳送給 {{site.data.keyword.amashort}} 服務。

**重要事項**：{{site.data.keyword.amashort}} 服務的監視功能，預計會移轉至新的 [{{site.data.keyword.mobileanalytics_short}} 服務](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新的 Swift SDK 會利用新的 {{site.data.keyword.mobileanalytics_short}} 服務，此服務提供更豐富的分析體驗。{{site.data.keyword.mobileanalytics_short}} 服務目前處於實驗階段，預計在今年稍晚正式上市。由於預計會在 {{site.data.keyword.mobileanalytics_short}} 正式上市時停止使用 {{site.data.keyword.amashort}} 服務的監視功能，因此建議您先研究移轉應用程式以使用新的 {{site.data.keyword.mobileanalytics_short}} 服務及 Swift SDK。

**附註：**請確定您已啟用記載擷取，再開始記錄用量分析。

使用下列 API 來開始記錄及傳送用量分析：

### Android
{: #usage-analytics-android}

```Java
// Enable recording of usage analytics
MFPAnalytics.enable();

// Start recording application startup time
// Add this code in the onCreate method of your main Activity
MFPAnalytics.startLoggingApplicationStartup();

// Record the duration of application startup
// Add this code in the onStart method of your main Activity
MFPAnalytics.logApplicationStartup();

// Record application foreground and background events
// Add this code in the onPause and onResume methods of your main Activity
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```

### iOS - Objective-C
{: #usage-analytics-objectc}

**重要事項**：雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix}} Mobile Services 的主要 SDK，不過預計在今年稍晚停止使用，改用新的 Swift SDK。

Objective-C SDK 會向 {{site.data.keyword.amashort}} 服務的「監視主控台」報告監視資料。如果您依賴 {{site.data.keyword.amashort}} 服務的監視功能，請繼續使用 Objective-C SDK。

```Objective-C
// Enable usage analytics recording
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Start recording application lifecycle events
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Enable usage analytics recording
IMFAnalytics.sharedInstance().setEnabled(true)

// Start recording application lifecycle events
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
MFPAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```
**附註：**當您開發 Cordova 應用程式時，請使用原生 API 來啟用應用程式生命週期事件記錄。
