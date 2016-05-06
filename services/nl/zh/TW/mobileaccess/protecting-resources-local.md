---

copyright:
  years: 2015, 2016

---

# 搭配使用 {{site.data.keyword.amashort}} 與本端開發環境
{: #protecting-local}

您可以配置本端開發環境來使用在 {{site.data.keyword.Bluemix}} 上執行的 {{site.data.keyword.amashort}} 服務。特別的是，當您使用本端開發伺服器來開發伺服器端程式碼（例如 Node.js）時，可以使用 {{site.data.keyword.amashort}} Server SDK。

{{site.data.keyword.amashort}} Server SDK 需要設定兩個環境變數。在 {{site.data.keyword.Bluemix_notm}} 上開發伺服器端程式碼時，這些變數是由 {{site.data.keyword.Bluemix_notm}} 基礎架構所提供。

* `VCAP_SERVICES`：包含連結至行動式後端應用程式之服務的相關資訊。
* `VCAP_APPLICATION`：包含行動式後端應用程式的相關資訊。

若要搭配使用 {{site.data.keyword.amashort}} 與本端開發伺服器，您必須手動新增這些環境變數。

1. 開啟使用 {{site.data.keyword.amashort}} 服務所保護之行動式後端的 {{site.data.keyword.Bluemix_notm}} 儀表板。

1. 按一下**行動式選項**，並複製 **AppGUID** 值。

1. 在本端開發環境中，設定 *VCAP_APPLICATION* 環境變數。此變數必須包含具有單一內容的字串化 JSON 物件。
```JavaScript
{
    application_id: "appGUID"
}
```
請將 *appGUID* 變數取代為**行動式選項**欄位中的值。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板的行動式後端應用程式中，按一下 {{site.data.keyword.amashort}} 服務磚上的**顯示認證**。即會顯示 JSON 物件與 {{site.data.keyword.amashort}} 提供給行動式後端應用程式的存取認證。

1. 在本端開發環境中，設定 `VCAP_SERVICES` 環境變數。此變數的值必須是包含 {{site.data.keyword.amashort}} 認證的字串化 JSON 物件。如需相關資訊，請參閱下列範例。

## 範例程式碼
{: #local-dev-sample}

若要在本端 Node.js 開發環境中使用 {{site.data.keyword.amashort}} 服務，請先新增下列程式碼，再要求 `bms-mca-token-validation-strategy` 模組。

```JavaScript
var vcapApplication = {
	application_id:"appGUID"
};

var vcapServices = {
	"AdvancedMobileAccess": [
		{
			"credentials": {
				"admin_url": "https://mobile.ng.bluemix.net/imfmobileplatformdashboard/?appGuid=appGUID",
				"clientId": "appGUID",
				"secret": "secret",
				"serverUrl": "https://imf-authserver.ng.bluemix.net/imf-authserver",
				"tenantId": "appGUID"
			}
		}
	]
};

process.env["VCAP_APPLICATION"] = JSON.stringify(vcapApplication);
process.env["VCAP_SERVICES"] = JSON.stringify(vcapServices);

var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Rest of your code
```
請將程式碼中出現的 *appGUID* 值取代為行動式後端 *appGUID* 值。


## 配置行動式應用程式以使用本端開發伺服器
{: #configuring-local}

使用 {{site.data.keyword.Bluemix_notm}} 應用程式的實際 URL 來起始設定 {{site.data.keyword.amashort}} Client SDK，並在每一個要求中使用 localhost（或 IP 位址）。請參閱下列範例。

您可能需要將 `localhost` 變更為下列範例中開發伺服器的實際 IP 位址。

### Android

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID);

Request request =
			new Request(baseRequestUrl + "/resource/path", Request.GET);

request.send(this, new ResponseListener() {
	@Override
	public void onSuccess (Response response) {
		Log.d("Myapp", "onSuccess :: " + response.getResponseText());
	}
	@Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
		if (null != t) {
			Log.d("Myapp", "onFailure :: " + t.getMessage());
		} else if (null != extendedInfo) {
			Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
		} else {
			Log.d("Myapp", "onFailure :: " + response.getResponseText());
		}
	}
});
```
### Cordova

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";

BMSClient.initialize(bluemixAppRoute, bluemixAppGUID);

var success = function(data){
   	console.log("success", data);
}

var failure = function(error){
	console.log("failure", error);
}

var request = new MFPRequest(baseRequestUrl +
							"/resource/path", MFPRequest.GET);

request.send(success, failure);
```

### iOS - Objective C

```Objective-C
NSString *baseRequestUrl = @"http://localhost:3000";
NSString *bluemixAppRoute = @"http://myapp.mybluemix.net";
NSString *bluemixAppGUID = @"your-bluemix-app-guid";

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];

NSString *requestPath = [NSString stringWithFormat:@"%@/resource/path",
								baseRequestUrl];

IMFResourceRequest *request =  [IMFResourceRequest
				requestWithPath:requestPath
				method:@"GET"];

[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
	if (error){
		NSLog(@"Error :: %@", [error description]);
	} else {
		NSLog(@"Response :: %@", [response responseText]);
	}
}];
```

### iOS - Swift

```Swift
let baseRequestUrl = "http://localhost:3000";
let bluemixAppRoute = "http://myapp.mybluemix.net";
let bluemixAppGUID = "your-bluemix-app-guid";

IMFClient.sharedInstance().initializeWithBackendRoute(bluemixAppRoute,
	 							backendGUID: bluemixAppGuid)

let requestPath = baseRequestUrl + "/resource/path"

let request = IMFResourceRequest(path: requestPath, method: "GET");

request.sendWithCompletionHandler { (response, error) -> Void in
	if (nil != error){
		NSLog("Error :: %@", error.description)
	} else {
		NSLog("Response :: %@", response.responseText)
	}
};

```
