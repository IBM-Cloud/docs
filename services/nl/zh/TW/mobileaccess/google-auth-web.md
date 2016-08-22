---

copyright:
  year: 2016

---

# 啟用 Web 應用程式的 Google 鑑別
{: #google-auth-web}

*前次更新：2016 年 7 月 18 日*
{: .last-updated}

在 Web 應用程式上使用「Google 登入」來鑑別使用者。


## 開始之前
{: #before-you-begin}

您必須具有：
* Web 應用程式。
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。




* 最終重新導向的 URI（在授權處理程序完成之後）。



## 配置網站的 Google 應用程式
若要開始使用 Google 作為身分提供者，請在 [Google Developer Console](https://console.developers.google.com) 中建立專案。
建立專案的一部分是取得 **Google 用戶端 ID** 及**密碼**。「Google 用戶端 ID」和「密碼」是 Google 鑑別所使用之您的應用程式的唯一 ID，並且是設定 {{site.data.keyword.amashort}} 儀表板的必要項目。


1. 在「Google 開發人員主控台」中，開啟 Google 應用程式。 
3. 新增 Google+ API。 
3. 使用 OAuth 建立認證。在應用程式類型中選取 Web 應用程式。在「授權重新導向 URI」方框中輸入 {{site.data.keyword.amashort}} 重新導向 URI。{{site.data.keyword.amashort}} 重新導向授權 URI 可從 {{site.data.keyword.amashort}} 儀表板的 Google 配置畫面中取得（請參閱下列步驟）。 
6. 儲存變更。記下「Google 用戶端 ID」及「應用程式密碼」。


## 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
有了「Google 應用程式 ID」和「密碼」之後，即可在 {{site.data.keyword.amashort}} 儀表板中啟用 Google 鑑別。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。
1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。
1. 按一下 Google 畫面上的按鈕。
1. 在**為 Web 進行配置**區段中，請執行下列動作：   
    * 記下 **Google 開發人員主控台的 Mobile Client Access 重新導向 URI** 文字框中的值。這是您需要新增至**授權重新導向 URI** 方框的值，此方框位於上述步驟 3 中 **Google 開發者入口網站**的**用戶端 ID 中針對 Web 應用程式的限制**中。
    * 輸入 **Google 應用程式 ID** 及**用戶端密碼**。
    * 在**您的 Web 應用程式重新導向 URI** 中輸入重新導向 URI。此值適用於要在授權處理程序完成之後存取的重新導向 URI，並由開發人員決定。
1. 按一下**儲存**。


## 使用 Google 作為身分提供者來實作 {{site.data.keyword.amashort}} 授權流程

`VCAP_SERVICES` 環境變數是針對每一個 {{site.data.keyword.amashort}} 服務實例自動建立的，並且包含授權處理程序所需的內容。其由 JSON 物件組成。若要檢視它，請按一下應用程式的左側導覽器中的**環境變數**。

若要啟動授權處理程序，請執行下列動作：

1. 從 `VCAP_SERVICES` 環境變數中儲存的服務認證，擷取授權端點 (`authorizationEndpoint`) 及用戶端 ID (`clientId`)。 

    **附註：**若在新增 Web 支援之前建立 {{site.data.keyword.amashort}} 服務，則在服務認證中您可能沒有授權端點。在此情況下，請使用下列授權端點，視您的 Bluemix 地區而定：


 	美國南部： 
 	```
 	https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization
 	```
 	倫敦：
 	```
 	https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
  	```
  	雪梨：
  	```
  	https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization
  	```
1. 使用 `response_type("code")`、`client_id` 及 `redirect_uri` 作為查詢參數，來建置授權伺服器 URI。
1. 從您的 Web 應用程式重新導向至產生的 URI。
  
下列範例會擷取 `VCAP_SERVICES` 變數中的參數、建置 URL，然後傳送重新導向要求。
  
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

請注意，`redirect_uri` 參數代表您的 Web 應用程式重新導向 URI，而且必須等於 {{site.data.keyword.amashort}} 儀表板中定義的 URI。
在重新導向至授權端點之後，使用者將從 Google 取得登入表單。在使用者授與可使用其 Google 身分進行登入的許可權之後，{{site.data.keyword.amashort}} 服務將呼叫您的 Web 應用程式重新導向 URI，並提供授權碼作為查詢參數。

## 取得記號
下一步是使用先前收到的授權碼，取得存取記號及身分記號。為了能夠這樣做，請執行下列動作： 

1. 從 `VCAP_SERVICES` 環境變數中儲存的服務認證，擷取記號 `tokenEndpoint`、`clientId` 及 `secret`。 
  
    **附註：**若在新增 Web 支援之前建立 {{site.data.keyword.amashort}} 服務，則在服務認證中您可能沒有授權端點。在此情況下，請使用下列授權端點，視您的 Bluemix 地區而定：
 
 	美國南部： 
 	```
 	https:// mobileclientaccess.ng.bluemix.net/oauth/v2/token 
  	```
 	倫敦：
  	```
  	https:// mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token  
   	```
   	雪梨：
  	```
   	https:// mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
  	```

2. 將 POST 要求傳送至記號伺服器 URI，並以 grant_type ("authorization_code")、client_id、redirect_uri 及 code 作為表單參數。傳送 `clientId` 及 `clientSecret` 作為基本 HTTP 鑑別認證。
 
下列程式碼會擷取必要值，並透過 POST 要求傳送它們。
    
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
		redirect_uri: "http://some-server/oauth/callback",// Your web application redirect uri 
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

  `redirect_uri` 參數是使用 Google+ 進行成功或失敗鑑別之後用於重新導向的 URI，而且必須符合來自步驟 1 的 `redirect_uri`。  
   
確定在 10 分鐘內傳送此 POST 要求，在此時間後授權碼將到期。10 分鐘之後，需要新的授權碼。

POST 回應內文將包含以 base64 編碼的 `access_token` 及 `id_token`。

在收到存取及識別記號之後，您就可以將 Web 階段作業標示為已鑑別，並可選擇性地持續保存這些記號。  


##使用取得的存取及身分記號 

身分記號包含使用者身分的相關資訊。若為 Google 鑑別，記號將包含使用者同意共用的所有資訊，例如完整名稱、人員資訊照片的 URL 等。  

存取記號可啟用與受到 {{site.data.keyword.amashort}} 授權過濾器保護的資源進行通訊，請參閱[保護資源](protecting-resources.html)。


若要對受保護的資源提出要求，請將結構如下的授權標頭新增至要求： 

`Authorization=Bearer <accessToken> <idToken>`

**附註：** 

* `accessToken` 及 `idToken` 必須以空格區隔。

* `idToken` 是選用項目。如果您未提供身分記號，則受保護的資源可被他人存取，但不會收到已獲授權之使用者的任何相關資訊。 



