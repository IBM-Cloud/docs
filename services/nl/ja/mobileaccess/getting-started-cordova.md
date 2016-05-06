---

copyright:
  years: 2015, 2016
  
---

# Cordova プラグインのセットアップ
{: #getting-started-cordova}

Cordova アプリケーションに {{site.data.keyword.amashort}} Client SDK を装備し、SDK を初期化し、保護されたリソースまたは無保護のリソースへの要求を実行します。

## 開始する前に
{: #before-you-begin}

- {{site.data.keyword.amashort}} サービスによって保護されたモバイル・バックエンドのインスタンスが存在している必要があります。モバイル・バックエンドの作成方法について詳しくは、[入門](getting-started.html)を参照してください。

- Cordova アプリケーションを作成するか、既存のプロジェクトを使用します。Cordova アプリケーションのセットアップ方法について詳しくは、[Cordova の Web サイト](https://cordova.apache.org/)を参照してください。

## {{site.data.keyword.amashort}} Cordova プラグインのインストール
{: #getting-started-cordova-plugin}

{{site.data.keyword.amashort}} Client SDK for Cordova は、ネイティブ {{site.data.keyword.amashort}} Client SDK をラップしている Cordova プラグインです。これは、Cordova コマンド・ライン・インターフェース (CLI) と、Cordova プロジェクト用のプラグイン・リポジトリーである `npmjs` を使用して配布されます。Cordova CLI は自動的にリポジトリーからプラグインをダウンロードし、Cordova アプリケーションで使用できるようにします。

1. Android プラットフォームおよび iOS プラットフォームを Cordova アプリケーションに追加します。以下のコマンドのいずれかまたは両方をコマンド・ラインから実行します。

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. Android プラットフォームを追加した場合は、Cordova アプリケーションの `config.xml` ファイルに、サポートされる最小 API レベルを追加する必要があります。`config.xml` ファイルを開き、以下の行を `<platform name="android">` エレメントに追加します。

	```XML
	<platform name="android">    
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	*minSdkVersion* の値は、`15` より大でなければなりません。*targetSdkVersion* の値は、Google から入手可能な最新の Android SDK でなければなりません。



1. iOS オペレーティング・システムを追加した場合は、以下のように、ターゲット宣言で `<platform name="ios">` エレメントを更新してください。

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
	</platform>
	```

1. 以下のようにして、{{site.data.keyword.amashort}} Cordova プラグインをインストールします。

 	```Bash
	cordova plugin add ibm-mfp-core```

1. Android、iOS、またはその両方に対応するようにプラットフォームを構成します。

	* **Android**

		Android Studio でプロジェクトを開く前に、コマンド・ライン・インターフェース (CLI) を通じて Cordova アプリケーションをビルドして、ビルド・エラーを回避します。

		```
		cordova build android
		```

	* **iOS**

		Xcode プロジェクトを以下のように構成して、ビルド・エラーを回避します。

		1. 最新バージョンの Xcode を使用して、&lt;*app_name*&gt;/platforms/ios ディレクトリー内の xcode.proj ファイルを開きます。

		**重要:** 「最新の Swift 構文に変換 (Convert to Latest Swift Syntax)」するようにというメッセージが表示されたら、「キャンセル」をクリックします。

		2. **「ビルド設定 (Build Settings)」>「Swift コンパイラー - コード生成 (Swift Compiler - Code Generation)」>「Objective-C ブリッジング・ヘッダー (Objective-C Bridging Header)」**に移動し、以下のパスを追加します。

			```
			<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. **「ビルド設定 (Build Settings)」>「リンク (Linking)」>「実行パスの検索パス (Runpath Search Paths)」**に移動し、以下の Frameworks パラメーターを追加します。

			```
			@executable_path/Frameworks
			```

		4. Xcode で、アプリケーションをビルドして実行します。

1. 次のコマンドを実行して、プラグインが正常にインストールされたことを確認します。
    

	```Bash
	cordova plugin list
	```

## {{site.data.keyword.amashort}} Client プラグインの初期化
{: #getting-started-cordova-initialize}

{{site.data.keyword.amashort}} Client SDK を使用するには、*applicationGUID* パラメーターと *applicationRoute* パラメーターを渡してこの SDK を初期化する必要があります。

1. 経路およびアプリ GUID の値は、{{site.data.keyword.Bluemix_notm}} ダッシュボードのメインページにあります。アプリ名をクリックし、次に**「モバイル・オプション」**をクリックして、SDK を初期化するための**「アプリケーション経路 (Application route)」**と**「アプリケーション GUID (Application GUID)」**の値を表示します。

3. 以下の呼び出しを `index.js` ファイルに追加して、{{site.data.keyword.amashort}} Client SDK を初期化します。
*applicationRoute* および *applicationGUID* は、{{site.data.keyword.Bluemix_notm}} ダッシュボード内の**「モバイル・オプション」**の値に置き換えます。

	```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

## モバイル・バックエンドへの要求の実行
{: #getting-started-request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンドに要求を出すことができるようになります。

1. 新しいモバイル・バックエンドの、保護されたエンドポイントに要求を送信してみてください。ブラウザーで次の URL を開きます。`{applicationRoute}/protected` 以下に例を示します。

	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、このメッセージが返されます。


1. Cordova アプリケーションを使用して、同じエンドポイントに要求を実行します。`BMSClient` を初期化した後に、以下のコードを追加してください。

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
		console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);```

1. 要求が正常に実行されると、LogCat コンソールまたは Xcode コンソール (使用しているプラットフォームによって決まる) に以下の出力が表示されます。

	![image](images/getting-started-android-success.png)

	## 次のステップ
	{: #next-steps}

	保護されているエンドポイントに繋がった場合、資格情報は必要とされません。アプリケーションにユーザーのログインを要求する場合、Facebook、Google またはカスタム認証を構成する必要があります。
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [カスタム](custom-auth-cordova.html)
