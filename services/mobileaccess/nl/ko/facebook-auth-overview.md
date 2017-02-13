---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Facebook 신임 정보로 사용자 인증
{: #facebook-auth-overview}

ID 제공자로 Facebook을 사용하여 리소스를 보호하도록 {{site.data.keyword.amafull}} 서비스를 구성할 수 있습니다. 모바일 또는 웹 애플리케이션 사용자는 인증을 위해 Facebook 신임 정보를 사용할 수 있습니다.

{:shortdesc}

**중요**: Facebook에서 제공하는 클라이언트 SDK를 별도로 설치할 필요가 없습니다. {{site.data.keyword.amashort}} Facebook 클라이언트 SDK를 구성할 때 종속성 관리자가 Facebook SDK를 자동으로 설치합니다.

## {{site.data.keyword.amashort}} 요청 플로우
{: #mca-facebook-sequence}

### 모바일 클라이언트 요청 플로우

모바일 클라이언트 앱에서 인증을 위해 Facebook과 {{site.data.keyword.amashort}}의 통합 방식을 이해하려면 다음 다이어그램을 참조하십시오.

![모바일 클라이언트 요청 플로우 다이어그램](images/mca-sequence-facebook.jpg)

* {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 {{site.data.keyword.amashort}} 서버 SDK로 보호되는 백엔드 리소스에 대한 요청을 작성합니다. 
* {{site.data.keyword.amashort}} 서버 SDK가 권한이 없는 요청을 발견하고 HTTP 401 코드 및 권한 범위를 리턴합니다.
* {{site.data.keyword.amashort}} 클라이언트 SDK가 자동으로 HTTP 401 코드를 자동으로 발견하고 인증 프로세스를 시작합니다.
* {{site.data.keyword.amashort}} 클라이언트 SDK가 {{site.data.keyword.amashort}} 서비스에 연결하여 권한 헤더를 요청합니다. 
* {{site.data.keyword.amashort}} 서비스는 인증 확인 방식을 제공함으로써 Facebook을 사용하여 먼저 인증하도록 클라이언트에 요청합니다. 
* {{site.data.keyword.amashort}} 클라이언트 SDK가 Facebook SDK를 사용하여 인증 프로세스를 시작합니다. 인증에 성공하면 Facebook SDK는 Facebook 액세스 토큰을 리턴합니다. 
* Facebook 액세스 토큰은 인증 확인 응답으로 간주됩니다. 토큰이 {{site.data.keyword.amashort}} 서비스로 전송됩니다. 
* 서비스는 Facebook 서버를 사용하여 인증 확인 응답의 유효성을 검증합니다. 
* 유효성 검증에 성공하면 {{site.data.keyword.amashort}} 서비스가 권한 헤더를 생성하고 이를 {{site.data.keyword.amashort}} 클라이언트 SDK로 리턴합니다. 권한 헤더에는 액세스 권한 정보를 포함하는 액세스 토큰과 현재 사용자, 디바이스 및 애플리케이션에 대한 정보를 포함하는 ID 토큰이 포함되어 있습니다. 
* 이 시점부터 {{site.data.keyword.amashort}} 클라이언트 SDK를 통해 작성된 모든 요청에는 새로 얻은 권한 헤더가 포함됩니다.
* {{site.data.keyword.amashort}} 클라이언트 SDK가 권한 플로우를 트리거한 원래 요청을 자동으로 재전송합니다.
* {{site.data.keyword.amashort}} 서버 SDK는 요청에서 권한 헤더를 추출하고 {{site.data.keyword.amashort}} 서비스를 사용하여 헤더의 유효성을 검증하며 백엔드 리소스에 액세스 권한을 부여합니다. 

### {{site.data.keyword.amashort}} 웹 애플리케이션 요청 플로우
{: #mca-facebook-web-sequence}

{{site.data.keyword.amashort}} 웹 애플리케이션 요청 플로우는 모바일 클라이언트 플로우와 유사합니다. 그러나 {{site.data.keyword.amashort}}는 {{site.data.keyword.Bluemix_notm}} 백엔드 리소스 대신 웹 애플리케이션을 보호합니다. 

  * 초기 요청은 웹 애플리케이션에서 전송합니다(예: 로그인 양식에서).
  * 최종 경로는 백엔드 보호 리소스보다 웹 애플리케이션 자체의 보호 영역으로 재지정됩니다.


## 개발자용 Facebook 웹 사이트에서 애플리케이션 작성
{: #facebook-appID}

Facebook을 ID 제공자로 사용하려면 개발자용 Facebook 웹 사이트에서 애플리케이션을 작성하십시오. 이 프로세스 중에 Facebook 앱 ID가 작성됩니다. 이 ID는 연결을 시도하는 애플리케이션을 알기 위해 Facebook에서 사용되는 고유 ID입니다. 

모바일 또는 웹 앱에 적합하게 Facebook 인증을 구성하는 데 이 값이 필요합니다. 

1. [개발자용 Facebook ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developers.facebook.com){: new_window} 사이트에 액세스하십시오. 

1. **내 앱** 풀다운 목록을 열고 **새 앱 추가**를 선택하십시오. 

1. **표시 이름** 값과 **문의 이메일 값** 값을 입력하고 풀다운 목록에서 **카테고리**를 선택하십시오. 

1. **새 앱 ID 작성**을 클릭하십시오. 

1. 보안 검사가 표시됩니다. 요청되는 조치를 수행하십시오. 

1. **제품 설정** 페이지가 표시됩니다. 표시되는 **앱 ID**를 복사하십시오. 

## 다음 단계
{: #next-steps}

* [Android 앱에서 Facebook 인증 사용](facebook-auth-android.html)
* [iOS 앱에서 Facebook 인증 사용(Swift SDK)](facebook-auth-ios-swift-sdk.html)
* [Cordova 앱에서 Facebook 인증 사용](facebook-auth-cordova.html)
