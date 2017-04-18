---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービスに置き換えられます。

# Web アプリ用の Google 認証の使用可能化
{: #google-auth-web}

Google Sign-In を使用して、Web アプリのユーザーを認証します。


## 開始する前に
{: #before-you-begin}

以下が必要です。
* Web アプリ。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンドの作成方法について詳しくは、[概説](index.html)を参照してください。

## Web サイト用の Google アプリケーションの構成
Google を ID プロバイダーとして使用し始めるには、[Google Developer Console](https://console.developers.google.com) にプロジェクトを作成します。プロジェクト作成の一環として、Google Client ID および Secret を取得します。Google Client ID および Secret は、Google 認証によって使用される、アプリケーションの固有の識別子であり、{{site.data.keyword.Bluemix_notm}} アプリケーションのセットアップに必要です。

1. Google+ API を使用してプロジェクトを作成します。
1. **OAuth** を使用して資格情報を作成します。資格情報を作成するには、以下を行う必要があります。
    * アプリケーション・タイプに**「Web application」**を選択します。
    * **「Authorized redirect URIs」**値を次のように指定します。

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. 資格情報作成を完了し、Google Client ID および Secret をメモします。


## Google 認証用の {{site.data.keyword.amashort}} の構成
Google Application ID および Secret を作成した後、{{site.data.keyword.amashort}} ダッシュボードで Google 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。
1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。
1. Google タイルをクリックします。
1. Google Client ID および Secret を入力し、保存します。


## Google Web 認証用の {{site.data.keyword.amashort}} の使用
許可プロセスを開始するには、以下のようにします。

1. Web アプリから、許可サーバーの以下のエンドポイントにリダイレクトします。  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  以下の照会パラメーターを使用します。
	```
   response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri which you want to return to after getting a grant code>
   scope= ‘openid’
   state= <state>
	```

  `state` パラメーターは、現在は使用されていないため、空のままにしておくことができます。

  `redirect_uri` パラメーターの uri は、Google での認証が成功または失敗した後のリダイレクトです。
  リダイレクトの後に得られる応答には、要求照会パラメーター中の許可コードが含まれます。
1. 許可サーバーのトークン・エンドポイントへの `POST` 要求を実行します。

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  以下の照会パラメーターを使用します。

	```
  	grant_type=’authorization_code’
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
`redirect_uri` パラメーターは、ステップ 1 の `redirect_uri` と一致している必要があり、`<authorization code>` 値は応答から受け取られます。
  認可コードは最大で 10 分間有効であるため、この `POST` 要求を 10 分以内に送信するように注意してください。

`POST` 応答本体には、base64 でエンコードされた `access_token` および `id_token` が含まれている必要があります。

## 認証のテスト

これで、保護リソースに要求を出すことができるようになりました。
保護リソースへのすべての要求には、許可要求ヘッダー・フィールド内にアクセス・トークンが含まれている必要があります。
