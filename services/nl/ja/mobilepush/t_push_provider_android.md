
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Google Cloud Messaging (GCM) の資格情報の構成
{: #create-push-enable-gcm}

Google Cloud Messaging (GCM) 資格情報を取得し、Push ダッシュボードで Push Notification Service をセットアップします。

##送信側 ID と API キーの取得

API キーは、Push Notification Service が安全に保管し、GCM サーバーに接続するために使用します。送信側 ID (プロジェクト番号) は、クライアント側の Android SDK が使用します。送信側 ID について詳しくは、[Google Cloud Message](https://developers.google.com/cloud-messaging/gcm#arch) を参照してください。

1. Google 開発アカウントを [Google Dev Console](https://console.developers.google.com/start){: new_window} で取得します。Google Cloud Messaging (GCM) について詳しくは、[「Creating a Google API Project (Google API プロジェクトの作成)」](https://developers.google.com/console/help/new/){: new_window} を参照してください。

2. Google Developers Console で、新規プロジェクトを作成します。例えば、「hello world」とします。

	![プロジェクトの作成](images/gcm_createproject.jpg)

3. **「プロジェクト名」**に、プロジェクトの名前を入力し、**「作成」**ボタンをクリックします。
4. **「ホーム」**をクリックして、プロジェクト番号を表示します。
プロジェクト番号を記録してください。

	![GCM プロジェクト番号](images/gcm_projectnumber.jpg)

	**注**: プロジェクトを作成すると、プロジェクト番号 (送信側 ID) が作成されます。この番号を使用して、Push ダッシュボードの画面上で Push Notification Service をセットアップします。


5. **「API と認証」**をクリックし、**「Mobile API」**セクションで**「Cloud Messaging for Android」**をクリックします。

	![API](images/gcm_mobileapi.jpg)

6. **「API」**をクリックし、次に**「API を有効にする」**ボタンをクリックして、ご使用のプロジェクトに対する API キーを作成します。
	![API を有効にする](images/gcm_enable_api.jpg)

7. **「API と認証」->「資格情報」**画面に移動します。**「認証情報を追加」**をクリックしてから、**「API キー」**をクリックします。
	![API 資格情報](images/api_credentials.jpg)

8. **「サーバーキー」**オプションを選び、Bluemix Push ダッシュボードで使用することになる GCM API キーを生成します。

9. **「名前」**フィールドで、サーバー API キーの名前を入力します。

	![GCM サーバー・キー](images/gcm_serverkey.jpg)

10. **「作成」**ボタンをクリックします。API キーが表示されます。


	![GCM API キー](images/gcm_apikey.jpg)

11. GCM API キーをコピーし、**「OK」**ボタンをクリックします。
Bluemix の Push Notification ダッシュボードの「構成」画面で資格情報を構成するには、プロジェクト番号 (送信側 ID) と API キーが必要になります。 
12. 次のステップ。Android 用 Push Notification Service のセットアップ

##Android 用 Push Notification Service のセットアップ

**始めに**

GCM の API キーと送信側 ID (プロジェクト番号) を取得します。 

1. Bluemix ダッシュボードでバックエンド・アプリケーションを開き、「IBM Push Notifications」サービスをクリックして、「Push Notification Service」ダッシュボードを開きます。
 
	![Push ダッシュボード](images/bluemixdashboard_push.jpg)

	「Push」ダッシュボードが表示されます。
	
	![プッシュのセットアップ](images/setup_push_main.jpg)

2. **「プッシュのセットアップ (Setup Push)」**ボタンをクリックし、GCM 資格情報を構成します。

1. **「構成」**タブで、**「Google Cloud Messaging」**セクションに移動し、送信側 ID (GCM プロジェクト番号) と API キーを構成します。

4. **「保存」**ボタンをクリックします。 
5. 次のステップ。[Android 用の通知の使用可能化](c_enable_push.html)を行います。
