---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 권한 부여 필터 및 헤더
{: #auth}

{{site.data.keyword.appid_short}} 서버 SDK는 두 가지 유형의 리소스(API 및 웹 애플리케이션)를 보호하기 위한 전략을 제공합니다.
{:shortdesc}


## 권한 필터
{: #auth-filter}

API 보호 전략은 인증되지 않은 클라이언트에 대한 권한을 확보하기 위해 범위의 목록이 있는 HTTP 401 응답을 리턴합니다. 웹 애플리케이션 보호 전략은 HTTP 302 경로 재지정을 리턴합니다. 구성에 따라서 경로 재지정이 인증되지 않은 클라이언트를 {{site.data.keyword.appid_short_notm}} 서비스에서 호스팅하는 로그인 페이지로 전송하거나 ID 제공자 로그인 페이지로 직접 전송합니다. 



### API 전략
{: #api}

API 전략은 요청에 올바른 액세스 토큰이 있는 권한 헤더가 포함될 것으로 예상합니다. 응답에도 ID 토큰이 포함될 수 있지만 필수는 아닙니다. [액세스 및 ID 토큰](/docs/services/appid/access-identity.html#access-and-identity)을 참조하십시오.

토큰이 올바르지 않거나 만료된 경우, API 전략은 다음 정보가 포함된 HTTP 401 오류를 리턴합니다: Www-Authenticate=Bearer scope="{scope}" error="{error}". `error` 컴포넌트는 선택사항입니다. 

요청이 올바른 토큰을 리턴하는 경우, 제어가 다음 미들웨어에 전달되며 `appIdAuthorizationContext` 특성이 요청 오브젝트에 삽입됩니다. 이 특성에는 일반 JSON 오브젝트로 디코드된 페이로드 정보 뿐만 아니라 원래 액세스 및 ID 토큰이 포함됩니다. 


### 웹 앱 전략
{: #web}

웹 앱 전략 클래스가 보호된 리소스에 액세스하려는 인증되지 않은 시도를 발견하면 사용자의 브라우저를 인증 페이지로 자동으로 경로 재지정합니다. 인증에 성공하면 사용자가 웹 애플리케이션의 콜백 URL로 리턴됩니다. 서비스는 웹 앱 전략 클래스를 사용하여 액세스 및 ID 토큰을 확보합니다. 해당 토큰을 확보한 후에 웹 앱 전략 클래스는 `WebAppStrategy.AUTH_CONTEXT` 아래의 HTTP 세션에 토큰을 저장합니다. 애플리케이션 데이터베이스에서 액세스 및 ID 토큰을 저장할 것인지 여부는 사용자가 결정합니다. 

## 권한 헤더
{: #auth-header}

수신 요청의 권한 헤더는 운반자, 액세스 토큰 및 ID 토큰의 세 가지 파트로 구성되며 공백으로 구분됩니다. 액세스 토큰은 필수 컴포넌트이며 ID 토큰은 선택사항입니다. 예상되는 헤더 구조: Authorization=Bearer {access_token} [{id_token}]
