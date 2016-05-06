---

copyright:
  years: 2015, 2016

---

# 使用分析の収集
{: #usage-analytics}

使用分析を記録し、記録されたデータを {{site.data.keyword.amashort}} サービスに送信するように、{{site.data.keyword.amashort}} Client SDK を構成できます。

**注:** 使用統計の記録を開始する前に、ロギング・キャプチャーを有効化したことを確認してください。

使用統計の記録と送信を開始するには、以下の API を使用します。

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
**注:** Cordova アプリケーションを開発している場合、ネイティブ API を使用して、アプリケーション・ライフサイクル・イベントの記録を有効にしてください。
