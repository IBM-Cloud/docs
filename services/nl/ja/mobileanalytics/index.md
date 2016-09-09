---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} (体験版) の開始  

{: #gettingstartedtemplate}
*最終更新日時: 2016 年 8 月 1 日*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} サービスを使用して、状態、動作、モバイル・アプリのコンテキスト、モバイル・ユーザー、モバイル・デバイスを測定します。
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} サービスを素早く稼働させるためには、次のステップに従います。

1. {{site.data.keyword.mobileanalytics_short}} サービスの [ インスタンスを作成](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)した後、{{site.data.keyword.Bluemix}} の「ダッシュボード」の「サービス」セクション内のタイルをクリックして、{{site.data.keyword.mobileanalytics_short}} コンソールにアクセスできます。

  **重要:** 新たに作成された Mobile Analytics サービスを最初に開く際に、ウィンドウが表示されて、サービスが ID を検証できるよう自分自身に関する必要な情報をサービスに {{site.data.keyword.Bluemix_notm}} が提供できるようにすることの確認が行われる場合があります。**「確認」**をクリックすると、続いて {{site.data.keyword.mobileanalytics_short}} コンソールが表示されます。キャンセルする場合、{{site.data.keyword.mobileanalytics_short}} コンソールは開きません。
2. {{site.data.keyword.mobileanalytics_short}} [クライアント SDK](install-client-sdk.html) をインストールします。
3. クライアント SDK をインポートし、次のコード・スニペットで初期設定して、使用分析を記録します。
  #### Android
  {: #android-initialize}
  1. Client SDK をインポートします。
		
		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```

  2. [アクセス・キー](sdk.html#analytics-clientkey)値を取得します。
  3. アプリケーション・コード内のクライアント SDK を初期化して使用分析やアプリケーション・セッションを記録します。
		
		```Java
		try {
		        BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
		    } catch (MalformedURLException e) {
		        Log.e("your_app_name","URL should not be malformed:  " + e.getLocalizedMessage());
		    }
		   Analytics.init(getApplication(), "your_app_name", "your_access_key", Analytics.DeviceEvent.LIFECYCLE);
		```
**bluemixRegion** パラメーターは、使用している Bluemix デプロイメントを指定します。例えば、`BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK`、あるいは `BMSClient.REGION_SYDNEY` などです。

  #### iOS
  {: #ios-initialize}
  1. `BMSCore` フレームワークと `BMSAnalytics` フレームワークをインポートします。

    ```
import BMSCore
    import BMSAnalytics
    ```

  2. [アクセス・キー](sdk.html#analytics-clientkey)値を取得します。

  3. アプリケーション・コード内のクライアント SDK を初期化して使用分析やアプリケーション・セッションを記録します。
	
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute("nil",bluemixAppGUID: "nil", bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName("your_app_name", accessKey: "your_access_key", deviceEvents: DeviceEvent.LIFECYCLE)
	```

    **bluemixRegion** パラメーターは、使用している Bluemix デプロイメントを指定します。例えば、`BMSClient.REGION_US_SOUTH` や `BMSClient.REGION_UK`、あるいは `BMSClient.REGION_SYDNEY` などです。

4. 記録した使用分析を Mobile Analytics サービスに送信します。分析のテストは、アプリケーションの開始時に次のコードを実行すると簡単に行えます。

	#### Android
	{: #android-send}
	
	`Analytics.send()` メソッドを、Android アプリケーションのメイン・アクティビティーの `onCreate` メソッド内か、プロジェクトで最も適切な場所に追加します。
	
	```
	Analytics.send(new ResponseListener() {
	    @Override
	    public void onSuccess(Response response) {
	        Log.d("your_app_name", "Successfully sent analytics: " + response.toString());
	    }
		
	    @Override
	    public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
	        Log.e("your_app_name", "Failed to send analytics: ");
	        if (response != null) {
	            Log.e("your_app_name", response.toString());
	        }
	        if (throwable != null) {
	            Log.e("your_app_name","Stack trace: ", throwable);
	        }
	    }
	});
	```
	
	#### iOS
	{: #ios-send}
	
	
	`Analytics.send` メソッドを使用して、分析データをサーバーに送信します。`Analytics.send` メソッドを、アプリケーション・デリゲートの `application(_:didFinishLaunchingWithOptions:)` メソッド内か、プロジェクトで最も適切な場所に置きます。 
		
	```
	Analytics.send { (response: Response?, error: NSError?) in
	  if response?.statusCode == 201 {
	      print("Successfully sent analytics: \(response?.responseText)")
	  }
	  else {
	      print("Failed to send analytics: \(response?.responseText). Error: \(error?.localizedDescription)")
	  }
	}
	```
[アプリケーションの装備](sdk.html)トピックを参照してください。
5. エミュレーターまたはデバイスでアプリケーションをコンパイルして実行します。

6. {{site.data.keyword.mobileanalytics_short}} の**「ダッシュボード」**に移動して、使用分析を表示します。例えば、アプリケーションを使用する新規デバイスやデバイスの総数などです。<!-- [creating custom charts](app-monitoring.html#custom-charts), --> [アラートを設定する](app-monitoring.html#alerts)こと、および[アプリの異常終了をモニターする](app-monitoring.html#monitor-app-crash)ことによって、アプリをモニターすることもできます。 


# 関連リンク

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
