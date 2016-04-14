---

copyright:
  years: 2015, 2016

---

# ローカル開発環境での {{site.data.keyword.amashort}} の使用
{: #protecting-local}

ローカル開発環境を、{{site.data.keyword.Bluemix}} 上で実行されている {{site.data.keyword.amashort}} サービスを使用するように構成することができます。具体的には、ローカル開発サーバーで Node.js などのサーバー・サイド・コードを開発している時に {{site.data.keyword.amashort}} Server SDK を使用することができます。

{{site.data.keyword.amashort}} Server SDK では、2 つの環境変数を設定する必要があります。{{site.data.keyword.Bluemix_notm}} 上でサーバー・サイド・コードを開発している場合、これらの変数は {{site.data.keyword.Bluemix_notm}} インフラストラクチャーによって提供されます。

* `VCAP_SERVICES`: モバイル・バックエンド・アプリケーションにバインドされたサービスに関する情報が含まれています。
* `VCAP_APPLICATION`: モバイル・バックエンド・アプリケーションに関する情報が含まれています。

{{site.data.keyword.amashort}} をローカル開発サーバーで使用するには、これらの環境変数を手動で追加する必要があります。

1. {{site.data.keyword.amashort}} サービスによって保護されているモバイル・バックエンドの {{site.data.keyword.Bluemix_notm}} ダッシュボードを開きます。

1. **「モバイル・オプション」**をクリックし、**AppGUID** の値をコピーします。

1. ローカル開発環境で、*VCAP_APPLICATION* 環境変数を設定します。この変数には、文字列化された JSON オブジェクトが単一プロパティーとともに含まれている必要があります。
```JavaScript
{
    application_id: "appGUID"
}
```
*appGUID* 変数を、**「モバイル・オプション」**フィールドの値に置換します。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボード上の、モバイル・バックエンド・アプリケーションの {{site.data.keyword.amashort}} サービス・タイルで**「資格情報の表示」**をクリックします。{{site.data.keyword.amashort}} がモバイル・バックエンド・アプリケーションに提供するアクセス権限の資格情報とともに JSON オブジェクトが表示されます。

1. ローカル開発環境で、`VCAP_SERVICES` 環境変数を設定します。この変数の値は、{{site.data.keyword.amashort}} 資格情報を含む、文字列化された JSON オブジェクトでなければなりません。詳細情報についは、以下のサンプルを参照してください。

## サンプル・コード
{: #local-dev-sample}

{{site.data.keyword.amashort}} サービスをローカルの Node.js 開発環境で使用するには、`bms-mca-token-validation-strategy` モジュールを要求する前に以下のコードを追加します。

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
このコード内の *appGUID* 値のオカレンスは、ユーザーのモバイル・バックエンドの *appGUID* 値に置換します。


## ローカル開発サーバーで作業するためのモバイル・アプリケーションの構成
{: #configuring-local}

{{site.data.keyword.Bluemix_notm}} アプリケーションの実際の URL を使用して {{site.data.keyword.amashort}} Client SDK を初期化し、各要求で localhost (または IP アドレス) を使用します。以下のサンプルを参照してください。

以下の例で、`localhost` を、開発サーバーの実際の IP アドレスに変更する必要がある場合があります。

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
