---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 애플리케이션 연결

{{site.data.keyword.iot_full}}에 애플리케이션을 연결하려면 API 키 및 토큰을 사용하거나 애플리케이션을 {{site.data.keyword.Bluemix_notm}}의 {{site.data.keyword.iot_short_notm}}에 직접 바인딩하여 연결해야 합니다. 액세스 대시보드를 사용하여 액세스를 부여합니다.
{:shortdesc}

## API 키 연결
{: #api-key}
API 키는 {{site.data.keyword.iot_short_notm}} 조직에 애플리케이션을 연결할 때 사용합니다. 애플리케이션에는 조직에 연결하기 위한 API 키와 해당 API 키와 함께 사용해야 하는 고유한 인증 토큰이 필요합니다.  

애플리케이션 연결에 대한 자세한 정보는 개발자 문서에서 [애플리케이션에 대한 MQTT 연결성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html){: new_window}을 참조하십시오. 

새 API 키와 인증 토큰 쌍을 작성하려면 다음을 수행하십시오.  
1.	{{site.data.keyword.iot_short_notm}} 대시보드에서 **앱 > API 키**로 이동합니다.  
2.	**API 키 생성**을 클릭합니다.  
**중요:** API 키와 토큰 쌍을 기록해 두십시오. 인증 토큰은 복구할 수 없습니다. 이 토큰을 잃어버리거나 잊어버리면 새 인증 토큰을 생성하기 위해 API 키를 다시 등록해야 합니다.
 - API 키의 예는 `a-organization_id-a84ps90Ajs`입니다.  
 - 토큰의 예는 `MP$08VKz!8rXwnR-Q*`입니다.  
3.	대시보드에서 API 키를 식별하는 주석을 추가하십시오(예: 내 애플리케이션에 연결할 키).
4.	**완료**를 클릭합니다.



## Bluemix 바인딩 연결
{: #bluemix-binding}
{{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.iot_short_notm}} 조직에 애플리케이션을 바인드할 수 있습니다. 애플리케이션을 바인딩하면 동일한 영역 또는 조직에 있는 서비스 인스턴스와만 통신할 수 있습니다. 애플리케이션이 VCAP_SERVICES 환경 변수의 서비스 인스턴스와 통신하는 데 필요한 모든 데이터를 찾을 수 있습니다. 애플리케이션이 여러 서비스에 바인드된 경우 VCAP_SERVICES 변수에는 각 서비스 인스턴스의 연결 정보가 포함됩니다.  

그러나 외부 앱과 동일한 방식으로 외부 영역 또는 조직에 있는 서비스 인스턴스를 사용할 수 있습니다. 바인딩을 작성하는 대신 신임 정보를 사용하여 앱 인스턴스를 직접 구성하십시오. 자세한 정보는 {{site.data.keyword.Bluemix_notm}} 문서에서 [새 서비스 인스턴스 요청](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)을 참조하십시오.

조직과 연관된 Bluemix 서비스 인스턴스에 바인드되는 Bluemix 애플리케이션에 대한 세부사항을 보려면 **앱 > Bluemix 앱**으로 이동하십시오.  
