---

copyright:
  years: 2016
lastupdated: "2016-10-19"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} の概説
{: #gettingstartedtemplate}


最終更新日: 2016 年 10 月 19 日
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} は、開発者、IT 管理者、ビジネス関係者に、モバイル・アプリのパフォーマンスや使用状況についての洞察を提供します。
アプリケーションのパフォーマンスと使用状況を、デスクトップまたはタブレットからモニターします。傾向と異常を迅速に検出し、詳しく調べて問題を解決し、主要な測定基準がクリティカルしきい値を超えた場合にはアラートをトリガーします。
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} サービスを素早く稼働させるためには、次のステップに従います。

1. {{site.data.keyword.mobileanalytics_short}} サービスのインスタンスを作成<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->した後、{{site.data.keyword.Bluemix}} ダッシュボードの**「サービス」**セクション内のタイルをクリックして、{{site.data.keyword.mobileanalytics_short}} コンソールにアクセスできます。

 {{site.data.keyword.mobileanalytics_short}} サービスは、**デモ・モード**が有効になった状態で起動します。デモ・モードによって**「APP DATA」**ページと**「ALERTS」**ページのグラフにデータが設定されるので、データがどのように表示されるのかを確認できます。独自のデータがある場合は、デモ・モードをオフに切り替えることができます。{{site.data.keyword.mobileanalytics_short}} コンソールはデモ・モードの場合は読み取り専用であるため、新規アラート定義を作成することはできません。

2. {{site.data.keyword.mobileanalytics_short}} [クライアント SDK](install-client-sdk.html) をインストールします。オプションで、{{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window} を使用できます。

3. クライアント SDK をインポートし、次のコード・スニペットで初期設定して、使用分析を記録します。

	#### Android
	{: #android-initialize}
	1. Client SDK をインポートします。

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
		{: codeblock}
		
	2. 使用分析やアプリケーション・セッションを記録するために、[API キー](sdk.html#analytics-clientkey)値を使用して、アプリケーション・コード内でクライアント SDK を初期化します。

		```Java
			BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
			
			Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.LIFECYCLE);
		```
		{: codeblock}
		
    アプリケーション用に選択した名前 (`your_app_name_here`) は、アプリケーション名として {{site.data.keyword.mobileanalytics_short}} コンソールに表示されます。アプリケーション名は、ダッシュボードでアプリケーション・ログを検索する場合にフィルターとして使用されます。複数のプラットフォーム (例えば Android と iOS) で同じアプリケーション名を使用すると、ログの送信元がどのプラットフォームであっても、同じ名前のアプリケーションからのすべてのログを表示できます。
    
    **bluemixRegion** パラメーターは、使用する {{site.data.keyword.Bluemix_notm}} デプロイメントを指定します。例えば、`BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK` などです。 
    <!-- , or `BMSClient.REGION_SYDNEY`.-->
    
    **注:** `hasUserContext` の値を **true** または **false** に設定します。false (デフォルト値) の場合、各デバイスがアクティブ・ユーザーとしてカウントされます。`hasUserContext` が false の場合、[`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) メソッドは機能しません。true の場合、[`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) を使用するたびにアクティブ・ユーザーとしてカウントされます。`hasUserContext` が true の場合、デフォルトのユーザー ID は存在しないため、アクティブ・ユーザー・グラフにデータを取り込む場合には、ユーザー ID を設定する必要があります。

  #### iOS
  {: #ios-initialize}
  
  1. `BMSCore` フレームワークと `BMSAnalytics` フレームワークをインポートします。
	```
	import BMSCore
    import BMSAnalytics
    ```
	{: codeblock}
    
  2. 使用分析やアプリケーション・セッションを記録するために、[API キー](sdk.html#analytics-clientkey)値を使用して、アプリケーション・コード内でクライアント SDK を初期化します。
 
	Swift:
	
	```Swift
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: DeviceEvent.lifecycle)	
	```
	{: codeblock}
		
	アプリケーション用に選択した名前 (`your_app_name_here`) は、アプリケーション名として {{site.data.keyword.mobileanalytics_short}} コンソールに表示されます。アプリケーション名は、ダッシュボードでアプリケーション・ログを検索する場合にフィルターとして使用されます。複数のプラットフォーム (例えば Android と iOS) で同じアプリケーション名を使用すると、ログの送信元がどのプラットフォームであっても、同じ名前のアプリケーションからのすべてのログを表示できます。
	
	**bluemixRegion** パラメーターは、使用する Bluemix デプロイメントを指定します。例えば、`BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK` などです。
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
	**注:** `hasUserContext` の値を **true** または **false** に設定します。false (デフォルト値) の場合、各デバイスがアクティブ・ユーザーとしてカウントされます。`hasUserContext` が false の場合、[`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) メソッドは機能しません。true の場合、[`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) を使用するたびにアクティブ・ユーザーとしてカウントされます。`hasUserContext` が true の場合、デフォルトのユーザー ID は存在しないため、アクティブ・ユーザー・グラフにデータを取り込む場合には、ユーザー ID を設定する必要があります。

4. 記録した使用分析を Mobile Analytics サービスに送信します。分析のテストは、アプリケーションの開始時に次のコードを実行すると簡単に行えます。

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

	その他の {{site.data.keyword.mobileanalytics_short}} 機能について詳しくは、[アプリケーションの装備](sdk.html)トピックを参照してください。
5. エミュレーターまたはデバイスでアプリケーションをコンパイルして実行します。

6. {{site.data.keyword.mobileanalytics_short}} の**「コンソール」**に移動して、ご使用のアプリケーションの使用分析を表示できます。<!--[creating custom charts](app-monitoring.html#custom-charts),-->[アラートを設定する](app-monitoring.html#alerts)こと、および[アプリの異常終了をモニターする](app-monitoring.html#monitor-app-crash)ことによって、アプリケーションをモニターすることもできます。


# 関連リンク

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API リファレンス
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
