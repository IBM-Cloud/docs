---

copyright:

years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# API
{: #overview}

다양한 API를 {{site.data.keyword.iot_full}}에 연결된 디바이스, 게이트웨이 및 애플리케이션의 코드를 개발하는 데 사용할 수 있습니다. 

HTTP API는 HTTP 기본 인증으로 보호됩니다. 대시보드를 사용하여 API 키를 생성하는 경우 키와 인증 토큰이 제공됩니다. 자세한 정보는 다음을 참조하십시오. 


## HTTP REST API

고유 조직을 등록하면 6자의 조직 ID를 받게 됩니다. 이 ID는 API 호출에 대한 호스트 이름에 필요하며 다음 주소에서 조직의 기본 URL에 액세스할 수 있습니다. 

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002/

애플리케이션 API에 대한 요청을 인증하려면 사용자 이름을 API 키로 설정하고 비밀번호를 인증 토큰으로 설정하십시오. 

Messaging API의 경우 다음 주소 https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002를 사용하십시오. 


## API 링크

다음 표의 링크를 사용하여 {{site.data.keyword.iot_short_notm}}에서 제공하는 API에 대해 자세히 알아볼 수 있습니다. 

### 일반 HTTP API

API                     | 용도       
------------- | -------------
[조직 관리 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | 조직을 구성하고(디바이스 작성 및 삭제 포함), 사용법 및 서비스 상태를 확인하고, 디바이스 연결 문제점을 진단합니다.
[보안 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | 사용자 초대 및 인증, 사용자 권한, API 키 및 디바이스를 관리합니다.
[정보 관리 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  디바이스 위치를 가져오고 업데이트할 뿐만 아니라 디바이스 이벤트 데이터에 액세스하고 해당 위치에 대한 날씨 정보를 가져옵니다. **참고:** 날씨 정보는 The Weather Company의 통합에 따라 결정됩니다.
[The Weather Company ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html#!/Device_Location_Weather){: new_window} | The Weather Company의 데이터를 기존 디바이스와 통합합니다.
[분석 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/analytics.html){: new_window} | 디바이스에서 {{site.data.keyword.iot_short_notm}}으로 들어오는 데이터에 대한 규칙, 경보 및 조치를 작성합니다.
[디바이스 관리 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/device-mgmt.html){: new_window} | 디바이스 관리 프로토콜을 사용하여 관리 디바이스와 상호작용합니다.
[메시징 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | HTTP를 사용하여 이벤트를 공개하고 명령을 전송합니다. **참고:** Messaging API의 경우, https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002 주소를 사용하십시오.



### 확장 HTTP API

API                     | 용도       
------------- | -------------
[AT&T Extension ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | AT&T 디바이스를 관리합니다.
[Jasper Extension ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Jasper 디바이스를 관리합니다.
[Orange Extension ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | {{site.data.keyword.iot_short_notm}} 조직에 연결되어 있고 Orange SIM 카드가 설치된 디바이스에서 SIM 카드 데이터를 확인합니다.

### 베타 HTTP API

API                     | 용도       
------------- | -------------
[게이트웨이 보안 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | 역할을 확인하고 게이트웨이 디바이스에 지정합니다.
[디바이스 보안  ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | 역할을 확인하고 디바이스에 지정합니다.
[인터페이스 맵핑 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   인터페이스를 사용하여 디바이스 데이터를 맵핑하고 액세스합니다.
