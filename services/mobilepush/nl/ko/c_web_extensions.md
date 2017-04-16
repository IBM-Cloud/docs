---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}}를 수신하도록 Chrome 앱과 확장 프로그램 설정
{: #web_notifications}
마지막 업데이트 날짜: 2017년 1월 18일
{: .last-updated}

Google Chrome 앱과 확장 프로그램에서 {{site.data.keyword.mobilepushshort}}를 수신하도록 설정할 수 있습니다.  단계를 진행하기 전에 [알림 제공자의 신임 정보 구성](t__main_push_config_provider.html)을 수행했는지 확인하십시오.

## {{site.data.keyword.mobilepushshort}}에 사용할 클라이언트 SDK 설치
{: #web_install}

이 주제에서는 클라이언트 JavaScript 푸시 SDK를 설치하고 이를 사용하여 추가적으로 Chrome 앱과 확장 프로그램을 개발하는 방법에 대해 설명합니다. 

### Google Chrome 앱과 확장 프로그램에서 초기화

Chrome 앱과 확장 프로그램에 Javascript SDK를 설치하려면 다음 단계를 완료하십시오. 

[Bluemix 웹 푸시 SDK
![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}에서
`BMSPushSDK.js` 및 `manifest_Chrome_Ext.json`(chrome 확장기능의 경우) 또는
`manifest_Chrome_App.json`(Chrome 앱의 경우)을 다운로드하십시오. 



- Chrome 앱의 경우 다음과 같이 Manifest 파일을 구성하십시오. 
 1. `manifest_Chrome_App.json` 파일에 이름, 설명, 아이콘을 제공하십시오. 
 2. `BMSPushSDK.js`를 `app.background.scripts`에 추가하십시오. 
 3. `manifest_Chrome_App.json`을 `manifest.json`으로 변경하십시오. 

- Chrome 확장 프로그램의 경우 다음과 같이 Manifest 파일을 구성하십시오. 
 1. `manifest_Chrome_Ext.json` 파일에 이름, 설명, 아이콘을 제공하십시오. 
 2. `BMSPushSDK.js`를 `background.scripts`에 추가하십시오. 
 3. `manifest_Chrome_Ext.json`을 `manifest.json`으로 변경하십시오. 

`background.js` 파일에서 푸시 알림을 수신하도록 다음을 추가하십시오.  
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



## 푸시 SDK 초기화 
{: #web_initialize}

Bluemix {{site.data.keyword.mobilepushshort}} 서비스 `app GUID` 및 `app Region`을 사용하여 푸시 SDK를 초기화하십시오.  

앱 GUID를 가져오려면 초기화된 푸시 서비스의 탐색 분할창에서 **구성** 옵션을 선택하고 **모바일 옵션**을 클릭하십시오. Bluemix 푸시 알림 서비스 appGUID 매개변수를 사용하도록 코드 스니펫을 수정하십시오.

`App Region`은 {{site.data.keyword.mobilepushshort}} 서비스가 호스팅되는 위치를 지정합니다. 다음 세 값 중 하나를 사용할 수 있습니다. 

 - 미국 댈러스의 경우: `.ng.bluemix.net`
 - 영국의 경우: `.eu-gb.bluemix.net`
 - 시드니의 경우: `.au-syd.bluemix.net`

```
    var bmsPush = new BMSPush();
    function callback(response) {
        alert(response.response)
    }
    var initParams = {
      "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Chrome 앱과 확장 프로그램 등록
{: #web_register}

{{site.data.keyword.mobilepushshort}} 서비스에 디바이스를 등록하려면 `register()` API를 사용하십시오. Google Chrome에서 등록하는 경우 Bluemix {{site.data.keyword.mobilepushshort}} 서비스 웹 구성 대시보드에 FCM(Firebase Cloud Messaging) 또는 GCM(Google Cloud Messaging) API 키와 웹 사이트 URL을 추가하십시오. 자세한 정보는 Chrome 설정 아래에 있는 [GCM(Google Cloud Messaging)의 신임 정보 구성](t_push_provider_android.html)을 참조하십시오.

Mozilla Firefox에서 등록하는 경우, Firefox 설정 아래의 Bluemix {{site.data.keyword.mobilepushshort}} 서비스 웹 구성 대시보드에 웹 사이트 URL을 추가하십시오.

Bluemix {{site.data.keyword.mobilepushshort}} 서비스에 등록하려면 다음 코드 스니펫을 사용하십시오.
```
var bmsPush = new BMSPush();
function callback(response) {
     alert(response.response)
  }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
  bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}




