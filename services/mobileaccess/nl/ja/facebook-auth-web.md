---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービスに置き換えられます。

# Web アプリケーション用の Facebook 認証の使用可能化
{: #facebook-auth-web}

Facebook を使用して、{{site.data.keyword.amafull}} Web アプリケーションのユーザーを認証します。{{site.data.keyword.amashort}} セキュリティー機能を追加します。

## 開始する前に
{: #facebook-auth-android-before}
以下が必要です。

* Web アプリ。
* {{site.data.keyword.amashort}} サービス。詳しくは、[始めに (Getting started) ](index.html)を参照してください。
* (許可プロセス完了後の) 最終リダイレクトのための URI。


## Facebook for Developers Web サイトでのアプリケーションの構成
{: #facebook-auth-config}

Web サイトで Facebook を ID プロバイダーとして使用するには、Facebook アプリケーションで Web サイトのプラットフォームを追加して構成する必要があります。

1. [Facebook for Developers](https://developers.facebook.com) サイトで自分のアカウントにログインします。新規アプリケーションの作成については、[Facebook for Developers Web サイトでのアプリケーションの作成](facebook-auth-overview.html#facebook-appID)を参照してください。
1. **「App ID」**および**「App Secret」**をメモします。Mobile Client Access ダッシュボードで Facebook 認証用に Web プロジェクトを構成するときに、これらの値が必要になります。
1. **「製品リスト (Products List)」**から、**「Facebook ログイン (Facebook Login)」**を選択します。
4. **Web** プラットフォームが存在しない場合は、追加します。
6. **「有効な OAuth リダイレクト URI (Valid OAuth redirect URIs)」**ボックスに、許可サーバーのコールバック・エンドポイント URI を入力します。以下のステップで {{site.data.keyword.amashort}} サービスを構成した後で、この値を追加できます。
7. 変更を保存します。


## Facebook 認証用の {{site.data.keyword.amashort}} の構成
{: #facebook-auth-config-ama}

Facebook App ID および App Secret を取得し、Web クライアントに対して機能するように Facebook for Developers アプリケーションを構成した後、{{site.data.keyword.amashort}} ダッシュボードで Facebook 認証を使用可能にすることができます。

1. {{site.data.keyword.amashort}} サービス・ダッシュボードを開きます。
1. **「管理」**タブで、**「許可」**をオンに切り替えます。
1. **「Facebook」**セクションを展開します。
1. **「Web アプリへの Facebook の追加 (Add Facebook to a Web App)」**を選択します。
5. **「Facebook for Developers の Mobile Client Access リダイレクト URI (Mobile Client Access Redirect URI for Facebook for Developers)」**テキスト・ボックス内の値をメモします。この値は、Facebook Developers ポータルの**「Facebook ログイン (Facebook Login)」**の**「有効な OAuth リダイレクト URI (Valid OAuth redirect URIs)」**ボックスに追加する必要があります。
6. Facebook for Developers Web サイトから取得した Facebook **「App ID」**および**「App Secret」**を入力します。
7. リダイレクト URI を**「Web アプリケーションのリダイレクト URI (Your Web Application Redirect URIs)」**に入力します。この値は、許可プロセス完了後にアクセスされるリダイレクト URI であり、開発者によって決定されます。
8. **「保存」**をクリックします。


## ID プロバイダーとして Facebook を使用した {{site.data.keyword.amashort}} 許可フローの実装
{: #facebook-auth-flow}

`VCAP_SERVICES` 環境変数が {{site.data.keyword.amashort}} サービス・インスタンスごとに自動的に作成され、許可プロセスに必要なプロパティーが含まれます。この環境変数は 1 つの JSON オブジェクトから成り、{{site.data.keyword.amashort}} サービス・ダッシュボードの **「サービス資格情報」**タブに表示できます。

許可プロセスを開始するには、以下のようにします。

1. `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、許可エンドポイント (`authorizationEndpoint`) とクライアント ID (`clientId`) を取り出します。

	`var cfEnv = require("cfenv");`

	**注:** Web サポートが追加される前に {{site.data.keyword.amashort}} サービスをアプリケーションに追加した場合は、**「サービス資格情報」**にトークン・エンドポイントが含まれていないことがあります。代わりに、{{site.data.keyword.Bluemix_notm}} 地域に応じて、以下の URL を使用します。

	米国南部:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	ロンドン:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	シドニー:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization`

2. 照会パラメーターとして `response_type("code")`、`client_id`、および `redirect_uri` を使用して、許可サーバー URI を構築します。

3. Web アプリから、生成された URI へリダイレクトします。

	次の例は、`VCAP_SERVICES` 変数からパラメーターを取り出し、URL を構築し、リダイレクト要求を送信します。

	```Java
  var cfEnv = require("cfenv"); 

  app.get("/protected", checkAuthentication, function(req, res, next){  
      res.send("Hello from protected endpoint"); 
    }
  );

	function checkAuthentication(req, res, next){
  // ユーザーが認証されているかどうかを検査

		if (req.session.userIdentity) {   
			next()  
		} else {   
			// If not - redirect to authorization server   
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;   
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;   
			var clientId = mcaCredentials.clientId;   
			var redirectUri = "http://some-server/oauth/callback"; 
			// Your Web application redirect URI   

			var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;   
        redirectUrl += "&redirect_uri=" + redirectUri;   
  
        res.redirect(redirectUrl);  
  
      } 
  }
	```
	{: codeblock}

	`redirect_uri` パラメーターは、Facebook での認証が成功または失敗した後のリダイレクト用の URI です。   

	許可エンドポイントへのリダイレクトの後、ユーザーに Facebook からログイン・フォームが示されます。ユーザーの ID が Facebook によって認可された後、{{site.data.keyword.amashort}} サービスは、照会パラメーターとして認可コードを提供して Web アプリケーション・リダイレクト URI を呼び出します。  


## トークンの取得
{: #facebook-auth-tokens}

次のステップでは、前に受け取った認可コードを使用してアクセス・トークンと識別トークンを取得します。

1.  `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、トークンの `tokenEndpoint`、`clientId`、および `secret` を取り出します。

	**注:** Web サポートが追加される前に {{site.data.keyword.amashort}} を使用した場合は、サービス資格情報にトークン・エンドポイントが含まれていないことがあります。代わりに、Bluemix 地域に応じて、以下の URL を使用します。

	米国南部:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	ロンドン:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	シドニー:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. 認可タイプ ("authorization_code")、`clientId`、およびリダイレクト URI をフォーム・パラメーターとして使用して、トークン・サーバー URI に POST 要求を送信します。`clientId` および `secret` を基本 HTTP 認証資格情報として送信します。

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
        var idTokenComponents = parsedBody.id_token.split("."); 
			// [header, payload, signature] 
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
			res.redirect("/");
		}
		).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
);
	```
	{: codeblock}

	`redirect_uri` パラメーターは、前に許可要求に使用された `redirect_uri` と一致している必要があることに注意してください。`code` パラメーター値は、許可要求から応答で受け取った認可コードである必要があります。認可コードが有効なのは 10 分間のみであり、それを過ぎると新しいコードの取得が必要です。

	応答本体には、アクセス・コードとトークン ID が JWT フォーマットで含まれます ([JWT Web サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://jwt.io/){: new_window}を参照してください)。

	アクセス・トークンを取得し、識別トークンを受け取ったら、Web セッションに認証済みのフラグを立てることができ、オプションでこれらのトークンを永続的に保持できます。  

##取得したアクセス・トークンおよび識別トークンの使用
{: #facebook-auth-using-token}

識別トークンには、ユーザー ID に関する情報が含まれます。Facebook 認証の場合、このトークンには、ユーザーが共有することに同意したすべての情報 (氏名、年齢グループ、プロファイル写真の URL など) が含まれます。  

アクセス・トークンは、{{site.data.keyword.amashort}} 許可フィルターによって保護されたリソースとの通信を可能にします。[リソースの保護](protecting-resources.html)を参照してください。

保護リソースへの要求を行うには、以下の構造の許可ヘッダーを要求に追加します。

`Authorization=Bearer <accessToken> <idToken>`

#### ヒント
{: #tips}

* `accessToken` と `idToken` は空白で分離する必要があります。

* `idToken` はオプションです。識別トークンを提供しない場合、保護リソースはアクセス可能ですが、許可ユーザーに関する情報を受け取ることはありません。
