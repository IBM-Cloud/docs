---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Trajectory Pattern Analysis 정보
{: #tp_iotdriverinsights_overview}
마지막 업데이트 날짜: 2016년 6월 16일
{: .last-updated}

Trajectory Pattern Analysis API는 자동차 프로브 데이터에서 운전 운행의 기점/종점(O/D) 및 경로 패턴을 분석하는 데 사용할 수 있는 {{site.data.keyword.iotdriverinsights_full}}에서 제공하는 서비스입니다.

{:shortdesc}

## 경로 궤적 패턴 분석
{: #tpa}

여러 운전 운행에서 O/D 및 경로 패턴을 식별하고 분석할 수 있습니다.
다음 다이어그램은 여러 운행에서 가져온 차량(차량-1)의 O/D 및 경로 패턴의 간단한 예제를 표시합니다. 이 예제에서, Trajectory Pattern Analysis는 두 개의 O/D 패턴을 식별합니다.
- 두 개의 경로 패턴을 갖는 집(기점1)에서 사무실(종점1)까지의 O/D 패턴
- 하나의 경로 패턴을 갖는 집(기점1)에서 상점(종점2)까지의 O/D 패턴

![OD 경로 예제](images/tp_odroute_example.png "O/D 및 경로 패턴 예제")

또한 Trajectory Pattern Analysis는 다음 표에 나열된 대로 각 차량의 운전 다양성 메트릭을 계산합니다. 이러한 메트릭을 사용하여 운전자의 운전 특성을 판별할 수 있습니다.

|메트릭 이름|설명|
|:---|:---|
|드문 O/D 비율|입력 운행의 총 수에 대하여 O/D 패턴에서 포함하지 않는 운행 수의 비율입니다.|
|드문 주행거리 비율|입력 운행의 총 주행거리에 대하여 경로 패턴에서 포함하지 않는 주행거리의 비율입니다.|
|드문 운행 비율|입력 운행의 총 수에 대하여 경로 패턴에서 포함하지 않는 운행 수의 비율입니다.|


## REST API
{: #rest_api}

Trajectory Pattern Analysis REST API는 {{site.data.keyword.Bluemix_notm}} 애플리케이션을 사용자 정의하고 빌드하는 데 사용할 수 있는 요청을 제공합니다.

 1. 자동차 데이터 명령:
   - `sendCarProbeData`는 분석할 자동차 프로브 데이터를 전송함
   - `getCarProbeDataListAsDate`는 자동차 프로브 데이터의 목록을 날짜별로 리턴함
   - `deleteCarProbeDataListByDate`는 자동차 프로브 데이터를 삭제함
 2. 분석 작업 명령:
   - `sendJobRequest`는 궤적 패턴 분석 작업 요청을 전송함
   - `getJobInfo`는 지정된 작업의 정보를 리턴함
   - `getJobInfoList`는 작업 정보의 목록을 리턴함
 3. 분석 결과 명령:
   - `getResultSummary`는 궤적 패턴 분석의 분석된 요약 정보를 리턴함
   - `getAnalyzedODDetail`은 지정한 분석된 O/D 패턴의 자세한 정보를 리턴함
   - `getRouteGPSList`는 지정한 분석된 경로 패턴의 GPS 정보 목록을 리턴함
   - `getODList`는 지정한 인수의 O/D 패턴 정보 목록을 리턴함
   - `deleteJobResult`는 작업에 관련된 모든 분석된 결과를 삭제함

자세한 정보는 [{{site.data.keyword.iotdriverinsights_short}} API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window} 문서를 참조하십시오.
