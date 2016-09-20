---

copyright:
  years: 2015, 2016
  
---

# アプリケーションのモニター
{: #app-monitoring}
最終更新日: 2016 年 6 月 28 日
{: .last-updated}

{{site.data.keyword.amafull}} は、セキュリティー機能に加えて、モバイル・アプリケーション向けのモニターおよび分析も提供します。{{site.data.keyword.amashort}} Client SDK を使用して、クライアント・ログおよびモニター・データを記録することができます。開発者は、このデータをいつ {{site.data.keyword.amashort}} サービスに送信するのかを制御できます。{{site.data.keyword.amashort}} サービスで発生するすべてのセキュリティー・イベント (認証の成功または失敗など) が自動的にログに記録されます。

**注**: {{site.data.keyword.amashort}} サービスのモニター機能は、新しい [{{site.data.keyword.mobileanalytics_short}} サービス](https://console.ng.bluemix.net/catalog/services/mobile-analytics)に移行される予定です。新しい Swift SDK は、豊富な分析機能を提供するこの新しい {{site.data.keyword.mobileanalytics_short}} サービスを利用します。{{site.data.keyword.mobileanalytics_short}} サービスは現在は試験段階であり、今年後半に一般出荷可能になる予定です。{{site.data.keyword.mobileanalytics_short}} が一般出荷可能になると {{site.data.keyword.amashort}} サービスのモニター機能は廃止される予定であるため、新しい {{site.data.keyword.mobileanalytics_short}} サービスおよび Swift SDK を使用するようにアプリケーションを移行するための調査を行うことをお勧めします。

データが {{site.data.keyword.amashort}} に送信されたら、{{site.data.keyword.amashort}} モニタリング・ダッシュボードを使用して、モバイル・アプリケーション、デバイス、およびクライアント・ログの分析についての洞察を得ることができます。{{site.data.keyword.amashort}} によって保護されているリソースに対してアプリケーションが行った要求についての情報は、デフォルトで記録されます。

自動的に記録されるデータには、認証の数、新規デバイス数、および新規ユーザー数などの情報があります。それに加えて、以下の情報を報告するように {{site.data.keyword.amashort}} Client SDK を構成できます。

### モバイル・アプリケーションの使用統計
{: #usage-stats}

モバイル・アプリケーションを構成して、単純な数回の API 呼び出しで、アプリケーションのライフサイクル・イベントを記録し、記録されたデータを {{site.data.keyword.amashort}} サービスに送信するようにできます。アプリのオープン回数、
受信したプッシュ通知の数などを記録できます。

### クライアント・サイド・ログのキャプチャー
{: #client-side-logcapture}

実際に使用されているアプリケーションでは、開発者による修正が必要な問題が起こることがあります。しかし、そうした問題を再現することは多くの場合、困難です。<!--in R&D.--> コードに関する作業を行った開発者は、
テスト用の環境や対象となるデバイスを持っていない場合があります。そのような状況では、
問題が起こった環境で、問題が起こったときに、クライアント・デバイスからデバッグ・ログを取り出すことができると便利です。

### キャプチャーされたデータの保存
{: #preserve-captureddata}

キャプチャーされたデータがクライアント・サイドですべて保存されることを保証する方法はありません。ユーザーがモバイル・アプリケーションをオフラインで実行すると同時に、
キャプチャーされた分析データおよびログ・データを累積しているといった場合があり得ます。クライアントがオフラインになっている際のファイル・システム・スペースは限られているため、
新しくログに記録されたイベントを保持できるように、ログに記録されたイベントのうち古いものは消去される必要があります。キャプチャーされたデータを、提供されている API を使用して {{site.data.keyword.amashort}} サービスにいつ送信するのかを決めるのは、開発者の役割です。

## {{site.data.keyword.amashort}} モニタリング・ダッシュボードの使用
{: #monitoring-dashboard}

1. {{site.data.keyword.Bluemix}} ダッシュボードを開き、{{site.data.keyword.Bluemix_notm}} アプリケーションをクリックします。

2. {{site.data.keyword.Bluemix_notm}} アプリケーション・ダッシュボードが開いたら、{{site.data.keyword.amashort}} タイルをクリックします。

3. 左の {{site.data.keyword.amashort}} ダッシュボード・ナビゲーション・バーにある**「モニタリング」**リンクをクリックします。


## Logger の有効化、構成、および使用
{: #enable-logger}

{{site.data.keyword.amashort}} Client SDK は、なじみのあるユーザーも多い `java.util.logging` や `log4j` といった他のロギング・フレームワークに似たロギング・フレームワークを提供します。このロギング・フレームワークは、パッケージあたり複数のロガー・インスタンス、さまざまなログ・レベル、アプリケーション・クラッシュに関するスタック・トレースのキャプチャーなどをサポートします。

また、ログに記録されたデータがローカル・ストアに保持されるように構成して、オンデマンドで {{site.data.keyword.amashort}} サービスに送信できるようにすることも可能です。

{{site.data.keyword.amashort}} Client SDK ロギング・フレームワークがサポートするログ・レベルは次のとおりです。以下のリストでは、詳細度の低いものから高いものへの順になっていて、推奨される使用指針も示されています。

* `FATAL` - リカバリー不能のクラッシュまたはハングに使用します。FATAL レベルは、
リカバリー不能エラー (ユーザーにはアプリケーション・クラッシュに見えます) のロギングのために予約されています。
* `ERROR` - 予期しない例外または予期しないネットワーク・プロトコル・エラーに使用します。
* `WARN` - 致命的エラーとは見なされない使用状況警告 (推奨されない API の使用や、遅いネットワーク応答など) をログに記録するために使用します。
* `INFO` - 初期化イベントおよび有用な他のデータを報告するために使用します。
* `DEBUG` - 開発者がアプリケーションの欠陥を解決する際に役立つデバッグ・ステートメントを報告するために使用します。

ロギング・フレームワークを使用する前に、{{site.data.keyword.amashort}} Client SDK を初期化したことを確認してください。以下の例は、{{site.data.keyword.amashort}} Client SDK ロギング・フレームワークの基本的な使用法を示します。

**重要**: {{site.data.keyword.amashort}} サービスのモニター機能は、新しい [{{site.data.keyword.mobileanalytics_short}} サービス](https://console.ng.bluemix.net/catalog/services/mobile-analytics)に移行される予定です。新しい Swift SDK は、豊富な分析機能を提供するこの新しい {{site.data.keyword.mobileanalytics_short}} サービスを利用します。{{site.data.keyword.mobileanalytics_short}} サービスは現在は試験段階であり、今年後半に一般出荷可能になる予定です。{{site.data.keyword.mobileanalytics_short}} が一般出荷可能になると {{site.data.keyword.amashort}} サービスのモニター機能は廃止される予定であるため、新しい {{site.data.keyword.mobileanalytics_short}} サービスおよび Swift SDK を使用するようにアプリケーションを移行するための調査を行うことをお勧めします。

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(context, appRoute, appGUID);

Logger logger = Logger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```

#### iOS - Objective-C
{: #enable-logger-objectc}

**重要**: Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix}} モバイル・サービス用の主要 SDK とされていますが、今年後半には廃止され、新しい Swift SDK が後継になる予定です。

Objective-C SDK は、モニター・データを {{site.data.keyword.amashort}} サービスのモニタリング・コンソールに報告します。{{site.data.keyword.amashort}} サービスのモニター機能に依存している場合は、Objective-C SDK を引き続き使用してください。

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

#### iOS - Swift
{: #enable-logger-swift}

```Swift
IMFClient.sharedInstance().initializeWithBackendRoute(appRoute, backendGUID: appGuid)

let logger = IMFLogger(forName: "myLogger");

logger.logDebugWithMessages("debug");
logger.logInfoWithMessages("info");
logger.logWarnWithMessages("warn");
logger.logErrorWithMessages("error");
logger.logFatalWithMessages("fatal");
```

**注:** {{site.data.keyword.amashort}} Client SDK は Objective-C で実装されているため、上記の logger API を使用するためには `IMFLoggerExtension.swift` ファイルを Swift プロジェクトに追加する必要がある場合があります。このファイルは [{{site.data.keyword.amashort}} Client SDK アーカイブ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)にあります。


#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(appRoute , appGUID);

var logger = MFPLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```

Logger クラスにはさらに以下のメソッドがあります。

* `setCapture` - {{site.data.keyword.amashort}} サービスに後で送信されるログ情報の保持を有効または無効にします。
* `setLevel` - ログ・メッセージを保存する最小ログ・レベルを設定します。
* `send` - 保持されたログを {{site.data.keyword.amashort}} サービスに送信します。

例えば、キャプチャーがオンで、ロガー・レベルが FATAL に構成されている場合、ロガーはキャッチされていない例外をキャプチャーします。キャッチされていない例外は、
多くの場合、ユーザーにはアプリケーション・クラッシュに見えますが、
クラッシュ・イベントの原因を示すログはキャプチャーされません。その代わりに、より詳細なロガー・レベルを使用すれば、FATAL ロガー項目の原因を示すログ (WARN や ERROR など) も確実にキャプチャーされます。

**注:** 各プラットフォームの完全な Logger API リファレンスは、[SDK、サンプル、API リファレンス](sdks-samples-apis.html)にあります。Logger API は {{site.data.keyword.amashort}} Client SDK Core の一部です。


### 使用例
{: #sample-logger-usage}

以下のコード・スニペットは、Logger の使用例を示します。

#### Android
{: #enable-logger-sample-android}

```Java
// Enable persisting logs
Logger.setCapture(true);

// Set the minimum log level to be printed and persisted
Logger.setLevel(Logger.LEVEL.INFO);

// Create two logger instances
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Log messages with different levels
logger1.debug("debug message");
logger2.info("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
Logger.send();
```

#### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Enable persisting logs
[IMFLogger setCapture:YES];

// Start capturing uncaught exceptions
[IMFLogger captureUncaughtExceptions];

// Set the minimum log level to be printed and persisted
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Create two logger instances
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Log messages with different levels
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Send persisted logs to the {{site.data.keyword.amashort}} service
[IMFLogger send];
```

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Enable persisting logs
IMFLogger.setCapture(true)

// Start capturing uncaught exceptions
IMFLogger.captureUncaughtExceptions()

// Set the minimum log level to be printed and persisted
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Create two logger instances
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Log messages with different levels
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Send persisted logs to the {{site.data.keyword.amashort}} service
IMFLogger.send()

```

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
MFPLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
MFPLogger.setLevel(MFPLogger.INFO);

// Create two logger instances
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
MFPLogger.send(success, failure);
```

### {{site.data.keyword.amashort}} Client SDK 内部ログの有効化
{: #enable-logger-sdklogs}
現在、このフィーチャーは Android 版の {{site.data.keyword.amashort}} Client SDK でのみ使用可能です。

{{site.data.keyword.amashort}} Client SDK は、Logcat 出力を内部デバッグ・メッセージで不必要に増やさないようにすることで、開発作業を改善します。したがって、デフォルトでは、{{site.data.keyword.amashort}} SDK によって DEBUG レベルで生成される内部ログ・メッセージは出力されません。以下の API を使用して、{{site.data.keyword.amashort}} Client SDK のすべての内部ログ・メッセージの出力を有効にすることができます。


```
Logger.setSDKInternalLoggingEnabled(true);
```

## 使用分析の収集
{: #usage-analytics}

使用分析を記録し、記録されたデータを {{site.data.keyword.amashort}} サービスに送信するように、{{site.data.keyword.amashort}} Client SDK を構成できます。

**重要**: {{site.data.keyword.amashort}} サービスのモニター機能は、新しい [{{site.data.keyword.mobileanalytics_short}} サービス](https://console.ng.bluemix.net/catalog/services/mobile-analytics)に移行される予定です。新しい Swift SDK は、豊富な分析機能を提供するこの新しい {{site.data.keyword.mobileanalytics_short}} サービスを利用します。{{site.data.keyword.mobileanalytics_short}} サービスは現在は試験段階であり、今年後半に一般出荷可能になる予定です。{{site.data.keyword.mobileanalytics_short}} が一般出荷可能になると {{site.data.keyword.amashort}} サービスのモニター機能は廃止される予定であるため、新しい {{site.data.keyword.mobileanalytics_short}} サービスおよび Swift SDK を使用するようにアプリケーションを移行するための調査を行うことをお勧めします。

**注:** 使用統計の記録を開始する前に、ロギング・キャプチャーを有効化したことを確認してください。

使用統計の記録と送信を開始するには、以下の API を使用します。

#### Android
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

#### iOS - Objective-C
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

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Enable usage analytics recording
IMFAnalytics.sharedInstance().setEnabled(true)

// Start recording application lifecycle events
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
MFPAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```
**注:** Cordova アプリケーションを開発している場合、ネイティブ API を使用して、アプリケーション・ライフサイクル・イベントの記録を有効にしてください。
