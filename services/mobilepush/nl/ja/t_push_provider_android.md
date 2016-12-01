
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# FCM の資格情報の構成
{: #create-push-enable-gcm}
最終更新日: 2016 年 11 月 15 日
{: .last-updated}

Firebase Cloud Messaging (FCM) は、プッシュ通知を Android デバイス、Google Chrome、および Mozilla の各 Web ブラウザーに配信するために使用されるゲートウェイです。Google Cloud Messaging (GCM) が FCM に置き換えられました。FCM 資格情報を取得してから、ダッシュボード上で {{site.data.keyword.mobilepushshort}} サービスをセットアップする必要があります。新規アプリケーションには必ず FCM 構成を使用してください。既存のアプリケーションは、引き続き GCM 構成で機能します。

##送信側 ID と API キーの取得
{: #android-senderid-apikey}

API キーは、{{site.data.keyword.mobilepushshort}} サービスによって安全に保管され、FCM サーバーに接続するために使用されます。送信側 ID (プロジェクト番号) は、クライアント側の Android SDK (Google Chrome の場合) および JS SDK (Mozilla Firefox の場合) によって使用されます。 

FCM をセットアップして、API キーおよび送信側 ID を生成するには、以下の手順を実行します。

1. [Firebase コンソール](https://console.firebase.google.com/?pli=1)にアクセスします。
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

###Google Chrome と Mozilla Firefox の Web プッシュの構成 (FCM/GCM を使用)
{: #config-gcm-mozilla}

1. Push ダッシュボードのナビゲーション・ペインで、**「構成」**を選択します。
2. 「Web」タブを選択します。
	![WebPush 構成](images/webpush_configure.jpg)
3. プッシュ通知を受信するために登録する FCM/GCM API キーと Web サイトの URL を構成します。
4. **「保存」**をクリックします。
5. 次のステップ。[Google Chrome および Mozilla Firefox ブラウザー用の通知の使用可能化](c_enable_push.html)を行います。
