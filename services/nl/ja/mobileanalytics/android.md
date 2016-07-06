<!-- Attribute definitions -->
{:codeblock: .codeblock}

# HelloWorld サンプルの開始
{: #gettingstarted-android}

新規 Android アプリケーションを開始する場合、HelloWorld アプリを使用できます。このアプリは、認証なしでモバイル・アプリから {{site.data.keyword.Bluemix}} バックエンドに接続する方法を示します。アプリには既に SDK がインストールされています。準備が整ったら、アプリで使用する特定のライブラリーを取得できます。

1. モバイル・バックエンドを {{site.data.keyword.Bluemix_notm}} に作成します。
    1. {{site.data.keyword.Bluemix_notm}} カタログの「ボイラープレート」セクションで、「MobileFirst Services Starter」をクリックします。
    2. アプリの名前とホストを入力し、**「作成」**をクリックします。
    3. **「完了」**をクリックします。
2. プロジェクトを GitHub から取得します。オプションで、git clone コマンドを使用してプロジェクトを取得することもできます。コンピューターから端末を開き、以下のコマンドを入力します。
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
```
{: codeblock}

開始する前に、`Gradle.zip` ファイルをダウンロードし、ダウンロードした圧縮ファイルを選択したディレクトリーに解凍して Gradle をインストールしておきます。サンプルの初回インポート時には、Android Studio によって GRADLE HOME を尋ねられる可能性があります。抽出した `Gradle.zip` ファイルにある `bin` ディレクトリーにパスを設定します。`build.gradle` ファイルは、必要な依存関係を取り込んでプロジェクトを自動的にビルドします。
3. `BMSClient.getInstance().initialize()` 関数内の try ブロックの &lt;APPLICATION_ROUTE&gt; と &lt;APPLICATION_ID&gt; をアプリケーション・ルートと GUID で置き換えて、プロジェクトを初期設定します。
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
{: codeblock}

4. 開発環境でサンプルを実行します。
Android Studio ツールバーから、**「再生」**ボタンをクリックし、シミュレーターを選択します。

  シミュレーターで**「{{site.data.keyword.Bluemix_notm}} を ping する」**をクリックします。サンプル・アプリは、{{site.data.keyword.Bluemix_notm}} の `Node.js` ランタイムで、Get 要求を保護リソースに送信します。要求に成功すると、接続が確認され、シミュレーターのテキストが更新されます。

  **注:** `Node.js` ランタイム・コードが「MobileFirst Services Starter」ボイラープレートに提供されます。バックエンド・アプリケーションが「MobileFirst Services Starter」ボイラープレートに作成されなかった場合、アプリケーションは正常に接続されません。

  Android Studio のモバイル・アプリから {{site.data.keyword.Bluemix_notm}} への接続に成功すると、
「おめでとうございます。接続されました。(Yay! You are connected)」
というメッセージが表示されます。{: screen}

  ![Hello World アプリケーションは正常に {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "図 1. Hello World アプリケーションは正常に Bluemix に接続されました") に接続されました

  接続が失敗すると、
「残念ながら、問題が発生しました (Bummer. Something went wrong)」
というメッセージが表示されます。{: screen}

  ![Hello World アプリケーションは、Bluemix に接続されていません](images/bummer_android.jpg "図 2. Hello World アプリケーションは Bluemix に接続されていません")

  接続に失敗した場合、次のようにトラブルシューティングできます。
   * ルートと GUID の値が正しく貼り付けられているか確認します。
   * 詳細については、デバッグ・ログを確認してください。

## 次のステップ:
{: #next}
SDK を取得してそれをモバイル・アプリに統合する方法については、Bluemix サービスのセットアップに関する情報を参照してください。
   * [モバイル・クライアント・アクセス](../../services/mobileaccess/index.html)
   * [プッシュ](../../services/mobilepush/index.html)

# 関連リンク

## サンプル
   * [HelloWorld (Android)](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [bms-clientsdk-android-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [コア API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
