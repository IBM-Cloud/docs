---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.iotmapinsights_short}} 시작하기
{: #iotdriverinsights_index}
마지막 업데이트 날짜: 2016년 6월 22일
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}}은 사용자의 애플리케이션으로 전 세계의 도로망에 대해 최단 경로 검색 및 맵 매칭 등의 지리공간 기능을 사용하도록 해 주는 {{site.data.keyword.Bluemix}}의 서비스입니다.  
{:shortdesc}

{{site.data.keyword.iotmapinsights_short}} REST API를 통해 다음 기능을 사용할 수 있습니다.

|기능|용도...|
|:---|:---|
|매우 정확한 맵 매칭|실제 맵핑된 도로망에 GPS 위치 매칭|
|도로 기하 구조 데이터 검색|맵핑된 도로망을 검색하여 맵에 도로 형태 그리기|
|동적 최단 경로 검색|교통량 등의 실시간 이벤트를 통합하는 최단 경로 검색|
|실시간 교통 이벤트 조작|교통 상태와 같은 실시간의 맵 매칭된 이벤트를 추가하여 경로 계획 결과 개선|

## 시작하기 전에
{: #byb}

1. [{{site.data.keyword.Bluemix_notm}} 카탈로그](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}에서 서비스의 인스턴스를 추가할 때, 앱에 바인딩되지 않았는지 확인하고 자동으로 생성된 테넌트 ID, 사용자 이름 및 비밀번호 값을 기록해 두십시오. 나중에 {{site.data.keyword.iotmapinsights_short}} API를 통해 서비스에 액세스하는 데 이러한 값이 필요합니다.

2. [OpenStreetMap](http://www.openstreetmap.org/){: new_window}에 익숙해지십시오.  

 {{site.data.keyword.iotmapinsights_short}} 서비스는 WGS84 좌표로 도로망 데이터를 사용하며, 이는 [OpenStreetMap](http://www.openstreetmap.org/){: new_window}에서 추출됩니다. 자동차가 이동할 수 있는 도로만 분석에 사용됩니다.  

 다음 맵 지역이 지원됩니다.

|지역|맵 ID|
|:---|:---|
|유럽|map_id=1|
|아프리카|map_id=2|
|아시아|map_id=3|
|오스트레일리아 오세아니아|map_id=4|
|북아메리카|map_id=5|
|중앙아메리카|map_id=6|
|남아메리카|map_id=7|

## 맵 매칭
{: #map_matching}
원시 GPS 좌표를 맵 매칭된 좌표에 맵핑하려면 다음 단계를 완료하십시오.

1. 분석할 원시 GPS 좌표의 세트를 준비하십시오.
2. `mapMatching` API 명령을 사용하여 원시 GPS 좌표를 전송하십시오. 선택적으로 각 위치의 기수방위 각도를 도 단위로 설정하여 이동 방향을 지정하십시오.
 - 요청: 원시 GPS 데이터
 - 응답: 맵 매칭된 GPS 데이터, 링크 ID
3. 선택사항: `getLinkInformation` API 명령을 사용하여 도로 유형 데이터를 가져오십시오. `getLinkInformation` REST API를 사용하여 일치된 도로 형태 데이터를 일련의 좌표로 검색할 수 있습니다.
 - 요청: 링크 ID
 - 응답: 도로 유형

## 경로 검색
{: #route_searching}

다음 단계를 사용하여 지정된 기점 및 종점 좌표 사이의 최단 경로 정보를 찾으십시오.

1. 최단 경로에 대한 시작 및 종료 위치를 판별하십시오.
2. `routeSearch` REST API를 사용하여 시작 및 종료 좌표를 전송하십시오.
선택적으로, 각 위치의 기수방위 각도를 도 단위로 설정하여 이동 방향을 지정하십시오.
 - 요청: 기점 및 종점 좌표
 - 응답: 맵 매칭된 최단 경로

리턴된 링크 형태 데이터를 사용하여 발견된 경로의 형태를 맵에 그리십시오.

## 교통 이벤트 추가
{: #traffic_events}

{{site.data.keyword.iotmapinsights_short}} 서비스에 교통 이벤트 정보를 추가하려면 다음 단계를 완료하십시오.

1. 작성하려는 교통 이벤트의 유형 및 위치를 선택하십시오.
2. `createEvent` API 명령을 사용하여 이벤트를 삽입하십시오.
{{site.data.keyword.iotmapinsights_short}} 서비스에 교통 이벤트 정보를 전송하십시오.
 - 요청: 이벤트 정보
 - 응답: 이벤트 ID
3. `queryEvent` REST API 명령을 사용하여 이벤트를 찾으십시오.
특정 사각형 영역 내의 교통 이벤트를 검색하고, 선택적으로 특정 교통 이벤트 유형을 검색하십시오.
 - 요청: 영역 정보
 - 응답: 이벤트 정보  
4. 선택사항: `deleteEvent` API 명령을 사용하여 더 이상 유효하지 않은 교통 이벤트를 제거하십시오.
5. 선택사항: `getAffectedLinksInformation` API 명령을 사용하여 교통 이벤트에 의해 영향을 받는 도로의 영역을 검색하십시오.

# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 튜토리얼 파트1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 튜토리얼 파트2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive 스타터 애플리케이션](https://iot-automotive-starter.mybluemix.net){:new_window}

## API 참조
{: #api}

* [API 문서](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## 관련 링크
{: #general}

* [{{site.data.keyword.iotdriverinsights_short}} 시작하기](../IotDriverInsights/index.html){:new_window}
* [{{site.data.keyword.iot_full}} 시작하기](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [IBM developerWorks의 dW Answers](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Bluemix 서비스의 새로운 기능](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy; OpenStreetMap 기여자](http://www.openstreetmap.org/copyright){:new_window}
* [ODbL(Open Data Commons Open Database License)](http://opendatacommons.org/licenses/odbl/){:new_window}
