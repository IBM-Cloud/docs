---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Chrome アプリケーションおよびエクステンションによる {{site.data.keyword.mobilepushshort}} の受信の可能化
{: #web_notifications}
最終更新日: 2017 年 1 月 18 日
{: .last-updated}

Google Chrome のアプリケーションおよび拡張機能を有効にして、{{site.data.keyword.mobilepushshort}} を受信することができます。以下のステップに進む前に、[通知プロバイダーの資格情報の構成](t__main_push_config_provider.html)を確実に実行してください。

## {{site.data.keyword.mobilepushshort}} 用のクライアント SDK のインストール
{: #web_install}

このトピックでは、Chrome アプリケーションおよびエクステンションの開発を促進するために、クライアント JavaScript Push SDK をインストールして使用する方法について説明します。

### Google Chrome アプリケーションおよびエクステンションの初期化

Chrome アプリケーションおよびエクステンションに Javascript SDK をインストールする場合、以下の手順を実行します。

`BMSPushSDK.js` と `manifest_Chrome_Ext.json` (Chrome 拡張機能の場合) または `manifest_Chrome_App.json` (Chrome アプリケーションの場合) を[Bluemix Web push SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master "外部リンク・アイコン"){: new_window}からダウンロードします。



- Chrome アプリケーションの場合、マニフェスト・ファイルを以下のように構成します。
 1. `manifest_Chrome_App.json` ファイルに、名前、記述、およびアイコンを指定します。
 2. `BMSPushSDK.js` を `app.background.scripts` に追加します。
 3. `manifest_Chrome_App.json` を `manifest.json` に変更します。

- Chrome エクステンションの場合、マニフェスト・ファイルを以下のように構成します。
 1. `manifest_Chrome_Ext.json` ファイルに、名前、記述、およびアイコンを指定します。
 2. `BMSPushSDK.js` を `background.scripts` に追加します。
 3. `manifest_Chrome_Ext.json` を `manifest.json` に変更します。

プッシュ通知を受信するために、`background.js` ファイルに以下を追加します。 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked);
```
	{: codeblock}



## Push SDK の初期化 
{: #web_initialize}

Bluemix {{site.data.keyword.mobilepushshort}} サービスの `app GUID` と `app Region` を使用して Push SDK を初期化します。  

app GUID を入手するには、初期化されたプッシュ・サービスのナビゲーション・ペインで**「構成」**オプションを選択し、**「モバイル・オプション」**をクリックします。Bluemix のプッシュ通知サービス appGUID パラメーターを使用するようにコード・スニペットを変更します。

`App Region` は、{{site.data.keyword.mobilepushshort}}サービスがホストされる場所を指定します。次の 3 つの値のいずれかを使用できます。

 - 米国のダラス:	 `.ng.bluemix.net`
 - 英国:      			 `.eu-gb.bluemix.net`
 - シドニー:   		 `.au-syd.bluemix.net`

```
var bmsPush = new BMSPush();
function callback(response) {
     alert(response.response)
  }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Chrome アプリケーションおよびエクステンションの登録
{: #web_register}

`register()` API を使用して、デバイスを{{site.data.keyword.mobilepushshort}}サービスに登録します。Google Chrome から登録する場合、Firebase Cloud Messaging (FCM) または Google Cloud Messaging (GCM) の API キーと Web サイト URL を、Bluemix {{site.data.keyword.mobilepushshort}} サービス Web 構成ダッシュボードに追加します。詳しくは、[Google Cloud Messaging の資格情報の構成](t_push_provider_android.html)で Chrome 用のセットアップを参照してください。

Mozilla Firefox から登録する場合は、Web サイト URL を Bluemix {{site.data.keyword.mobilepushshort}}サービスの Web 構成ダッシュボードで Firefox 用セットアップの下に追加してください。

以下のコード・スニペットを使用して、 Bluemix {{site.data.keyword.mobilepushshort}}サービスに登録します。
```
var bmsPush = new BMSPush();
function callback(response) {
     alert(response.response)
  }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
  bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}




