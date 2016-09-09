---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# iOS 用 Hello Bluemix サンプル入門
{: #gettingstarted-android}
最終更新日: 2016 年 6 月 1 日
{: .last-updated}  

新規 iOS アプリを始める場合は、Hello Bluemix というアプリが使用できます。このアプリは、モバイル・アプリから {{site.data.keyword.Bluemix}} バックエンドへ認証を行わずに接続する方法を示す実例となっています。
準備ができたら、アプリで使用したい特定のライブラリーが取得できます。

1. {{site.data.keyword.Bluemix_notm}} にモバイル・バックエンドを作成します。
    1. {{site.data.keyword.Bluemix_notm}} カタログの「ボイラープレート」セクションで、MobileFirst Services Starter をクリックします。
    2. アプリの名前とホストを入力して**「作成」**をクリックします。

    3. **「完了」**をクリックします。
2. Hello Bluemix サンプル・アプリケーションを実行します。
	1. GitHub からプロジェクトを入手します。オプションで、git clone コマンドを使用してプロジェクトを入手することも可能です。ご使用のコンピューターから、ターミナルを開いて次のコマンドを入力します。
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. プロジェクトが複製された `bms-samples-swift-hellobluemix` ディレクトリー内から `pod install` コマンドを実行します。Cocoapods がインストールされていない場合、[https://cocoapods.org](https://cocoapods.org) から入手してください。
	3. `open HelloBluemix.xcworkspace` コマンドで Xcode ワークスペースを開きます。
	4. `AppDelegate.swift` ファイル内で、appRoute 値および appGuid 値を更新して、前に作成した Bluemix バックエンドから取得した値にします。

3. 開発環境でサンプルを実行します。Xcode で、**「Product」&gt;「Run」**をクリックします。iOS シミュレーターが開始します。

	**重要:** appRoute では `http` ではなく `https` プロトコルを使用する必要があります。そうでない場合、アプリのトランスポート・セキュリティー設定が原因で接続障害が起こる可能性があります。それらの設定について詳しくは、[Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/) ブログ投稿を参照してください。
	
4. シミュレーターで、**「{{site.data.keyword.Bluemix_notm}} を ping する」**をクリックします。サンプル・アプリが、Mobile Client Access サービスから許可ヘッダーを取得します。ping が成功した場合は、シミュレーター内のテキストが更新されます。

  Xcode のモバイル・アプリから {{site.data.keyword.Bluemix_notm}} への接続に成功すると、以下が表示されます。
  `成功! つながりました (Yay! You are connected)`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  接続に失敗すると、以下が表示されます。
  `失敗。問題が発生しました (Bummer. Something went wrong)`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

	以下のようにして、失敗した接続をトラブルシューティングできます。
	* 経路値と GUID 値を正しく貼り付けたことを検証してください。

	* デバッグ・ログで詳細を確認してください。


## 次のステップ:
{: #next}
SDK の取得方法および SDK とモバイル・アプリの統合方法については、Bluemix サービスのセットアップに関する情報を参照してください。
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [プッシュ](../../services/mobilepush/index.html)

# 関連リンク

## サンプル
   * [Hello Bluemix サンプル (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## sdk
   * [コア SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [コア API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
