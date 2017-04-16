---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}

# Cordova プラグインの初期化
{: #cordova_enable}

Push Notification Service の Cordova プラグインを使用するには、事前に、アプリケーション経路とアプリケーション GUID を受け渡すことでプラグインを初期化しておく必要があります。
プラグインを初期化したら、Bluemix ダッシュボードで作成したサーバー・アプリに接続することができます。Cordova プラグインは、Cordova アプリが Bluemix サービスと通信できるようにするための Android および iOS のクライアント SDK のラッパーです。

1. 以下のコード・スニペットをメイン JavaScript ファイル (通常、**www/js** ディレクトリーの下にある) にコピー・アンド・ペーストして、BMSClient を初期化します。

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");```
1. Bluemix の Route パラメーターと appGUID パラメーターを使用するように、コード・スニペットを変更します。Bluemix アプリケーション・ダッシュボード内の**「モバイル・オプション」**リンクをクリックして、アプリケーション経路とアプリ GUID を取得します。この経路とアプリ GUID の値を `BMSClient.initialize` コード・スニペットのパラメーターとして使用します。


	**注**: Cordova CLI (例えば、Cordova の create app-name コマンド) を使用して Cordova アプリを作成した場合、この Javascript コードを **index.js** ファイルの `onDeviceReady: function()` 関数内の `app.receivedEvent` 関数の後に置いて BMS クライアントを初期化します。

	```
	onDeviceReady: function() {app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. 次のステップ。[デバイスの登録](t_cordova_register.html)を行います。
