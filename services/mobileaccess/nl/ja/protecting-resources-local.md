---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc} 

# ローカル開発環境での {{site.data.keyword.amashort}} の使用
{: #protecting-local}

ローカル開発を、{{site.data.keyword.Bluemix}} 上で実行されている {{site.data.keyword.amafull}} サービスを使用するように構成することができます。具体的には、{{site.data.keyword.amashort}} サーバー SDK を使用してコードをローカルに開発し、{{site.data.keyword.amashort}} 要求を開発サーバーに送信することができます。これらの要求は、{{site.data.keyword.Bluemix}} 上で実行している {{site.data.keyword.amashort}} サービスによって保護されます。

## 開始する前に
{: #before-you-begin}
以下が必要です。

* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。
* サービス・パラメーター値。{{site.data.keyword.Bluemix_notm}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**をクリックします。`applicationRoute` および `appGUID` (`tenantId` とも呼ばれる) の値が、**「経路」**および**「アプリ GUID」/「TenantId」**フィールドに表示されます。これらの値は、SDK を初期化するため、および要求をバックエンド・アプリケーションに送信するために必要になります。
*  {{site.data.keyword.Bluemix_notm}} アプリケーションがホストされている地域を見つけます。{{site.data.keyword.Bluemix_notm}} 地域を表示するには、メニュー・バーにある**「アバター」**アイコン ![「アバター」アイコン](images/face.jpg "「アバター」アイコン") をクリックして、**「アカウントとサポート」**ウィジェットを開きます。
地域値は、**「米国南部」**、**「シドニー」**、または**「英国」**のいずれかでなければなりません。これらの名前に対応する正確な SDK の定数値は、コードの例に示しています。 

## Server SDK のセットアップ
{: #serversetup}

{{site.data.keyword.amashort}} Server SDK では、2 つの環境変数を設定する必要があります。{{site.data.keyword.Bluemix_notm}} 上でサーバー・サイド・コードを開発している場合、これらの変数は {{site.data.keyword.Bluemix_notm}} インフラストラクチャーによって提供されます。

* `VCAP_SERVICES`: モバイル・バックエンド・アプリケーションにバインドされたサービスに関する情報が含まれています。
* `VCAP_APPLICATION`: モバイル・バックエンド・アプリケーションに関する情報が含まれています。

{{site.data.keyword.amashort}} をローカル開発サーバーで使用するには、これらの環境変数を手動で追加する必要があります。

1. {{site.data.keyword.amashort}} サービスによって保護されているモバイル・バックエンド・アプリケーションの {{site.data.keyword.Bluemix_notm}} ダッシュボードを開きます。

1. ローカル開発環境で、*VCAP_APPLICATION* 環境変数を設定します。この変数には、文字列化された JSON オブジェクトが単一プロパティーとともに含まれている必要があります。
```JavaScript
{
    application_id: "appGUID"
}
```

*appGUID* 値を、[「開始する前に」](#before-you-begin)で取得した `appGUID` 値に置き換えます。 

1. {{site.data.keyword.Bluemix_notm}} ダッシュボード上の、モバイル・バックエンド・アプリケーションの {{site.data.keyword.amashort}} サービス・タイルで**「資格情報の表示」**をクリックします。{{site.data.keyword.amashort}} がモバイル・バックエンド・アプリケーションに提供するアクセス権限の資格情報とともに JSON オブジェクトが表示されます。

1. ローカル開発環境で、`VCAP_SERVICES` 環境変数を設定します。この変数の値は、{{site.data.keyword.amashort}} 資格情報を含む、文字列化された JSON オブジェクトでなければなりません。詳細情報についは、以下のサンプルを参照してください。

## サーバー・コード例
{: #local-dev-sample}

{{site.data.keyword.amashort}} サービスをローカルの Node.js 開発環境で使用するには、以下のコードを追加します。  

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

*appGUID* 値を、[「開始する前に」](#before-you-begin)で取得した `appGUID` 値に置き換えます。 


## ローカル開発サーバーで作業するための {{site.data.keyword.amashort}} アプリケーションの構成
{: #configuring-local}

{{site.data.keyword.Bluemix_notm}} アプリケーションの実際の URL を使用して {{site.data.keyword.amashort}} Client SDK を初期化し、各要求で localhost (または IP アドレス) を使用します。以下のサンプルを参照してください。

地域は該当する地域に置き換えます。

*appGUID* および *bluemixAppRoute* の値は、[『開始する前に』](#before-you-begin)で取得した値に置き換えます。 

以下の例で、`localhost` を、開発サーバーの実際の IP アドレスに変更する必要がある場合があります。

### Android
{: #android}
```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID, BMSClient.REGION_UK);
// MCA アプリケーションの地域をここに設定。現在指定可能な値は BMSClient.REGION_US_SOUTH、BMSClient.REGION_SYDNEY、または BMSClient.REGION_UK
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
// MCA アプリケーションの地域をここに設定。現在、BMSClient.Region.usSouth、BMSClient.Region.unitedKingdom、BMSClient.Region.sydney が指定可能

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

