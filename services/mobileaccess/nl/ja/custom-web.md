---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---

**重要: {{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービス**に置き換えられます。

# Web アプリのカスタム認証
{: #custom-web}

Web アプリにカスタム認証を追加します。

## 開始する前に
{: #before-you-begin}

以下が必要です。
* 認証が成功したらユーザー ID を返す、`/apps/:Guid/<RealmName>/handleChallengeAnswer` エンドポイントのある Web アプリ。ユーザー ID JSON 構造は次のようになっている必要があります。

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンドの作成方法について詳しくは、[概説](index.html)を参照してください。



## カスタム認証用の {{site.data.keyword.amashort}} アプリの構成


1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。
1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。
1. 「カスタム」タイルをクリックします。
1. **カスタム・レルム**、**カスタム ID プロバイダー URL**、および **redirect_uri** を入力します。「保存」をクリックします。



## カスタム Web 認証用の {{site.data.keyword.amashort}} の使用

許可プロセスを開始するには、以下のようにします。

1. Web アプリから、許可サーバーの以下のエンドポイントにリダイレクトします。

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  以下の照会パラメーターを使用します。
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri for the redirect after getting an authorization code>
   scope= ‘openid’
   state= <state>
   ```

    `state` パラメーターは、現在は使用されていないため、空のままにしておくことができます。

    `redirect_uri` パラメーターには、カスタム ID プロバイダーの認証が成功または失敗した後のリダイレクトを指定します。

1. 許可エンドポイントへのリダイレクトの後、ログイン・フォームが示されます。ID プロバイダーに照らした認証を開始するためのユーザー名とパスワード、および `redirect_uri` へのリダイレクトを入力します。
認証が成功した後に返される応答には、要求照会パラメーター中の許可コードが含まれます。

4. 許可サーバーのトークン・エンドポイントへの `POST` 要求を実行します。

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 以下の照会パラメーターを使用します。
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
`redirect_uri` パラメーターは、ステップ 1 の `redirect_uri` と一致している必要があります。許可コードはステップ 2 の要求で返されました。
    認可コードは最大で 10 分間有効であるため、この `POST` 要求を 10 分以内に送信するように注意してください。

`POST` 応答本体には、base64 でエンコードされた *access_token* および
*id_token* が含まれます。

## 認証のテスト


これで、保護リソースに要求を出すことができるようになりました。
保護リソースへのすべての要求には `access_token` が含まれている必要があります。
アクセス・トークンは `the-Authorization-request` ヘッダー・フィールドに入れて送信します。
