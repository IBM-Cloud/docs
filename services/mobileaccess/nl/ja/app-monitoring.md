---

copyright:
  years: 2015, 2016
  
---

# アプリケーションのモニター
{: #app-monitoring}
最終更新日: 2016 年 9 月 22 日
{: .last-updated}

{{site.data.keyword.amafull}} は、セキュリティー機能に加えて、モバイル・アプリケーション向けのモニターおよび分析も提供します。{{site.data.keyword.amashort}} Client SDK を使用して、クライアント・ログおよびモニター・データを記録することができます。開発者は、このデータをいつ {{site.data.keyword.amashort}} サービスに送信するのかを制御できます。{{site.data.keyword.amashort}} サービスで発生するすべてのセキュリティー・イベント (認証の成功または失敗など) が自動的にログに記録されます。
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

データが {{site.data.keyword.amashort}} に送信されたら、{{site.data.keyword.amashort}} モニタリング・ダッシュボードを使用して、モバイル・アプリケーション、デバイス、およびクライアント・ログの分析についての洞察を得ることができます。{{site.data.keyword.amashort}} によって保護されているリソースに対してアプリケーションが行った要求についての情報は、デフォルトで記録されます。

自動的に記録されるデータには、認証の数、新規デバイス数、および新規ユーザー数などの情報があります。それに加えて、以下の情報を報告するように {{site.data.keyword.amashort}} Client SDK を構成できます。

### モバイル・アプリケーションの使用統計
{: #usage-stats}

モバイル・アプリケーションを構成して、単純な数回の API 呼び出しで、アプリケーションのライフサイクル・イベントを記録し、記録されたデータを {{site.data.keyword.amashort}} サービスに送信するようにできます。アプリのオープン回数、
受信したプッシュ通知の数などを記録できます。

### クライアント・サイド・ログのキャプチャー
{: #client-side-logcapture}

実際に使用されているアプリケーションでは、開発者による修正が必要な問題が起こることがあります。しかし、そうした問題を再現することは多くの場合、困難です。コードに関する作業を行った開発者は、
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

3. {{site.data.keyword.amashort}} ダッシュボード・ナビゲーションの**「モニタリング」**ボタンをクリックします。


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

#### ログ・レベルのシナリオ
{: #log-level-scenario}

ロガー・レベルが`「FATAL」`に構成されている場合、ロガーは、キャッチされていない例外をキャプチャーしますが、異常終了イベントにつながったログをキャプチャーしません。より詳細なロガー・レベルを設定して、`「FATAL」`ロガー項目につながる可能性があるログ (`「WARN」`や`「ERROR」`など) も確実にキャプチャーできます。

ロギング・フレームワークを使用する前に、{{site.data.keyword.amashort}} Client SDK を初期化したことを確認してください。以下の例は、{{site.data.keyword.amashort}} Client SDK ロギング・フレームワークの基本的な使用法を示します。

<!-- **Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.-->

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // 自分の地域を指しているかを確認

Logger logger = Logger.getLogger("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

**bluemixRegion** パラメーターでは、使用している Bluemix デプロイメントを指定します (例えば、`BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK`)。 

#### iOS - Swift
{: #enable-logger-swift}

```Swift
BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // 地域は変更可能
Analytics.initializeWithAppName(your_app_name_here, apiKey: your_api_key_here, hasUserContext: false, deviceEvents: DeviceEvent.LIFECYCLE)

let logger = Logger.logger(forName: "myLogger")

logger.debug(“debug info")
logger.info(“info message")
logger.warn(“warning message")
logger.error(“error message")
logger.fatal(“fatal message")
```
{: codeblock}
<!--
**Note:** The {{site.data.keyword.amashort}} client SDK is implemented with Objective-C, therefore you might need to add the `IMFLoggerExtension.swift` file to your Swift project to use the previous logger API. You can find this file in the [{{site.data.keyword.amashort}} client SDK archive](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).
-->

#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(BMSClient.REGION_US_SOUTH); // 地域は変更可能

var logger = BMSLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

Logger クラスにはさらに以下のメソッドがあります。

* `setCapture` - {{site.data.keyword.amashort}} サービスに後で送信されるログ情報の保持を有効または無効にします。
* `setLevel` - ログ・メッセージを保存する最小ログ・レベルを設定します。
* `send` - 保持されたログを {{site.data.keyword.amashort}} サービスに送信します。

例えば、キャプチャーがオンで、ロガー・レベルが FATAL に構成されている場合、ロガーはキャッチされていない例外をキャプチャーします。キャッチされていない例外は、
多くの場合、ユーザーにはアプリケーション・クラッシュに見えますが、
クラッシュ・イベントの原因を示すログはキャプチャーされません。その代わりに、より詳細なロガー・レベルを使用すれば、FATAL ロガー項目の原因を示すログ (WARN や ERROR など) も確実にキャプチャーされます。

**注:** 各プラットフォームの完全な Logger API リファレンスは、[SDK、サンプル、API リファレンス](sdks-samples-apis.html)にあります。Logger API は {{site.data.keyword.amashort}} Client SDK Core の一部です。


### サンプル Logger の使用
{: #sample-logger-usage}

以下のコード・スニペットは、Logger の使用例を示します。

#### Android
{: #enable-logger-sample-android}

```Java
// 後から {{site.data.keyword.amashort}} サービスに送信できる
// ようにするため、ログをデバイスに保存するように Logger を構成
// デフォルトでは無効。有効にするには、true に設定
Logger.storeLogs(true);

// 最小ログ・レベルを変更 (オプション)
// デフォルト設定は Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// 2 つのロガー・インスタンスを作成
// 複数のログ・インスタンスを作成してログを編成可能
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// 異なるレベルのメッセージのログ・メッセージ
// 機能 1 にはデバッグ・メッセージ
// 機能 2 には通知メッセージ
logger1.debug("debug message");
// logLevelFilter が Info に設定されているため、logger1.debug メッセージはログに記録されない
logger2.info("info message");

// ログを {{site.data.keyword.amashort}} サービスに送信
Logger.send();
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// 後から {{site.data.keyword.amashort}} サービスに送信できるようにするため、ログをデバイスに保存するように Logger を構成
// デフォルトでは無効。有効にするには、true に設定
Logger.logStoreEnabled = true

// 最小ログ・レベルを変更 (オプション)
// デフォルト設定は LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// 2 つのロガー・インスタンスを作成
// 複数のログ・インスタンスを作成してログを編成可能
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")

// 異なるレベルのログ・メッセージ
logger1.debug("debug message for feature 1")
// logLevelFilter が Info に設定されているため、logger1.debug メッセージはログに記録されない
logger2.info("info message for feature 2")

// ログを {{site.data.keyword.amashort}} サービスに送信
Logger.send()
```
{: codeblock}

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// 永続ログを有効化
BMSLogger.setCapture(true);

// 出力して永続化する最小ログ・レベルを設定
BMSLogger.setLevel(BMSLogger.INFO);

// 2 つのロガー・インスタンスを作成
var logger1 = BMSLogger.getInstance("logger1");
var logger2 = BMSLogger.getInstance("logger2");

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// 永続化したログを {{site.data.keyword.amashort}} サービスに送信
BMSLogger.send(success, failure);
```
{: codeblock}

### {{site.data.keyword.amashort}} Client SDK 内部ログの有効化
{: #enable-logger-sdklogs}
現在、このフィーチャーは Android 版の {{site.data.keyword.amashort}} Client SDK でのみ使用可能です。

{{site.data.keyword.amashort}} Client SDK は、Logcat 出力を内部デバッグ・メッセージで不必要に増やさないようにすることで、開発作業を改善します。したがって、デフォルトでは、{{site.data.keyword.amashort}} SDK によって DEBUG レベルで生成される内部ログ・メッセージは出力されません。以下の API を使用して、{{site.data.keyword.amashort}} Client SDK のすべての内部ログ・メッセージの出力を有効にすることができます。


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## 使用分析の収集
{: #usage-analytics}

使用分析を記録し、記録されたデータを {{site.data.keyword.amashort}} サービスに送信するように、{{site.data.keyword.amashort}} Client SDK を構成できます。
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**注:** 使用統計の記録を開始する前に、ロギング・キャプチャーを有効化したことを確認してください。

使用統計の記録と送信を開始するには、以下の API を使用します。

#### Android
{: #usage-analytics-android}

```Java
// 使用分析の記録を無効化 (例えば、ディスク・スペースの節約のため)
// デフォルトでは、記録は有効
Analytics.disable();
	
// 使用分析の記録を有効化
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// 記録した使用分析を Mobile Analytics Service に送信
Analytics.send();
```
{: codeblock}

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// 使用分析の記録を無効化 (例えば、ディスク・スペースの節約のため)
// デフォルトでは、記録は有効
Analytics.enabled = false

// 使用分析の記録を有効化
Analytics.enabled = true

// 記録した使用分析を {{site.data.keyword.mobileanalytics_short}} Service に送信
Analytics.send()
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// 使用分析の記録を有効化
BMSAnalytics.enable();

// 記録した使用分析を {{site.data.keyword.amashort}} Service に送信
BMSAnalytics.send();
```
{: codeblock}

**注:** Cordova アプリケーションを開発している場合、ネイティブ API を使用して、アプリケーション・ライフサイクル・イベントの記録を有効にしてください。

