---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Chrome 앱 및 확장 프로그램을 사용하여 푸시 알림 수신
{: #web_notifications}
마지막 업데이트 날짜: 2017년 4월 12일
{: .last-updated}

Google Chrome 앱 및 확장 프로그램에서 {{site.data.keyword.mobilepushshort}}를 수신하도록 설정할 수 있습니다.  단계를 진행하기 전에 [알림 제공자의 신임 정보 구성](t__main_push_config_provider.html)을 수행했는지 확인하십시오.

## Push Notifications의 클라이언트 SDK 설치
{: #web_install}

이 주제에서는 클라이언트 JavaScript Push SDK를 설치하고 이를 사용하여 추가적으로 Chrome 앱 및 확장 프로그램을 개발하는 방법에 대해 설명합니다. 

### Google Chrome 앱 및 확장 프로그램에서 초기화
{: #initialize_google_extn_app}

Chrome 앱 및 확장 프로그램에 Javascript SDK를 설치하려면 다음 단계를 완료하십시오. 

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



### 푸시 SDK 초기화 
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

### Chrome 앱 및 확장 프로그램 등록
{: #web_register}

{{site.data.keyword.mobilepushshort}} 서비스에 디바이스를 등록하려면 `register()` API를 사용하십시오. Google Chrome에서 등록하려면 Bluemix {{site.data.keyword.mobilepushshort}} 서비스 웹 구성 대시보드에서 FCM(Firebase Cloud Messaging) API 키와 웹 사이트 URL을 추가하십시오. 자세한 정보는 [알림 제공자의 신임 정보 구성](t__main_push_config_provider.html)을 참조하십시오.  

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


## Chrome 앱 및 확장 프로그램에 기본 알림 전송 
{: #web_extensions_notifications}

애플리케이션을 개발한 후에는 푸시 알림을 전송할 수 있습니다.  

1. **알림 전송**을 선택하고 **받는 사람** 옵션으로 **웹 알림**을 선택하여 메시지를 작성하십시오.  
2. **메시지** 필드에 전달할 메시지를 입력하십시오.
3. 다음과 같은 선택적 설정을 제공하도록 선택할 수 있습니다.
  - **알림 제목**: 메시지 경보 표제로 표시할 텍스트입니다.
  - **알림 아이콘 URL**: 메시지를 앱 알림 아이콘과 함께 전달해야 하는 경우 필드에서 아이콘에 대한 링크를 제공하십시오.
  - **접기 키**: 접기 키는 알림에 첨부됩니다. 디바이스가 오프라인 상태일 때 접기 키가 동일한 여러 개의 알림이 순차적으로 도착하는 경우 해당 알림은 접혀 있습니다. 디바이스가 온라인 상태가 되면 FCM/GCM 서버에서 알림을 수신하고 동일한 접기 키가 있는 최신 알림만 표시합니다. 접기 키가 설정되어 있지 않는 경우에는 나중에 전달할 수 있도록 새 메시지와 이전 메시지가 모두 저장됩니다.
  - **유효 기간**: 이 값은 초 단위로 설정됩니다. 이 매개변수를 지정하지 않는 경우 FCM/GCM 서버는 메시지를 4주 동안 저장하고 전달하려고 합니다. 4주 후에 유효성이 만료됩니다. 가능한 값 범위는 0 - 2,419,200초입니다.
  - **유휴 시 지연**: 이 값을 `true`로 설정하면 디바이스가 유휴 상태인 경우 FCM/GCM 서버가 알림을 전달하지 않습니다. 디바이스가 유휴 상태인 경우에도 알림이 전달되도록 하려면 이 값을 `false`로 설정하십시오.
  - **추가 페이로드**: 알림에 대한 사용자 정의 페이로드 값을 지정합니다.

다음 이미지는 대시보드의 Chrome 앱 및 확장 프로그램 알림 옵션을 표시합니다.

  ![알림 화면](images/push_chrome_extns.jpg)
  
### 다음 단계
{: #next_steps_tags}

정상적으로 기본 알림을 설정한 후에는 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

이러한 {{site.data.keyword.mobilepushshort}} 서비스 기능을 사용자의 앱에 추가하십시오.
태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오. 고급 알림 옵션을 사용하려면 [고급 알림](t_advance_badge_sound_payload.html)을 참조하십시오. 



