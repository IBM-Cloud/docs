---

copyright:
  year: 2016, 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**重要: {{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービス**に置き換えられます。

# Web アプリケーション用の Google 認証の使用可能化
{: #google-auth-web}

Google Sign-In を使用して、Web アプリケーションのユーザーを認証します。{{site.data.keyword.amafull}} セキュリティー機能を追加します。


## 開始する前に
{: #before-you-begin}

以下が必要です。

* Web アプリ。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。




* (許可プロセス完了後の) 最終リダイレクトのための URI。


## Web サイト用の Google アプリケーションの構成
{: #google-auth-config}

Google を ID プロバイダーとして使用し始めるには、[Google Developer Console ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.developers.google.com){: new_window}にプロジェクトを作成します。プロジェクト作成の一環として、**Google Client ID** および **Secret** を取得します。Google Client ID および Secret は、Google 認証によって使用される、アプリケーションの固有の識別子であり、{{site.data.keyword.amashort}} ダッシュボードのセットアップに必要です。

1. Google Developer Console で Google アプリケーションを開きます。
3. **Google+** API を追加します。
3. OAuth を使用して資格情報を作成します。アプリケーション・タイプに「Web application」を選択します。「承認済みのリダイレクト URI」ボックスに {{site.data.keyword.amashort}} リダイレクト URI を入力します。{{site.data.keyword.amashort}} リダイレクト許可 URI は、{{site.data.keyword.amashort}} ダッシュボードの Google 構成画面から取得します (下記の手順を参照してください)。
4. 変更を保存します。**Google Client ID** および **Application Secret** をメモします。


## Google 認証用の Mobile Client Access の構成
{: #google-auth-config-ama}

Google Application ID および Secret を作成した後、{{site.data.keyword.amashort}} ダッシュボードで Google 認証を使用可能にすることができます。

1. {{site.data.keyword.amashort}} サービス・ダッシュボードを開きます。
1. **「管理」**タブで、**「許可」**をオンに切り替えます。
1. **「Google」**セクションを開きます。
1. **「Web アプリへの Google の追加 (Add Google to a Web App)」**にチェック・マークを付けます。
4. **「Web 用の構成 (Configure for Web)」**セクションで以下を行います。   
    * **「Google Developer Console の Mobile Client Access リダイレクト URI (Mobile Client Access Redirect URI for Google Developer Console)」**テキスト・ボックス内の値をメモします。これは、**Google Developers ポータル**の**「Web アプリケーションのクライアント ID の制限 (Restrictions in the Client ID for Web application)」**の下の**「承認済みのリダイレクト URI (Authorized redirect URIs)」**ボックスに追加する必要のある値です。
    * **Client ID** および **Client Secret** を入力します。
    * リダイレクト URI を**「Web アプリケーションのリダイレクト URI (Your Web Application Redirect URIs)」**に入力します。この値は、許可プロセス完了後にアクセスされるリダイレクト URI であり、開発者によって決定されます。
5. **「保存」**をクリックします。


## Google を ID プロバイダーとして使用した Mobile Client Access 許可フローの実装
{: #google-auth-flow}

`VCAP_SERVICES` 環境変数が {{site.data.keyword.amashort}} サービス・インスタンスごとに自動的に作成され、許可プロセスに必要なプロパティーが含まれます。この環境変数は 1 つの JSON オブジェクトから成り、{{site.data.keyword.amashort}} サービス・ダッシュボードの **「サービス資格情報」**タブをクリックすることによって表示できます。

許可プロセスを開始するには、以下のようにします。

1. `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、許可エンドポイント (`authorizationEndpoint`) およびクライアント ID (`clientId`) を取り出します。

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**注:** Web サポートが追加される前に {{site.data.keyword.amashort}} サービスをアプリケーションに追加した場合は、サービス資格情報にトークン・エンドポイントが含まれていないことがあります。代わりに、{{site.data.keyword.Bluemix_notm}} 地域に応じて、以下の URL を使用します。

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
 }); 

 function checkAuthentication(req, res, next) {
		// Check if user is authenticated 
  if (req.session.userIdentity){ 
    next()
		} else {
			// If not - redirect to authorization server 
				var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
				var authorizationEndpoint = mcaCredentials.authorizationEndpoint; 
				var clientId = mcaCredentials.clientId; 
				var redirectUri = "http://some-server/oauth/callback"; // Your Web application redirect URI 
				var redirectUrl = authorizationEndpoint + "?response_type=code";
				redirectUrl += "&client_id=" + clientId; 
				redirectUrl += "&redirect_uri=" + redirectUri; 
				res.redirect(redirectUrl); 
			} 
		}
	```
	{: codeblock}

	`redirect_uri` パラメーターは Web アプリケーション・リダイレクト URI を表していて、{{site.data.keyword.amashort}} ダッシュボードで定義されたものと等しくなければならないことに注意してください。

	許可エンドポイントへのリダイレクトの後、ユーザーに Google からログイン・フォームが示されます。ユーザーが自分の Google ID を使用してログインすることが認可された後、{{site.data.keyword.amashort}} サービスは、照会パラメーターとして認可コードを提供して Web アプリケーション・リダイレクト URI を呼び出します。

## トークンの取得
{: #google-auth-tokens}

次のステップは、前に受け取った認可コードを使用してアクセス・トークンおよび識別トークンを取得することです。

1. `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、トークンの `tokenEndpoint`、`clientId`、および `secret` を取り出します。

	**注:** Web サポートが追加される前に {{site.data.keyword.amashort}} を使用した場合は、サービス資格情報にトークン・エンドポイントが含まれていないことがあります。代わりに、Bluemix 地域に応じて、以下の URL を使用します。

	米国南部:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	ロンドン:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	シドニー:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

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
			redirect_uri: "http://some-server/oauth/callback",// Your Web application redirect uri
			code: req.query.code
		}

		request.post({
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
			var parsedBody = JSON.parse(body); 
        req.session.accessToken = parsedBody.access_token; 
        req.session.idToken = parsedBody.id_token; 
        var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
			res.redirect("/"); 
			}
			).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
);
	```
	{: codeblock}

	`redirect_uri` パラメーターは、Google+ での認証が成功または失敗した後のリダイレクト用の URI であり、{{site.data.keyword.amashort}} ダッシュボードに定義されている `redirect_uri` に一致している必要があります。  

	この POST 要求は、必ず 10 分以内に送信してください。10 分後に認可コードの有効期限が切れます。10 分を過ぎると新しいコードが必要です。

	POST 応答本体には、base64 でエンコードされた `access_token` および `id_token` が含まれます。

	アクセス・トークンおよび識別トークンを受け取ったら、Web セッションに認証済みのフラグを立てることができ、オプションでこれらのトークンを永続的に保持できます。  


## 取得したアクセス・トークンおよび識別トークンの使用
{: #google-auth-using-token}

識別トークンには、ユーザー ID に関する情報が含まれます。Google 認証の場合、このトークンには、ユーザーが共有することに同意したすべての情報 (氏名、プロファイル写真の URL など) が含まれます。  

アクセス・トークンは、{{site.data.keyword.amashort}} 許可フィルターによって保護されたリソースとの通信を可能にします。[リソースの保護](protecting-resources.html)を参照してください。

保護リソースへの要求を行うには、以下の構造の許可ヘッダーを要求に追加します。

`Authorization=Bearer <accessToken> <idToken>`

#### ヒント:
{: #tips}

* `accessToken` と `idToken` は空白で分離する必要があります。

* `idToken` はオプションです。識別トークンを提供しない場合、保護リソースはアクセス可能ですが、許可ユーザーに関する情報を受け取ることはありません。
