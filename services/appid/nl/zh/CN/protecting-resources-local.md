---

copyright:
  years:  2017
lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}



# 将 {{site.data.keyword.appid_short_notm}} 用于本地开发环境
{: #protecting-local}

您可以将本地环境配置为使用 {{site.data.keyword.appid_short}} 服务。具体来说，您可以使用 {{site.data.keyword.appid_short_notm}} 服务器 SDK 在本地开发代码，然后向开发服务器发送请求。{:shortdesc}


## 设置服务器 SDK
{: #serversetup}

要将 {{site.data.keyword.appid_short_notm}} 用于本地开发服务器，必须在创建策略时通过以下属性传递选项参数：

* APIStrategy：`oauthServerUrl`
* WebAppStrategy：tenantId、clientId、secret、oauthServerUrl 和 redirectUri

将“redirectUri”属性设置为包含回调路径的 localhost 应用程序端口，即：`http://localhost:<port>/callback`。回调端点会完成授权过程。

要获取服务凭证，请完成以下步骤：

1. 打开 {{site.data.keyword.Bluemix_notm}} 仪表板，然后单击**服务凭证**选项卡。
2. 单击**显示凭证**。访问凭证将显示为 JSON 对象。

有关样本和更多信息，请参阅<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">服务器 SDK GitHub 存储库 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。


## 将 {{site.data.keyword.appid_short_notm}} 应用程序配置为使用本地开发服务器
{: #configuring-local}

要将应用程序配置为使用本地开发服务器，请在每个请求中使用本地主机。

1. 将租户标识替换为您的 {{site.data.keyword.appid_short_notm}} 租户标识。您可以在服务仪表板中找到此标识。
2. 将区域替换为相应的区域，如下表中所示。

<table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 区域及对应的 Android 和 iOS SDK 区域</caption>
<tr>
  <th> Bluemix 区域</th>
  <th> Android</th>
  <th> iOS</th>
</tr>
<tr>
  <td> 美国南部</td>
  <td> AppID.REGION_US_SOUTH</td>
  <td> BMSClient.Region.usSouth</td>
</tr>
<tr>
  <td> 悉尼</td>
  <td> AppID.REGION_SYDNEY</td>
  <td> BMSClient.Region.sydney</td>
</tr>
<tr>
  <td> 英国</td>
  <td> AppID.REGION_UK</td>
  <td> BMSClient.Region.unitedKingdom</td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or AppID.REGION_UK.

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

 let baseRequestUrl = "http://localhost:<port>"; //set to your server running port
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.Region.unitedKingdom; //set your App ID application region here. Currently possible values are AppID.Region.usSouth, AppID.Region.sydney, or AppID.Region.unitedKingdom.

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
