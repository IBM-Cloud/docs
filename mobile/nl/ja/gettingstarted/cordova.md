<!-- Attribute definitions -->
{:codeblock: .codeblock}

# HelloWorld サンプル入門
{: #gettingstarted-cordova}
*最終更新日: 2016 年 3 月 2 日*

新規 Cordova アプリケーションを始める場合は、HelloWorld というアプリが使用できます。このアプリは、モバイル・アプリから {{site.data.keyword.Bluemix}} 上のモバイル・バックエンドへ認証を行わずに接続する方法を示す実例となっています。
このアプリには既に SDK がインストールされています。準備ができたら、アプリで使用したい特定のライブラリーが取得できます。

1. {{site.data.keyword.Bluemix_notm}} にモバイル・バックエンドを作成します。

	1. {{site.data.keyword.Bluemix_notm}} カタログの「ボイラープレート」セクションで、MobileFirst Services Starter をクリックします。
	1. アプリの名前とホストを入力して**「作成」**をクリックします。

	1. **「完了」**をクリックします。

2. GitHub からプロジェクトを入手します。git clone コマンドを使用してプロジェクトを入手することも可能です。
ご使用のコンピューターから、ターミナルを開いて次のコマンドを入力します。

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. プロジェクト・ディレクトリーから以下のコマンドを実行して、Android および iOS のプラットフォーム環境を追加します。

	Android:

	```Bash
	cordova platform add android
	```

	iOS:

	```Bash
	cordova platform add ios
	```

4. 次のコマンドを使用して Cordova プラグインを追加します。

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Cordova アプリを Android 用、iOS 用、またはその両方用に構成します。

	* **Android**

		Android Studio でプロジェクトを開く前に、ビルド・エラーを回避するために、コマンド・ライン・インターフェース (CLI) から Cordova アプリケーションをビルドして実行します。

		```Bash
		cordova build android
		```

		```Bash
		cordova run android
		```

	* **iOS**

		ビルド・エラーを回避するために Xcode プロジェクトを次のように構成します。

		- 最新バージョンの Xcode を使用して、*&lt;app_name&gt;*/platforms/ios ディレクトリー内の `xcode.proj` ファイルを開きます。

			**重要:** 「最新の Swift 構文に変換する」メッセージを受け取った場合は、**「キャンセル」**をクリックします。

		- **「ビルド設定」>「Swift コンパイラー - コード生成」>「Objective-C ブリッジング・ヘッダー」**へ移動し、次のパスを追加します。

			```
			<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		- **「ビルド設定」>「リンク」>「Runpath 検索パス」**へ移動し、次の Frameworks パラメーターを追加します。

			```
			@executable_path/Frameworks
			```

		- Xcode を使用してアプリケーションをビルドおよび実行します。		
6. HelloWorld サンプルを構成します。

	- プロジェクトを複製したディレクトリーに変更します。
	- *&lt;your_app_dir&gt;*/www/js/index.js ファイルを開き、*&lt;APPLICATION_ROUTE&gt;* と *&lt;APPLICATION_ID&gt;* を Bluemix のアプリケーション ID と経路値で置き換えます。

		**注:** 経路が確実に https プロトコルを使用しているか確認してください。

		```Javascript
		// Bluemix credentials
		route: "<APPLICATION_ROUTE>",
		GUID: "<APPLICATION_GUID>",
		```

7. モバイル・エミュレーターまたはモバイル・デバイスでサンプルを実行します。

	以下のコマンドを使用して Cordova アプリをビルドします。

	```Bash
	cordova build android
	```

	```Bash
	cordova build ios
	```

	以下のコマンドを使用してサンプル・アプリを実行します。

	```Bash
	cordova run android
	```

	```Bash
	cordova run ios
	```

**PING BLUEMIX** ボタンを含む単一ビュー・アプリケーションが表示されます。
このボタンをタップすると、このアプリケーションがクライアントからバックエンド {{site.data.keyword.Bluemix_notm}} アプリケーションへの接続をテストします。
接続テストは、`index.js` ファイルで指定したアプリケーション経路を使用して行われます。


![Hello World アプリケーションから Bluemix への接続に成功](images/yayconnected.jpg "図 1. Hello World アプリケーションから Bluemix への接続に成功")


モバイル・アプリから {{site.data.keyword.Bluemix_notm}} への接続に成功すると、「成功! つながりました (Yay! You are connected)」というメッセージが表示されます。


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

接続に失敗すると、エラー・メッセージが表示されます。
エラーの詳細がメッセージに含まれています。
以下の項目をチェックしてエラーをトラブルシューティングすることができます。

- 経路値と GUID 値を正しく貼り付けたことを検証してください。

- Xcode または Android デバッグ・ログを表示します。
- {{site.data.keyword.Bluemix_notm}} でアプリの状況を調べます。

## 次のステップ:
{: #next}
SDK を取得して SDK をモバイル・アプリに統合する方法については、以下を参照してください。
* [Mobile Client Access: Cordova プラグインのセットアップ](../services/mobileaccess/getting-started-cordova.html)
* [プッシュ通知: Cordova プラグインのセットアップ](../mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# 関連リンク

## サンプル
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
