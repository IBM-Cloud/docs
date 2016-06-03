---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.iotdriverinsights_short}} 정보
{: #iotdriverinsights_overview}

{{site.data.keyword.iotdriverinsights_full}}를 사용하여 자동차 조사 데이터 및 컨텍스트 데이터에서 드라이버의 동작을 분석할 수 있습니다.
{:shortdesc}

## 드라이버 동작 분석
{: #driver_behavior_analysis}
자동차 조사 데이터 및 컨텍스트 데이터에서 급가속 또는 급제동, 빈번한 제동, 속도위반, 급격한 회전 및 기타 동작 등의 드라이버 동작을 분석할 수 있습니다.

다음 동작 및 컨텍스트가 포함됩니다.
 - 운전 동작 
    - 속도 관련
       - 급가속
       - 급제동
       - 속도위반
       - 빈번한 정차
       - 빈번한 가속
       - 빈번한 제동
    - 회전 관련
       - 급격한 회전(고속 회전)
       - 회전 전 가속
       - 회전 동안 과도한 제동
    - 기타
       - 피로 운전
 - 운전 컨텍스트
    - 시간 범위
       - 아침 최대 활동 시간
       - 저녁 최대 활동 시간
       - 낮
       - 밤
    - 도로 유형
       - 고속도로
       - 도시고속도로
       - 간선도로
       - 지선도로
       - 기타
    - 도로 유형을 기반으로 하는 속도 패턴
       - 자유 흐름
       - 안정 흐름
       - 혼잡
       - 심각한 혼잡
       - 혼합 상태

## 빅데이터 분석 인프라
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}}에서는 하둡을 백엔드 인프라로 사용합니다. 하둡은 {{site.data.keyword.iotdriverinsights_short}}를 사용하여 자동차 조사 데이터 및 컨텍스트 데이터에서 빅데이터를 분석하기 위한 고확장성을 실현합니다.

## REST API
{: #rest_api}
개발자는 REST API의 분석 결과를 검색하여 {{site.data.keyword.Bluemix_notm}} 애플리케이션에서 사용할 수 있습니다.
 1. 차량 데이터
   - `sendCarProbeData`는 분석할 자동차 조사 데이터를 전송합니다.
   - `getCarProbeDataListAsDate`는 날짜별 자동차 조사 데이터의 목록을 리턴합니다.
   - `deleteCarProbeDataListByDate`는 자동차 조사 데이터를 삭제합니다.
 2. 분석 작업
   - `sendJobRequest`는 운전 동작 분석 작업 요청을 전송합니다.
   - `getJobInfo`는 지정된 작업의 정보를 리턴합니다.
   - `getJobInfoList`는 작업 정보의 목록을 리턴합니다.
 3. 분석 결과 
   - `getAnalyzedTripSummaryList`는 분석된 궤도 요약 정보의 목록을 리턴합니다.
   - `getAnalyzedTripInfo`는 지정된 분석된 궤도의 정보를 리턴합니다.
   - `deleteJobResult`는 작업과 연관된 모든 분석된 결과를 삭제합니다.

## 구성 가능성
{: #configurability}
분석 임계값 매개변수 중 일부(예: 도로 유형별 속도 범위, 회전 각 범위 등)는 사용자 인터페이스(UI)에서 구성할 수 있습니다.
