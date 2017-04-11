---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cordova アプリでの MQA の装備 (非推奨)
{: #instrumentcord}

Cordova アプリで {{site.data.keyword.mqafull}} を使用するには、SDK をダウンロードし、コマンド・ライン・インターフェースを使用していくつかの変更を行って装備する必要があります。
{: shortdesc}

アプリに {{site.data.keyword.mqa}} を装備するには、事前に {{site.data.keyword.Bluemix}} アカウントを取得し、装備するアプリのプラットフォームに対応するバージョンの開発環境を正しくインストールしておく必要があります。

Cordova アプリと連携するように {{site.data.keyword.mqa}} を装備するには、以下のタスクを実行します。

1. 必要な許可、およびダウンロードした SDK を Cordova プロジェクトに追加します。

	1. コマンド・プロンプトを開き、プロジェクト・ファイルが入っているディレクトリーに移動します。

	2. 環境に応じて以下の手順を実行して、{{site.data.keyword.mqa}} プラグインを Cordova プロジェクトに追加します。

		**重要**: iOS 9 上で Xcode 7.x を使用している場合は、Xcode の「Build Settings」で「Enable Bitcode」設定を「No」に設定する必要があります。この設定の変更は、platform\iPhone フォルダー内にある Cordova プロジェクト・ファイル .xcodeproj を使用して、Xcode を開いて行うことができます。

		* IBM MobileFirst™ Platform Foundation バージョン 7.1:

			1. 次のコマンドを入力して {{site.data.keyword.mqa}} プラグインをインストールします。

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			ここで、*plugin_location* は、ダウンロードした解凍済み {{site.data.keyword.mqa}} プラグインがあるディレクトリーへのパスです。

			2. Android 上でアプリを実行する場合は、`project_name/app_name/platforms/android/custom_rules.xml` ファイルの名前を `custom_rules.xml.bak` に変更します。

		* Apache Cordova バージョン 4.0 より前:
			1. 次のコマンドを入力して {{site.data.keyword.mqa}} プラグインをインストールします。

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			ここで、*plugin_location* は、ダウンロードした解凍済み {{site.data.keyword.mqa}} プラグインがあるディレクトリーへのパスです。

			2. 次のコマンドを入力して、必要なプラグインを追加します。

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. Android 上でアプリを実行する場合は、`project_name/app_name/platforms/android/custom_rules.xml` ファイルの名前を `custom_rules_bak.xml` に変更します。

		* Apache Cordova バージョン 4.0 以降:

			1. 次のコマンドを入力します。

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			ここで、*plugin_location* は、ダウンロードした解凍済み {{site.data.keyword.mqa}} Cordova プラグインがあるディレクトリーへのパスです。

			2. 次のコマンドを入力して、必要なプラグインを追加します。

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. ログインごとに {{site.data.keyword.mqa}} の新規セッションを開始します。

	1. `index.js` ファイルを開きます。このファイルは `your_project_name\www\js` ディレクトリーにあります。

	2. `index.js` ファイルにある `onDeviceReady()` 関数内に、以下の関数とパラメーターを追加します。関数は、関数の終了中括弧の前に配置します。

	制約事項: アプリが Cordova 用の旧バージョンのプラグインを使用して既に Mobile Quality Assurance 用に装備されていていて、Cordova バージョン 3.0.18 以降の Mobile Quality Assurance プラグインに含まれているフィーチャーを使用している場合は、アプリ・キーを再生成して置き換える必要があります。アプリ・キーを再生成する方法について詳しくは、『アプリの設定の管理 (Managing app settings)』を参照してください。2016 年 2 月より前に生成されたアプリ・キーは、旧プラグインでは引き続き機能しますが、プラグインをバージョン 3.0.18 以降にアップグレードした後は機能しなくなります。

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// or mode: "MARKET" for production mode.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. [{{site.data.keyword.mqa}} の開始](index.html)のステップを続けます。



# 関連リンク
{: #rellinks notoc}

## 関連リンク
{: #general notoc}
* [{{site.data.keyword.mqa}} の開始](index.html){:new_window}
