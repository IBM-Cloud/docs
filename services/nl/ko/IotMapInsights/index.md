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
{: #gettingstartedtemplate}
*마지막 업데이트 날짜: 2016년 5월 13일*

{{site.data.keyword.iotmapinsights_full}}을 사용하면 개발자가 쉽게 자신의 애플리케이션에서 전 세계의 도로망을 기반으로 맵 매칭 및 최단 경로 검색 등의 지리공간 기능을 사용할 수 있습니다.
{:shortdesc}

{{site.data.keyword.iotmapinsights_short}} REST API를 통해 다음 기능을 사용할 수 있습니다.

- 도로망 기하 구조를 사용하는 매우 정확한 맵 매칭
- 교통량과 같은 실시간 이벤트를 맵에서 처리
- 교통량과 같은 실시간 이벤트를 고려하는 동적 최단 경로 검색(루트 검색)
- 맵에 도로 형태를 그리는 데 사용할 수 있는 도로 기하 구조 데이터 검색

{{site.data.keyword.iotmapinsights_short}} 서비스는 OpenStreetMap에서 추출한 WGS84 좌표 형식의 도로망 데이터를 사용합니다. 차량이 이동할 수 있는 도로만 분석에 사용됩니다.

지원되는 맵 지역은 다음과 같습니다.

- 유럽(map_id=1)
- 아프리카(map_id=2)
- 아시아(map_id=3)
- 오세아니아 오스트레일리아(map_id=4)
- 북미(map_id=5)
- 중미(map_id=6)
- 남미(map_id=7)


다음 단계에 따라 {{site.data.keyword.iotmapinsights_short}} 서비스의 분석 기능을 사용하십시오.

## 맵 매칭에 {{site.data.keyword.iotmapinsights_short}} 사용

1. 분석할 원시 GPS 좌표 데이터를 준비하십시오.
2. `mapMatching` REST API를 사용하여 {{site.data.keyword.iotmapinsights_short}} 서비스에 시계열 순서로 원시 GPS 좌표 데이터를 전송하십시오. 선택적으로, 각 위치의 기수방위 각도를 도 단위(북쪽은 0, 시계방향 각도)로 설정하여 이동 방향을 지정하십시오.
3. `mapMatching` REST API 호출에 대한 응답으로 맵 매칭 좌표 및 연계 도로 정보를 수신하십시오.
4. 선택적으로, `getLinkInformation` REST API를 사용하여 맵 매칭 연계 도로의 도로 형태 데이터를 수신하십시오. 링크 ID와 함께 `getLinkInformation` REST API를 호출하여 도로 형태로 구성된 일련의 좌표를 가져오십시오.

## 루트 검색에 {{site.data.keyword.iotmapinsights_short}} 사용

1. 최단 경로를 얻을 시작 및 종료 위치를 판별하십시오.
2. `routeSearch` REST API를 사용하여 시작 및 종료 좌표를 {{site.data.keyword.iotmapinsights_short}} 서비스에 전송하십시오. 선택적으로, 각 위치의 기수방위 각도를 도 단위(북쪽은 0, 시계방향 각도)로 설정하여 이동 방향을 지정하십시오.
3. `routeSearch` REST API 호출에 대한 응답으로 연계 도로의 목록을 수신하십시오. 결과 데이터에 포함되는 형태 데이터를 사용하여 맵에서 발견된 경로의 형태를 그릴 수 있습니다.

## 교통 이벤트 처리에 {{site.data.keyword.iotmapinsights_short}} 사용

1. 작성할 교통 이벤트의 유형 및 위치를 판별하십시오.
2. `createEvent` REST API를 사용하여 교통 이벤트 정보를 {{site.data.keyword.iotmapinsights_short}} 서비스에 전송하십시오.
3. `createEvent` REST API 호출에 대한 응답으로 작성된 교통 이벤트의 이벤트 ID를 수신하십시오.
4. `queryEvent` REST API를 사용하여 특정 사각형 영역 내에서, 선택적으로 특정 교통 이벤트 유형을 사용하여 교통 이벤트를 검색하십시오.

- 선택적으로, `deleteEvent` REST API를 사용하여 더 이상 유효하지 않은 교통 이벤트를 제거하십시오.
- 선택적으로, `getAffectedLinksInformation` REST API를 사용하여 교통 이벤트에 의해 영향을 받는 도로의 영역을 검색하십시오.


# 관련 링크
{: #rellinks}
## 학습서 및 샘플
{: #samples}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 학습서 파트1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 학습서 파트2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

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

