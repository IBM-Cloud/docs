<!-- Attribute definitions -->
{:codeblock: .codeblock}

# HelloWorld サンプルの開始
{: #gettingstarted-cordova}

新規 Cordova アプリケーションを開始する場合、HelloWorld アプリを使用できます。このアプリは、認証なしでモバイル・アプリから Bluemix バックエンドに接続する方法を示します。アプリには既に SDK がインストールされています。準備が整ったら、アプリで使用する特定のライブラリーを取得できます。

1. モバイル・バックエンドを Bluemix に作成します。
<ol>
	<li>Bluemix カタログの「ボイラープレート」セクションで、「MobileFirst Services Starter」をクリックします。</li>
    	<li>アプリの名前とホストを入力し、**「作成」**をクリックします。</li>
    	<li>**「完了」**をクリックします。</li>
</ol>
2. プロジェクトを GitHub から取得します。オプションで、git clone コマンドを使用してプロジェクトを取得することもできます。コンピューターから端末を開き、以下のコマンドを入力します。
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. プロジェクト・ディレクトリーから以下のコマンドを実行して、Android プラットフォーム環境と iOS プラットフォーム環境を追加します。

Android:
```
cordova platform add android
```

iOS:
```
cordova platform add ios
```

4. 以下のコマンドを使用して Cordova プラグインを追加します。
```
cordova plugin add ibm-mfp-core
```

5. Android、iOS、またはその両方に対して Cordova アプリを構成します。

 * Android

	 Android Studio でプロジェクトを開く前に、コマンド・ライン・インターフェース (CLI) で Cordova アプリケーションをビルドおよび実行し、ビルド・エラーを回避します。

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 Xcode プロジェクトを以下のように構成し、ビルド・エラーを回避します。

	    1. 最新バージョンの Xcode を使用して、&lt;app_name&gt;/platforms/ios ディレクトリーの xcode.proj ファイルを開きます。

			**重要:**「最新の Swift 構文に変換」するメッセージを受け取ったら、「キャンセル」をクリックします。

		2. **「ビルド設定 (Build Settings)」>「Swift コンパイラー - コード生成 (Swift Compiler - Code Generation)」>「Objective-C ブリッジング・ヘッダー (Objective-C Bridging Header)」**と移動し、以下のパスを追加します。

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```
		3. **「ビルド設定 (Build settings)」>「リンク (Linking)」>「実行パスの検索パス (Runpath Search Paths)」**と移動し、以下の Frameworks パラメーターを追加します。

		```
		@executable_path/Frameworks
		```
		4. アプリケーションを Xcode でビルドおよび実行します。

6. HelloWorld サンプルの構成
<ol>
	<li>プロジェクトを複製したディレクトリーに移動します。</li>
	<li>&lt;your_app_dir&gt;/www/js/index.js ファイルを開き、&lt;APPLICATION_ROUTE&gt; と &lt;APPLICATION_ID&gt; を、Bluemix アプリケーション ID とルート値で置き換えます。</li>
</ol>

注: &lt;APPLICATION_ROUTE&gt; が安全のために https プロトコルを使用していることを確認します。

```
// Bluemix credentials
route: "<APPLICATION_ROUTE>",
GUID: "<APPLICATION_GUID>",
```

7. モバイル・エミュレーターまたはデバイスでサンプルを実行します。

   以下のコマンドを使用して Cordova アプリをビルドします。
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   以下のコマンドを使ってサンプル・アプリを実行します。
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


**PING BLUEMIX** ボタンを持つ単一ビューのアプリケーションが表示されます。ボタンをタップすると、アプリケーションは、クライアントからバックエンド Bluemix アプリケーションへの接続をテストします。接続は、index.js ファイルで指定するアプリケーション・ルートを使用してテストされます。


![Hello World アプリケーションは正常に Bluemix に接続されました](images/yayconnected.jpg "図 1. Hello World アプリケーションは正常に Bluemix に接続されました")

モバイル・アプリから Bluemix への接続に成功すると、「おめでとうございます。接続されました。(Yay! You are connected)」というメッセージが表示されます。
8. 問題があれば解決します。

<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

接続が失敗すると、「残念ながら、問題が発生しました (Bummer Something went wrong)」というメッセージが表示されます。エラーに関する詳細が含まれています。
以下の項目を確認してください。
 * ルートと GUID の値が正しく貼り付けられているか確認します。
 * Xcode または Android デバッグ・ログを表示します。
 * Bluemix のアプリの状況を確認します。

## 次のステップ:
{: #next}
SDK を取得してそれをモバイル・アプリに統合する方法については、「Cordova クライアント SDK のセットアップ」を参照してください。

# 関連リンク

## サンプル
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
