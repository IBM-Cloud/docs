---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Chrome のアプリケーションおよび拡張機能によるプッシュ通知受け取りの可能化
{: #web_notifications}
最終更新日: 2017 年 4 月 12 日
{: .last-updated}

Google Chrome のアプリケーションおよび拡張機能を有効にして、{{site.data.keyword.mobilepushshort}} を受信することができます。以下のステップに進む前に、[通知プロバイダーの資格情報の構成](t__main_push_config_provider.html)を確実に実行してください。

## プッシュ通知用のクライアント SDK のインストール
{: #web_install}

このトピックでは、Chrome アプリケーションおよびエクステンションの開発を促進するために、クライアント JavaScript Push SDK をインストールして使用する方法について説明します。

### Google Chrome アプリケーションおよびエクステンションの初期化
{: #initialize_google_extn_app}

Chrome アプリケーションおよびエクステンションに Javascript SDK をインストールする場合、以下の手順を実行します。

`BMSPushSDK.js` と `manifest_Chrome_Ext.json` (Chrome エクステンションの場合) または `manifest_Chrome_App.json` (Chrome アプリケーションの場合) を [Bluemix Web push SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}からダウンロードします。



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



### Push SDK の初期化 
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

### Chrome アプリケーションおよびエクステンションの登録
{: #web_register}

`register()` API を使用して、デバイスを{{site.data.keyword.mobilepushshort}}サービスに登録します。Google Chrome から登録する場合、Firebase Cloud Messaging (FCM) API キーと Web サイト URL を Bluemix {{site.data.keyword.mobilepushshort}} サービス Web 構成ダッシュボードに追加します。詳しくは、[通知プロバイダーの資格情報の構成](t__main_push_config_provider.html)を参照してください。 

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


## Chrome アプリケーションおよびエクステンションへの基本通知の送信 
{: #web_extensions_notifications}

アプリケーションの開発が完了したら、プッシュ通知を送信できます。 

1. **「通知の送信 (Send Notifications)」**を選択し、**「送信先 (Send To)」**オプションとして**「Web 通知 (Web Notifications)」**を選択することでメッセージを構成します。 
2. **「メッセージ」**フィールドに、配信する必要があるメッセージを入力します。
3. 以下のオプションの設定を指定することを選択できます。
  - **通知タイトル (Notification Title)**: メッセージ・アラートの見出しとして表示されるテキストです。
  - **通知アイコン URL (Notification Icon URL)**: メッセージにアプリ通知アイコンを付けて配信する必要がある場合、このフィールドにアイコンへのリンクを指定します。
  - **省略キー (Collapse key)**: 省略キーは通知にアタッチされます。デバイスがオフラインのときに、同じ省略キーを持つ複数の通知が連続して到着すると、それらは省略されます。デバイスがオンラインになると、FCM/GCM サーバーから通知を受け取り、同じ省略キーを持つ最新の通知のみを表示します。省略キーが設定されていない場合、新しいメッセージと古いメッセージの両方が将来の配信のために保管されます。
  - **存続時間**: この値は秒単位で設定します。このパラメーターを指定しないと、FCM/GCM サーバーはメッセージを 4 週間保管し、配信を試行します。4 週間が経過すると、有効期限が切れます。可能な値の範囲は、0 から 2,419,200 秒です。
  - **アイドル時は遅延 (Delay when idle)**: デバイスがアイドル状態の場合、通知を配信しないように FCM/GCM サーバーに指示するには、この値を `true` に設定します。デバイスがアイドル状態であっても通知を配信できるようにするには、この値を `false` に設定します。
  - **追加のペイロード (Additional payload)**: 通知用のカスタム・ペイロードの値を指定します。

以下のイメージは、ダッシュボードの Chrome アプリケーションおよびエクステンションの通知オプションを示しています。

  ![「通知」画面](images/push_chrome_extns.jpg)
  
### 次のステップ
{: #next_steps_tags}

基本通知を正常にセットアップしたら、タグ・ベースの通知および詳細オプションの構成を行うことができます。

{{site.data.keyword.mobilepushshort}}サービスの以下の機能をご使用のアプリに追加します。
  タグ・ベースの通知を使用する場合は、[タグ・ベースの通知](c_tag_basednotifications.html)を参照してください。拡張通知オプションを使用する場合は、[拡張通知](t_advance_badge_sound_payload.html)を参照してください。



