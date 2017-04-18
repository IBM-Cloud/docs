---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-07"

---

**중요: {{site.data.keyword.amafull}} 서비스는 {{site.data.keyword.appid_full}} 서비스로 대체되었습니다. **

# 사용자 정의 인증을 위한 Mobile Client Access 구성
{: #custom-dash}


모바일 앱에서 사용자 정의 인증을 사용하려면 사용자 정의 ID 제공자의 사용자 정의 인증 영역과 기본 URL을 {{site.data.keyword.amashort}} 서비스 대시보드에 등록해야 합니다. 

## 시작하기 전에
{: #custom-dash-begin}
다음이 있어야 합니다.
* {{site.data.keyword.amafull}} 서비스의 인스턴스
* 사용자 정의 ID 제공자 애플리케이션

## 대시보드에서 사용자 정의 인증 구성
{: #custom-dash-config}

사용자 정의 인증을 구성하려면 {{site.data.keyword.amafull}} 대시보드를 사용하십시오. 

1. {{site.data.keyword.amafull}} 대시보드에서 서비스를 여십시오. 
1. **관리** 탭에서 **권한**을 토글하여 켜십시오. 
1. **사용자 정의** 섹션을 펼치십시오. 
1. **영역 이름**, **사용자 정의 ID 제공자 URL**을 입력하십시오. **웹 애플리케이션 경로 재지정 URI** 값은 웹 애플리케이션에만 필요합니다. 

## 다음 단계
{: #next-steps}
* [Android용 사용자 정의 인증 구성](custom-auth-android.html)
* [iOS용 사용자 정의 인증 구성](custom-auth-ios-swift-sdk.html)
* [Cordova용 사용자 정의 인증 구성](custom-auth-cordova.html)
