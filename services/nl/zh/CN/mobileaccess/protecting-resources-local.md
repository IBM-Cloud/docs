---

copyright:
  years: 2015, 2016

---

# 将 {{site.data.keyword.amashort}} 用于本地开发环境
{: #protecting-local}

您可以配置本地开发环境来使用在 {{site.data.keyword.Bluemix}} 上运行的 {{site.data.keyword.amashort}} 服务。具体而言，在使用本地开发服务器（例如，Node.js）开发服务器端代码时，您可以使用 {{site.data.keyword.amashort}} 服务器 SDK。

{{site.data.keyword.amashort}} 服务器 SDK 需要设置两个环境变量。在 {{site.data.keyword.Bluemix_notm}} 上开发服务器端代码时，{{site.data.keyword.Bluemix_notm}} 基础结构会提供这两个变量。

* `VCAP_SERVICES`：包含有关绑定到移动后端应用程序的服务的信息。
* `VCAP_APPLICATION`：包含有关移动后端应用程序的信息。

要将 {{site.data.keyword.amashort}} 用于本地开发服务器，必须手动添加这两个环境变量。

1. 打开通过 {{site.data.keyword.amashort}} 服务进行保护的移动后端的 {{site.data.keyword.Bluemix_notm}}“仪表板”。

1. 单击**移动选项**，然后复制 **AppGUID** 值。

1. 在本地开发环境中，设置 *VCAP_APPLICATION* 环境变量。此变量必须包含具有单个属性的字符串化 JSON 对象。
```JavaScript
{
    application_id: "appGUID"
}
```
将 *appGUID* 变量替换为**移动选项**字段中的值。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，单击移动后端应用程序中的 {{site.data.keyword.amashort}} 服务磁贴上的**显示凭证**。这将显示一个 JSON 对象，其中带有 {{site.data.keyword.amashort}} 向移动后端应用程序提供的访问凭证。

1. 在本地开发环境中，设置 `VCAP_SERVICES` 环境变量。此变量的值必须是包含 {{site.data.keyword.amashort}} 凭证的字符串化 JSON 对象。请参阅以下样本以获取更多信息。

## 样本代码
{: #local-dev-sample}

要在本地 Node.js 开发环境中使用 {{site.data.keyword.amashort}} 服务，请在需要 `bms-mca-token-validation-strategy` 模块之前，添加以下代码。

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
将代码中的 *appGUID* 值替换为移动后端的 *appGUID* 值。


## 将移动应用程序配置为使用本地开发服务器
{: #configuring-local}

使用 {{site.data.keyword.Bluemix_notm}} 应用程序的真实 URL 初始化 {{site.data.keyword.amashort}} 客户端 SDK，并在每个请求中使用 localhost（或 IP 地址）。请参阅以下样本。

您可能需要在以下示例中将 `localhost` 更改为开发服务器的实际 IP 地址。

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

request.send(success, failure);```

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

IMFResourceRequest* request = [IMFResourceRequest

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
