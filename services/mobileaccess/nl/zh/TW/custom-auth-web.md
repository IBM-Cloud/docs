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

#配置適用於 {{site.data.keyword.amashort}} Web 應用程式的自訂鑑別
{: #custom-web}

將自訂鑑別及 {{site.data.keyword.amafull}} 安全功能新增至 Web 應用程式。

## 開始之前
{: #before-you-begin}

開始之前，您必須具有：

* Web 應用程式。
* 配置為使用自訂身分提供者之 {{site.data.keyword.amashort}} 服務實例所保護的資源（請參閱[配置自訂鑑別](custom-auth-config-mca.html)）。  
* **承租戶 ID** 值。在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* **領域**名稱。這是您在 {{site.data.keyword.amashort}} 儀表板的**管理**標籤上，**自訂**區段內的**領域名稱**欄位中指定的值。
* 後端應用程式的 URL（**應用程式路徑**）。在傳送要求至後端應用程式的受保護端點時，將需要此值。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`雪梨`或`英國`，並對應至 Javascript 程式碼中所需的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_SYDNEY` 或 `BMSClient.REGION_UK`。您需要此值來起始設定 {{site.data.keyword.amashort}} 用戶端。
* 最終重新導向的 URI（在授權處理程序完成之後）。這是您在**管理**標籤的**自訂**區段中輸入的**您的 Web 應用程式重新導向 URI** 值。

如需相關資訊，請參閱：

* [開始使用 {{site.data.keyword.amashort}}](getting-started.html)
* [使用自訂身分提供者](custom-auth.html)
* [建立自訂身分提供者](custom-auth-identity-provider.html)
* [配置 {{site.data.keyword.amashort}} 進行自訂鑑別](custom-auth-config-mca.html)


##配置自訂身分提供者
{: #custom-auth-config}

建立自訂身分提供者時，您必須定義 POST 方法，其中包含結構如下的路徑：

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` 是 URL 參數，而 `<your-realm-name>` 是您選擇的任何領域名稱。

要求內文將包含 `challengeAnswer` 物件，其包含 `username` 及 `password`。


驗證使用者之後，此路徑必須傳回結構如下的 JSON 物件。

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

**附註：**`attributes` 是選用欄位。

下列程式碼示範這類 POST 要求。

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


##配置 {{site.data.keyword.amashort}} 進行自訂鑑別
{: #custom-auth-config-mca}

配置您的自訂身分提供者之後，您可以在 {{site.data.keyword.amashort}} 儀表板中啟用自訂鑑別。

1. 在 {{site.data.keyword.amashort}} 儀表板中，開啟服務。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 展開**自訂**區段。
1. 輸入**領域名稱**、**自訂身分提供者 URL**。
1. 輸入**您的 Web 應用程式重新導向 URI** 值。這是授權成功之後，最終重新導向的 URI。
1. 按一下**儲存**。


##使用自訂身分提供者實作 {{site.data.keyword.amashort}} 授權流程
{: #custom-auth-flow}

`VCAP_SERVICES` 環境變數是針對每一個 {{site.data.keyword.amashort}} 服務實例自動建立的，並且包含授權處理程序所需的內容。其由 JSON 物件組成，您可以在 {{site.data.keyword.amashort}} 儀表板的**服務認證**標籤中進行檢視。

若要要求使用者授權，請將瀏覽器重新導向至授權伺服器端點。為了能夠這樣做，請執行下列動作：

1. 從 `VCAP_SERVICES` 環境變數中儲存的服務認證，擷取授權端點 (`authorizationEndpoint`) 及用戶端 ID (`clientId`)。

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**附註：**如果您已在新增 Web 支援之前將 {{site.data.keyword.amashort}} 服務新增至應用程式，則在服務認證中可能沒有記號端點。請改用下列 URL（視 {{site.data.keyword.Bluemix_notm}} 地區而定）：

	美國南部：

	`  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization 
  `

	  倫敦：
  

	` https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
   `

	  雪梨：
  

	`  https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization 
  `

2. 使用 `response_type("code")`、`client_id` 及 `redirect_uri` 作為查詢參數，來建置授權伺服器 URI。  

3. 從您的 Web 應用程式重新導向至所產生的 URI。

   下列範例會擷取 `VCAP_SERVICES` 變數中的參數、建置 URL，然後傳送重新導向要求。

	```Java
var cfEnv = require("cfenv"); 
app.get("/protected", checkAuthentication, function(req, res, next){ 
  res.send("Hello from protected endpoint"); 
  }
);

	function checkAuthentication(req, res, next){ 
  // Check if user is authenticated 
  if (req.session.userIdentity){ 
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

	請注意，`redirect_uri` 參數代表您的 Web 應用程式重新導向 URI，而且必須等於 {{site.data.keyword.amashort}} 儀表板中定義的 URI。  

	`state` 參數可與要求一起傳遞。此參數將傳播至自訂身分提供者 POST 方法，而且可從要求內文 (`req.body.stateId`) 存取。  

	重新導向至授權端點之後，使用者將取得登入表單。使用自訂身分提供者鑑別使用者的認證之後，{{site.data.keyword.amashort}} 服務會呼叫您的 Web 應用程式重新導向 URI，以提供授權碼作為查詢參數。  

	重新導向之後，使用者將取得登入表單。自訂身分提供者鑑別使用者的認證之後，{{site.data.keyword.amashort}} 服務會呼叫 Web 應用程式重新導向 URI，以提供授權碼作為查詢參數。

##取得記號
{: custom-auth-tokens}

下一步是使用先前收到的授權碼，取得存取記號及身分記號。為了能夠這樣做，請執行下列動作：

1. 從 `VCAP_SERVICES` 環境變數中儲存的服務認證，擷取 `authorizationEndpoint`、`clientId` 及 `secret`。

	**附註：**如果您在新增 Web 支援之前，已將 {{site.data.keyword.amashort}} 服務新增至應用程式，則在服務認證中可能沒有記號端點。請改用下列 URL（視 {{site.data.keyword.Bluemix_notm}} 地區而定）：

	美國南部：

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	倫敦：

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	雪梨：

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. 將 POST 要求傳送至記號伺服器 URI，並以 `grant_type`、`client_id`、`redirect_uri` 及 `code` 作為表單參數，同時以 `clientId` 及 `secret` 作為「基本」HTTP 鑑別認證。

	下列範例程式碼會擷取必要值，並透過 POST 要求傳送它們。

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

	請注意，`redirect_uri` 參數必須符合先前的授權要求中所使用的 `redirect_uri`。code 參數值應該是授權要求結束時的回應中收到的授權碼。授權碼的有效時間只有 10 分鐘，過了此時間您將需要取得新的授權碼。

	回應內文將包含 JWT 格式的 `access_token` 及 `id_token`。請參閱 [JWT 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://jwt.io "外部鏈結圖示"){: new_window}。

	收到存取權和身分記號之後，您可以將 Web 階段作業標示為已鑑別，並可選擇持續保存這些記號。


##使用取得的存取及身分記號
{: #custom-auth-using-token}

身分記號包含使用者身分的相關資訊。若為自訂鑑別，記號將包含自訂身分提供者在鑑別時所傳回的所有資訊。在 `imf.user` 欄位下，欄位 `displayName` 將包含自訂身分提供者所傳回的 `displayName`，而欄位 `id` 將包含 `userName`。`imf.user` 下的欄位 `attributes` 內會傳回自訂身分提供者所傳回的所有其他值。  

存取記號容許與 {{site.data.keyword.amashort}} 授權過濾器所保護的資源進行通訊（請參閱[保護資源](protecting-resources.html)）。若要對受保護的資源提出要求，請將結構如下的授權標頭新增至要求：

`Authorization=Bearer <accessToken> <idToken>`

####提示：
{: #tips_token}

* `<accessToken>` 及 `<idToken>` 必須以空格區隔。

* 身分記號是選用項目。如果您未提供身分記號，則可以存取受保護的資源，但不會收到已授權使用者的任何相關資訊。
