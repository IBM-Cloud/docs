---

copyright:
  years:  2017
lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}



# ローカル開発環境での {{site.data.keyword.appid_short_notm}} の使用
{: #protecting-local}

ローカル環境を、{{site.data.keyword.appid_short}} サービスを使用するように構成できます。具体的には、{{site.data.keyword.appid_short_notm}} サーバー SDK を使用してコードをローカルで開発し、要求を開発サーバーに送信することができます。
{:shortdesc}


## Server SDK のセットアップ
{: #serversetup}

{{site.data.keyword.appid_short_notm}} をローカル開発サーバーで使用するには、戦略の作成時に以下の属性を指定したオプション・パラメーターを渡す必要があります。

* APIStrategy: `oauthServerUrl`
* WebAppStrategy: tenantId、clientId、secret、oauthServerUrl、redirectUri

「redirectUri」属性には、ローカル・ホストのアプリ・ポートとコールバック・パス (`http://localhost:<port>/callback`) を設定します。コールバック・エンドポイントで許可プロセスは完了します。

サービスの資格情報を取得するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードを開いて、**「サービス資格情報」**タブをクリックします。
2. **「資格情報の表示」**をクリックします。アクセス資格情報が JSON オブジェクトとして表示されます。

サンプルおよび詳しい情報については、<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">サーバー SDK GitHub リポジトリー<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>を参照してください。


## ローカル開発サーバーで作業するための {{site.data.keyword.appid_short_notm}} アプリケーションの構成
{: #configuring-local}

ローカルの開発サーバーで機能するようにアプリを構成するには、各要求でローカル・ホストを使用します。

1. テナント ID を {{site.data.keyword.appid_short_notm}} テナント ID に置き換えます。この ID は、サービスのダッシュボードで確認できます。
2. 地域を、以下の表に示している該当地域に置き換えます。

<table> <caption> 表 1。{{site.data.keyword.Bluemix_notm}} 地域および対応する Android と iOS SDK 地域</caption>
<tr>
  <th> Bluemix 地域</th>
  <th> Android</th>
  <th> iOS</th>
</tr>
<tr>
  <td> 米国南部</td>
  <td> AppID.REGION_US_SOUTH </td>
  <td> BMSClient.Region.usSouth </td>
</tr>
<tr>
  <td> シドニー</td>
  <td> AppID.REGION_SYDNEY </td>
  <td> BMSClient.Region.sydney </td>
</tr>
<tr>
  <td> 英国</td>
  <td> AppID.REGION_UK </td>
  <td> BMSClient.Region.unitedKingdom </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //サーバーの実行ポートを設定
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //App ID アプリケーションの地域をここで設定。現在使用可能な値は AppID.REGION_US_SOUTH、AppID.REGION_SYDNEY、または AppID.REGION_UK。

BMSClient bmsClient= BMSClient.getInstance();
bmsClient.initialize(getApplicationContext(), region);
AppID appId = AppID.getInstance();
appId.initialize(getApplicationContext(), tenantId, region);

AppIDAuthorizationManager appIDAuthorizationManager = new AppIDAuthorizationManager(appId);
bmsClient.setAuthorizationManager(appIDAuthorizationManager);

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
{:pre}

### iOS - Swift
{: #swift}
```swift

 let baseRequestUrl = "http://localhost:<port>"; //サーバーの実行ポートを設定
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.Region.unitedKingdom; //App ID アプリケーションの地域をここで設定。現在使用可能な値は AppID.Region.usSouth、AppID.Region.sydney、または AppID.Region.unitedKingdom。

BMSClient.sharedInstance.initialize(bluemixRegion: region)
BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)

var request:Request =  Request(url: baseRequestUrl + "/resource/path", method: HttpMethod.GET)
request.send(completionHandler: {(response:Response?, error:Error?) in
    if let error = error {
            print("Connection failure")
     		print("Error :: \(error)");
     		print("Status :: \(response?.statusCode)");
    	} else {
           print("Connection success")
            print("Response :: \(response?.responseText)")
        }
    });
```
{:pre}
