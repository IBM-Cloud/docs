---

copyright:
  years: 2015, 2016
  
---

# 사용자 정의 인증을 사용하도록 {{site.data.keyword.amashort}} 구성
{: #custom-dash}
모바일 앱에서 사용자 정의 인증을 사용하려면 사용자 정의 ID 제공자의
사용자 정의 인증 영역과 기본 URL을 {{site.data.keyword.amashort}} 서비스 대시보드에
등록해야 합니다. 

## 시작하기 전에
{: #custom-dash-begin}
* [시작하기](getting-started.html)를 읽으십시오. 
* {{site.data.keyword.amashort}} 서버 SDK로 백엔드 애플리케이션을
보호하십시오. 자세한 정보는 [자원 보호](protecting-resources.html)를 참조하십시오. 
* 사용자 정의 ID 제공자 애플리케이션을 실행하십시오. 

## {{site.data.keyword.Bluemix}} 대시보드에서 사용자 정의 인증을 구성하십시오. 
{: #custom-dash-config}
사용자 정의 인증을 구성하려면 {{site.data.keyword.amashort}} 대시보드를 사용하십시오. 

1. {{site.data.keyword.Bluemix}} 대시보드에서 앱을 여십시오. 

1. **모바일 옵션**을 클릭하고 **라우트**(`applicationRoute`) 및 **앱 GUID**(`applicationGUID`)를 기록해 두십시오. SDK를 초기화하는 경우 이 값이 필요합니다. 

1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 

1. **사용자 정의** 타일을 클릭하십시오.

1. 사용자 정의 ID 제공자의 **영역 이름**과 **기본 URL**을
입력하고 변경사항을 저장하십시오. 

## 다음 단계
{: #next-steps}
* [Android에 대해 사용자 정의 인증 구성](custom-auth-android.html)
* [iOS에 대해 사용자 정의 인증 구성](custom-auth-ios.html)
* [Cordova에 대해 사용자 정의 인증 구성](custom-auth-cordova.html)
