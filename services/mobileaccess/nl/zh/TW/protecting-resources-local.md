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


# 搭配使用 {{site.data.keyword.amashort}} 與本端開發環境
{: #protecting-local}

您可以配置本端開發來使用 {{site.data.keyword.Bluemix}} 上執行的 {{site.data.keyword.amafull}} 服務。尤其，您可以在本端使用 {{site.data.keyword.amashort}} 伺服器 SDK 開發程式碼，並將 {{site.data.keyword.amashort}} 要求傳送至開發伺服器。{{site.data.keyword.Bluemix}} 上執行的 {{site.data.keyword.amashort}} 服務將保護這些要求。

## 開始之前
{: #before-you-begin}

您必須具有：

* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端應用程式的相關資訊，請參閱[開始使用](index.html)。
* **承租戶 ID**。在 {{site.data.keyword.amafull}} 儀表板中，開啟服務。按一下**行動選項**按鈕。`tenantId`（也稱為 `appGUID`）值會顯示在**應用程式 GUID/承租戶 ID** 欄位中。您需要此值來起始設定「授權管理程式」。
* **應用程式路徑**。這是後端應用程式的 URL。在傳送要求至其受保護端點時，將需要此值。
* {{site.data.keyword.Bluemix_notm}} **地區**。您可以在標頭中找到您目前的 {{site.data.keyword.Bluemix_notm}} 地區，就在**虛擬人像**圖示 ![「虛擬人像」圖示](images/face.jpg "「虛擬人像」圖示") 的旁邊。出現的地區值應該是下列其中一項：`美國南部`、`雪梨`或`英國`。如需 SDK 所需的確切語法，請參閱程式碼範例中的註解。您需要此值來起始設定 {{site.data.keyword.amashort}} 用戶端。
* 設定成使用 Gradle 的 Android Studio 專案。如需如何設定 Android 開發環境的相關資訊，請參閱 [Google Developer Tools ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://developer.android.com/sdk/index.html "外部鏈結圖示"){: new_window}。

## 設定伺服器 SDK
{: #serversetup}

{{site.data.keyword.amashort}} 伺服器 SDK 需要設定兩個環境變數。在 {{site.data.keyword.Bluemix_notm}} 上開發伺服器端程式碼時，這些變數是由 {{site.data.keyword.Bluemix_notm}} 基礎架構所提供。

* `VCAP_SERVICES`：包含連結至行動後端應用程式之服務的相關資訊。
* `VCAP_APPLICATION`：包含行動後端應用程式的相關資訊。

若要搭配使用 {{site.data.keyword.amashort}} 與本端開發伺服器，您必須手動新增這些環境變數。

1. 開啟使用 {{site.data.keyword.amashort}} 服務保護之行動後端應用程式的 {{site.data.keyword.Bluemix_notm}} 儀表板。

1. 在本端開發環境中，設定 *VCAP_APPLICATION* 環境變數。此變數必須包含具有單一內容的字串化 JSON 物件。
	```JavaScript
	{
		application_id: "appGUID"
	}
	```
	{: codeblock}

1. 按一下 {{site.data.keyword.amashort}} 儀表板中的**顯示認證**標籤。即會顯示 JSON 物件與 {{site.data.keyword.amashort}} 提供給行動後端應用程式的存取認證。

1. 在本端開發環境中，設定 `VCAP_SERVICES` 環境變數。此變數的值必須是包含 {{site.data.keyword.amashort}} 認證的字串化 JSON 物件。如需相關資訊，請參閱下列範例。

## 範例伺服器程式碼
{: #local-dev-sample}

若要在本端 Node.js 開發環境中使用 {{site.data.keyword.amashort}} 服務，請新增下列程式碼。  

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

如需尋找 *tenantID* 值的相關資訊，請參閱[開始之前](#before-you-begin)。


## 配置 {{site.data.keyword.amashort}} 應用程式以使用本端開發伺服器
{: #configuring-local}

使用 {{site.data.keyword.Bluemix_notm}} 應用程式的實際 URL 來起始設定 {{site.data.keyword.amashort}} 用戶端 SDK，並在每一個要求中使用 localhost（或 IP 位址）。請參閱下列範例。

將地區取代為適當的地區。請參閱程式碼範例，以取得正確語法。

取代 *appGUID* 及 *bluemixAppRoute* 值。如需取得這些值的相關資訊，請參閱[開始之前](#before-you-begin)。

在下列範例中，您可能需要將 `localhost` 變更為開發伺服器的實際 IP 位址。

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
{: codeblock}


### iOS - Swift
{: #swift}

```Swift

 let baseRequestUrl = "http://localhost:3000";
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

var request = new MFPRequest(baseRequestUrl + "/resource/path", MFPRequest.GET);

request.send(success, failure);
```
{: codeblock}
