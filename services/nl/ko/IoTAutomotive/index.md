---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot4auto_short}}(베타) 시작하기
{: #getting_started_iotautomotive}

마지막 업데이트 날짜: 2016년 7월 29일
{: .last-updated}

{{site.data.keyword.iot4auto_full}}는 커넥티드 차량에서 빅데이터를 검색, 관리 및 분석하는 데 사용할 수 있는 {{site.data.keyword.Bluemix_notm}} 서비스입니다. {{site.data.keyword.iot4auto_short}}의 분석은 운전 행동, 차량 위치 및 기타 자동차 관련 활동과 관심 이벤트에 대한 강력하고 실질적인 통찰력을 제공합니다.

{:shortdesc}

{{site.data.keyword.iot4auto_short}}를 사용하여 다음 태스크를 수행할 수 있습니다.

- 자동차 프로브 데이터 및 정규화 데이터를 데이터 저장소에 전송하여 분석
- 이벤트를 컨텍스트 맵에 삽입하고 특정 차량이 영향을 받는 이벤트 검색
- 자동차 프로브 데이터에서 새 이벤트 식별
- 커넥티드 차량에 대한 정보 검색
- 운전자, 차량, 이벤트 규칙, 이벤트 유형 및 공급업체에 대한 자산 데이터 관리


{{site.data.keyword.iot4auto_short}} 서비스에는 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 개별적으로도 사용할 수 있는 다음 {{site.data.keyword.Bluemix_notm}} 서비스가 포함되어 있습니다.

|서비스|설명|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html){:new_window}| 커넥티드 차량에서 검색한 자동차 프로브 및 컨텍스트 데이터를 통해 여정의 궤적 패턴을 식별하고 운전자 행동을 분석할 수 있는 서비스입니다.
|[Context Mapping](../IotMapInsights/index.html){:new_window}| 맵 매칭 및 도로망의 최단 경로 검색과 같은 지리공간 기능을 제공하는 서비스입니다.
*표 1. {{site.data.keyword.iot4auto_short}}*의 서비스

자동차 디바이스와 애플리케이션을 서비스와 통합하기 전에 다음 단계를 완료하십시오.

1. [{{site.data.keyword.iot4auto_short}} 정보](iotautomotive_overview.html) 주제를 검토하여 서비스에서 제공 및 지원되는 기능과 분석을 익히십시오.
2. [{{site.data.keyword.Bluemix_notm}} 카탈로그](https://console.ng.bluemix.net/catalog/labs/){:new_window}에서 서비스 인스턴스를 추가할 때 인스턴스가 앱에 바인딩되지 않았는지 확인하고 자동으로 생성된 테넌트 ID, 사용자 이름 및 비밀번호 값을 기록해 두십시오. 나중에 {{site.data.keyword.iot4auto_short}} API를 통해 서비스에 액세스하려면 이 값이 필요합니다.
3. 대시보드의 콘솔을 사용하여 {{site.data.keyword.iot4auto_short}}의 포트, 대상 호스트 이름 및 기타 설정을 구성하십시오. 자세한 정보는 [관리](iotautomotive_admin.html)를 참조하십시오.

{{site.data.keyword.iot4auto_short}} REST API 명령을 사용하여 자동차 디바이스와 애플리케이션을 이 서비스와 통합할 수 있습니다.

신속하게 시작하려면 다음 단계를 완료하십시오.

1. 분석할 이벤트를 보내기 위해 `sendEvent` API 요청 명령을 사용하여 이벤트를 삽입하십시오.
  - 요청: 위치가 포함된 이벤트 데이터
2. 이벤트를 검색하는 `getEvent` API 요청 명령을 사용하여 이벤트 데이터가 맵 매칭을 포함하여 저장되었는지 확인하십시오.
  - 요청: 영역 데이터(시작 또는 종료 지점의 경도 및 위도)
  - 응답: 연계 도로 ID가 포함된 이벤트 데이터
3.  `sendCarProbe` API 요청 명령을 사용하여 분석할 자동차 프로브 데이터를 전송하십시오.
  - 요청: 위치가 포함된 자동차 프로브 데이터
4. 데이터를 검색하는 `getCarProbe` API 요청 명령을 사용하여 자동차 프로브 데이터가 맵 매칭을 포함하여 저장되었는지 확인하십시오.
  - 요청: 영역 데이터(시작 또는 종료 지점의 경도 및 위도)
  - 응답: 연계 도로 ID가 포함된 자동차 프로브 데이터
5. 운전자 데이터를 분석하십시오. 자세한 정보는 [Driver Behavior](../IotDriverInsights/index.html){:new_window}를 참조하십시오.

# 관련 링크
{: #rellinks}

## API 참조
{: #api}
* [{{site.data.keyword.iot4auto_short}} API 문서](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [Context Mapping 서비스 API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [Driver Behavior 서비스 API]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## 관련 링크
{: #general}
* [{{site.data.keyword.iotdriverinsights_short}} 시작하기](../IotDriverInsights/index.html){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} 시작하기](../IotMapInsights/index.html){:new_window}
* [{{site.data.keyword.iot_full}} 시작하기](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Bluemix 서비스의 새로운 기능](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [IBM developerWorks의 dW Answers](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
