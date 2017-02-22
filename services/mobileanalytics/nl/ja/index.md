---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} の概説

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} は、開発者、IT 管理者、ビジネス関係者に、モバイル・アプリのパフォーマンスや使用状況についての洞察を提供します。{{site.data.keyword.mobileanalytics_short}} では、以下を行うことができます。

* アプリケーションのパフォーマンスと使用状況を、デスクトップまたはタブレットからモニターします。 
* 傾向と異常を迅速に特定し、詳しく調べて問題を解決し、主要な測定基準がクリティカルしきい値を超えた場合にはアラートをトリガーします。
{: shortdesc}

**重要:** {{site.data.keyword.mobileanalytics_short}} コンソールは、Internet Explorer ブラウザーに未対応であるため、一部の機能が正しく作動しない場合があります。Firefox、Chrome、または Safari を使用することをお勧めします。

{{site.data.keyword.mobileanalytics_short}} サービスを迅速に稼働するには、以下のステップを実行します。

1. {{site.data.keyword.mobileanalytics_short}} サービスのインスタンスを作成<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->した後、{{site.data.keyword.Bluemix}} ダッシュボードの**「サービス」**セクション内のタイルをクリックして、{{site.data.keyword.mobileanalytics_short}} コンソールにアクセスできます。

 さまざまなビューやグラフ、およびそれらに表示される値を即時に把握できるようにするために、{{site.data.keyword.mobileanalytics_short}} コンソールには**「デモ・モード (demo mode)」**というオプションが用意されています。これを使用すると、ビューやグラフに*デモ・データ* が表示されます。デモ・データは、サービスのインスタンスが生成された後で、コンソールが最初に起動するときのコンソールのデフォルト・モードです。独自のアプリケーションと分析データがサービスに取り込まれている場合は、デモ・モードを*「オフ」*に切り替えると、アプリケーションのデータを別のグラフに表示できます。Mobile Analytics コンソールは、デモ・モードの場合には読み取り専用であるため、新規アラート定義を作成することはできません。

2. {{site.data.keyword.mobileanalytics_short}} [クライアント SDK](/docs/services/mobileanalytics/install-client-sdk.html) をインストールします。オプションで、{{site.data.keyword.mobileanalytics_short}} [REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "外部リンク・アイコン"){:new_window} を使用できます。

3. クライアント SDK をインポートし、次のコード・スニペットで初期設定して、使用分析を記録するようにします。

	#### Android
	{: #android-import}

	以下の `import` ステートメントをプロジェクト・ファイルの先頭に追加します。
	
    ```
import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
	import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
	import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  	```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **注:** Swift SDK は iOS と watchOS 向けに使用できます。
	
 以下の `import` ステートメントを `AppDelegate.swift` プロジェクト・ファイルの先頭に追加して、`BMSCore` および `BMSAnalytics` フレームワークをインポートします。

   ```Swift
   import BMSCore
   import BMSAnalytics
   ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 Cordova アプリケーション・ルート・ディレクトリーから次のコマンドを実行して、Cordova プラグインを追加します。

 ```Javascript
 cordova plugin add bms-core
 ```
 {: codeblock}  

4. 使用分析やアプリケーション・セッションを記録するために、[API キー](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)値を使用して、アプリケーション・コード内で {{site.data.keyword.mobileanalytics_short}} クライアント SDK を初期化します。	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 **bluemixRegion** パラメーターは、使用する {{site.data.keyword.Bluemix_notm}} デプロイメントを指定します。例えば、`BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK` などです。 
    <!-- , or `BMSClient.Region.Sydney`.-->
    
 `hasUserContext` の値を **true** または **false** に設定します。false (デフォルト値) の場合、各デバイスがアクティブ・ユーザーとしてカウントされます。

 #### iOS
 {: #ios-initialize}
  
  使用分析やアプリケーション・セッションを記録するために、[API キー](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)値を使用して、アプリケーション・コード内でクライアント SDK を初期化します。
	
  ```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
		```
  {: codeblock}
			
   **bluemixRegion** パラメーターは、使用する Bluemix デプロイメント (例: `BMSClient.Region.usSouth` や `BMSClient.Region.unitedKingdom` など) を指定します。
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
 
 `hasUserContext` の値を **true** または **false** に設定します。false (デフォルト値) の場合、各デバイスがアクティブ・ユーザーとしてカウントされます。
	
 #### Cordova
 {: #cordova-initialize}
	
 使用分析やアプリケーション・セッションを記録するために、[API キー](/docs/services/mobileanalytics/sdk.html#analytics-clientkey)値を使用して、アプリケーション・コード内でクライアント SDK を初期化します。
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  **bluemixRegion** パラメーターは、使用する {{site.data.keyword.Bluemix_notm}} デプロイメントを指定します。例えば、`BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK` などです。
  
 **注:** アプリケーション用に選択した名前 (`your_app_name_here`) は、アプリケーション名として {{site.data.keyword.mobileanalytics_short}} コンソールに表示されます。アプリケーション名は、ダッシュボードでアプリケーション・ログを検索する場合にフィルターとして使用されます。複数のプラットフォーム (例えば Android と iOS) で同じアプリケーション名を使用すると、ログの送信元がどのプラットフォームであっても、同じ名前のアプリケーションからのすべてのログを表示できます。

5. 記録した使用分析を Mobile Analytics サービスに送信します。分析のテストは、アプリケーションの開始時に次のコードを実行すると簡単に行えます。

	#### Android
	{: #android-send}

	`Analytics.send()` メソッドを使用して、分析データをサーバーに送信します。`Analytics.send()` メソッドを、Android アプリケーションのメインアクティビティーの `onCreate` メソッド内か、プロジェクトで最も適切な場所に置きます。 
	
	`Analytics.send()` はどこにでも挿入できます。

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	`Analytics.send` メソッドを使用して、分析データをサーバーに送信します。`Analytics.send` メソッドを、アプリケーション・デリゲートの `application(_:didFinishLaunchingWithOptions:)` メソッド内の任意の場所か、プロジェクトで最も適切な場所に置くことができます。 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	`BMSAnalytics.send` メソッドを使用して、分析データをサーバーに送信します。`BMSAnalytics.send` メソッドを、プロジェクトで最もうまく動作する場所に配置してください。
	
	```
	BMSAnalytics.send()
	```
	{: codeblock}
	
	[ロギング](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger)、[ネットワーク要求](/docs/services/mobileanalytics/sdk.html#network-requests)、[クラッシュ分析](/docs/services/mobileanalytics/sdk.html#report-crash-analytics)など、その他の {{site.data.keyword.mobileanalytics_short}} 機能について詳しくは、[アプリケーションの装備](/docs/services/mobileanalytics/sdk.html)トピックを参照してください。
	
6. エミュレーターまたはデバイスでアプリケーションをコンパイルして実行します。

7. {{site.data.keyword.mobileanalytics_short}} のコンソールに移動して、ご使用のアプリケーションの使用量分析を表示できます。<!--[creating custom charts](app-monitoring.html#custom-charts),-->[アラートを設定する](/docs/services/mobileanalytics/app-monitoring.html#alerts)こと、および[アプリの異常終了をモニターする](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash)ことによって、アプリケーションをモニターすることもできます。


# 関連リンク

## SDK
* [Android SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics "外部リンク・アイコン"){: new_window}  
* [iOS SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics "外部リンク・アイコン"){: new_window}
* [Cordova Plugin Core SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.npmjs.com/package/bms-core "外部リンク・アイコン"){: new_window}

## API リファレンス
{: #api}
* [REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "外部リンク・アイコン"){:new_window}
