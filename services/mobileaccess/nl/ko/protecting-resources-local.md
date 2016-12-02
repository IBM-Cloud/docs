---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---
{:shortdesc: .shortdesc}

# 로컬 개발 환경에서 {{site.data.keyword.amashort}} 사용
{: #protecting-local}

{{site.data.keyword.Bluemix}}에서 실행 중인 {{site.data.keyword.amafull}} 서비스를 사용하도록 로컬 개발을 구성할 수 있습니다. 특히, {{site.data.keyword.amashort}} 서버 SDK를 사용하여 로컬로 코드를 개발하고 {{site.data.keyword.amashort}} 요청을 개발 서버에 전송할 수 있습니다. 이러한 요청은 {{site.data.keyword.Bluemix}}에서 실행 중인 {{site.data.keyword.amashort}} 서비스에서 보호합니다. 

## 시작하기 전에
{: #before-you-begin}

다음이 있어야 합니다.
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.
* 서비스 매개변수 값. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. **모바일 옵션**을 클릭하십시오. `applicationRoute` 값과 `appGUID`(`tenantId`라고도 함) 값이 **라우트** 필드와 **앱 GUID/TenantId** 필드에 표시됩니다. 이들 값은 SDK를 초기화하고 백엔드 애플리케이션에 요청을 보내는 데 필요합니다. 
*  {{site.data.keyword.Bluemix_notm}} 애플리케이션이 호스팅되는 지역을 찾으십시오. {{site.data.keyword.Bluemix_notm}} 지역을 보려면 메뉴 표시줄의 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘")을 클릭하여 **계정 및 지원** 위젯을 여십시오. 지역 값은 **미국 남부**, **시드니** 또는 **영국** 중 하나여야 합니다. 이들 이름에 해당하는 정확한 SDK 상수 값은 코드 예제에 표시되어 있습니다. 

## 서버 SDK 설정
{: #serversetup}

{{site.data.keyword.amashort}} 서버 SDK는 두 개의 환경 변수가 설정되어 있어야 합니다. {{site.data.keyword.Bluemix_notm}}에서 서버 측 코드를 개발 중인 경우 {{site.data.keyword.Bluemix_notm}} 인프라에서 해당 변수를 제공합니다. 

* `VCAP_SERVICES`: 모바일 백엔드 애플리케이션에 바인드되는 서비스에 대한 정보를 포함합니다. 
* `VCAP_APPLICATION`: 모바일 백엔드 애플리케이션에 대한 정보를 포함합니다. 

로컬 개발 서버를 사용하여 {{site.data.keyword.amashort}}를 사용하려면, 해당 환경 변수를 수동으로 추가해야 합니다. 

1. {{site.data.keyword.amashort}} 서비스로 보호되는 모바일 백엔드 애플리케이션의 {{site.data.keyword.Bluemix_notm}} 대시보드를 여십시오. 

1. 로컬 개발 환경에 *VCAP_APPLICATION* 환경 변수를 설정하십시오. 변수는 단일 특성이 설정되어 있으며 문자열로 변환된 JSON 오브젝트를 포함해야 합니다. 
```JavaScript
{
    application_id: "appGUID"
}
```

*appGUID* 값을 [시작하기 전에](#before-you-begin)에서 얻은 `appGUID` 값으로 바꾸십시오. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 모바일 백엔드 애플리케이션의 {{site.data.keyword.amashort}} 서비스 타일에 있는 **신임 정보 표시**를 클릭하십시오. JSON 오브젝트는 {{site.data.keyword.amashort}}에서 모바일 백엔드 애플리케이션에 제공하는 액세스 신임 정보와 함께 표시됩니다. 

1. 로컬 개발 환경에서 `VCAP_SERVICES` 환경 변수를 설정하십시오. 이 변수의 값은 {{site.data.keyword.amashort}} 신임 정보를 포함하는 문자열로 변환된 JSON 오브젝트여야 합니다. 자세한 정보는 다음 샘플을 참조하십시오. 

## 샘플 서버 코드
{: #local-dev-sample}

로컬 Node.js 개발 환경에서 {{site.data.keyword.amashort}} 서비스를 사용하려면, 다음 코드를 추가하십시오.   

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
				"tenantId": "tenantId"
			}
		}
	]
};

process.env["VCAP_APPLICATION"] = JSON.stringify(vcapApplication);
process.env["VCAP_SERVICES"] = JSON.stringify(vcapServices);

// Now you can require the bms-mca-token-validation-strategy module:
var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// 코드의 나머지 부분
```

*appGUID* 값을 `appGUID` 값으로 대체하십시오([시작하기 전에](#before-you-begin) 참조).


## 로컬 개발 서버에 대해 작업할 수 있도록 {{site.data.keyword.amashort}} 애플리케이션 구성
{: #configuring-local}

{{site.data.keyword.Bluemix_notm}} 애플리케이션의 실제 URL을 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하고, localhost(또는 IP 주소)를 각 요청에 사용하십시오. 다음 샘플을 참조하십시오. 

지역을 해당 지역으로 바꾸십시오. 

*appGUID* 값과 *bluemixAppRoute* 값을 [시작하기 전에](#before-you-begin)에서 얻은 값으로 바꾸십시오. 

다음 예제에서 `localhost`를 개발 서버의 실제 IP 주소로 변경해야 할 수 있습니다. 

### Android
{: #android}
```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID, BMSClient.REGION_UK); 
//  set your MCA application region here. Currently possible values are BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY, or BMSClient.REGION_UK
BMSClient.getInstance().setAuthorizationManager(
                 MCAAuthorizationManager.createInstance(this, tenantId));

Request request = new Request(baseRequestUrl + "/resource/path", Request.GET);

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



### iOS - Objective C
{: #objc}

```Objective-C
NSString *baseRequestUrl = @"http://localhost:3000";
NSString *bluemixAppRoute = @"http://myapp.mybluemix.net";
NSString *bluemixAppGUID = @"your-bluemix-app-guid";
NSString *tenantId = "your-MCA-service-tenantID";

[[IMFClient sharedInstance] initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];

[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: tenantId];


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
{: #swift}

```Swift

let baseRequestUrl = "http://localhost:3000"
let bluemixAppRoute = "http://myapp.mybluemix.net"
let tenantId = "your-MCA-service-tenantID"
let regionName = BMSClient.Region.usSouth
// set your MCA application region here. Currently these can be BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney

BMSClient.sharedInstance.initialize(bluemixAppRoute: bluemixAppRoute, bluemixAppGUID: tenantId, bluemixRegion: regionName)

BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance
           
let requestPath = baseRequestUrl + "/resource/path"               
let request = Request(url: requestPath, method: HttpMethod.GET)
            
request.send { (response, error) in
	if let error = error {
    			print("Connection failure")
     		print("Error :: \(error)");
     		print("Status :: \(response?.statusCode)");
    	} else {
           print("Connection success")
           print("Response :: \(response?.responseText)")
    }                
}



```


### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";
Var tenantId = "your-MCA-service-tenantID";

BMSClient.initialize(bluemixAppRoute, bluemixAppGUID);

var success = function(data){
   	console.log("success", data);
}

var failure = function(error){
	console.log("failure", error);
}

var request = new MFPRequest(baseRequestUrl + "/resource/path", MFPRequest.GET);

request.send(success, failure);
```
