---

copyright:
  years: 2015, 2016

---

# 建立自訂身分提供者
{: #custom-create}
若要建立自訂身分提供者，請開發可公開 RESTful API 的 Web 應用程式：

```
POST <base_url>/apps/<tenant_id>/<realm_name>/<request_type>
```

* `base_url`：指定自訂身分提供者 Web 應用程式的基本 URL。基本 URL 是要在 {{site.data.keyword.amashort}} 儀表板中登錄的 URL。
* `tenant_id`：指定承租戶的唯一 ID。{{site.data.keyword.amashort}} 呼叫此 API 時，一律會提供 {{site.data.keyword.Bluemix}} 應用程式 GUID (`applicationGUID`)。
* `realm_name`：指定 {{site.data.keyword.amashort}} 儀表板中所定義的自訂領域名稱。
* `request_type`：指定下列其中一項：
	* `startAuthorization`：指定鑑別處理程序的首要步驟。自訂身分提供者必須使用 "challenge"、"success" 或 "failure" 狀態進行回應。
	* `handleChallengeAnswer`：處理來自行動式用戶端的鑑別盤查回應。

## `startAuthorization` API
{: #custom-startauthorization}

`POST <base_url>/apps/<tenant_id>/<realm_name>/startAuthorization`

`startAuthorization` API 是用來作為鑑別處理程序的首要步驟。自訂身分提供者必須使用 "challenge"、"success" 或 "failure" 狀態進行回應。

為了容許鑑別處理程序的最大彈性，自訂身分提供者可以存取要求內文中行動式用戶端所傳送的所有 HTTP 標頭。標頭是以下列格式所提供：

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

自訂身分提供者可能會使用鑑別盤查進行回應，或直接使用 success 或 failure 進行回應。回應 HTTP 狀態必須是 `HTTP 200`，而且回應 JSON 必須包含下列內容：

* `status`：指定要求的 `success`、`challenge` 或 `failure`。
* `stateId`（選用）：指定隨機產生的字串 ID，以向行動式用戶端識別鑑別階段作業。如果自訂身分提供者未儲存任何狀態，則可以省略此屬性。
* `challenge`：指定 JSON 物件，這個 JSON 物件代表要傳回給行動式用戶端的鑑別盤查。只有在狀態設為 `challenge` 時才會將此屬性傳送至用戶端。
* `userIdentity`：指定 JSON 物件，這個 JSON 物件代表使用者身分。使用者身分是由 `userName`、`displayName` 及 `attributes` 這類內容所組成。如需相關資訊，請參閱[使用者身分物件](#custom-user-identity)。只有在狀態設為 `success` 時才會將此內容傳送至行動式用戶端。

例如：

```
{
	"status":"challenge",
	"stateId":"some-random-guid"
	"challenge":{
		message:"Enter username and password",
		attemptsLeft: 3
	}
}
```

## `handleChallengeAnswer` API
{: #custom-handleChallengeAnswer}

`POST <base_url>/apps/<tenant_id>/<realm_name>/handleChallengeAnswer`

`handleChallengeAnswer` API 處理來自行動式用戶端的鑑別盤查回應。與 `startAuthorization` API 相同，`handleChallengeAnswer` API 會使用 `challenge`、`success` 或 `failure` 狀態進行回應。

與 `startAuthorization` 要求類似，自訂身分提供者可以存取要求內文中行動式用戶端所傳送的所有 HTTP 標頭。除了行動式用戶端要求標頭之外，`handleChallengeAnswer` 要求的內文也會包括 `stateId` 及 `challengeAnswer` 內容。

### `handleChallengeAnswer` 要求內文範例
{: #custom-handleChallengeAnswer-example}

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
	},
    "stateId" : "123123123",
    "challengeAnswer" : {
    	"pinCode":12345
 	}
}
```

來自 `handleChallengeAnswer` API 的回應結構必須與 `startAuthorization` API 的回應相同。

## 使用者身分物件
{: #custom-user-identity}

對成功鑑別要求的回應必須包括具有下列屬性的使用者身分物件：
* `userName`：指定唯一的使用者名稱。
* `displayName`：指定使用者的顯示名稱。
* `attributes`（選用）：指定包含自訂使用者屬性的 JSON 物件。

### 使用者身分物件範例
{: #custom-user-identity-example}
```JavaScript
{
    "userName" : "janesmith",
    "displayName" : "Jane Smith",
    "attributes" : {
        "Language" : "French",
        "Country" : "Canada"
    }
}
```

{{site.data.keyword.amashort}} 服務利用使用者身分物件來產生 ID 記號，並作為授權標頭的一部分傳送給行動式用戶端。成功鑑別之後，行動式用戶端即具有使用者身分物件的完整存取權。

## 安全考量
{: #custom-security}

從 {{site.data.keyword.amashort}} 服務到自訂身分提供者的每一個要求都會包含授權標頭，讓自訂身分提供者可以驗證要求是來自授權來源。雖然未嚴格強制要求，但是請考慮使用 {{site.data.keyword.amashort}} Server SDK 檢測您的自訂身分提供者，來驗證授權標頭。若要使用此 SDK，自訂身分提供者應用程式必須使用 Node.js 或 Liberty for Java&trade;&trade; 進行實作，並在 {{site.data.keyword.Bluemix_notm}} 上執行。

授權標頭包含已觸發鑑別處理程序的行動式用戶端及行動式應用程式的相關資訊。您可以使用安全環境定義來擷取此資料。如需相關資訊，請參閱[保護資源](protecting-resources.html)。

## 自訂身分提供者範例實作
{: #custom-sample}
在您開發自訂身分提供者時，可以使用自訂身分提供者的下列任何 Node.js 範例實作作為參照。請從 GitHub 儲存庫下載完整應用程式碼。

* [簡式範例](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [進階範例](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

<!---
 ### JSON structure (simple sample)
{: #custom-sample-json}
This implementation assumes that the supplied authentication challenge answer is a JSON object with the following structure:

```
{
 	username: "my.username",
 	password: "my.password"
 }
 ```

### Custom identity provider sample code (simple sample)
{: #custom-sample-code}
```JavaScript
var express = require('express');
var cfenv = require('cfenv');
var log4js = require('log4js');
var jsonParser = require('body-parser').json();

// Using hardcoded user repository
var userRepository = {
	"john.lennon":      { password: "12345", displayName:"John Lennon", dob:"October 9, 1940"},
	"paul.mccartney":   { password: "67890", displayName:"Paul McCartney", dob:"June 18, 1942"},
	"ringo.starr":      { password: "abcde", displayName:"Ringo Starr", dob: "July 7, 1940"},
	"george.harrison":  { password: "fghij", displayName: "George Harrison", dob:"Feburary 25, 1943"}
}

var app = express();
var logger = log4js.getLogger("CustomIdentityProviderApp");
logger.info("Starting up");

app.post('/apps/:tenantId/:realmName/startAuthorization', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var headers = req.body.headers;

	logger.debug("startAuthorization", tenantId, realmName, headers);

	var responseJson = {
		status: "challenge",
		challenge: {
			text: "Enter username and password"
		}
	};

	res.status(200).json(responseJson);
});

app.post('/apps/:tenantId/:realmName/handleChallengeAnswer', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var challengeAnswer = req.body.challengeAnswer;


	logger.debug("handleChallengeAnswer", tenantId, realmName, challengeAnswer);

	var username = req.body.challengeAnswer["username"];
	var password = req.body.challengeAnswer["password"];

	var userObject = userRepository[username];

	var responseJson = { status: "failure" };

	if (userObject && userObject.password == password ){
		logger.debug("Login success for userId ::", username);
		responseJson.status = "success";
		responseJson.userIdentity = {
			userName: username,
			displayName: userObject.displayName,
			attributes: {
				dob: userObject.dob
			}
		}
	} else {
		logger.debug("Login failure for userId ::", username);
	}

	res.status(200).json(responseJson);
});

app.use(function(req, res, next){
	res.status(404).send("This is not the URL you're looking for");
});

var server = app.listen(cfenv.getAppEnv().port, function () {
	var host = server.address().address;
	var port = server.address().port;
	logger.info('Server listening at %s:%s', host, port);
});
```
--->

## 後續步驟
{: #next-steps}
* [配置 {{site.data.keyword.amashort}} 進行自訂鑑別](custom-auth-config-mca.html)
* [配置適用於 Android 的自訂鑑別](custom-auth-android.html)
* [配置適用於 iOS 的自訂鑑別](custom-auth-ios.html)
* [配置適用於 Cordova 的自訂鑑別](custom-auth-cordova.html)
