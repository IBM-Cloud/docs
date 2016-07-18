---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# iOS 用 Hello Bluemix サンプル入門
{: #gettingstarted-android}
*最終更新日: 2016 年 6 月 1 日*
{: .last-updated}  

新規 iOS アプリを始める場合は、HelloWorld というアプリが使用できます。このアプリは、モバイル・アプリから {{site.data.keyword.Bluemix}} バックエンドへ認証を行わずに接続する方法を示す実例となっています。
このアプリには既に SDK がインストールされています。準備ができたら、アプリで使用したい特定のライブラリーが取得できます。

1. {{site.data.keyword.Bluemix_notm}} にモバイル・バックエンドを作成します。
    1. {{site.data.keyword.Bluemix_notm}} カタログの「ボイラープレート」セクションで、MobileFirst Services Starter をクリックします。
    2. アプリの名前とホストを入力して**「作成」**をクリックします。

    3. **「完了」**をクリックします。
2. GitHub からプロジェクトを入手します。オプションで、git clone コマンドを使用してプロジェクトを入手することも可能です。ご使用のコンピューターから、ターミナルを開いて次のコマンドを入力します。```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld.git
    ```

3. プロジェクトを初期化します。SDK を初期化するために、以下のコードを Application Delegate の `didFinishLaunchingWithOptions` メソッドにコピーします。

	###Ojbective-C
	{: initializeobjc}

	**重要**: Objective-C SDK は引き続きフルにサポートされており、{{site.data.keyword.Bluemix}} モバイル・サービスのプライマリー SDK とまだ見なされていますが、新しい Swift SDK のほうを支持して、Objective-C SDK は年内に廃止されることが計画されています。

	Objective-C SDK は、モニター・データを {{site.data.keyword.amashort}} サービスのモニター・コンソールに報告します。{{site.data.keyword.amashort}} サービスのモニター機能に依存している場合は、引き続き Objective-C SDK を使用してください。

	```
	// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```

	###Swift
	{: initializeswift}
	```
	// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```

4. 開発環境でサンプルを実行します。Xcode で、**「Product」&gt;「Run」**をクリックします。iOS シミュレーターが開始します。
5. シミュレーターで、**「{{site.data.keyword.Bluemix_notm}} を ping する」**をクリックします。サンプル・アプリが、Mobile Client Access サービスから許可ヘッダーを取得します。ping が成功した場合は、シミュレーター内のテキストが更新されます。

  Xcode のモバイル・アプリから {{site.data.keyword.Bluemix_notm}} への接続に成功すると、以下のメッセージが表示されます。

  `成功! つながりました (Yay! You are connected)`
  {: screen}

  ![Hello World アプリケーションから {{site.data.keyword.Bluemix_notm}} への接続に成功](images/yayconnected.jpg "図 1. Hello World アプリケーションから Bluemix への接続に成功")

  接続に失敗すると、以下が表示されます。
  `失敗。問題が発生しました (Bummer. Something went wrong)`
  {: screen}

  ![Hello World アプリケーションから Bluemix へ接続されない](images/bummer_android.jpg "図 2. Hello World アプリケーションから Bluemix へ接続されない")

	以下のようにして、失敗した接続をトラブルシューティングできます。
	* 経路値と GUID 値を正しく貼り付けたことを検証してください。

		####Objective-C
		{: #objcvals}
		```
		[imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ```

		####Swift
		{: #swiftvals}
		```
		IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")```

	* デバッグ・ログで詳細を確認してください。


## 次のステップ:
{: #next}
SDK の取得方法および SDK とモバイル・アプリの統合方法については、Bluemix サービスのセットアップに関する情報を参照してください。
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [プッシュ](../../services/mobilepush/index.html)

# 関連リンク

## サンプル
   * [Hello Bluemix サンプル](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [コア SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [コア API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
