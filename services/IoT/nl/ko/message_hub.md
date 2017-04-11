---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}}를 사용하여 히스토리언 서비스 연결 및 구성  
{: #messagehub_main}

{{site.data.keyword.messagehub_full}}를 {{site.data.keyword.iot_short}}에 연결하면 히스토리 데이터 스토리지에 확장 가능한 대용량 메시지 버스가 제공됩니다. {{site.data.keyword.messagehub}}는 실시간 데이터 피드 처리를 위해 지연시간이 짧은 플랫폼을 제공하는 오픈 소스 대용량 메시징 시스템인 Apache Kafka를 기반으로 빌드됩니다.

## 시작하기 전에  
{: #byb}

{{site.data.keyword.messagehub}}를 {{site.data.keyword.iot_short}} 서비스에 연결하기 전에 다음 태스크를 완료하십시오.

- {{site.data.keyword.Bluemix_notm}} 카탈로그를 사용하여 {{site.data.keyword.iot_short_notm}}과 동일한 {{site.data.keyword.Bluemix_notm}} 영역에서 {{site.data.keyword.messagehub}}를 설정하십시오. {{site.data.keyword.messagehub}}에 대한 자세한 정보는 [{{site.data.keyword.messagehub}} 시작하기](https://console.{DomainName}/docs/services/MessageHub/index.html)를 참조하십시오.

- {{site.data.keyword.Bluemix_notm}} 조직에서 개발자 권한이 있는지와 {{site.data.keyword.Bluemix_notm}}를 통해 로그인했는지 확인하십시오. {{site.data.keyword.Bluemix_notm}}를 통해 로그인하지 않았거나 이 {{site.data.keyword.Bluemix_notm}} 조직에서 개발자 권한이 없는 경우에는 {{site.data.keyword.messagehub}} 및 {{site.data.keyword.iot_short_notm}}의 바인딩에 대해 권한 부여할 수 없습니다.

## 연결

히스토리 데이터 스토리지의 {{site.data.keyword.messagehub}}를 연결하려면 다음을 수행하십시오.

1. {{site.data.keyword.iot_short}} 대시보드의 탐색줄에서 **확장**을 클릭하십시오. 
2. 히스토리 데이터 스토리지 타일에서 **설정**을 클릭하십시오. 
4. 연결할 {{site.data.keyword.messagehub}} 서비스를 선택하십시오.  
{{site.data.keyword.iot_short}} 서비스와 동일한 {{site.data.keyword.Bluemix_notm}} 영역 내에서 사용 가능한 모든 {{site.data.keyword.messagehub}} 서비스가 히스토리 데이터 스토리지 구성 섹션에 나열됩니다.
5. {{site.data.keyword.messagehub}} 구성 옵션을 선택하십시오. 
 1. 시간대를 선택하십시오.  
{{site.data.keyword.messagehub}}로 보낸 디바이스 데이터의 시간소인이 선택한 시간대로 변환됩니다.
 2. 기본 주제를 선택하십시오.  
디바이스 이벤트를 기본 주제(여기에 정의되어 있는 경우)로 보냅니다. 세부적인 주제 지정을 사용하려면 기본 주제를 공백으로 두고 사용자 정의 전달 규칙을 추가하십시오.
 3. 선택사항: 사용자 정의 전달 규칙을 지정하십시오.  
디바이스 이벤트 전달을 위한 추가 규칙을 지정하십시오. 사용자 정의 전달 규칙과 일치하는 이벤트만 전달됩니다.   
 **참고:** 이벤트는 여러 전달 규칙과 일치할 수 있으며 여러 {{site.data.keyword.messagehub}} 주제로 전달됩니다.
 4. 선택사항: 주제를 구성하십시오.  
둘 이상의 기본 파티션에서 주제를 작성하기 위해 파티션 구성을 지정할 수 있습니다.
 5. **완료**를 클릭하십시오.
5. **권한 부여**를 클릭하십시오. 
6. 권한 대화 상자에서 **확인**을 클릭하십시오.

이제 디바이스 데이터가 {{site.data.keyword.messagehub}}에 저장됩니다.
