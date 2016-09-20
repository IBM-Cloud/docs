---

copyright:
  years: 2015, 2016

---

# 收集使用情况分析信息
{: #usage-analytics}
上次更新时间：2016 年 5 月 6 日
{: .last-updated}

您可以将 {{site.data.keyword.amashort}} 客户端 SDK 配置为记录使用情况分析信息，并将记录的数据发送到 {{site.data.keyword.amashort}} 服务。

**重要信息**：{{site.data.keyword.amashort}} 服务的监视功能计划迁移到新的 [{{site.data.keyword.mobileanalytics_short}} 服务](https://console.ng.bluemix.net/catalog/services/mobile-analytics)。新 Swift SDK 将使用新的 {{site.data.keyword.mobileanalytics_short}} 服务，该服务提供了更加丰富的分析体验。{{site.data.keyword.mobileanalytics_short}} 服务目前在试验阶段，计划在今年晚些时候正式发布。我们建议您着手对迁移应用程序以使用新的 {{site.data.keyword.mobileanalytics_short}} 服务和 Swift SDK 进行调查，因为我们计划在 {{site.data.keyword.mobileanalytics_short}} 正式发布时，停止使用 {{site.data.keyword.amashort}} 服务的监视功能。

**注：**开始记录使用情况分析信息之前，请确保您已启用日志记录捕获。

使用以下 API 来开始记录和发送使用情况分析信息：

### Android
{: #usage-analytics-android}

```Java
// Enable recording of usage analytics
MFPAnalytics.enable();

// Start recording application startup time
// Add this code in the onCreate method of your main Activity
MFPAnalytics.startLoggingApplicationStartup();// Record the duration of application startup
// Add this code in the onStart method of your main Activity
MFPAnalytics.logApplicationStartup();// Record application foreground and background events
// Add this code in the onPause and onResume methods of your main Activity
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```

### iOS - Objective-C
{: #usage-analytics-objectc}

**重要信息：**虽然 Objective-C SDK 仍受到完全支持，且仍视为 {{site.data.keyword.Bluemix}} Mobile Services 的主 SDK，但是有计划要在今年晚些时候停止使用此 SDK，以支持新的 Swift SDK。

Objective-C SDK 会将监视数据报告给 {{site.data.keyword.amashort}} 服务的监视控制台。如果您依赖于 {{site.data.keyword.amashort}} 服务的监视功能，请继续使用 Objective-C SDK。

```Objective-C
// Enable usage analytics recording
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Start recording application lifecycle events
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Enable usage analytics recording
IMFAnalytics.sharedInstance().setEnabled(true)

// Start recording application lifecycle events
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
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
**注：**开发 Cordova 应用程序时，请使用本机 API 来启用应用程序生命周期事件记录。
