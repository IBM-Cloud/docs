---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc} 

# 将 {{site.data.keyword.amashort}} 用于本地开发环境
{: #protecting-local}

您可以配置本地开发来使用在 {{site.data.keyword.Bluemix}} 上运行的
{{site.data.keyword.amafull}} 服务。具体来说，您可以使用 {{site.data.keyword.amashort}} 服务器 SDK 在本地开发代码，然后向开发服务器发送 {{site.data.keyword.amashort}} 请求。这些请求将由 {{site.data.keyword.Bluemix}} 上运行的 {{site.data.keyword.amashort}} 服务保护。

## 开始之前
{: #before-you-begin}
您必须具有：

* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。
* 服务参数值。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开服务。单击**移动选项**。`applicationRoute` 和 `appGUID`（也称为 `tenantId`）值会显示在**路由**和**应用程序 GUID/TenantId** 字段中。您将需要这些值来初始化 SDK，并将请求发送到后端应用程序。
*  找到托管 {{site.data.keyword.Bluemix_notm}} 应用程序的区域。要查看 {{site.data.keyword.Bluemix_notm}} 区域，请单击菜单栏中的**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标")，以打开**帐户和支持**窗口小部件。区域值应为以下某个值：**美国南部**、**悉尼**或**英国**。对应于这些名称的准确 SDK 常量值如代码示例中所示。 

## 设置服务器 SDK
{: #serversetup}

{{site.data.keyword.amashort}} 服务器 SDK 需要设置两个环境变量。在 {{site.data.keyword.Bluemix_notm}} 上开发服务器端代码时，{{site.data.keyword.Bluemix_notm}} 基础架构会提供这两个变量。

* `VCAP_SERVICES`：包含有关绑定到移动后端应用程序的服务的信息。
* `VCAP_APPLICATION`：包含有关移动后端应用程序的信息。

要将 {{site.data.keyword.amashort}} 用于本地开发服务器，必须手动添加这两个环境变量。

1. 打开通过 {{site.data.keyword.amashort}} 服务进行保护的移动后端应用程序的 {{site.data.keyword.Bluemix_notm}} 仪表板。

1. 在本地开发环境中，设置 *VCAP_APPLICATION* 环境变量。此变量必须包含具有单个属性的字符串化 JSON 对象。

```JavaScript
{
    application_id: "appGUID"
}
```

将 *appGUID* 值替换为在[开始之前](#before-you-begin)中获取的 `appGUID` 值。 

1. 在 {{site.data.keyword.Bluemix_notm}} 仪表板上，单击移动后端应用程序中的 {{site.data.keyword.amashort}} 服务磁贴上的**显示凭证**。这将显示一个 JSON 对象，其中带有 {{site.data.keyword.amashort}} 向移动后端应用程序提供的访问凭证。

1. 在本地开发环境中，设置 `VCAP_SERVICES` 环境变量。此变量的值必须是包含 {{site.data.keyword.amashort}} 凭证的字符串化 JSON 对象。请参阅以下样本以获取更多信息。

## 样本服务器代码
{: #local-dev-sample}

要在本地 Node.js 开发环境中使用 {{site.data.keyword.amashort}} 服务，请添加以下代码。  

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

// Rest of your code
```

将 *appGUID* 值替换为在[开始之前](#before-you-begin)中获取的 `appGUID` 值。 


## 将 {{site.data.keyword.amashort}} 应用程序配置为使用本地开发服务器
{: #configuring-local}

使用 {{site.data.keyword.Bluemix_notm}} 应用程序的真实 URL 初始化 {{site.data.keyword.amashort}} 客户端 SDK，并在每个请求中使用 localhost（或 IP 地址）。请参阅以下样本。

将区域替换为相应的区域。

将 *appGUID* 和 *bluemixAppRoute* 值替换为在[开始之前](#before-you-begin)中获取的值。 

您可能需要在以下示例中将 `localhost` 更改为开发服务器的实际 IP 地址。

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

Request request =
			new Request(baseRequestUrl + "/resource/path", Request.GET);

request.send(this, new ResponseListener() {@Override
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

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
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

```Swiftlet baseRequestUrl = "http://localhost:3000"
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

var request = new MFPRequest(baseRequestUrl +
							"/resource/path", MFPRequest.GET);

request.send(success, failure);
```

