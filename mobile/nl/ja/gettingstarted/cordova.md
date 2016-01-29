# HelloWorld サンプル入門
{: #gettingstarted-cordova}

新規 Cordova アプリケーションを始める場合は、HelloWorld というアプリが使用できます。このアプリは、モバイル・アプリから Bluemix バックエンドへ認証を行わずに接続する方法を示す実例となっています。このアプリには既に SDK がインストールされています。準備ができたら、アプリで使用したい特定のライブラリーが取得できます。

1. Bluemix にモバイル・バックエンドを作成します。
<ol>
	<li>Bluemix カタログの「ボイラープレート」セクションで、「MobileFirst Services Starter」をクリックします。</li>
    	<li>アプリの名前とホストを入力して**「作成」**をクリックします。
</li>
    	<li>**「完了」**をクリックします。</li>
</ol>
2. GitHub からプロジェクトを入手します。オプションで、git clone コマンドを使用してプロジェクトを入手することも可能です。ご使用のコンピューターから、ターミナルを開いて次のコマンドを入力します。```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-Cordova-helloworld.git
```
開始する前に、Gradle.zip ファイルをダウンロードし、ダウンロードした圧縮ファイルを任意のディレクトリーに解凍して Gradle をインストールします。初めてサンプルをインポートしたときに、Android Studio によって GRADLE HOME を求められることがあります。そのパスを、解凍した Gradle.zip ファイルに存在する bin ディレクトリーに設定します。build.gradle ファイルは、必要な依存関係を取り込んでプロジェクトを自動的にビルドします。

3. プロジェクトを初期化します。SDK を初期化するために、try ブロック内の BMSClient.getInstance().initialize() 関数の中で、&lt;APPLICATION_ROUTE&gt; と &lt;APPLICATION_ID&gt; をご使用のアプリケーション経路と GUID に置き換えます。
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
4. 開発環境でサンプルを実行します。Android Studio ツールバーから、再生ボタンをクリックしてシミュレーターを選択します。シミュレーターで、**「Bluemix を ping する」**をクリックします。サンプル・アプリは、Bluemix の Node.js ランタイムの保護リソースに Get 要求を送信します。要求が成功した場合は、接続が検証され、シミュレーター内のテキストが更新されます。注: Node.js ランタイム・コードは、MobileFirst Services Starter ボイラープレートで提供されます。バックエンド・アプリケーションが MobileFirst Services Starter ボイラープレートで作成されなかった場合、アプリケーションは正常に接続されません。


![Hello World アプリケーションから Bluemix への接続に成功](images/yayconnected.jpg "図 1. Hello World アプリケーションから Bluemix への接続に成功")

Android Studio のモバイル・アプリから Bluemix への接続に成功すると、「成功! つながりました (Yay! You are connected)」というメッセージが表示されます。
5. 問題点があればすべて解決します。

![Hello World アプリケーションから Bluemix へ接続されない](images/bummer_android.jpg "図 2. Hello World アプリケーションから Bluemix へ接続されない")

接続に失敗すると、「残念 不具合があります (Bummer Something went wrong)」というメッセージが表示されます。エラーの詳細が含まれます。以下の項目を確認してください。

 * 経路値と GUID 値を正しく貼り付けたことを検証してください。

 * デバッグ・ログで詳細を確認することもできます。

## 次のステップ:
{: #next}
SDK の取得方法および SDK とモバイル・アプリの統合方法については、『Android クライアント SDK のセットアップ』を参照してください。
