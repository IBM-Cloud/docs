---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}}를 수신하도록 웹 애플리케이션 설정
{: #web_notifications}
마지막 업데이트 날짜: 2017년 1월 18일
{: .last-updated}

Google Chrome, Mozilla Firefox 및 Safari 웹 애플리케이션을 사용하여 {{site.data.keyword.mobilepushshort}}를 수신할 수 있습니다. 단계를 진행하기 전에 [알림 제공자의 신임 정보 구성](t__main_push_config_provider.html)을 수행했는지 확인하십시오.

## {{site.data.keyword.mobilepushshort}}를 위한 웹 브라우저 클라이언트 SDK 설치
{: #web_install}

이 주제에서는 클라이언트 JavaScript 푸시 SDK를 설치하고 이를 사용하여 추가적으로 웹 애플리케이션을 개발하는 방법에 대해 설명합니다.

### 웹 애플리케이션에서 초기화

Google Chrome 웹 애플리케이션에 Javascript SDK를 설치하려면 다음 단계를 완료하십시오.

[Bluemix 웹 푸시 SDK](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}에서 `BMSPushSDK.js`, `BMSPushServiceWorker.js`, `manifest_Website.json` 파일을 다운로드하십시오. 

1. `manifest_Website.json` 파일을 편집하십시오. 
	- Google Chrome 브라우저의 경우 `name`을 사용하는 사이트의 이름으로 변경하십시오. 예: `www.dailynewsupdates.com`. `gcm_sender_id`를 FCM(Firebase Cloud Messaging) 또는 GCM(Google Cloud Messaging) sender_ID로 변경하십시오. 자세한 정보는 [발신인 ID 및 API 키 가져오기](t_push_provider_android.html)를 참조하십시오. gcm_sender_id 값에는 숫자만 포함됩니다.

		```
 			{
 			 "name": "YOUR_WEBSITE_NAME",
  			"gcm_sender_id": "GCM_Sender_Id"
			 }
		```
    		{: codeblock}
 
	- Mozilla Firefox 브라우저의 경우, `manifest_Website.json` 파일에 다음 값을 추가하십시오. 적절한 `이름`을 제공하십시오. 이 이름은 웹 사이트의 이름이 됩니다. 

		```
			{
 			 "name": "YOUR_WEBSITE_NAME"
			 }
		```
    		{: codeblock}

2. `manifest_Website.json` 파일 이름을 `manifest.json`으로 변경하십시오. 
3. 웹 사이트의 루트 디렉토리에 `BMSPushSDK.js`, `BMSPushServiceWorker.js` 및 `manifest.json`을 추가하십시오. 
3. html 파일의 `<head>` 태그에 `manifest.json`을 포함시키십시오.
```<link rel="manifest" href="manifest.json">
```
    {: codeblock}
4. 웹 애플리케이션에 Bluemix 웹 푸시 SDK를 포함시키십시오. 
```<script src="BMSPushSDK.js" async></script>
```
    {: codeblock}

## 웹 푸시 SDK 초기화 
{: #web_initialize}

Bluemix {{site.data.keyword.mobilepushshort}} 서비스 `app GUID` 및 `app Region`을 사용하여 푸시 SDK를 초기화하십시오.  

앱 GUID를 가져오려면 초기화된 푸시 서비스의 탐색 분할창에서 **구성** 옵션을 선택하고 **모바일 옵션**을 클릭하십시오. Bluemix 푸시 알림 서비스 appGUID 매개변수를 사용하도록 코드 스니펫을 수정하십시오.

`App Region`은 {{site.data.keyword.mobilepushshort}} 서비스가 호스팅되는 위치를 지정합니다. 다음 세 값 중 하나를 사용할 수 있습니다. 

 - 미국 댈러스의 경우: `.ng.bluemix.net`
 - 영국의 경우: `.eu-gb.bluemix.net`
 - 시드니의 경우: `.au-syd.bluemix.net`

```     var bmsPush = new BMSPush();
    function callback(response) {
        alert(response.response)
    }
    var initParams = {
      "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
   "websitePushIDSafari": "Optional parameter for Safari Push Notifications only. The value should match the website Push ID provided during the server side configuration."
    }
  bmsPush.initialize(initParams, callback)
```
	{: codeblock}

**참고**: 웹 푸시 SDK의 FCM 신임 정보를 변경한 경우 Chrome 브라우저에 대한 메시지 전달이 실패할 수 있습니다. 실패를 방지하려면 `bmsPush.unRegisterDevice`를 호출하십시오. 

잘못된 매개변수를 제공하는 경우 구성 관련 오류가 표시될 수 있습니다. 자세한 정보는 [웹 푸시 구성 오류 해결](troubleshooting_config_errors.html)을 참조하십시오.

## 웹 애플리케이션 등록
{: #web_register}

{{site.data.keyword.mobilepushshort}} 서비스에 디바이스를 등록하려면 **register()** API를 사용하십시오. 사용하는 브라우저에 따라 다음 옵션을 사용하십시오. 

- Google Chrome에서 등록하는 경우 Bluemix {{site.data.keyword.mobilepushshort}} 서비스 웹 구성 대시보드에 FCM(Firebase Cloud Messaging) 또는 GCM(Google Cloud Messaging) API 키와 웹 사이트 URL을 추가하십시오. 자세한 정보는 Chrome 설정 아래에 있는 [GCM(Google Cloud Messaging)의 신임 정보 구성](t_push_provider_android.html)을 참조하십시오.

- Mozilla Firefox에서 등록하는 경우, Firefox 설정 아래의 Bluemix {{site.data.keyword.mobilepushshort}} 서비스 웹 구성 대시보드에 웹 사이트 URL을 추가하십시오.

Bluemix {{site.data.keyword.mobilepushshort}} 서비스에 등록하려면 다음 코드 스니펫을 사용하십시오.
```var bmsPush = new BMSPush();
function callback(response) {
     alert(response.response)
  }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  "websitePushIDSafari": "Optional parameter for Safari Push Notifications only. The value should match the website Push ID provided during the server side configuration."
  }
  bmsPush.initialize(params, callback)
  bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}






