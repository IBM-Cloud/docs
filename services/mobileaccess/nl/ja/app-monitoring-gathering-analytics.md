---

copyright:
  years: 2015, 2016

---

# 使用分析の収集
{: #usage-analytics}
最終更新日: 2016 年 5 月 6 日
{: .last-updated}

使用分析を記録し、記録されたデータを {{site.data.keyword.amashort}} サービスに送信するように、{{site.data.keyword.amashort}} Client SDK を構成できます。

**重要**: {{site.data.keyword.amashort}} サービスのモニター機能は、新しい [{{site.data.keyword.mobileanalytics_short}} サービス](https://console.ng.bluemix.net/catalog/services/mobile-analytics)に移行される予定です。新しい Swift SDK は、豊富な分析機能を提供するこの新しい {{site.data.keyword.mobileanalytics_short}} サービスを利用します。{{site.data.keyword.mobileanalytics_short}} サービスは現在は試験段階であり、今年後半に一般出荷可能になる予定です。{{site.data.keyword.mobileanalytics_short}} が一般出荷可能になると {{site.data.keyword.amashort}} サービスのモニター機能は廃止される予定であるため、新しい {{site.data.keyword.mobileanalytics_short}} サービスおよび Swift SDK を使用するようにアプリケーションを移行するための調査を行うことをお勧めします。

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

**重要**: Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix}} モバイル・サービス用の主要 SDK とされていますが、今年後半には廃止され、新しい Swift SDK が後継になる予定です。

Objective-C SDK は、モニター・データを {{site.data.keyword.amashort}} サービスのモニタリング・コンソールに報告します。{{site.data.keyword.amashort}} サービスのモニター機能に依存している場合は、Objective-C SDK を引き続き使用してください。

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
