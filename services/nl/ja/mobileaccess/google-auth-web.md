---

copyright:
  year: 2016

---

# Web アプリケーション用の Google 認証の使用可能化
{: #google-auth-web}

*最終更新日: 2016 年 7 月 18 日*
{: .last-updated}

Google Sign-In を使用して、Web アプリケーションのユーザーを認証します。


## 開始する前に
{: #before-you-begin}

以下が必要です。
* Web アプリ。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[入門](index.html)を参照してください。




* (許可プロセス完了後の) 最終リダイレクトのための URI。



## Web サイト用の Google アプリケーションの構成
Google を ID プロバイダーとして使用し始めるには、[Google Developer Console](https://console.developers.google.com) にプロジェクトを作成します。プロジェクト作成の一環として、**Google Client ID** および **Secret** を取得します。Google Client ID および Secret は、Google 認証によって使用される、アプリケーションの固有の識別子であり、{{site.data.keyword.amashort}} ダッシュボードのセットアップに必要です。


1. Google Developer Console で Google アプリケーションを開きます。 
3. Google+ API を追加します。 
3. OAuth を使用して資格情報を作成します。アプリケーション・タイプに「Web application」を選択します。「承認済みのリダイレクト URI」ボックスに {{site.data.keyword.amashort}} リダイレクト URI を入力します。{{site.data.keyword.amashort}} リダイレクト許可 URI は、{{site.data.keyword.amashort}} ダッシュボードの Google 構成画面から取得できます (下の手順を参照してください)。 
6. 変更を保存します。Google Client ID および Application Secret をメモします。


## Google 認証用の {{site.data.keyword.amashort}} の構成
Google Application ID および Secret を作成した後、{{site.data.keyword.amashort}} ダッシュボードで Google 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。
1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。
1. Google パネルでボタンをクリックします。
1. **「Web 用の構成 (Configure for Web)」**セクションで以下を行います。   
    * **「Google Developer Console の Mobile Client Access リダイレクト URI (Mobile Client Access Redirect URI for Google Developer Console)」**テキスト・ボックス内の値をメモします。これは、上のステップ 3 で **Google Developers ポータル**の**「Web アプリケーションのクライアント ID の制限 (Restrictions in the Client ID for Web application)」**の下の**「承認済みのリダイレクト URI (Authorized redirect URIs)」**ボックスに追加する必要のある値です。
    * **Google Client ID** および **Client Secret** を入力します。
    * リダイレクト URI を**「Web アプリケーションのリダイレクト URI (Your Web Application Redirect URIs)」**に入力します。この値は、許可プロセス完了後にアクセスされるリダイレクト URI であり、開発者によって決定されます。
1. **「保存」**をクリックします。


## ID プロバイダーとして Google を使用した {{site.data.keyword.amashort}} 許可フローの実装

`VCAP_SERVICES` 環境変数が {{site.data.keyword.amashort}} サービス・インスタンスごとに自動的に作成され、許可プロセスに必要なプロパティーが含まれます。これは 1 つの JSON オブジェクトからなり、アプリケーションの左側のナビゲーターで**「環境変数」**をクリックすることによって表示できます。

許可プロセスを開始するには、以下のようにします。

1. `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、許可エンドポイント (`authorizationEndpoint`) およびクライアント ID (`clientId`) を取り出します。 

    **注:** Web サポートが追加される前に {{site.data.keyword.amashort}} サービスを作成した場合、サービス資格情報に許可エンドポイントが含まれていないことがあります。この場合、Bluemix 地域に基づいて、以下の許可エンドポイントを使用してください。


 	米国南部: 
 	```
 	https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization
 	```
 	ロンドン:
 	```
 	https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
  	```
  	シドニー:
  	```
  	https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization
  	```
1. 照会パラメーターとして `response_type("code")`、`client_id`、および `redirect_uri` を使用して、許可サーバー URI を構築します。
1. Web アプリから、生成された URI へリダイレクトします。
  
次の例は、`VCAP_SERVICES` 変数からパラメーターを取り出し、URL を構築し、リダイレクト要求を送信します。
  
```Java
var cfEnv = require("cfenv"); 
app.get("/protected", checkAuthentication, function(req, res, next){ 
  res.send("Hello from protected endpoint"); 
 }); 

 app.get("/protected", checkAuthentication, function(req, res, next){  
      res.send("Hello from protected endpoint"); 
 	function checkAuthentication(req, res, next){ 

	// Check if user is authenticated 
  if (req.session.userIdentity){ 
    next() 
  } else {
// If not - redirect to authorization server 
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
		var authorizationEndpoint = mcaCredentials.authorizationEndpoint; 
		var clientId = mcaCredentials.clientId; 
		var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect URI 
		var redirectUrl = authorizationEndpoint + "?response_type=code";
		redirectUrl += "&client_id=" + clientId; 
		redirectUrl += "&redirect_uri=" + redirectUri; 
		res.redirect(redirectUrl); 
	} 
} 

  ```

`redirect_uri` パラメーターは Web アプリケーション・リダイレクト URI を表していて、{{site.data.keyword.amashort}} ダッシュボードで定義されたものと等しくなければならないことに注意してください。
許可エンドポイントへのリダイレクトの後、ユーザーに Google からログイン・フォームが示されます。ユーザーが自分の Google ID を使用してログインすることが認可された後、{{site.data.keyword.amashort}} サービスは、照会パラメーターとして認可コードを提供して Web アプリケーション・リダイレクト URI を呼び出します。

## トークンの取得
次のステップは、前に受け取った認可コードを使用してアクセス・トークンおよび識別トークンを取得することです。これには、次のようにします。 

1. `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、トークンの `tokenEndpoint`、`clientId`、および `secret` を取り出します。 
  
    **注:** Web サポートが追加される前に {{site.data.keyword.amashort}} サービスを作成した場合、サービス資格情報に許可エンドポイントが含まれていないことがあります。この場合、Bluemix 地域に基づいて、以下の許可エンドポイントを使用してください。
 
 	米国南部: 
 	```
 	     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 ```
 	ロンドン:
  	```
  	     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 ```
   	シドニー:
  	```
   	     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 ```

2. grant_type ("authorization_code")、client_id、redirect_uri、および code をフォーム・パラメーターとして使用して、トークン・サーバー URI に POST 要求を送信します。`clientId` および `clientSecret` を基本 HTTP 認証資格情報として送信します。
 
以下のコードは、必要な値を取り出し、それらを POST 要求で送信します。
    
   ```Java
  var cfEnv = require("cfenv");
  var base64url = require("base64url ");
  var request = require('request');
  
  app.get("/oauth/callback", function(req, res, next){ 
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint; 
    var formData = { 
      grant_type: "authorization_code", 
      client_id: mcaCredentials.clientId, 
      redirect_uri: "http://some-server/oauth/callback",   // Your web application redirect uri 
      code: req.query.code 
    } 

  request.post({ 
    url: tokenEndpoint, 
    formData: formData 
    }, function (err, response, body){ 
      var parsedBody = JSON.parse(body); 
        req.session.accessToken = parsedBody.access_token; 
        req.session.idToken = parsedBody.id_token; 
        var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
      var decodedIdentity= base64url(idTokenComponents[1]);
      req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
      res.redirect("/"); 
    }
    ).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
); 
  ```

  `redirect_uri` パラメーターは、Google+ での認証が成功または失敗した後のリダイレクト用の URI であり、ステップ 1 の `redirect_uri` と一致する必要があります。  
   
この POST 要求は、必ず 10 分以内に送信してください。10 分後に認可コードの有効期限が切れます。10 分を過ぎると新しいコードが必要です。

POST 応答本体には、base64 でエンコードされた `access_token` および `id_token` が含まれます。

アクセス・トークンおよび識別トークンを受け取ったら、Web セッションに認証済みのフラグを立てることができ、オプションでこれらのトークンを永続的に保持できます。  


##取得したアクセス・トークンおよび識別トークンの使用 

識別トークンには、ユーザー ID に関する情報が含まれます。Google 認証の場合、このトークンには、ユーザーが共有することに同意したすべての情報 (氏名、プロファイル写真の URL など) が含まれます。  

アクセス・トークンは、{{site.data.keyword.amashort}} 許可フィルターによって保護されたリソースとの通信を可能にします。[リソースの保護](protecting-resources.html)を参照してください。


保護リソースへの要求を行うには、以下の構造の許可ヘッダーを要求に追加します。 

`Authorization=Bearer <accessToken> <idToken>`

**注:** 

* `accessToken` と `idToken` は空白で分離する必要があります。

* `idToken` はオプションです。識別トークンを提供しない場合、保護リソースはアクセス可能ですが、許可ユーザーに関する情報を受け取ることはありません。 



