<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# HelloWorld サンプルの開始
{: #gettingstarted-ios}
新規 iOS アプリを開始する場合、HelloWorld アプリを使用できます。このアプリは、認証なしでモバイル・アプリから {{site.data.keyword.Bluemix}} バックエンドに接続する方法を示します。アプリには既に SDK がインストールされています。準備が整ったら、アプリで使用する特定のライブラリーを取得できます。

1. モバイル・バックエンドを {{site.data.keyword.Bluemix_notm}} に作成します。
<ol>
	<li>{{site.data.keyword.Bluemix_notm}} カタログの「ボイラープレート」セクションで、**「MobileFirst Services Starter」**をクリックします。</li>
    <li>アプリの名前とホストを入力し、**「作成」**をクリックします。</li>
    <li>**「完了」**をクリックします。</li>
</ol>
2. プロジェクトを GitHub から取得します。
コンピューターから端末を開いてから、以下のコマンドを入力します。
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. プロジェクトを初期設定します。
SDK を初期設定するには、以下のコードを Application Delegate の `didFinishLaunchingWithOptions` メソッドにコピーします。
   * Objective-C:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. 開発環境でサンプルを実行します。
Xcode で、**「製品」&gt;「実行」**をクリックします。iOS シミュレーターが始動します。
シミュレーターで、**「{{site.data.keyword.Bluemix_notm}} を ping する」**をクリックします。サンプル・アプリが許可ヘッダーを Mobile Client Access サービスから取得します。ping が成功すると、シミュレーターのテキストが更新されます。
<br/>Xcode のモバイル・アプリから {{site.data.keyword.Bluemix_notm}} への接続に成功すると、「おめでとうございます。接続されました。 (Yay! You are connected)」というメッセージが表示されます:<br/>
![Hello World アプリケーションは正常に {{site.data.keyword.Bluemix_notm}} に接続されました](images/yayconnected.jpg "図 1. Hello World アプリケーションは正常に {{site.data.keyword.Bluemix_notm}} に接続されました")
<br/>
接続に成功すると、デバッグ・ログイン Xcode に以下のメッセージが表示されます:
```
You have connected to {{site.data.keyword.Bluemix_notm}} successfully
```
5. 問題があれば解決します。
接続に失敗すると、「残念ながら、問題が発生しました (Bummer Something went wrong)」というメッセージが表示されます。エラーに関する詳細情報が記載されています。<br/>
![Hello World アプリケーションが {{site.data.keyword.Bluemix_notm}} に接続されていません](images/bummer_android.jpg "図 2. Hello World アプリケーションが Bluemix に接続されていません")
<br/>ルートと GUID の値が正しく貼り付けられているか確認します。
   * Objective-C:
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift:
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


詳細については、デバッグ・ログも確認してください。

## 次のステップ:
{: #next}
SDK を入手してそれをモバイル・アプリに統合する方法については、{{site.data.keyword.Bluemix}} サービスのセットアップに関する情報を参照してください。
   * [モバイル・クライアント・アクセス](../../services/mobileaccess/index.html)
   * [プッシュ](../../services/mobilepush/index.html)

# 関連リンク

## サンプル
   * [HelloWorld (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## sdk
   * [bms-clientsdk-ios-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## api
   *
[コア API](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
