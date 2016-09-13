---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Driving Behavior Analysis 시작하기
{: #drb_index}
마지막 업데이트 날짜: 2016년 6월 16일
{: .last-updated}

Driving Behavior Analysis는 자동차 프로브 및 컨텍스트 데이터에서 운전자 행동을 수집하고 분석하는 데 사용할 수 있는 {{site.data.keyword.Bluemix_notm}}  {{site.data.keyword.iotdriverinsights_full}} 서비스 내의 서비스입니다. 또한, {{site.data.keyword.iotdriverinsights_short}} API를 사용하여 분석된 운전자 행동 데이터를 다른 {{site.data.keyword.Bluemix_notm}} 애플리케이션에 통합할 수 있습니다.

{:shortdesc}

다음 다이어그램은 Driving Behavior Analysis 서비스의 일반적인 API 호출 순서를 대략적으로 보여줍니다.

![일반 분석 순서](images/sequence_diagram.png "일반 분석 순서")

바인딩되지 않은 서비스 인스턴스로 {{site.data.keyword.iotdriverinsights_short}}를 작성하고 배치한 후, 다음 태스크를 완료하여 사용자의 애플리케이션을 {{site.data.keyword.iotdriverinsights_short}} API와 통합하십시오.

또한 [{{site.data.keyword.iotmapinsights_short}} 및 {{site.data.keyword.iotdriverinsights_short}} 튜토리얼](https://github.com/IBM-Bluemix/car-data-management){:new_window}을 사용하여 샘플 자동차 프로브 데이터로 샘플 애플리케이션을 작성하는 데 도움을 받을 수 있습니다.


## 시작하기 전에
{: #drb_byb}

- [Driving Behavior Analysis 정보](drb_iotdriverinsights_overview.html) 주제를 검토하여 분석 가능한 행동 및 컨텍스트를 익히십시오.
- 자동으로 생성된 *테넌트 ID*, *사용자 이름* 및 *비밀번호* 값을 가져오십시오. 이는 {{site.data.keyword.iotdriverinsights_short}} API에 액세스하는 데 필요합니다.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.iotdriverinsights_short}} 서비스 타일을 클릭하십시오.
2. 서비스 인스턴스의 **관리** 보기를 선택하십시오.
3. 표시되는 *테넌트 ID*, *사용자 이름* 및 *비밀번호* 값을 기록해 두십시오.

- 선택사항: 운전자 데이터로 지리공간 기능을 사용하려는 경우 해당 조직에서 {{site.data.keyword.iotmapinsights_short}} {{site.data.keyword.Bluemix_notm}} 서비스를 배치하십시오.

## 태스크 1: 차량 및 컨텍스트 데이터 업로드
{: #drb_task1}
하나 이상의 운전자 운행 데이터 세트를 {{site.data.keyword.iotdriverinsights_short}} 테넌트에 업로드하여 운전자 데이터를 분석에 사용할 수 있도록 만드십시오.

1. 선택사항: {{site.data.keyword.iotmapinsights_short}} 서비스를 배치한 경우 운전자 데이터를 지리공간 데이터에 맵핑하십시오.
사용자의 애플리케이션이 자동차 프로브 데이터를 [{{site.data.keyword.iotdriverinsights_short}} API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}에 전송하기 전에, [{{site.data.keyword.iotmapinsights_short}} API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}를 사용하여 지리공간 데이터에 이를 맵핑할 수 있습니다. 지리공간 데이터는 분석된 운전자 행동 결과의 품질을 향상시킵니다.

     1. `mapMatching` API를 사용하여 맵 매칭된 자동차 프로브 데이터를 가져오십시오.
     맵 매칭은 자동차 프로브에서 지리공간 도로 데이터로 운전 데이터를 맵핑합니다.
        - 요청: 자동차 프로브 데이터
        - 응답: 맵 매칭된 자동차 프로브 데이터
     2. `getLinkInformation` API를 사용하여 도로 유형 데이터를 가져오십시오.  
        - 요청: 연계 도로 ID
        - 응답: 도로 유형
2. `sendCarProbeData` API를 사용하여 자동차 프로브 데이터를 분석할 저장소에 전송하십시오.
원시 자동차 프로브 데이터 및 선택적 일치된 지리공간 데이터를 {{site.data.keyword.iotdriverinsights_short}}에 업로드하십시오.
   - 요청: 맵 매칭된 자동차 프로브 데이터 및 도로 유형

## 태스크 2: 차량 및 컨텍스트 데이터 처리  
{: #drb_task2}
구성 가능한 분석 매개변수에 대하여 차량 및 컨텍스트 데이터를 처리하십시오. 분석 매개변수 구성 방법에 대한 정보는 [서비스에 대한 매개변수 구성](drb_iotdriverinsights_admin.html#configureparameters) 주제를 참조하십시오.

1. `sendJobRequest` API를 통해 작업 요청을 전송하여 특정 기간의 자동차 프로브 데이터를 분석하십시오.
   - 요청: 시작 및 종료 날짜
   - 응답: 작업 ID
2. `getJobInfo` API를 사용하여 작업 상태를 확인하십시오.
운전자 행동 데이터 처리는 작업 상태가 'SUCCEEDED' 상태를 리턴했을 때 완료됩니다. 이제 운전자 행동 데이터를 요청할 수 있습니다.
   - 요청: 작업 ID
   - 응답: 작업 상태

## 태스크 3: 운행 분석
{: #drb_task3}
특정 날짜 범위에서 운행을 분석하여 분석 임계값 매개변수를 준수하는 방식을 파악하십시오.

1. `getAnalyzedTripSummaryList` API를 사용하여 분석된 운행 요약 목록을 가져오십시오.
운행 요약 목록에는 입력 매개변수에 따라 분석된 운행 요약 정보가 포함됩니다.
   - 요청: 작업 ID
   - 응답: 분석된 운행 요약의 목록
2. `getAnalyzedTripInfo` API를 사용하여 자세한 분석된 운행 정보를 가져오십시오.
최종적으로, 특정한 분석된 운행의 자세한 운전자 행동 정보를 가져오십시오.
   - 요청: 운행 uuid
   - 응답: 분석된 운행의 세부사항

## 다음 단계
{: #drb_post}
단계를 완료하면 운전자 행동 데이터의 세트가 해당 조직에서 생성됩니다. 사용자의 애플리케이션 또는 선호되는 분석 소프트웨어를 사용하여 정보를 더 의미 있는 비즈니스 데이터로 처리하십시오.

# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 튜토리얼 파트1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 튜토리얼 파트2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive 스타터 애플리케이션](https://iot-automotive-starter.mybluemix.net){:new_window}


## API 참조
{: #api}

* [API 문서](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}

## 기타 리소스
{: #general}

* [{{site.data.keyword.iotmapinsights_short}} 시작하기](../IotMapInsights/index.html){:new_window}
* [{{site.data.keyword.iot_full}} 시작하기](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [IBM developerWorks의 dW Answers](https://developer.ibm.com/answers/topics/iot-driver-behavior){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-driver-behavior){:new_window}
* [Bluemix 서비스의 새로운 기능](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
