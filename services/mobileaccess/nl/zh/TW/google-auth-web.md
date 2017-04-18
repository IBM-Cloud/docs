---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 啟用 Web 應用程式的 Google 鑑別
{: #google-auth-web}

在 Web 應用程式上使用「Google 登入」來鑑別使用者。新增 {{site.data.keyword.amafull}} 安全功能。


## 開始之前
{: #before-you-begin}

您必須具有：

* Web 應用程式。
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。




* 最終重新導向的 URI（在授權處理程序完成之後）。


## 配置網站的 Google 應用程式
{: #google-auth-config}

若要開始使用 Google 作為身分提供者，請在 [Google Developer Console ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.developers.google.com "外部鏈結圖示"){: new_window} 中建立專案。建立專案的一部分是取得 **Google 用戶端 ID** 及**密碼**。「Google 用戶端 ID」和「密碼」是 Google 鑑別所使用之您的應用程式的唯一 ID，並且是設定 {{site.data.keyword.amashort}} 儀表板的必要項目。

1. 在 Google Developer Console 中，開啟 Google 應用程式。
3. 新增 **Google+** API。
3. 使用 OAuth 建立認證。在應用程式類型中選取 Web 應用程式。在「授權重新導向 URI」方框中輸入 {{site.data.keyword.amashort}} 重新導向 URI。從 {{site.data.keyword.amashort}} 儀表板的 Google 配置畫面中取得 {{site.data.keyword.amashort}} 重新導向授權 URI（請參閱下列步驟）。
4. 儲存變更。請記下 **Google 用戶端 ID** 和**應用程式密碼**。


## 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
{: #google-auth-config-ama}

有了「Google 應用程式 ID」和「密碼」之後，即可在 {{site.data.keyword.amashort}} 儀表板中啟用 Google 鑑別。

1. 開啟 {{site.data.keyword.amashort}} 服務儀表板。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 開啟 **Google** 區段。
1. 勾選**新增 Google 至 Web 應用程式**。
4. 在**為 Web 進行配置**區段中，請執行下列動作：   
    * 記下 **Google Developer Console 的 Mobile Client Access 重新導向 URI** 文字框中的值。這是您需要新增至**授權重新導向 URI** 方框的值，此方框位於 **Google 開發人員入口網站**的 **Web 應用程式用戶端 ID 的限制**中。
    * 輸入**用戶端 ID** 和**用戶端密碼**。
    * 在**您的 Web 應用程式重新導向 URI** 中輸入重新導向 URI。此值適用於要在授權處理程序完成之後存取的重新導向 URI，並由開發人員決定。
5. 按一下**儲存**。


## 使用 Google 作為身分提供者來實作 {{site.data.keyword.amashort}} 授權流程
{: #google-auth-flow}

`VCAP_SERVICES` 環境變數是針對每一個 {{site.data.keyword.amashort}} 服務實例自動建立的，並且包含授權處理程序所需的內容。其由 JSON 物件組成，按一下 {{site.data.keyword.amashort}} 服務儀表板中的**服務認證**標籤，即可進行檢視。

若要開始授權處理程序，請執行下列動作：

1. 從 `VCAP_SERVICES` 環境變數中儲存的服務認證，擷取授權端點 (`authorizationEndpoint`) 及用戶端 ID (`clientId`)。

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**附註：**如果您在新增 Web 支援之前，已將 {{site.data.keyword.amashort}} 服務新增至應用程式，則在服務認證中可能沒有記號端點。請改用下列 URL（視 {{site.data.keyword.Bluemix_notm}} 地區而定）：

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
	});

	app.get("/protected", checkAuthentication, function(req, res, next) {
		res.send("Hello from protected endpoint");
		function checkAuthentication(req, res, next) {

			// Check if user is authenticated
			if (req.session.userIdentity) {
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
	   	}
       }
	```
	{: codeblock}

	請注意，`redirect_uri` 參數代表您的 Web 應用程式重新導向 URI，而且必須等於 {{site.data.keyword.amashort}} 儀表板中定義的 URI。

	重新導向至授權端點之後，使用者將從 Google 取得登入表單。使用者授與使用其 Google 身分進行登入的許可權之後，{{site.data.keyword.amashort}} 服務會提供授權碼作為查詢參數，以呼叫您的 Web 應用程式重新導向 URI。

## 取得記號
{: #google-auth-tokens}

下一步是使用先前收到的授權碼，取得存取記號及身分記號。

1. 從 `VCAP_SERVICES` 環境變數中所儲存的服務認證，擷取記號 `tokenEndpoint`、`clientId` 及 `secret`。

	**附註：**如果您在新增 Web 支援之前，已使用 {{site.data.keyword.amashort}}，則在服務認證中可能沒有記號端點。請改用下列 URL（視 Bluemix 地區而定）：

	美國南部：

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	倫敦：

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	雪梨：

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. 將 POST 要求傳送至記號伺服器 URI，並以 grant_type ("authorization_code")、client_id、redirect_uri 及 code 作為表單參數。傳送 `clientId` 及 `clientSecret` 作為基本 HTTP 鑑別認證。

	下列程式碼會擷取必要值，並透過 POST 要求傳送它們。

	```Java
	var cfEnv = require("cfenv");
	var base64url = require("base64url ");
	var request = require('request');

	app.get("/oauth/callback", function(req, res, next) {
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

	`redirect_uri` 參數是使用 Google+ 進行成功或失敗鑑別之後用於重新導向的 URI，而且必須符合 {{site.data.keyword.amashort}} 儀表板中定義的 `redirect_uri`。  

	確定在 10 分鐘內傳送此 POST 要求，在此時間後授權碼將到期。10 分鐘之後，需要新的授權碼。

	POST 回應內文會包含以 base64 編碼的 `access_token` 及 `id_token`。

	收到存取權和身分記號之後，您可以將 Web 階段作業標示為已鑑別，並可選擇持續保存這些記號。  


## 使用取得的存取及身分記號
{: #google-auth-using-token}

身分記號包含使用者身分的相關資訊。若為 Google 鑑別，記號會包含使用者同意共用的所有資訊，例如完整名稱、人員資訊照片的 URL 等。  

存取記號會啟用與 {{site.data.keyword.amashort}} 授權過濾器所保護的資源進行通訊。請閱讀[保護資源](protecting-resources.html)。

若要對受保護的資源提出要求，請將結構如下的授權標頭新增至要求：

`Authorization=Bearer <accessToken> <idToken>`

#### 提示：
{: #tips}

* `accessToken` 及 `idToken` 必須以空格區隔。

* `idToken` 是選用項目。如果您未提供身分記號，則可以存取受保護的資源，但不會收到已授權使用者的任何相關資訊。
