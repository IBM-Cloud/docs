---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.appid_short_notm}} 정보
{: #about}

{{site.data.keyword.appid_full}}를 사용하여 개발자는 몇 행의 코드로 자신의 {{site.data.keyword.Bluemix}} 앱에 인증을 추가하고 보호할 수 있습니다. 개발자는 개인화된 앱 인터페이스를 구축하기 위해 사용자 특정 데이터를 관리할 수도 있습니다.
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

![{{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램](/images/appid_architecture.png)

그림 1. {{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램

{{site.data.keyword.appid_short_notm}} 서버 SDK로 클라우드 리소스를 보호할 수 있습니다. 보호된 클라우스 리소스와 통신하려면 {{site.data.keyword.appid_short_notm}} 클라이언트 SDK에서 제공되는 요청 클래스를 사용하십시오. 

* 서버 SDK가 권한이 없는 요청을 발견하고 HTTP 401 권한 인증 확인을 리턴합니다.
* 클라이언트 SDK가 HTTP 401 권한 인증 확인을 발견하고 ID 제공자의 구성을 기반으로 인증 프로세스를 자동으로 시작합니다.
* 현재 구성된 ID 제공자에 따라서 인증이 시도됩니다.
* 인증에 성공하면 서비스가 권한 및 ID 토큰을 리턴합니다.
* 클라이언트 SDK는 인증 토큰을 원래 요청에 자동 추가하고, 해당 요청을 클라우드 리소스에 재전송합니다.
* 서버 SDK는 요청에서 액세스 토큰을 추출하고 {{site.data.keyword.appid_short_notm}}로 해당 토큰의 유효성을 검증합니다. 액세스 권한이 부여되고 응답이 애플리케이션에 리턴됩니다. 


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

## 액세스 및 ID 토큰
{: #access-and-identity}

{{site.data.keyword.appid_short}}에서는 두 가지 유형의 토큰(액세스 및 ID)을 사용합니다. 토큰은 <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>으로 형식화됩니다.


### 액세스 토큰
{: #access-tokens notoc}

액세스 토큰은 {{site.data.keyword.appid_short_notm}} 권한 필터에서 보호하는 리소스와의 통신을 가능하게 합니다.
[백엔드 리소스 보호](/docs/services/appid/protecting-resources.html)를 참조하십시오. 토큰은 JOSE(JavaScript Object Signing and Encryption) 스펙을 준수하며 다음과 같은 형식입니다. 

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. Most probably userId

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", the AppID tenantId the token was issued for

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // the scope[s] this token was issued for

}
```
{:screen}

### ID 토큰
{: #identity-tokens notoc}

ID 토큰에는 이름, 이메일, 성별, 사진 및 위치를 포함하는 사용자에 대한 정보가 포함됩니다. 

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. AppID userid.

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", // the AppID tenantId the token was issued for

    "name": "John Smith", // user's full name as reported by IDP, mandatory,

    "email": "js@mail.com", // user's email as reported by IDP, only if available,

    "gender", "male", // user's gender as reported by IDP, only if available,

    "locale": "en", // user's locale as reported by IDP, only if available

    "picture": "https://url.to.photo", // URL to user's picture, only if available

    "auth_by": "appid_facebook/appid_google", // the name of IDP used for authentication, mandatory

    "identities": [

        "provider: "appid_facebook/appid_google", // mandatory

        "id": "unique user id as reported by IDP", // mandatory

        "profile": { ... } // JSON object returned by IDP,  mandatory

      },

      {...}, {...} // more linked identities

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // mandatory

      "name": "client_name as reported during client registration", // mandatory

      "software_id": "software_id as reported during client registration", // mandatory

      "software_version": "software_version as reported during client registration", // mandatory

      "device_id": "device_id from client registration", //mobile only

      "device_model": "device_model from client registration", //mobile only

      "device_os": "device_os from client registration", //mobile only

    }

}
```
{:screen}


## ID 제공자 개요
{: #identity-providers-overview}

모바일 및 웹 애플리케이션에서 다음과 같은 ID 제공자를 사용할 수 있습니다. 

* **Facebook** - 사용자는 자신의 Facebook 신임 정보로 모바일 또는 웹 앱에 로그인합니다.
* **Google** - 사용자는 자신의 Google+ 신임 정보로 모바일 또는 웹 앱에 로그인합니다.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## 기본 구성 사용
{: #default-configuration}

{{site.data.keyword.appid_short_notm}}는 ID 제공자를 처음 설정할 때 기본 구성을 제공합니다. 개발 모드에서만 기본 구성을 사용할 수 있습니다. 각 ID 제공자의 경우, 이러한 신임 정보는 하루에 {{site.data.keyword.appid_short_notm}} 인스턴스당 100회의 사용으로 제한됩니다. 애플리케이션을 공개하기 전에 기본 구성을 사용자 자신의 신임 정보에 업데이트하십시오. 구성을 업데이트하려면,
[ID 제공자 구성](/docs/services/appid/identity-providers.html)을 참조하십시오. 
