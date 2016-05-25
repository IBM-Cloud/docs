---

copyright:
  years: 2015, 2016

---

# 로컬 개발 환경에서 {{site.data.keyword.amashort}} 사용
{: #protecting-local}

{{site.data.keyword.Bluemix}}에서 실행 중인 {{site.data.keyword.amashort}} 서비스를 사용하도록 로컬 개발 환경을 구성할 수 있습니다. 특히, Node.js와 같은 로컬 개발 서버를 사용하여 서버 측 코드를 개발하는 경우 {{site.data.keyword.amashort}} 서버 SDK를 사용할 수 있습니다. 

{{site.data.keyword.amashort}} 서버 SDK는 환경 변수가 설정되어 있어야 합니다. {{site.data.keyword.Bluemix_notm}}에서 서버 측 코드를 개발 중인 경우 {{site.data.keyword.Bluemix_notm}} 인프라에서 해당 변수를 제공합니다. 

* `VCAP_SERVICES`: 모바일 백엔드 애플리케이션에 바인드되는 서비스에 대한 정보를 포함합니다. 
* `VCAP_APPLICATION`: 모바일 백엔드 애플리케이션에 대한 정보를 포함합니다. 

로컬 개발 서버를 사용하여 {{site.data.keyword.amashort}}를 사용하려면, 해당 환경 변수를 수동으로 추가해야 합니다. 

1. {{site.data.keyword.amashort}} 서비스를 사용하여 보호되는 모바일 백엔드의 {{site.data.keyword.Bluemix_notm}} 대시보드를 여십시오. 

1. **모바일 옵션**을 클릭하고 **AppGUID** 값을 복사하십시오. 

1. 로컬 개발 환경에 *VCAP_APPLICATION* 환경 변수를 설정하십시오. 변수는 단일 특성이 설정되어 있으며 문자열로 변환된 JSON 오브젝트를 포함해야 합니다.
```JavaScript
{
    application_id: "appGUID"
}
```
*appGUID* 변수를 **모바일 옵션** 필드의 값으로 대체하십시오. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 모바일 백엔드 애플리케이션의 {{site.data.keyword.amashort}} 서비스 타일에 있는 **신임 정보 표시**를 클릭하십시오. JSON 오브젝트는 {{site.data.keyword.amashort}}에서 모바일 백엔드 애플리케이션에 제공하는 액세스 신임 정보와 함께 표시됩니다. 

1. 로컬 개발 환경에서 `VCAP_SERVICES` 환경 변수를 설정하십시오. 이 변수의 값은 {{site.data.keyword.amashort}} 신임 정보를 포함하는 문자열로 변환된 JSON 오브젝트여야 합니다. 자세한 정보는 다음 샘플을 참조하십시오. 

## 샘플 코드
{: #local-dev-sample}

로컬 Node.js 개발 환경에서 {{site.data.keyword.amashort}} 서비스를 사용하려면, `bms-mca-token-validation-strategy` 모듈을 요청하기 전에 다음 코드를 추가하십시오. 

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

// 코드의 나머지 부분
```
코드에서 *appGUID* 값을 모바일 백엔드 *appGUID* 값으로 모두 대체하십시오. 


## 로컬 개발 서버에 대해 작업할 수 있도록 모바일 애플리케이션 구성
{: #configuring-local}

{{site.data.keyword.Bluemix_notm}} 애플리케이션의 실제 URL로 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하고 각 요청에서 localhost(또는 IP 주소)를 사용하십시오. 다음 샘플을 참조하십시오. 

다음 예제에서 `localhost`를 개발 서버의 실제 IP 주소로 변경해야 할 수 있습니다. 

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
