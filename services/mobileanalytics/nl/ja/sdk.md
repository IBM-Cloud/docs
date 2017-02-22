---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} クライアント SDK を使用するためのアプリケーションの装備
{: #mobileanalytics_sdk}

{{site.data.keyword.mobileanalytics_full}} SDK によって、モバイル・アプリケーションを装備できるようになります。
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} を使用すると、2 つの<!--three-->カテゴリーのデータを収集できます。カテゴリーごとに異なるレベルの計装を行う必要があります:

1. 事前定義データ - このカテゴリーには、すべてのアプリケーションに適用される一般的な使用情報およびデバイス情報が含まれます。このカテゴリー内には、デバイス・メタデータ (オペレーティング・システムおよびデバイス・モデル) および使用データ (アクティブ・ユーザー数およびアプリケーション・セッション数) が含まれており、アプリケーション使用のボリューム、頻度、または期間を示します。事前定義データは、アプリケーションで {{site.data.keyword.mobileanalytics_short}} SDK を初期設定すると自動的に収集されます。

2. アプリケーション・ログ・メッセージ - このカテゴリーでは、開発者は、開発およびデバッグに役立つカスタム・メッセージをログに記録するコード行をアプリケーション全体に追加できます。開発者は重大度/詳細レベルを各ログ・メッセージに割り当て、その後、割り当てたレベルによってメッセージをフィルター操作したり、指定したログ・レベルの下位レベルのメッセージを無視するようにアプリケーションを構成してストレージ・スペースを維持したりできます。アプリケーション・ログ・データを収集するには、アプリケーション内で {{site.data.keyword.mobileanalytics_short}} SDK を初期化し、各ログ・メッセージのコード行を追加する必要があります。

3. カスタム・イベント - このカテゴリーには、ユーザー自身が定義するデータと、アプリ固有のデータが含まれます。このデータは、ページ・ビューやボタン・タップ、アプリ内購入など、アプリ内で発生するイベントを表します。アプリでの {{site.data.keyword.mobileanalytics_short}} SDK の初期化に加えて、追跡するカスタム・イベントごとにコード行を追加する必要があります。 

SDK は、現在 Android、iOS、WatchOS、Cordova で使用できます。

## サービス資格情報 API キー値の特定
{: #analytics-clientkey}

クライアント SDK をセットアップする前に、**API キー**値を特定します。クライアント SDK の初期化には API キーが必要です。

1. {{site.data.keyword.mobileanalytics_short}} サービス・ダッシュボードを開きます。
2. **「資格情報の表示」**を展開すると、API キー値が表示されます。この API キー値は、{{site.data.keyword.mobileanalytics_short}} Client SDK を初期設定する場合に必要です。


## 分析を収集するためのアプリケーションの初期設定
{: #initalize-ma-sdk}

{{site.data.keyword.mobileanalytics_short}} サービスにログを送れるようにアプリケーションを初期設定します。

1. Client SDK をインポートします。

	### Android
	{: #android-import}

	以下の `import` ステートメントをプロジェクト・ファイルの先頭に追加します。
	
  	```
  	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
	import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
	import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  	```
  	{: codeblock}
  
	### iOS
	{: #ios-import}
	
	**注:** Swift SDK は iOS と watchOS 向けに使用できます。
	
	以下の `import` ステートメントを `AppDelegate.swift` プロジェクト・ファイルの先頭に追加して、`BMSCore` および `BMSAnalytics` フレームワークをインポートします。

   ```Swift
   import BMSCore
   import BMSAnalytics
   ```
   {: codeblock}  
   
   ### Cordova
	{: #cordova-import}
		
	Cordova アプリケーション・ルート・ディレクトリーから次のコマンドを実行して、Cordova プラグインを追加します。

   ```Javascript
   cordova plugin add bms-core
   ```
   {: codeblock}  

2. {{site.data.keyword.mobileanalytics_short}} アプリケーション内で Client SDK を初期化します。

	### Android
	{: #android-init}
	
	Android アプリケーションのメイン・アクティビティーの `onCreate` メソッド、またはご使用のプロジェクトで最も適切な場所に初期設定コードを追加して、Android アプリケーションの {{site.data.keyword.mobileanalytics_short}} Client SDK を初期設定します。

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
	{: codeblock}

  **bluemixRegion** パラメーターを指定して `BMSClient` を初期化する必要があります。初期化指定子において、**bluemixRegion** 値には、使用している {{site.data.keyword.Bluemix_notm}} デプロイメント (例: `BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK` など) を指定します。 
    <!-- , or `BMSClient.REGION_SYDNEY`.--> 
    
 ### iOS
 {: #ios-init}
    
 最初に、以下のコードを使用して `BMSClient` クラスを初期化します。初期設定コードを、アプリケーション・デリゲートの `application(_:didFinishLaunchingWithOptions:)` メソッド内か、プロジェクトで最も適切な場所に置きます。
	
    ```Swift 
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
    ```
   {: codeblock}

   **bluemixRegion** パラメーターを指定して `BMSClient` を初期化する必要があります。初期化指定子において、**bluemixRegion** 値には、使用している {{site.data.keyword.Bluemix_notm}} デプロイメント (例: `BMSClient.Region.usSouth` や `BMSClient.Region.unitedKingdom` など) を指定します。
    <!-- , or `BMSClient.Region.Sydney`. -->
    
 ### Cordova
 {: #cordova-init}
    
 **BMSClient** と **BMSAnalytics** を初期化します。[**API キー**](#analytics-clientkey)値が必要になります。

  ```Javascript
  var applicationName = "HelloWorld";
  var apiKey =  "your_api_key_here";
  var hasUserContext = true;
  var deviceEvents = [BMSAnalytics.ALL];

  BMSClient.initialize(BMSClient.REGION_US_SOUTH); //Make sure you point to your region	
  BMSAnalytics.initialize(applicationName, apiKey, hasUserContext, deviceEvents)
  ```
  {:codeblock}

 {{site.data.keyword.mobileanalytics_short}} Client SDK を使用するには、**bluemixRegion** パラメーターを指定して `BMSClient` を初期設定する必要があります。初期化指定子において、**bluemixRegion** 値には、使用している {{site.data.keyword.Bluemix_notm}} デプロイメント (例: `BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK` など) を指定します。
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
    
3. アプリケーション・オブジェクトを使用して分析を初期設定し、アプリケーション名を付けます。 

	アプリケーション用に選択した名前 (`your_app_name_here`) は、アプリケーション名として {{site.data.keyword.mobileanalytics_short}} コンソールに表示されます。アプリケーション名は、ダッシュボードでアプリケーション・ログを検索する場合にフィルターとして使用されます。複数のプラットフォーム (例えば Android と iOS) で同じアプリケーション名を使用すると、ログの送信元がどのプラットフォームであっても、同じ名前のアプリケーションからのすべてのログを表示できます。

	また、[**API キー**](#analytics-clientkey)値も必要です。

	### Android
	{: #android-init-analytics}
	
	```Java
	
	// In this code example, Analytics is configured to record lifecycle events.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
	
	**注:** `hasUserContext` の値を **true** または **false** に設定します。false (デフォルト値) の場合、各デバイスがアクティブ・ユーザーとしてカウントされます。`hasUserContext` が false の場合、[`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) メソッドは機能しません。このメソッドは、デバイスごとにアクティブにアプリケーションを使用しているユーザー数をトラッキングできます。true の場合、[`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) を使用するたびにアクティブ・ユーザーとしてカウントされます。`hasUserContext` が true の場合、デフォルトのユーザー ID は存在しないため、アクティブ・ユーザー・グラフにデータを取り込む場合には、ユーザー ID を設定する必要があります。
	
	### iOS
	{: #ios-initialize-analytics}
	
 	```Swift 
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: .lifecycle, .network)
 	```
 	{: codeblock}
 	
   ### watchOS
   {: #watchos-initialize-analytics}
	 	
 	```Swift
 	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", deviceEvents: .network)
 	```
 	{: codeblock}
 	
 	オプションの `deviceEvents` パラメーターを使用すると、デバイス・レベルのイベントに関する分析が自動的に収集されます。
	
 **注:** `hasUserContext` の値を **true** または **false** に設定します。false (デフォルト値) の場合、各デバイスがアクティブ・ユーザーとしてカウントされます。`hasUserContext` が false の場合、[`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) メソッドは機能しません。このメソッドは、デバイスごとにアクティブにアプリケーションを使用しているユーザー数をトラッキングできます。`hasUserContext` が true の場合、[`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) を使用するたびにアクティブ・ユーザーとしてカウントされます。`hasUserContext` が true の場合、デフォルトのユーザー ID は存在しないため、アクティブ・ユーザー・グラフにデータを取り込む場合には、ユーザー ID を設定する必要があります。

 #### watchOS
 {: #watchos-record-device}

 `Analytics.recordApplicationDidBecomeActive()` メソッドと `Analytics.recordApplicationWillResignActive()` メソッドを使用すると、WatchOS に関するデバイス・イベントを記録できます。
  
 次の行を ExtensionDelegate クラスの `applicationDidBecomeActive()` メソッドに追加します。
 
	```
	Analytics.recordApplicationDidBecomeActive()
	```
   {: codeblock}

 次の行を ExtensionDelegate クラスの `applicationWillResignActive()` メソッドに追加します。
 
	```
	Analytics.recordApplicationWillResignActive()
	```
	{: codeblock}	
		
4. これで、分析を収集するアプリケーションが初期化されました。次に、{{site.data.keyword.mobileanalytics_short}} サービスに[分析データを送信](sdk.html#app-monitoring-gathering-analytics)することができます。


## 使用分析の収集
{: #app-monitoring-gathering-analytics}

  使用分析を記録し、記録されたデータを {{site.data.keyword.mobileanalytics_short}} サービスに送信するように、{{site.data.keyword.mobileanalytics_short}} Client SDK を構成できます。

  以下の API を使用して、使用分析の記録と送信を始めます:

#### Android
{: #android-usage-api}
	
```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();
	
// Enable recording of usage analytics
Analytics.enable();
		
// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send(new ResponseListener() {
            @Override
            public void onSuccess(Response response) {
                // Handle Analytics send success here.
            }

            @Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                // Handle Analytics send failure here.
            }
        });
```
{: codeblock}
	
イベントをログに記録するための使用分析例を以下に示します。
	
```
// Log a custom analytics event
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");

Analytics.log(eventJSONObject);
```
{: codeblock}


#### iOS - Swift
{: #ios-usage-api}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.isEnabled = false

// Enable recording of usage analytics
Analytics.isEnabled = true

// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send(completionHandler: { (response: Response?, error: Error?) in

    if let response = response {
        // Handle Analytics send success here.
    }
    if let error = error {
        // Handle Analytics send failure here.
    }
})
```
{: codeblock}

イベントをログに記録するための使用分析例を以下に示します。

```Swift
// Log a custom analytics event
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(metadata: eventObject)
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

  ```JavaScript
  // Enable usage analytics recording
  BMSAnalytics.enable();
  
  // Disable usage analytics recording
  BMSAnalytics.disable();

  // Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
  BMSAnalytics.send(
	function(response) {
		console.log('success: ' + response);
		},
	function (err) {
		console.log('fail: ' + err);
		});
  ```
  {: codeblock}

イベントをログに記録するための使用分析例を以下に示します。

```JavaScript
// Log a custom analytics event
var eventObject = {"customProperty": "propertyValue"}
BMSAnalytics.log(eventObject)
```
{: codeblock}

  
  **注:** Cordova アプリケーションを開発する際には、ネイティブ API を使用してアプリケーション・ライフサイクル・イベントの記録機能を有効にしてください。
  
## ロガーの有効化、構成、および使用
{: #app-monitoring-logger}

  {{site.data.keyword.mobileanalytics_full}} Client SDK には、`java.util.logging` や `log4j` など、ユーザーが精通している他のログ・フレームワークに似たロギング・フレームワークが用意されています。このロギング・フレームワークは、複数のパッケージ別ロガー・インスタンス、さまざまなログ・レベル、アプリケーション異常終了のスタック・トレースのキャプチャーなどをサポートしています。

  また、ログに記録されたデータをアプリケーションが稼働するデバイスに保管し、あとでこれらのデバイス・ログを {{site.data.keyword.mobileanalytics_short}} サービスに送信するように構成することもできます。

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  {{site.data.keyword.mobileanalytics_short}} Client SDK のロギング・フレームワークでは、以下のログ・レベルがサポートされます。詳細の程度が最も低いものから高いものの順に、推奨される使用法ガイドラインと共にリストします。

  * `FATAL` - リカバリー不能な異常終了またはハングの場合に使用します。`FATAL` レベルは、ユーザーがアプリケーション異常終了として認識するリカバリー不能エラーのロギング用に予約されています
  * `ERROR` - 予期しない例外または予期しないネットワーク・プロトコル・エラーの場合に使用します
  * `WARN` - 推奨されない API の使用やネットワーク応答の遅延など、致命的なエラーではないと考えられる使用上の警告をログに記録する場合に使用します
  * `INFO` - 初期設定イベントや、重要と思われるが緊急ではないその他のデータを報告する場合に使用します
  * `DEBUG` - 開発者がアプリケーションの問題を解決する際に役立つデバッグ・ステートメントを報告する場合に使用します

    #### ログ・レベルのシナリオ
    {: #log-level-scenario}

    ロガー・レベルが `FATAL` に設定されている場合、ロガーはキャッチされていない例外をキャプチャーしますが、異常終了イベントにつながるログはキャプチャーしません。より詳細なロガー・レベルを設定して、`FATAL` ロガー項目につながる可能性のあるログ (`WARN` や `ERROR` など) もキャプチャーするようにできます。

    ロガー・レベルが `DEBUG` に設定されている場合は、ログの送信時に含められる Mobile Analytics Client SDK ログも取得できます。

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

### ロガーの使用例
{: #sample-logger-usage}

**注:** ロギング・フレームワークを使用する前に、{{site.data.keyword.mobileanalytics_short}} Client SDK を使用するようにアプリケーションを装備したことを確認してください。
 
  以下のコード・スニペットにロガーの使用例を示します:
#### Android
{: #android-logger-sample}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

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

// Send logs to the Mobile Analytics Service
        Logger.send(new ResponseListener() {
                    @Override
                    public void onSuccess(Response response) {
                        // Handle Logger send success here.
                    }

                    @Override
                    public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                        // Handle Logger send failure here.
                    }
                });        
```
{: codeblock}

#### iOS - Swift
{: #ios-logger-sample-swift2}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.isLogStorageEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(name: "feature1Logger")
let logger2 = Logger.logger(name: "feature2Logger")

// Log messages with different levels
logger1.debug(message: "debug message for feature 1") 
// The logger1.debug message is not logged because the 
// logLevelFilter is set to info
logger2.info(message: "info message for feature 2")

// Send logs to the Mobile Analytics Service
Logger.send(completionHandler: { (response: Response?, error: Error?) in
    
    if let response = response {
        logger.debug(message: "Status code: \(response.statusCode)")
        logger.debug(message: "Response: \(response.responseText)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
})
```
{: codeblock}

**ヒント:** プライバシーに関する懸念から、リリース・モードでビルドされたアプリケーションのロガー出力を無効にすることができます。デフォルトでは、ロガー・クラスはログを Xcode コンソールに出力します。ターゲットのビルド設定で、リリース・ビルド構成の **Other Swift Flags** セクションに `-D RELEASE_BUILD` フラグを追加します。
    

#### Cordova
{: #enable-logger-sample-cordova}

  ```
  // Enable persisting logs
  BMSLogger.storeLogs(true);

  // Set the minimum log level to be printed and persisted
  BMSLogger.setLogLevel(BMSLogger.INFO);

  var logger1 = BMSLogger.getLogger("logger1");
  var logger2 = BMSLogger.getLogger("logger2");

  // Log messages with different levels
  logger1.debug ("debug message");
  logger2.info ("info message");

  // Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service
  BMSLogger.send();
  BMSAnalytics.send();
  ```
  {: codeblock}


<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
{: codeblock}
Logger.setSDKDebugLoggingEnabled(true);
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
{: codeblock}
-->

## ネットワーク要求の実行
{: #network-requests}

[ネットワーク要求を行う](/docs/mobile/sdk_network_request.html)ように {{site.data.keyword.mobileanalytics_short}} クライアント SDK を構成することができます。既に `BMSClient` と `BMSAnalytics` が初期化されていて、クライアント SDK がインポートされていることを確認してください。

<!--
#### Android
{: #android-network-requests}

**Note:** This code snippet assumes that you have [imported the Client SDKs](#android-import).

```
public void makeGetCall(){
    Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            try  {
                Request request = new Request("http://httpbin.org/get", "GET");
                    request.send(null, null);
            } catch (Exception e) {
                // Handle failure here.
            }
        }
    });
    thread.start();
}
```
{: codeblock}

-->

<!-- 
#### Swift 3.0
{: #ios-network-requests}

 ```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
 
 -->

<!-- Commenting out bmsurlsession
```
// Make a network request
let urlSession = BMSURLSession(configuration: .default, delegate: nil, delegateQueue: nil)
var request = URLRequest(url: URL(string: "http://httpbin.org/get")!)
request.httpMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTask(with: request) { (data: Data?, response: URLResponse?, error: Error?) in
    if let httpResponse = response as? HTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = String(data: data!, encoding: .utf8) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->

<!--
#### Swift 2.2
{: ios-swift22-network-requests}

```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
-->
<!--
```
// Make a network request
let urlSession = BMSURLSession(configuration: .defaultSessionConfiguration(), delegate: nil, delegateQueue: nil)
let request = NSMutableURLRequest(URL: NSURL(string: "http://httpbin.org/get")!)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTaskWithRequest(request) { (data: NSData?, response: NSURLResponse?, error: NSError?) in
    if let httpResponse = response as? NSHTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = NSString(data: data!, encoding: NSUTF8StringEncoding) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->
<!--
#### Cordova
{: #cordova-network-requests}

```
var success = function(data){
     console.log("success", data);
 }
 var failure = function(error)
     {console.log("failure", error);
 }
 var request = new BMSRequest("<your application route>", BMSRequest.GET);
 request.send(success, failure);
```
{: codeblock}

-->

## 異常終了分析の報告
{: #report-crash-analytics}

分析およびログ情報を {{site.data.keyword.mobileanalytics_short}} に送信することによって、[アプリケーションの異常終了データ](app-monitoring.html#monitor-app-crash)を表示することができます。

`Analytics.send()` メソッドによって、**「異常終了」**ページの**「異常終了の概要」**表および**「異常終了」**表にデータが設定されます。このセクションにあるグラフは、分析の初期設定および送信プロセスを使用して有効にすることができます。特別な構成は必要ありません。

`Logger.send()` メソッドによって、**「トラブルシューティング」**ページの**「異常終了の要約」**および**「異常終了の詳細」**表にデータが設定されます。以下のような追加のステートメントをアプリケーション・コードに追加することによって、アプリケーションがログを保管および送信してこのセクションのグラフにデータを設定できるようにする必要があります。

#### Android
{: #android-crash-statement}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

[サンプル・ロガーの使用法](sdk.html#android-logger-sample)を参照してください。

#### iOS
{: #ios-crash-statement}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

[サンプル・ロガーの使用法](sdk.html##ios-logger-sample-swift2)を参照してください。

#### Cordova
{: #cordova-crash-statement}

* `BMSLogger.storeLogs(true);`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

[サンプル・ロガーの使用法](sdk.html##ios-logger-sample-swift2)を参照してください。


## アクティブ・ユーザーのトラッキング
{: #trackingusers}

アプリケーションが 1 つのデバイスの固有のユーザーを認識できる場合は、オプションで、アクティブ・ユーザーのユーザー名を {{site.data.keyword.mobileanalytics_short}} に渡すことで、アプリケーションをアクティブに使用しているユーザー数をトラッキングできます。 

`hasUserContext=true` を指定して {{site.data.keyword.mobileanalytics_short}} を初期設定することで、ユーザー・トラッキングを有効にします。そうしないと、{{site.data.keyword.mobileanalytics_short}} はデバイス 1 つにつきユーザーを 1 人しかキャプチャーしません。 
#### Android
{: #android-tracking-users}

ユーザーのログイン時刻をトラッキングする場合は、以下のコードを追加します。

```
Analytics.setUserIdentity("username");
```
{: codeblock}

<!--Add the following code for when the user logs out:

```
Analytics.clearUserIdentity();
```
{: codeblock}
-->

#### iOS - Swift
{: #ios-tracking-users}

ユーザーのログイン時刻をトラッキングする場合は、以下のコードを追加します。

```
Analytics.userIdentity = "username"
```
{: codeblock}

<!--
Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```
{: codeblock}
-->

#### Cordova
{: #cordova-tracking-users}

ユーザーのログイン時刻をトラッキングする場合は、以下のコードを追加します。

```
BMSAnalytics.setUserIdentity("username");
```
{: codeblock}


<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before ``/analytics/console/dashboard``.  

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

## 次の作業
{: #what-to-do-next}

{{site.data.keyword.mobileanalytics_short}} コンソールに移動して、使用分析 (例: アプリケーションを使用する新規デバイスやデバイスの総数など) を確認できます。<!--[creating custom charts](app-monitoring.html#custom-charts),-->[アラートを設定する](app-monitoring.html#alerts)こと、および[アプリの異常終了をモニターする](app-monitoring.html#monitor-app-crash)ことによって、アプリケーションをモニターすることもできます。

# 関連リンク

## API リファレンス
{: #api}
* [REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "外部リンク・アイコン"){:new_window}
