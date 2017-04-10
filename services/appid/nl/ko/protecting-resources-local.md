---

copyright:
  years:  2017
lastupdated: "2017-03-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}



# 로컬 개발 환경에서 {{site.data.keyword.appid_short_notm}} 사용
{: #protecting-local}

{{site.data.keyword.appid_short}} 서비스를 사용하도록 로컬 환경을 구성할 수 있습니다. 특히, {{site.data.keyword.appid_short_notm}} 서버 SDK를 사용하여 로컬로 코드를 개발하고 요청을 개발 서버에 전송할 수 있습니다.
{:shortdesc}


## 서버 SDK 설정
{: #serversetup}

로컬 개발 서버와 함께 {{site.data.keyword.appid_short_notm}}를 사용하려면 전략을 작성할 때 다음과 같은 속성이 있는 옵션 매개변수를 전달해야 합니다. 

* APIStrategy: `oauthServerUrl`
* WebAppStrategy: tenantId, clientId, secret, oauthServerUrl, redirectUri

'redirectUri' 속성을 콜백 경로가 있는 로컬 호스트 앱 포트로 설정하십시오. 예: `http://localhost:<port>/callback`. 콜백 엔드포인트가 권한 부여 프로세스를 완료합니다.

서비스 신임 정보를 가져오려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드를 열고 **서비스 신임 정보** 탭을 클릭하십시오.
2. **신임 정보 표시**를 클릭하십시오. 액세스 신임 정보가 JSON 오브젝트로 표시됩니다.

샘플 및 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">server SDK GitHub repository <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 참조하십시오.


## 로컬 개발 서버에 대해 작업할 수 있도록 {{site.data.keyword.appid_short_notm}} 애플리케이션 구성
{: #configuring-local}

로컬 개발 서버와 작업하도록 앱을 구성하려면 각 요청에서 로컬 호스트를 사용하십시오.

1. 테넌트 ID를 사용자의 {{site.data.keyword.appid_short_notm}} 테넌트 ID로 바꾸십시오. 서비스 대시보드에서 이 ID를 찾을 수 있습니다.
2. 다음 표에 표시된 대로 지역을 적합한 지역으로 바꾸십시오. 

<table> <caption> 표 1. {{site.data.keyword.Bluemix_notm}} 지역 및 해당하는 Android 및 iOS용 {{site.data.keyword.appid_short_notm}} 지역</caption>
<tr>
  <th> Bluemix 지역 </th>
  <th> Android</th>
</tr>
<tr>
  <td> 미국 남부</td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> 시드니</td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> 영국</td>
  <td> AppID.REGION_UK </td>
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
 let region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or AppID.REGION_UK.

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
