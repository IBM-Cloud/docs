---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# Web アプリ用の Facebook 認証の使用可能化
{: #facebook_web}

Facebook を使用して、Web アプリのユーザーを認証します。

## 開始する前に
{: #facebook-auth-android-before}
以下が必要です。
* Web アプリ。  
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンドの作成方法について詳しくは、[概説](index.html)を参照してください。
* Facebook Application ID および App Secret。詳しくは、[Facebook Developer Portal から Facebook アプリケーション ID を取得する](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)を参照してください。


## Web サイト用の Facebook アプリケーションの構成
Web サイトで Facebook を ID プロバイダーとして使用するには、Facebook アプリケーションで Web サイトのプラットフォームを追加して構成する必要があります。

1. Facebook アプリケーションを Facebook Developer Portal で開きます。
1. アプリの Application ID、および App Secret をメモします。Web プロジェクトを Facebook 認証用に構成するときに、この値が必要になります。
1. **「設定」**ページから**「プラットフォームの追加」**をクリックして**「Web サイト」**を選択します。
1. 変更を保存します。
1. 左のサイドバーにある**「Facebook ログイン」**をクリックします。
1. **「有効な OAuth リダイレクト URI (Valid OAuth redirect URIs)」**ボックスに、許可サーバーのコールバック・エンドポイントを入力します (https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback)。変更を保存します。




# Facebook 認証用の {{site.data.keyword.amashort}} の構成
Facebook Application ID および App Secret を取得し、Web クライアントに対して機能するよう Facebook アプリケーションを構成した後、{{site.data.keyword.Bluemix_notm}} ダッシュボードで Facebook 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。
1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。
1. Facebook タイルをクリックします。
1. Facebook Application ID および App Secret を入力し、保存します。




## Facebook Web 認証用の Mobile Client Access の使用

許可プロセスを開始するには、以下のようにします。

1. Web アプリから、許可サーバーのエンドポイント (https://imf-newauthserver.bluemix.net/oauth/v2/authorization) にリダイレクトします。

1. 以下の照会パラメーターを追加します。
   
   ```
response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri for redirecting after receiving the authorization code>
    scope= 'openid'
    state= <state>
    ```


  `state` パラメーターは、現在は使用されていないため、空のままにしておくことができます。`redirect_uri` パラメーターは、Facebook での認証が成功または失敗した後のリダイレクト用の URI です。

1. 許可エンドポイントへのリダイレクトの後、Facebook からログイン・フォームが示されます。  `redirect_uri` にリダイレクトするためのユーザー名とパスワードを入力します。
   リダイレクトの後に得られる応答には、要求照会パラメーター中の許可コードが含まれます。

1. 許可サーバーのトークン・エンドポイントへの `POST` 要求を実行します。

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  以下の照会パラメーターを使用します。
  ```
grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
`redirect_uri` パラメーターは、ステップ 2 の `redirect_uri` と一致している必要があります。
`code` 値は、ステップ 3 の最後に応答で受け取った許可コードです。
許可コードは最大で 10 分間有効であるため、この `POST` 要求を 10 分以内に送信するように注意してください。  `POST` 応答本体には、base64 でエンコードされた `access_token` および `id_token` が含まれている必要があります。

## 認証のテスト
これで、保護リソースに要求を出すことができるようになりました。
保護リソースへのすべての要求には、許可要求ヘッダー・フィールド内に `access_token` が含まれている必要があります。
