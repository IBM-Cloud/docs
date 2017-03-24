---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# 사용자 프로파일
{: #user-profile}

사용자 프로파일은 {{site.data.keyword.appid_short}}에서 저장하고 유지보수하는 엔티티입니다. 프로파일에는 사용자의 속성과 ID가 있으며 익명이거나 ID 제공자가 관리하는 ID에 링크할 수 있습니다.
{:shortdesc}

{{site.data.keyword.appid_short_notm}}에서는 익명으로 또는 OIDC(OpenId Connect) IdP로 인증하여 로그인을 위한 API를 제공합니다. [ID 제공자 구성](https://console.stage1.ng.bluemix.net/docs/services/appid/identity-providers.html#setting-up-idp)을 참조하십시오. 사용자 프로파일 속성 API 엔드포인트는 로그인 및 권한 부여 프로세스 중에 {{site.data.keyword.appid_short_notm}}에서 생성된 액세스 토큰이 보호하는 리소스입니다.


## 사용자 속성 저장, 읽기 및 삭제
{: #storing-data}

{{site.data.keyword.appid_short_notm}}에서는 [Android](https://github.com/ibm-cloud-security/appid-clientsdk-android) 및 [Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift) 모바일 클라이언트용 SDK 뿐 아니라 사용자의 속성에서 CRUD 오퍼레이션 수행을 위한 [REST API](http://mobileclientaccess.stage1.mybluemix.net/swagger-ui/#!/Authorization_Server_V3/authorization)를 제공합니다. 


## OAuth ID
{: #oauth}

OAuth 로그인 API를 호출할 때 {{site.data.keyword.appid_short_notm}}에서는 OAuth 2.0 및 OIDC 프로토콜을 사용하여 선택된 ID 제공자로 호출자에게 권한을 부여하고 인증합니다. 일단 인증이 되면 ID는 {{site.data.keyword.appid_short_notm}} 사용자 레코드와 연관됩니다. {{site.data.keyword.appid_short_notm}}에서는 사용자의 속성에 액세스하는 데 사용할 수 있는 액세스 토큰 및 ID 제공자에서 제공하는 ID 정보가 들어 있는 ID 토큰을 리턴합니다. 이와 동일한 ID로 인증하는 클라이언트에서 동일한 사용자 레코드와 그 속성에 다시 액세스할 수 있습니다. 


## 익명 사용자
{: #anonymous}

익명으로 로그인하면 {{site.data.keyword.appid_short_notm}}는 익명으로 표시되는 임시 사용자 레코드를 작성합니다. {{site.data.keyword.appid_short_notm}}는 익명 액세스 및 ID 토큰을 호출자에게 리턴합니다. 익명 액세스 토큰을 사용하여 사용자 애플리케이션은 사용자 레코드에 저장된 속성을 작성, 읽기, 업데이트, 삭제할 수 있습니다. 예를 들면, 개발자는 사용자가 로그인하지 않고도 장바구니에 항목 추가하기를 즉각적으로 시작할 수 있는 애플리케이션을 작성할 수 있습니다. 


## 식별된 사용자
{: #identified}

ID 제공자에서 제공된 ID가 있는 익명 사용자는 식별된 사용자가 될 수 있습니다. 익명 사용자에서 알려진 사용자로 이동하기 위한 플로우의 개요는 다음 단계와 같습니다. 

* 개발자가 익명 액세스 토큰을 로그인 API에 전달합니다.
* {{site.data.keyword.appid_short_notm}}가 ID 제공자로 호출자를 인증합니다. 
* {{site.data.keyword.appid_short_notm}}가 액세스 토큰에서 정의한 익명 사용자 레코드를 찾아서 거기에 ID를 지정합니다.
    **참고**: 같은 ID가 다른 사용자에게 이미 지정되지 않은 경우에만 ID를 익명 레코드에 지정할 수 있습니다. ID가 다른 {{site.data.keyword.appid_short_notm}} 사용자와 이미 연관되어 있는 경우, 액세스 및 ID 토큰에 그 사용자 레코드의 정보가 포함되며 그 속성에 대한 액세스를 제공합니다. 이전 익명 사용자와 해당 속성은 새 액세스 토큰을 통해 액세스할 수 없습니다. 토큰이 만료될 때까지는 익명 액세스 토큰을 통해 정보에 계속 액세스할 수 있습니다. 알려진 사용자 및 익명 사용자의 익명 속성을 병합하는 방식을 개발자가 선택할 수 있습니다. 
* {{site.data.keyword.appid_short_notm}}에서 수신된 새 액세스 및 ID 토큰은 알려진 사용자를 가리키며 ID 토큰에는 ID 제공자에서 수신된 공용 정보가 포함됩니다. 
* 익명 토큰이 사용자에 유효하지 않게 됩니다. 

이 사용자가 익명이었을 때 이 사용자가 포함시킨 속성에 새 액세스 토큰으로 액세스 가능합니다. 새 토큰을 추가, 변경하거나 삭제할 수 있습니다. 앞으로 이동해서 사용자와 해당 속성을 분석하여 클라이언트에서 같은 ID로 로그인할 때 액세스 가능합니다. 


## 데이터 분리 및 암호화
{: #data}

{{site.data.keyword.appid_short_notm}}는 사용자 프로파일 속성을 저장하고 암호화합니다. 다중 테넌트 서비스로서 모든 테넌트에는 지정된 암호화 키가 있으며 각 테넌트의 사용자 데이터는 그 테넌트의 키로만 암호화됩니다.

{{site.data.keyword.appid_short_notm}}는 개인 정보를 저장하기 전에 암호화되었는지 확인합니다.
