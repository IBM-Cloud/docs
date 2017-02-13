---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 将 {{site.data.keyword.amashort}} 用于本地开发环境
{: #protecting-local}

您可以配置本地开发来使用在 {{site.data.keyword.Bluemix}} 上运行的
{{site.data.keyword.amafull}} 服务。具体来说，您可以使用 {{site.data.keyword.amashort}} 服务器 SDK 在本地开发代码，然后向开发服务器发送 {{site.data.keyword.amashort}} 请求。这些请求将由 {{site.data.keyword.Bluemix}} 上运行的 {{site.data.keyword.amashort}} 服务保护。

## 开始之前
{: #before-you-begin}

您必须具有：

* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。
* **TenantID**。在 {{site.data.keyword.amafull}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* **应用程序路径**。这是后端应用程序的 URL。您将需要此值来向其受保护端点发送请求。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应该为以下某个值：`US South`、`Sydney` 或 `United Kingdom`。有关 SDK 所需的确切语法，请参阅代码样本中的注释。您将需要此值来初始化 {{site.data.keyword.amashort}} 客户端。
* Android Studio 项目，设置为使用 Gradle。有关如何设置 Android 开发环境的更多信息，请参阅 [Google 开发者工具![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://developer.android.com/sdk/index.html "外部链接图标"){: new_window}。

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
	{: codeblock}

1. 在 {{site.data.keyword.amashort}} 仪表板中单击**显示凭证**选项卡。这将显示一个 JSON 对象，其中带有 {{site.data.keyword.amashort}} 向移动后端应用程序提供的访问凭证。

1. 在本地开发环境中，设置 `VCAP_SERVICES` 环境变量。此变量的值必须是包含 {{site.data.keyword.amashort}} 凭证的字符串化 JSON 对象。请参阅以下样本以获取更多信息。

## 样本服务器代码
{: #local-dev-sample}

要在本地 Node.js 开发环境中使用 {{site.data.keyword.amashort}} 服务，请添加以下代码。  

```JavaScript
var vcapApplication = {
	application_id:"tenantID"
};

var vcapServices = {
"AdvancedMobileAccess": [
		{
			"credentials": {
"admin_url": "https://mobile.ng.bluemix.net/imfmobileplatformdashboard/?appGuid=appGUID",
				"clientId": "tenantID",
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
{: codeblock}

有关查找 *tenantID* 值的信息，请参阅[开始之前](#before-you-begin)。


## 将 {{site.data.keyword.amashort}} 应用程序配置为使用本地开发服务器
{: #configuring-local}

使用 {{site.data.keyword.Bluemix_notm}} 应用程序的真实 URL 初始化 {{site.data.keyword.amashort}} 客户端 SDK，并在每个请求中使用 localhost（或 IP 地址）。请参阅以下样本。

将区域替换为相应的区域。请参阅代码示例，以获取正确的语法。

替换 *appGUID* 和 *bluemixAppRoute* 值。有关获取这些值的信息，请参阅[开始之前](#before-you-begin)。

您可能需要在以下示例中将 `localhost` 更改为开发服务器的实际 IP 地址。

### Android
{: #android}

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";

BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

//  set your MCA application region here. Currently possible values are BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY, or BMSClient.REGION_UK

BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));
						
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
{: codeblock}


### iOS - Swift
{: #swift}

```Swiftlet baseRequestUrl = "http://localhost:3000";
 let tenantId = "<serviceTenantID>"
 let regionName = <applicationBluemixRegion>
 //possible values: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
 let mcaAuthManager = MCAAuthorizationManager.sharedInstance
 mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
 BMSClient.sharedInstance.authorizationManager = mcaAuthManager
        
        
 let requestPath = baseRequestUrl + "/protectedResource"
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
{: codeblock}


### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";
Var tenantId = "your-MCA-service-tenantID";

BMSClient.initialize(<applicationBluemixRegion>);

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
{: codeblock}
