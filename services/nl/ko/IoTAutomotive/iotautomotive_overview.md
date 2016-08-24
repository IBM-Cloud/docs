---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.iot4auto_short}}(베타) 정보
{: #iotautomotive_overview}

마지막 업데이트 날짜: 2016년 7월 29일
{: .last-updated}

{{site.data.keyword.iot4auto_full}}는 차량의 빅데이터를 보고 분석하는 데 사용할 수 있는 {{site.data.keyword.Bluemix_notm}}의 서비스입니다.

{{site.data.keyword.iot4auto_short}} 서비스를 사용하여 대량의 차량 데이터를 수집하고 처리할 수 있습니다. {{site.data.keyword.iot4auto_short}}의 분석은 운전자 행동, 차량 위치 및 기타 자동차 관련 활동과 관심 이벤트에 대한 강력하고 실질적인 통찰력을 제공합니다.
{:shortdesc}

## 아키텍처
{: #architecture}
{{site.data.keyword.iot4auto_short}}는 자동차 애플리케이션 및 커넥티드 차량 디바이스의 기본적 실시간 인프라 플랫폼입니다. 이 서비스는 미래의 새로운 자율 운전 기능도 지원하도록 설계되어 있습니다.

![{{site.data.keyword.iot4auto_full}} 아키텍처](images/architecture_iotautomotive.png "{{site.data.keyword.iot4auto_full}} 아키텍처")

{{site.data.keyword.iot4auto_short}} 서비스에는 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 개별적으로도 사용할 수 있는 다음 {{site.data.keyword.Bluemix_notm}} 서비스가 포함되어 있습니다.

|서비스|설명|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html)| 커넥티드 차량에서 검색한 자동차 프로브 및 컨텍스트 데이터를 통해 여정의 궤적 패턴을 식별하고 운전자 행동을 분석할 수 있는 서비스입니다.
|[Context Mapping](../IotMapInsights/index.html)| 맵 매칭 및 도로망의 최단 경로 검색과 같은 지리공간 기능을 제공하는 서비스입니다.
*표 1. {{site.data.keyword.iot4auto_short}} 서비스*

## 기능
{: #features}

{{site.data.keyword.iot4auto_short}}는 커넥티드 차량 디바이스의 자동차 프로브 데이터를 제공하는 솔루션을 위해 다음 기능을 지원합니다.

### {{site.data.keyword.iot4auto_short}} 디바이스에서 데이터 검색

- 다음의 프로토콜 및 데이터 모델 지원:
   - TPEG
   - ITS
   - ISO 자동차 표준
- 기타 비차량 디바이스 및 센서 지원

### 데이터 정규화 및 스토리지

- 이상 항목 데이터 식별 및 필터링
- 분석을 위해 데이터를 표준 데이터 모델로 맵핑, 변환 및 형식화
- 애플리케이션 또는 서비스 사용, 대기 시간 및 볼륨에 따라 다음 데이터 저장소 중 하나에 데이터 저장:
   -  빅데이터 분석을 위한 하둡 데이터 저장소
   -  실시간 분석을 위한 에이전트 데이터 저장소

### 지리공간 맵 기반 서비스

- 실시간 맵 매칭
- 이벤트 서비스
- 차량 및 외부 소스로부터의 동적 이벤트 삽입
- 링크 또는 노드 기반 토폴로지 인식 검색
- 통합 기상 데이터를 포함하는 컨텍스트 맵 지원

### 확장성이 높고 대기 시간이 낮은 실시간 분석 플랫폼

- 에이전트 기반 기술
- 개인화된 분석
- 유연한 규칙 기반 분석

### MOMA(Moving Object Map Analysis)

- 차량의 데이터를 사용한 일괄처리 (빅데이터) 분석
- 운전자 행동 분석
- 운전자 프로파일링
- 궤적 패턴 분석

### 데이터 제공자 서비스

- 써드파티 애플리케이션 및 서비스를 위한 API

### 자산 관리와 통합

- 차량 자산 관리 시스템

## REST API
{: #api}

[{{site.data.keyword.iot4auto_short}} API](http://ibm.biz/IoT4Automotive_APIdoc)는 요구사항에 맞추어 추가로 {{site.data.keyword.iot4auto_short}}를 개발하도록 돕는 명령을 제공합니다.

사용 가능한 REST API 명령을 이용하여 {{site.data.keyword.iot4auto_short}} 서비스 인스턴스를 사용자 정의할 수 있습니다.

- 시스템에 특정 이벤트 삽입
- 차량의 정규화된 자동차 프로브 데이터를 선호 분석 데이터 저장소에 저장
- 차량의 지리적 위치와 함께 관심 이벤트를 실시간으로 검색

### REST API 명령

|목표 |API 명령 |설명 |
|:---|:---|:---|
|이벤트 삽입|`sendEvent`|교통량 또는 기타 이벤트를 플랫폼에 전송합니다.|
|자동차 프로브 데이터 전송|`sendCarProbe`|차량에서 위치 기반 센서 데이터를 전송하고 실시간 분석 결과를 통해 차량에 영향을 주는 이벤트를 검색합니다.|
|차량 데이터 작성|`createVehicle`|자산으로서의 차량 레코드를 작성합니다. 이 정보는 인증, 인벤토리 및 기타 용도로 사용됩니다.|
|맵 API|해당되지 않음|자세한 정보는 [Context Mapping 서비스 API](http://ibm.biz/IoTContextMapping_APIdoc)를 참조하십시오.|
|분석 API|해당되지 않음|자세한 정보는 [Driver Behavior 서비스 API]( http://ibm.biz/IoTDriverBehavior_APIdoc)를 참조하십시오.|
|자동차 프로브 데이터 가져오기|`getCarProbe`|`sendCarProbe` API 명령을 통해 전송된 차량의 최신 자동차 프로브 데이터를 가져옵니다.|
|맵 이벤트 가져오기|`getEvent` |`sendEvent` API 명령을 통해 전송된 맵의 이벤트를 가져옵니다.|
|차량 자산 데이터 가져오기|`getVehicle`| `createVehicle` API 명령에서 자산으로서의 차량 데이터를 가져옵니다.|
*표 2. {{site.data.keyword.iot4auto_short}} REST API 명령*
