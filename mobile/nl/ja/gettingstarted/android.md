---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Android 用 Hello Bluemix サンプル入門
{: #gettingstarted-android}
*最終更新日: 2016 年 5 月 27 日*
{: .last-updated}  

新規 Android アプリケーションを始める場合は、HelloWorld というアプリが使用できます。このアプリは、モバイル・アプリから {{site.data.keyword.Bluemix}} バックエンドへ認証を行わずに接続する方法を示す実例となっています。
このアプリには既に SDK がインストールされています。準備ができたら、アプリで使用したい特定のライブラリーが取得できます。

1. {{site.data.keyword.Bluemix_notm}} にモバイル・バックエンドを作成します。
    1. {{site.data.keyword.Bluemix_notm}} カタログの「ボイラープレート」セクションで、MobileFirst Services Starter をクリックします。
    2. アプリの名前とホストを入力して**「作成」**をクリックします。

    3. **「完了」**をクリックします。
2. GitHub からプロジェクトを入手します。オプションで、git clone コマンドを使用してプロジェクトを入手することも可能です。ご使用のコンピューターから、ターミナルを開いて次のコマンドを入力します。```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git```

3. `try` ブロック内の `BMSClient.getInstance().initialize()` 関数内で、&lt;APPLICATION_ROUTE&gt; と &lt;APPLICATION_ID&gt; をご使用のアプリケーション経路と GUID に置き換えることで、プロジェクトを初期化します。
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
4. 開発環境でサンプルを実行します。Android Studio ツールバーから、**「Play」**ボタンをクリックしてシミュレーターを選択します。
5. シミュレーターで、**「{{site.data.keyword.Bluemix_notm}} を ping する」**をクリックします。サンプル・アプリは、{{site.data.keyword.Bluemix_notm}} の `Node.js` ランタイムに Get 要求を送信します。要求が成功した場合は、接続が検証され、シミュレーター内のテキストが更新されます。

  **注:** `Node.js` ランタイム・コードは、MobileFirst Services Starter ボイラープレートで提供されます。バックエンド・アプリケーションが MobileFirst Services Starter ボイラープレートで作成されなかった場合、アプリケーションは正常に接続されません。

  Android Studio のモバイル・アプリから {{site.data.keyword.Bluemix_notm}} への接続に成功すると、以下のメッセージが表示されます。

  `成功! つながりました (Yay! You are connected)`
  {: screen}

  ![Hello World アプリケーションから {{site.data.keyword.Bluemix_notm}} への接続に成功](images/yayconnected.jpg "図 1. Hello World アプリケーションから Bluemix への接続に成功")

  接続に失敗すると、以下が表示されます。
  `失敗。問題が発生しました (Bummer. Something went wrong)`
  {: screen}

  ![Hello World アプリケーションから Bluemix へ接続されない](images/bummer_android.jpg "図 2. Hello World アプリケーションから Bluemix へ接続されない")

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
   * [Hello Bluemix サンプル](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [コア SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [コア API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
