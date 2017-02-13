---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#{{site.data.keyword.amashort}} Web アプリケーション用のカスタム認証の構成
{: #custom-web}

カスタム認証と {{site.data.keyword.amafull}} セキュリティー機能を Web アプリに追加します。

## 開始する前に
{: #before-you-begin}

開始する前に以下が必要です。

* Web アプリ。
* カスタム ID プロバイダーを使用するように構成済みの {{site.data.keyword.amashort}} サービスのインスタンスによって保護されているリソース ([カスタム認証の構成](custom-auth-config-mca.html)を参照してください)。  
* **TenantID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* **「レルム」**名。これは、{{site.data.keyword.amashort}} ダッシュボードの**「管理」**タブで、**「カスタム」**セクションの**「レルム名」**フィールドに指定した値です。
* バックエンド・アプリケーションの URL (**「アプリの経路 (App Route)」**)。バックエンド・アプリケーションの保護されたエンドポイントに要求を送信するためにこの値が必要になります。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域の値は、`「米国南部」`、`「英国」`、または`「シドニー」`のいずれかでなければならず、また Javascript コードで必要な SDK 値 (`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY`、または `BMSClient.REGION_UK`) に対応している必要があります。{{site.data.keyword.amashort}} クライアントを初期化するためにこの値が必要になります。
* (許可プロセス完了後の) 最終リダイレクトのための URI。これは、**「管理」**タブの**「カスタム」**セクションで入力した**「Web アプリケーションのリダイレクト URI (Your Web Application Redirect URIs)」**値です。

詳細情報:

* [{{site.data.keyword.amashort}} 概説](getting-started.html)
* [カスタム ID プロバイダーの使用](custom-auth.html)
* [カスタム ID プロバイダーの作成](custom-auth-identity-provider.html)
* [カスタム認証用の {{site.data.keyword.amashort}} の構成 ](custom-auth-config-mca.html)


##カスタム ID プロバイダーの構成
{: #custom-auth-config}

カスタム ID プロバイダーを作成するときには、次の構造の経路と共に POST メソッドを定義する必要があります。

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` は、URL パラメーターであり、`<your-realm-name>` は任意のレルム名です。

要求本体には `challengeAnswer` オブジェクトが含まれ、これには `username` と `password` が含まれます。

ユーザーを検証した後、この経路は以下の構造の JSON オブジェクトを返す必要があります。

```json
{
	status: "success",
	userIdentity: {
		userName: <user name>,
		displayName: <display name>
		attributes: <additional attributes json>
	}
}
```
{: codeblock}

**注:** `attributes` フィールドはオプションです。

以下のコードは、そのような POST 要求を示します。

```Java
var app = express();
var bodyParser = require('body-parser');
app.use(bodyParser.json());

var users = {
	"John": {
		password: "123",
		displayName: "John Doe"
	}
};

app.post('/apps/:tenantID/customAuthRealm_1/handleChallengeAnswer', function(req, res) {
	console.log ("tenantID " + req.params.tenantID);

	var challengeAnswer = req.body.challengeAnswer;
	console.log ("challengeAnswer " + JSON.stringify(challengeAnswer));

	if (challengeAnswer && users[challengeAnswer.username] && challengeAnswer.password === users[challengeAnswer.username].password) {
		res.json({
			status: "success",
			userIdentity: {
				userName: challengeAnswer.username,
				displayName: users[challengeAnswer.username].displayName
			}
		});
	} else {
		res.json({
			status: "failure"
		});
	}

});
```
{: codeblock}


##カスタム認証用の {{site.data.keyword.amashort}} の構成
{: #custom-auth-config-mca}

カスタム ID プロバイダーを構成した後、{{site.data.keyword.amashort}} ダッシュボードでカスタム認証を使用可能にすることができます。

1. {{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。
1. **「管理」**タブで、**「許可」**をオンに切り替えます。
1. **「カスタム」**セクションを展開します。
1. **「レルム名」**、**「カスタム ID プロバイダー URL」**を入力します。
1. **「Web アプリケーションのリダイレクト URI (Your Web Application Redirect URIs)」**値を入力します。これは、正常に許可された後の最終リダイレクトの URI です。
1. **「保存」**をクリックします。


##カスタム ID プロバイダーを使用した {{site.data.keyword.amashort}} 許可フローの実装
{: #custom-auth-flow}

`VCAP_SERVICES` 環境変数が {{site.data.keyword.amashort}} サービス・インスタンスごとに自動的に作成され、許可プロセスに必要なプロパティーが含まれます。この環境変数は 1 つの JSON オブジェクトから成り、{{site.data.keyword.amashort}} ダッシュボード内の **「サービス資格情報」**タブに表示できます。

ユーザー許可を要求するには、ブラウザーを許可サーバー・エンドポイントにリダイレクトします。これには、次のようにします。

1. `VCAP_SERVICES` 環境変数に保管されているサービス資格情報から、許可エンドポイント (`authorizationEndpoint`) とクライアント ID (`clientId`) を取得します。

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

   以下の例は、`VCAP_SERVICES` 変数からパラメーターを取り出し、URL を構築し、リダイレクト要求を送信します。

	```Java
	var cfEnv = require("cfenv");
	app.get("/protected", checkAuthentication, function(req, res, next) {
		res.send("Hello from protected endpoint");
	}
	);

	function checkAuthentication(req, res, next) {
		// Check if user is authenticated
		if (req.session.userIdentity) {
			next()
		} else {
			// If not - redirect to authorization server
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
			var clientId = mcaCredentials.clientId;
			var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect uri
			var redirectUrl = authorizationEndpoint + "?response_type=code";
			redirectUrl += "&client_id=" + clientId;
			redirectUrl += "&redirect_uri=" + redirectUri;
			res.redirect(redirectUrl);
		}
	}
	```
	{: codeblock}

	`redirect_uri` パラメーターは Web アプリケーション・リダイレクト URI を表していて、{{site.data.keyword.amashort}} ダッシュボードで定義されたものと等しくなければならないことに注意してください。  

	要求と一緒に `state` パラメーターを渡すことができます。このパラメーターは、カスタム ID プロバイダー POST メソッドに伝搬され、要求本体からアクセスできます (`req.body.stateId`)。  

	許可エンドポイントへのリダイレクトの後、ユーザーにログイン・フォームが示されます。ユーザーの資格情報がカスタム ID プロバイダーで認証された後、{{site.data.keyword.amashort}} サービスは、照会パラメーターとして認可コードを提供して Web アプリケーション・リダイレクト URI を呼び出します。  

	リダイレクトの後、ユーザーにログイン・フォームが示されます。ユーザーの資格情報がカスタム ID プロバイダーによって認証された後、{{site.data.keyword.amashort}} サービスは、照会パラメーターとして認可コードを提供して Web アプリケーション・リダイレクト URI を呼び出します。

##トークンの取得
{: custom-auth-tokens}

次のステップは、前に受け取った認可コードを使用してアクセス・トークンおよび識別トークンを取得することです。これには、次のようにします。

1. `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、`authorizationEndpoint`、`clientId`、および `secret` を取り出します。

	**注:** Web サポートが追加される前に {{site.data.keyword.amashort}} サービスをアプリケーションに追加した場合は、サービス資格情報にトークン・エンドポイントが含まれていないことがあります。代わりに、{{site.data.keyword.Bluemix_notm}} 地域に応じて、以下の URL を使用します。

	米国南部:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	ロンドン:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	シドニー:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. `grant_type`、`client_id`、`redirect_uri`、および `code` をフォーム・パラメーターとして使用し、`clientId` および `secret` を基本 HTTP 認証資格情報として使用して、トークン・サーバー URI に POST 要求を送信します。

	以下の例に示すコードは、必要な値を取り出し、それらを POST 要求で送信します。

	```Java
	var cfEnv = require("cfenv");
	var base64url = require("base64url");
	app.get("/oauth/callback", function(req, res, next) {
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
		var tokenEndpoint = mcaCredentials.tokenEndpoint;

		var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",   // Your Web application redirect uri
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

	`redirect_uri` パラメーターは、前に許可要求で使用された `redirect_uri` と一致している必要があることに注意してください。code パラメーター値は、許可要求の最後に応答で受け取った認可コードでなければなりません。認可コードは 10 分間のみ有効であり、それを過ぎると新しいコードの取得が必要になります。



	応答本体には、`access_token` および `id_token` が JWT フォーマットで含まれます ([JWT Web サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://jwt.io "外部リンク・アイコン"){: new_window}を参照してください)。

	アクセス・トークンおよび識別トークンを受け取ったら、Web セッションに認証済みのフラグを立てることができ、オプションでこれらのトークンを永続的に保持できます。


##取得したアクセス・トークンおよび識別トークンの使用
{: #custom-auth-using-token}

識別トークンには、ユーザー ID に関する情報が含まれます。カスタム認証の場合、このトークンには、カスタム ID プロバイダーによって認証時に返されるすべての情報が含まれます。`imf.user` フィールドの下で、`displayName` フィールドには、カスタム ID プロバイダーによって返される `displayName` が含まれ、`id` フィールドには `userName` が含まれます。カスタム ID プロバイダーによって返される他のすべての値は、`imf.user` の下の `attributes` フィールド内に返されます。  

アクセス・トークンは、{{site.data.keyword.amashort}} 許可フィルターによって保護されたリソースとの通信を許可します ([リソースの保護](protecting-resources.html) を参照してください)。保護リソースへの要求を行うには、以下の構造の許可ヘッダーを要求に追加します。

`Authorization=Bearer <accessToken> <idToken>`

####ヒント:
{: #tips_token}

* `<accessToken>` と `<idToken>` は空白で分離する必要があります。

* 識別トークンはオプションです。識別トークンを提供しない場合、保護リソースはアクセス可能ですが、許可ユーザーに関する情報を受け取ることはありません。
