---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.mobileanalytics_short}} クライアント SDK を使用するためのアプリケーションの装備
{: #mobileanalytics_sdk}
*最終更新日時: 2016 年 4 月 27 日*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} SDK によって、モバイル・アプリケーションを装備できるようになります。
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} を使用すると、3 つのカテゴリーのデータを収集できます。それぞれ異なるレベルの装備をする必要があります:

1.  事前定義データ - このカテゴリーには、すべてのアプリに適用される一般的な使用情報およびデバイス情報が含まれます。このカテゴリー内には、デバイス・メタデータ (オペレーティング・システムおよびデバイス・モデル) および使用データ (アクティブ・ユーザー数およびアプリ・セッション数) が含まれており、アプリ使用のボリューム、頻度、または期間を示します。事前定義データは、アプリで {{site.data.keyword.mobileanalytics_short}} SDK を初期設定すると自動的に収集されます。
2. カスタム・イベント - このカテゴリーには、自身で定義したデータ、およびアプリに固有のデータが含まれます。このデータは、ページ・ビュー、ボタン・タップ、アプリ内購入など、アプリ内で発生するイベントを表します。アプリでの {{site.data.keyword.mobileanalytics_short}} SDK の初期設定に加えて、追跡対象の各カスタム・イベントに対してコードを 1 行追加する必要があります。
3. クライアント・ログ・メッセージ - このカテゴリーを使用すると、カスタム・メッセージをログに記録するコード行を開発者がアプリ全体にわたって追加できるようになり、開発およびデバッグに役立ちます。開発者は重大度/詳細レベルを各ログ・メッセージに割り当て、その後、割り当てたレベルによってメッセージをフィルター操作したり、指定したログ・レベルを下回るメッセージを無視するようアプリを構成することでストレージ・スペースを確保したりできます。クライアント・ログ・データを収集するには、アプリ内の {{site.data.keyword.mobileanalytics_short}} SDK を初期設定し、また、各ログ・メッセージのコード行を追加する必要があります。

SDK は、現在 Android、iOS、および WatchOS で使用できます。

## クライアント・キー値の識別
{: #analytics-clientkey}

クライアント SDK をセットアップする前に、**クライアント・キー**値を識別します。クライアント・キーは、クライアント SDK の初期設定に必要です。
1. {{site.data.keyword.mobileanalytics_short}} サービス・ダッシュボードを開きます。
2. レンチ・アイコンをクリックして「API キー」タブを開きます。
3. 「API キー」タブで、クライアント・キー値をメモに取ります。


## 分析を収集するための Android アプリの初期設定
{: #initalize-ma-sdk-android}

{{site.data.keyword.mobileanalytics_short}} サービスにログを送れるようにアプリケーションを初期設定します。

1. 以下の `import` ステートメントをプロジェクト・ファイルの先頭に追加して、クライアント SDK をインポートします:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Android アプリケーションのメイン・アクティビティーの `onCreate` メソッド、もしくはご使用のプロジェクトで最も適切な場所に初期設定コードを追加して、Android アプリケーションの {{site.data.keyword.mobileanalytics_short}} クライアント SDK を初期設定します。

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
        } catch (MalformedURLException e) {
            Log.e(your_app_name,"URL should not be malformed:  " + e.getLocalizedMessage());
        } 
  ```
  {: codeblock}

  {{site.data.keyword.mobileanalytics_short}} クライアント SDK を使用するには、**bluemixRegion** パラメーターを指定して `BMSClient` を初期設定する必要があります。初期化指定子において、**bluemixRegion** 値は、使用している {{site.data.keyword.Bluemix_notm}} デプロイメントを指定します。例えば `BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK`、あるいは `BMSClient.REGION_SYDNEY` などです。
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Android アプリケーション・オブジェクトを使用して分析を初期設定し、アプリケーション名を付けます。また、[**クライアント・キー**](#analytics-clientkey)値も必要です。
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// In this code example, Analytics is configured to record lifecycle events.
	```
  {: codeblock}

	**ヒント:** アプリケーション名は、ダッシュボードでクライアント・ログを検索する場合にフィルターとして使用されます。複数のプラットフォーム (例えば Android と iOS) で同じアプリケーション名を使用すると、ログの送信元がどのプラットフォームであっても、同じ名前のアプリケーションからのすべてのログを表示できます。

## 分析収集のための iOS アプリの初期設定
{: #init-ma-sdk-ios}

{{site.data.keyword.mobileanalytics_short}} サービスにログを送れるようにアプリケーションを初期設定します。Swift SDK は iOS および watchOS で使用できます。

1. 以下の `import` ステートメントを `AppDelegate.swift` プロジェクト・ファイルの先頭に追加して、`BMSCore` および `BMSAnalytics` フレームワークをインポートします:

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. {{site.data.keyword.mobileanalytics_short}} クライアント SDK を使用するには、まず以下のコードを使用して `BMSClient` クラスを初期設定する必要があります。

  初期設定コードを、アプリケーション・デリゲートの `application(_:didFinishLaunchingWithOptions:)` メソッド内か、プロジェクトで最も適切な場所に置きます。

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    {{site.data.keyword.mobileanalytics_short}} クライアント SDK を使用するには、**bluemixRegion** パラメーターを指定して `BMSClient` を初期設定する必要があります。初期化指定子において、**bluemixRegion** 値は、使用している {{site.data.keyword.Bluemix_notm}} デプロイメントを指定します。例えば `BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK`、あるいは `BMSClient.REGION_SYDNEY` などです。
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. モバイル・アプリケーション名を付けて分析を初期設定します。また、[**クライアント・キー**](#analytics-clientkey)値も必要です。

  アプリケーション名は、{{site.data.keyword.mobileanalytics_short}} ダッシュボードでクライアント・ログを検索する場合にフィルターとして使用されます。複数のプラットフォーム (例えば Android と iOS) で同じアプリケーション名を使用すると、ログの送信元がどのプラットフォームであっても、同じ名前のアプリケーションからのすべてのログを表示できます。

  オプションの `deviceEvents` パラメーターを使用すると、デバイス・レベルのイベントに関する分析が自動的に収集されます。

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: your_client_key,
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: your_api_key)
	```

  `Analytics.recordApplicationDidBecomeActive()` メソッドと `Analytics.recordApplicationWillResignActive()` メソッドを使用すると、WatchOS に関するデバイス・イベントを記録できます。
  
  以下の行を ExtensionDelegate クラスの `applicationDidBecomeActive()` メソッドに追加します。

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  以下の行を ExtensionDelegate クラスの applicationWillResignActive() メソッドに追加します:
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

## 使用分析の収集
{: #app-monitoring-gathering-analytics}

  使用分析を記録し、記録されたデータを {{site.data.keyword.mobileanalytics_short}} サービスに送信するように、{{site.data.keyword.mobileanalytics_short}} クライアント SDK を構成できます。

  以下の API を使用して、使用分析の記録と送信を始めます:

#### Android
{: #android-usage-api}
	
```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();
	
// Enable recording of usage analytics
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send();
```
	
イベントをログに記録するための使用分析の例:
	
```
// Log a custom analytics event for custom charts, which is represented by a JSON object:
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.enabled = false

// Enable recording of usage analytics
Analytics.enabled = true

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send()
```

イベントをログに記録するための使用分析の例:

```
// Log a custom analytics event for custom charts
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```

  <!--Removing Cordova for experimental-->
  <!--### Cordova-->
  <!--{: #usage-analytics-cordova}-->

  <!--```JavaScript-->
  <!--// Enable usage analytics recording-->
  <!--Analytics.enable();-->

  <!--// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--Analytics.send();-->
  <!--```-->
  <!--**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.-->

## ロガーの有効化、構成、および使用
{: #app-monitoring-logger}

  {{site.data.keyword.mobileanalytics_full}} クライアント SDK には、`java.util.logging` や `log4j` など、ユーザーが精通している他のログ・フレームワークに似たロギング・フレームワークが用意されています。このロギング・フレームワークは、複数のパッケージ別ロガー・インスタンス、さまざまなログ・レベル、アプリケーション異常終了のスタック・トレースのキャプチャーなどをサポートしています。

  また、ログに記録されたデータをアプリケーションが稼働するデバイスに保管し、あとでこれらのデバイス・ログを {{site.data.keyword.mobileanalytics_short}} サービスに送信するように構成することもできます。

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  {{site.data.keyword.mobileanalytics_short}} クライアント SDK のロギング・フレームワークでは、以下のログ・レベルがサポートされます。詳細の程度が最も低いものから高いものの順に、推奨される使用法ガイドラインとともにリストします:

  * `FATAL` - リカバリー不能な異常終了またはハングの場合に使用します。`FATAL` レベルは、ユーザーがアプリケーション異常終了として認識するリカバリー不能エラーのロギング用に予約されています
  * `ERROR` - 予期しない例外または予期しないネットワーク・プロトコル・エラーの場合に使用します
  * `WARN` - 推奨されない API の使用やネットワーク応答の遅延など、致命的なエラーではないと考えられる使用上の警告をログに記録する場合に使用します
  * `INFO` - 初期設定イベントや、重要と思われるが緊急ではないその他のデータを報告する場合に使用します
  * `DEBUG` - 開発者がアプリケーションの問題を解決する際に役立つデバッグ・ステートメントを報告する場合に使用します

    #### ログ・レベルのシナリオ
    {: #log-level-scenario}

    ロガー・レベルが `FATAL` に設定されている場合、ロガーはキャッチされていない例外をキャプチャーしますが、異常終了イベントにつながるログはキャプチャーしません。より詳細なロガー・レベルを設定して、`FATAL` ロガー項目につながる可能性のあるログ (`WARN` や `ERROR` など) もキャプチャーするようにできます。

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### ロガーの使用例
{: #sample-logger-usage}

**注:** ロギング・フレームワークを使用する前に、[{{site.data.keyword.mobileanalytics_short}} クライアント SDK](sdk.html) を使用するようにアプリを装備しておく必要があります。
 
  以下のコード・スニペットにロガーの使用例を示します:

#### Android
{: #android-logger-sample}

```
// Configure Logger to save logs to the device so that they
// can later be sent to the {{site.data.keyword.mobileanalytics_short}} service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service
Logger.send();
```

ロガーのシナリオ:

```
// Create two logger instances
// You can create multiple log instances to organize your logs
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Log messages with different levels
// Debug message for feature 1
// Info message for feature 2
logger1.debug("debug message"); 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message");
```

#### iOS - Swift
{: ios-logger-sample}

```
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.mobileanalytics_short}} service
// Disabled by default; set to true to enable
Logger.logStoreEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service
Logger.send()
```

ロガーのシナリオ:
    
```
// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")
	
// Log messages with different levels
logger1.debug("debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message for feature 2")
```

**ヒント**: プライバシーに関する懸念から、リリース・モードでビルドされたアプリケーションのロガー出力を無効にすることができます。デフォルトでは、ロガー・クラスはログを Xcode コンソールに出力します。ターゲットのビルド設定で、リリース・ビルド構成の **Other Swift Flags** セクションに `-D RELEASE_BUILD` フラグを追加します。
    

  <!-- ### Cordova-->
  <!--{: #enable-logger-sample-cordova}-->

  <!--// Enable persisting logs-->
  <!--MFPLogger.setCapture(true);-->

  <!--// Set the minimum log level to be printed and persisted-->
  <!--MFPLogger.setLevel(MFPLogger.INFO);-->

  <!--var logger1 = MFPLogger.getInstance("logger1");-->
  <!--var logger2 = MFPLogger.getInstance("logger2");   -->

  <!--// Log messages with different levels-->
  <!--logger1.debug ("debug message");-->
  <!--logger2.info ("info message");-->

  <!--// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--```-->

<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
Logger.setSDKDebugLoggingEnabled(true);
```

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
-->

## アクティブ・ユーザーのトラッキング
{: #trackingusers}
オプションで、アクティブ・ユーザーのユーザー名を {{site.data.keyword.mobileanalytics_short}} に渡すことで、アプリケーションをアクティブに使用しているユーザー数をトラッキングできます。

#### Android
{: #android-tracking-users}

ユーザーのログイン時用の以下のコードを追加します:

```
Analytics.setUserIdentity("username");
```

ユーザーのログアウト時用の以下のコードを追加します:

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

ユーザーのログイン時用の以下のコードを追加します:

```
Analytics.userIdentity = "username"
```

ユーザーのログアウト時用の以下のコードを追加します:

```
Analytics.userIdentity = nil
```

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before `/analytics/console/dashboard`.  

  		For example, if the dashboard URL is: `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde`
      {: screen}

  		then the Analytics Service Route is
      `http://mobile-analytics-dashboard.ng.bluemix.net`
      {: screen}

  	2. Get the [Client API Key](#analytics-clientkey) value from the Analytics dashboard.

  	You will use the {{site.data.keyword.mobileanalytics_short}} service route and API Key to construct a URL to report analytics data, depending on the version of your MobileFirst Platform server. -->

<!--  3. Copy the URL for your {{site.data.keyword.mobileanalytics_short}} service dashboard. Include the `instanceId` query parameter, for example:
      `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=1212345abcde`
      {: screen}

  4. Configure the values for the MobileFirst Platform server JNDI properties, as follows:-->

<!--    ### MobileFirst Platform V7.0
    {: #mfp70}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values}

        For a MobileFirst Platform project named `Myproj7000`, based on the examples in steps 2 and 3, replace the current JNDI property values in the `server.xml` file with:
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
        ```
        {: screen}
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
        ```
        {: screen}

    ### MobileFirst Platform V7.1
    {: #mfp71}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values}

      For a MobileFirst Platform project named `MyProj7101`, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/v2/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}

      ### MobileFirst Platform V8.0
      {: #mfp80}

      The format of the `mfp.analytics.url` JNDI property is:
      `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`  

    #### Example MobileFirst Platform V8.0 Beta JNDI property values
      {: example-mfp80b-jndi-values}

      For a MobileFirst Platform project named `mfp`, which is the default, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}
-->
<!-- #### Ignored events and event retention
{: #ignored-events}
The {{site.data.keyword.mobileanalytics_short}} service saves the following data for ignored events and event retention:
  
<dl>	
<dt>Ignored events</dt>
	<dd>`ANALYTICS_SDK_CFG_IGNORE_AppPushAction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_ServerLog: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransaction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransactionSummarizedHourly: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushNotification: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushSubscription: true`</dd>
</dt>
<dt>Event retention</dd>
<dd>
`ANALYTICS_TTL_AlertNotification: 14d`<br>
`ANALYTICS_TTL_CustomData: 7d`<br>
`ANALYTICS_TTL_Device: 90d`<br>
`ANALYTICS_TTL_AppLog: 3d`<br>
`ANALYTICS_TTL_AppSession: 7d`
</dd>
</dt>
</dl>
  
-->

# 関連リンク

## API リファレンス
{: #api}
* [REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
