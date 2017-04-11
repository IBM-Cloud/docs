---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# FCM の資格情報の構成
{: #create-push-enable-gcm}
最終更新日: 2017 年 1 月 16 日
{: .last-updated}

Firebase Cloud Messaging (FCM) は、プッシュ通知を Android デバイスおよび Google Chrome に送信するために使用されるゲートウェイです。FCM は、Google Cloud Messaging (GCM) の新規バージョンです。ダッシュボード上に {{site.data.keyword.mobilepushshort}} サービスをセットアップするには、FCM の資格情報が必要です。新規アプリケーションには必ず FCM 構成を使用してください。既存のアプリケーションは、引き続き GCM 構成で機能します。

##送信側 ID と API キーの取得
{: #android-senderid-apikey}

API キーは、{{site.data.keyword.mobilepushshort}} サービスによって安全に保管され、FCM サーバーに接続するために使用されます。送信側 ID (プロジェクト番号) は、クライアント側の Android SDK (Google Chrome の場合) および JS SDK (Mozilla Firefox の場合) によって使用されます。 

FCM をセットアップして、API キーおよび送信側 ID を生成するには、以下の手順を実行します。

1. [Firebase コンソール![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.firebase.google.com/?pli=1){: new_window}にアクセスします。
2. **「新規プロジェクトを作成」**を選択します。 
3. 「プロジェクトの作成」ウィンドウで、プロジェクト名を指定し、国/地域を選択して、**「プロジェクトを作成」**をクリックします。
3. ナビゲーション・ペインで、「Settings」アイコンをクリックして、**「プロジェクトの設定」**を選択します。
4. 「クラウド メッセージング」タブを選択して、「サーバー API キー」および「送信側 ID」を生成します。

##Android および Chrome アプリケーションおよびエクステンションの {{site.data.keyword.mobilepushshort}} サービスのセットアップ
{: #setup-push-android}

**注:** FCM/GCM API キーと送信側 ID (プロジェクト番号) が必要になります。

1. Bluemix ダッシュボードを開き、次に、作成した「{{site.data.keyword.mobilepushfull}}」サービス・インスタンスをクリックしてダッシュボードを開きます。「Push」ダッシュボードが表示されます。Android 用のアンバインド・{{site.data.keyword.mobilepushshort}}サービスをセットアップするには、アンバインド・{{site.data.keyword.mobilepushshort}}サービスのアイコンを選択して、{{site.data.keyword.mobilepushshort}}サービスのダッシュボードを開きます。  

![Push ダッシュボード](images/push_unbound.jpg)

2. **「プッシュのセットアップ (Setup Push)」**ボタンをクリックし、Android アプリケーションと Google Chrome アプリケーションおよびエクステンションの FCM/GCM 資格情報を構成します。
3. Android の場合、**「構成 (Configuration)」**ページで、**「モバイル」**タブに移動し、送信側 ID (GCM プロジェクト番号) と API キーを構成します。Google Chrome アプリケーションおよびエクステンションの場合、**「Web」**タブに移動して、送信側 ID (FCM/GCM プロジェクト番号) と API キーを適切に構成します。
4. **「保存」**をクリックします。
5. 次のステップ。[Android 用の通知の使用可能化](c_enable_push.html)または[Google Chrome アプリケーション & エクステンション用の通知の使用可能化](c_enable_push.html)。


