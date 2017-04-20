---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 작동 방식
{: #about}

{{site.data.keyword.appid_short_notm}}에서 사용하는 컴포넌트, 아키텍처 및 요청 플로우에 대해 알아볼 수 있습니다.
{:shortdesc}


다음과 같은 방법으로 서비스를 사용할 수 있습니다. 

* 모바일 및 웹 애플리케이션에 인증 추가
* 보호된 백엔드 리소스 및 웹 앱에 액세스 부여
* {{site.data.keyword.Bluemix_notm}}에서 호스팅하는 Node.js 및 Swift 애플리케이션 보호
* 앱 환경 설정과 같은 사용자 데이터 또는 공용 소셜 프로파일의 정보 저장
* 개인화된 앱 인터페이스를 구축하기 위해 저장된 데이터 사용
* 인증된 사용자와 익명 사용자 모두의 리소스 보호

**참고**: 구현된 프로토콜은 OIDC(OpenID Connect)를 완전히 준수합니다.


## 컴포넌트
{: #components}

* 대시보드 - 내장된 샘플 다운로드, 활동 로그 확인, 다양한 인증 유형 및 ID 제공자 구성
* 클라이언트 SDK - 서비스를 사용하여 사용자 인증을 구현하도록 모바일 및 웹 앱 빌드
    * Android 전제조건: API 25 이상, Java 8.x, Android SDK 도구 25.2.5 이상, Android SDK 플랫폼 도구 25.0.3 이상, Android 빌드 도구 버전 25.0.2
    * iOS 전제조건: iOS9 이상, MacOS 10.11.5, Xcode 8.2
* 서버 SDK - {{site.data.keyword.Bluemix_notm}}에서 호스팅되는 리소스 보호
    * 지원되는 런타임 - Node.js 및 Swift

## 아키텍처 개요
{: #architecture}

{{site.data.keyword.appid_short_notm}}에서 사용자에게 사인인하도록 요구하여 애플리케이션에 보안 레벨을 추가할 수 있습니다. 서버 SDK를 사용하여 백엔드 리소스를 보호할 수도 있습니다. 

다음 다이어그램은 {{site.data.keyword.appid_short_notm}} 서비스가 작동하는 방식에 대한 개요를 보여줍니다. 

![{{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램](/images/appid_architecture2.png)

그림 1. {{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램

<dl>
  <dt> 클라이언트 SDK</dt>
    <dd> 클라이언트 SDK는 클라우드 리소스와 통신하기 위한 요청 클래스를 제공합니다. 권한 부여 인증 확인을 발견하는 경우, 클라이언트 SDK는 자동으로 인증 프로세스를 시작합니다. </dd>
  <dt> Bluemix</dt>
    <dd>  서버 SDK는 요청에서 액세스 토큰을 추출하고 {{site.data.keyword.appid_short_notm}}로 해당 토큰의 유효성을 검증합니다. 인증에 성공하면 {{site.data.keyword.appid_short_notm}}에서 권한 및 ID 토큰을 애플리케이션에 리턴합니다. </dd>
  <dt> ID 제공자</dt>
    <dd> 앱을 인증하도록 Facebook, Google 또는 둘 모두를 구성할 수 있습니다.</dd>
</dl>


## 요청 플로우
{: #request}

다음 다이어그램은 클라이언트 SDK에서 백엔드 애플리케이션 및 ID 제공자로 요청이 어떻게 이동되는지 설명합니다. 

![{{site.data.keyword.appid_short_notm}} 요청 플로우](/images/appidflow.png)


* {{site.data.keyword.appid_short_notm}} 클라이언트 SDK를 사용하여 {{site.data.keyword.appid_short_notm}} 서버 SDK로 보호되는 백엔드 리소스에 대한 요청을 작성합니다. 
* {{site.data.keyword.appid_short_notm}} 서버 SDK가 권한이 없는 요청을 발견하고 HTTP 401 및 권한 범위를 리턴합니다. 
* 클라이언트 SDK가 자동으로 HTTP 401을 발견하고 인증 프로세스를 시작합니다. 
* 클라이언트 SDK가 서비스에 접속하면 둘 이상의 ID 제공자가 구성되어 있는 경우 서버 SDK는 로그인 위젯을 리턴합니다. {{site.data.keyword.appid_short_notm}}는 ID 제공자를 호출하고 해당 제공자에 대한 로그인 양식을 표시하거나, ID 제공자가 구성되지 않은 경우 인증할 수 있는 승인 코드를 리턴합니다. 
* {{site.data.keyword.appid_short_notm}}는 인증 확인 방식을 제공함으로써 인증하도록 클라이언트 앱에 요청합니다. 
* Facebook 또는 Google이 구성되어 있고 사용자가 로그인하는 경우 각각의 ID 제공자 OAuth 플로우에서 인증을 처리합니다. 
* 동일한 승인 코드로 인증이 종료되는 경우 토큰 엔드포인트에 코드가 전송됩니다. 엔드포인트는 두 가지 토큰(액세스 토큰과 ID 토큰)을 리턴합니다. 이 시점부터, 클라이언트 SDK로 작성된 모든 요청에는 새로 얻은 권한 헤더가 포함됩니다. 
* 클라이언트 SDK가 권한 플로우를 트리거한 원래 요청을 자동으로 재전송합니다. 
* 서버 SDK는 요청에서 권한 헤더를 추출하고 서비스를 사용하여 해당 헤더의 유효성을 검증하고 백엔드 리소스에 액세스를 부여합니다. 
