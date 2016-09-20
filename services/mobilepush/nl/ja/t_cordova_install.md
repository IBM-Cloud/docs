---

copyright:
 years: 2015, 2016

---

# Cordova の Push プラグインのインストール
{: #cordova_install}

Cordova アプリケーションをさらに開発するために、クライアントの Push プラグインをインストールして使用します。これにより、Cordova Core のプラグインもインストールされます。これは、Bluemix への接続を初期化するものです。


### 始めに

1. 最新バージョンの Android Studio SDK と Xcode をダウンロードします。
1. エミュレーターをセットアップします。Android Studio では、Google Play API をサポートするエミュレーターを使用します。
1. Git のコマンド・ライン・ツールをインストールします。Windows では、必ず **「Windows コマンド・プロンプトから Git を実行する (Run Git from the Window Command Prompt)」**オプションを選択してください。このツールのダウンロードとインストールの方法については、[Git](https://git-scm.com/downloads) を参照してください。

1. Node.js と Node Package Manager (NPM) ツールをインストールします。NPM コマンド・ライン・ツールは Node.js とバンドルされています。Node.js のダウンロードとインストールの方法については、[Node.js](https://nodejs.org/en/download/) を参照してください。
1. コマンド・ラインから、**npm install -g cordova** コマンドを使用して、Cordova コマンド・ライン・ツールをインストールします。これは、Cordova の Push プラグインを使用するために必要です。
Cordova のインストールと Cordova アプリのセットアップの方法については、[Cordova Apache](https://cordova.apache.org/#getstarted) を参照してください。

	**注**: Cordova の Push プラグインの readme ファイルを確認する場合は、[https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push) にアクセスしてください。


## Cordova の Push プラグインのインストール
1. Cordova アプリを作成するフォルダーに移動し、次のコマンドを実行して Cordova アプリケーションを作成します。
既存の Cordova アプリがある場合は、ステップ 3 に進みます。



	cordova create your_app_name
	cd your_app_name
	```
1. オプション: (オプション) **config.xml** ファイルを編集し、<name> エレメント内のアプリケーション名を、デフォルトの HelloCordova という名前ではなく、自分で選択した名前に変更します。

	**注**: 正しいバンドル ID を指定してください。正しいバンドル ID を指定しないと、Xcode に次のエラー・メッセージが表示されます。
	* 実行可能ファイルの署名に使用された資格が無効です (The executable was signed with invalid entitlements.) 
	* アプリケーションのコード署名資格ファイルに指定された資格が、プロビジョニング・プロファイルに指定された資格と一致しません (The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile.)

	この問題を修正するには、Xcode または Cordova アプリ **config.xml** ファイルに正しいバンドル ID を指定します。

1. サポートされる最低レベルの API またはデプロイメント・ターゲット (Deployment Target) の宣言を、Cordova アプリケーションの config.xml ファイルに追加します。minSdkVersion の値は、15 より高くなければなりません。targetSdkVersion の値は、常に、Google から入手可能な最新の Android SDK を反映している必要があります。
	* **Android** - ご使用のエディターで config.xml ファイルを開き、```<platform name="android">``` エレメントを最低レベルのターゲット SDK バージョンに更新します。

	```
	<!-- add deployment target declaration -->
	<platform name="android">    
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - <platform name="ios"> エレメントを、デプロイメント・ターゲット (Deployment Target) の宣言で更新します。

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Cordova コマンド・ライン・インターフェース (CLI) から、以下のコマンドを使用して、プラットフォーム (iOS、Android、またはその両方) を追加します。

	```
	cordova platform add ios
	cordova platform add android
	```
1. Cordova アプリケーションのルート・ディレクトリーで、以下のコマンドを入力して Cordova の Push プラグイン **cordova plugin add ibm-mfp-push** をインストールします。

	追加したプラットフォームに応じて、以下のような内容が表示されます。


	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. *your-app-root-folder* から、コマンド **cordova plugin list** を使用して、Cordova の Core および Push のプラグインが正常にインストールされたことを確認します。

	追加したプラットフォームに応じて、以下のような内容が表示されます。


	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (iOS のみ) - iOS 開発環境を構成します。a. Xcode を使用して、*your-app-name***/platforms/ios** ディレクトリーにある your-app-name.xcodeproj ファイルを開きます。

	b. ブリッジング・ヘッダーを追加します。**「ビルド設定」>「Swift コンパイラー - コード生成」>「 Objective-C ブリッジング・ヘッダー」**に移動し、パス *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h** を追加します。

	c. Frameworks パラメーターを追加します。**「ビルド設定」>「 リンク」>「実行パス検索パス (Runpath Search Paths)」**に移動し、以下のパラメーターを追加します。```
	@executable_path/Frameworks
	```
	d. ブリッジング・ヘッダーの以下の Push インポート・ステートメントをアンコメントします。 *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h** に移動します。

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Xcode で、アプリケーションをビルドして実行します。
1. (Android のみ)- コマンド **cordova build android** を使用して、Android プロジェクトをビルドします。

	**注**: Android Studio でプロジェクトを開く前に、最初に Cordova CLI を使用して Cordova アプリケーションをビルドする必要があります。そうしないと、ビルド・エラーが発生します。

1. 次のステップ。[Cordova プラグインの初期化](t_cordova_initalize.html)を行います。

