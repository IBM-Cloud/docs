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

**重要事項：{{site.data.keyword.amafull}} 服務取代為 {{site.data.keyword.appid_full}} 服務。**

# 啟用 Web 應用程式的 Facebook 鑑別
{: #facebook-auth-web}

在 {{site.data.keyword.amafull}} Web 應用程式上使用 Facebook 來鑑別使用者。新增 {{site.data.keyword.amashort}} 安全功能。

## 開始之前
{: #facebook-auth-android-before}
您必須具有：

* Web 應用程式。
* {{site.data.keyword.amashort}} 服務。如需相關資訊，請參閱[開始使用](index.html)。
* 最終重新導向的 URI（在授權處理程序完成之後）。


## 在 Facebook for Developers 網站上配置應用程式
{: #facebook-auth-config}

若要使用 Facebook 作為網站上的身分提供者，您必須在 Facebook 應用程式上新增及配置網站平台。

1. 在 [Facebook for Developers](https://developers.facebook.com) 網站上登入您的帳戶。
	如需建立新應用程式的相關資訊，請參閱[在 Facebook for Developers 網站上建立應用程式](facebook-auth-overview.html#facebook-appID)。
1. 記下**應用程式 ID** 及**應用程式密碼**。當您在 Mobile Client Access 儀表板中配置 Web 專案來進行 Facebook 鑑別時，會需要這些值。
1. 從**產品清單**中，選擇 **Facebook 登入**。
4. 新增 **Web** 平台（如果不存在）。
6. 在**有效 OAuth 重新導向 URI** 方框中，輸入授權伺服器回呼端點 URI。您可以在後續步驟中配置 {{site.data.keyword.amashort}} 服務之後，再新增此值。
7. 儲存變更。


## 配置 {{site.data.keyword.amashort}} 進行 Facebook 鑑別
{: #facebook-auth-config-ama}

您有了「Facebook 應用程式 ID」和「應用程式密碼」，並已配置 Facebook for Developers 應用程式來服務 Web 用戶端之後，即可在 {{site.data.keyword.amashort}} 儀表板中啟用 Facebook 鑑別。

1. 開啟 {{site.data.keyword.amashort}} 服務儀表板。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 展開 **Facebook** 區段。
1. 選取**新增 Facebook 至 Web 應用程式**。
5. 記下 **Facebook for Developers 的 Mobile Client Access 重新導向 URI** 文字框中的值。您需要在 Facebook Developers 入口網站的 **Facebook 登入**中，將此值新增至**有效 OAuth 重新導向 URI** 方框。
6. 輸入從 Facebook for Developers 網站取得的 Facebook **應用程式 ID** 和**應用程式密碼**。
7. 在**您的 Web 應用程式重新導向 URI** 中輸入重新導向 URI。此值適用於要在授權處理程序完成之後存取的重新導向 URI，並由開發人員決定。
8. 按一下**儲存**。


## 使用 Facebook 作為身分提供者來實作 {{site.data.keyword.amashort}} 授權流程
{: #facebook-auth-flow}

`VCAP_SERVICES` 環境變數是針對每一個 {{site.data.keyword.amashort}} 服務實例自動建立的，並且包含授權處理程序所需的內容。其由 JSON 物件組成，並可在 {{site.data.keyword.amashort}} 服務儀表板中的**服務認證**標籤中進行檢視。

若要開始授權處理程序，請執行下列動作：

1. 從 `VCAP_SERVICES` 環境變數中儲存的服務認證，擷取授權端點 (`authorizationEndpoint`) 及用戶端 ID (`clientId`)。

	`var cfEnv = require("cfenv");`

	**附註：**如果您在新增 Web 支援之前，已將 {{site.data.keyword.amashort}} 服務新增至應用程式，則在**服務認證**中可能沒有記號端點。請改用下列 URL（視 {{site.data.keyword.Bluemix_notm}} 地區而定）：

	美國南部：

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	倫敦：

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	雪梨：

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization`

2. 使用 `response_type("code")`、`client_id` 及 `redirect_uri` 作為查詢參數，來建置授權伺服器 URI。

3. 從您的 Web 應用程式重新導向至所產生的 URI。

	下列範例會擷取 `VCAP_SERVICES` 變數中的參數，並建置 URL，然後傳送重新導向要求。

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

	`redirect_uri` 參數是使用 Facebook 進行成功或不成功鑑別之後用於重新導向的 URI。   

	重新導向至授權端點之後，使用者將從 Facebook 取得登入表單。Facebook 授權使用者的身分之後，{{site.data.keyword.amashort}} 服務將呼叫您的 Web 應用程式重新導向 URI，並提供授權碼作為查詢參數。  


## 取得記號
{: #facebook-auth-tokens}

下一步是使用先前收到的授權碼，取得存取記號及身分記號：

1.  從 `VCAP_SERVICES` 環境變數中儲存的服務認證，擷取記號 `tokenEndpoint`、`clientId` 及 `secret`。

	**附註：**如果您已在新增 Web 支援之前使用 {{site.data.keyword.amashort}}，則在服務認證中可能沒有記號端點。請改用下列 URL（視 Bluemix 地區而定）：

	美國南部：

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	倫敦：

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	雪梨：

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. 將 POST 要求傳送至記號伺服器 URI，並以授權類型 ("authorization_code")、`clientId` 及您的重新導向 URI 作為表單參數。傳送 `clientId` 及 `secret` 作為基本 HTTP 鑑別認證。

	下列程式碼會擷取必要值，並透過 POST 要求傳送它們。

	```Java
	var cfEnv = require("cfenv");
	var base64url = require("base64url");
	var request = require('request');

	app.get("/oauth/callback", function(req, res, next) {
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
		var tokenEndpoint = mcaCredentials.tokenEndpoint;
		var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",
			// Your web application redirect uri
			code: req.query.code
		}

		request.post( {
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
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

	請注意，`redirect_uri` 參數必須符合前一個授權要求所使用的 `redirect_uri`。`code` 參數值應該是來自授權要求之回應中收到的授權碼。授權碼的有效時間只有 10 分鐘，過了此時間則必須擷取新的授權碼。

	回應內文將包含 JWT 格式的存取碼及記號 ITD（請參閱 [JWT 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://jwt.io/){: new_window}）。

	取得存取記號並收到身分記號之後，您就可以將 Web 階段作業標示為已鑑別，並可選擇性地持續保存這些記號。  

##使用取得的存取及身分記號
{: #facebook-auth-using-token}

身分記號包含使用者身分的相關資訊。若為 Facebook 鑑別，記號將包含使用者同意共用的所有資訊，例如完整名稱、年齡群組、人員資訊照片的 URL 等。  

存取記號可容許與受到 {{site.data.keyword.amashort}} 授權過濾器保護的資源進行通訊，請參閱[保護資源](protecting-resources.html)。

若要對受保護的資源提出要求，請將結構如下的授權標頭新增至要求：

`Authorization=Bearer <accessToken> <idToken>`

#### 提示
{: #tips}

* 您必須以空格區隔 `accessToken` 及 `idToken`。

* `idToken` 是選用項目。如果您未提供身分記號，則可以存取受保護的資源，但不會收到已授權使用者的任何相關資訊。
