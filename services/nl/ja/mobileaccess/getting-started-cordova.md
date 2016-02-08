# Cordova プラグインのセットアップ
{: #getting-started-cordova}

Cordova アプリケーションに {{site.data.keyword.amashort}} Client SDK を装備し、SDK を初期化し、保護されたリソースまたは無保護のリソースへの要求を実行します。

## 開始する前に
{: #before-you-begin}
* {{site.data.keyword.amashort}} サービスによって保護されたモバイル・バックエンドのインスタンスが存在している必要があります。モバイル・バックエンドの作成方法について詳しくは、[入門](getting-started.html)を参照してください。
* Cordova アプリケーションを作成するか、既存のプロジェクトを使用します。Cordova アプリケーションのセットアップ方法について詳しくは、[Cordova の Web サイト](https://cordova.apache.org/)を参照してください。


## {{site.data.keyword.amashort}} Cordova プラグインのインストール
{: #getting-started-cordova-plugin}

{{site.data.keyword.amashort}} Client SDK for Cordova は、ネイティブ {{site.data.keyword.amashort}} Client SDK をラップしている Cordova プラグインです。これは、Cordova コマンド・ライン・インターフェース (CLI) と、Cordova プロジェクト用のプラグイン・リポジトリーである `npmjs` を使用して配布されます。Cordova CLI は自動的にリポジトリーからプラグインをダウンロードし、Cordova アプリケーションで使用できるようにします。


1. iOS プラットフォームと Android プラットフォームを Cordova アプリケーションに追加します。以下のコマンドのいずれかまたは両方をコマンド・ラインから実行します。

	```Bash
	cordova platform add ios
	```
```Bash
	cordova platform add android
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

1. 次のコマンドを実行して、プラグインが正常にインストールされたことを確認します。
    ```Bash
     cordova plugin list
		 ```

## {{site.data.keyword.amashort}} Client プラグインの初期化
{: #getting-started-cordova-initialize}

{{site.data.keyword.amashort}} Client SDK を使用するには、*applicationGUID* パラメーターと *applicationRoute* パラメーターを渡してこの SDK を初期化する必要があります。

1. 経路およびアプリ GUID の値は、{{site.data.keyword.Bluemix_notm}} ダッシュボードのメインページにあります。アプリ名をクリックし、次に**「モバイル・オプション」**をクリックして、SDK を初期化するための**「アプリケーション経路 (Application route)」**と**「アプリケーション GUID (Application GUID)」**の値を表示します。

3. 以下の呼び出しを `index.js` ファイルに追加して、{{site.data.keyword.amashort}} Client SDK を初期化します。<br/>*applicationRoute* および *applicationGUID* は、{{site.data.keyword.Bluemix_notm}} ダッシュボード内の**「モバイル・オプション」**の値に置換します。


	```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```



## モバイル・バックエンドへの要求の実行
{: #getting-started-request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンドに要求を出すことができるようになります。

1. 新しいモバイル・バックエンドの、保護されたエンドポイントに要求を送信してみてください。ブラウザーで次の URL を開きます。 `http://{appRoute}/protected` 例えば、次のようになります。
```
http://my-mobile-backend.mybluemix.net/protected
```
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}}で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、このメッセージが返されます。
1. Cordova アプリケーションを使用して、同じエンドポイントに要求を実行します。`BMSClient` を初期化した後に、以下のコードを追加してください。

	```JavaScript
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
