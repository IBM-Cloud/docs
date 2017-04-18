---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービスに置き換えられます。

# ローカル開発環境での {{site.data.keyword.amashort}} の使用
{: #protecting-local}

ローカル開発を、{{site.data.keyword.Bluemix}} 上で実行されている {{site.data.keyword.amafull}} サービスを使用するように構成することができます。具体的には、{{site.data.keyword.amashort}} サーバー SDK を使用してコードをローカルに開発し、{{site.data.keyword.amashort}} 要求を開発サーバーに送信することができます。これらの要求は、{{site.data.keyword.Bluemix}} 上で実行している {{site.data.keyword.amashort}} サービスによって保護されます。

## 開始する前に
{: #before-you-begin}

以下が必要です。

* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。
* **「TenantID」**。{{site.data.keyword.amafull}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* **「アプリケーションの経路 (Application Route)」**。これは、バックエンド・アプリケーションの URL です。保護されているエンドポイントに要求を送信するためにこの値が必要になります。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域値は、`US South`、`Sydney`、または  `United Kingdom` のいずれかでなければなりません。SDK に必要な正確な構文については、コード・サンプル中のコメントを参照してください。{{site.data.keyword.amashort}} クライアントを初期化するためにこの値が必要になります。
* Gradle と連動して機能するようにセットアップされた Android Studio プロジェクト。Android 開発環境のセットアップ方法について詳しくは、[Google 開発者ツール![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://developer.android.com/sdk/index.html){: new_window}を参照してください。

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
	{: codeblock}

1. {{site.data.keyword.amashort}} ダッシュボードで**「資格情報の表示」**タブをクリックします。{{site.data.keyword.amashort}} がモバイル・バックエンド・アプリケーションに提供するアクセス権限の資格情報とともに JSON オブジェクトが表示されます。

1. ローカル開発環境で、`VCAP_SERVICES` 環境変数を設定します。この変数の値は、{{site.data.keyword.amashort}} 資格情報を含む、文字列化された JSON オブジェクトでなければなりません。詳細情報についは、以下のサンプルを参照してください。

## サーバー・コード例
{: #local-dev-sample}

{{site.data.keyword.amashort}} サービスをローカルの Node.js 開発環境で使用するには、以下のコードを追加します。  

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

*tenantID* 値を知る方法については、[開始する前に](#before-you-begin)を参照してください。


## ローカル開発サーバーで作業するための {{site.data.keyword.amashort}} アプリケーションの構成
{: #configuring-local}

{{site.data.keyword.Bluemix_notm}} アプリケーションの実際の URL を使用して {{site.data.keyword.amashort}} Client SDK を初期化し、各要求で localhost (または IP アドレス) を使用します。以下のサンプルを参照してください。

地域は該当する地域に置き換えます。正しい構文については、コードの例を参照してください。

*appGUID* および *bluemixAppRoute* の値を置き換えます。これらの値の取得については、[開始する前に](#before-you-begin)を参照してください。

以下の例で、`localhost` を、開発サーバーの実際の IP アドレスに変更する必要がある場合があります。

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
