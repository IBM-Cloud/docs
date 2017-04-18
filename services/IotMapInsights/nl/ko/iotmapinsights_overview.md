---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.iotmapinsights_short}} 정보
{: #iotmapinsights_overview}
마지막 업데이트 날짜: 2016년 7월 20일
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}}은 정적 도로망 데이터 및 동적 이벤트 데이터에 신속히 액세스하는 데 사용할 수 있는 {{site.data.keyword.Bluemix_notm}}의 서비스입니다. 또한 {{site.data.keyword.iotmapinsights_short}}은 도로망에 대한 지리공간 도구를 제공하며, 사용자는 이를 사용하여 사용자의 애플리케이션에 지리공간 기능을 통합할 수 있습니다.
{:shortdesc}

{{site.data.keyword.iotmapinsights_short}} 서비스는 다음 기능을 제공합니다.

- 정적 맵 데이터
- 동적 이벤트 데이터
- 지리공간 도구

{{site.data.keyword.iotmapinsights_short}} 서비스는 처리를 위해 서비스 메모리 캐시에 저장된 [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 도로망 데이터를 수집하고 사용합니다.

OpenStreetMap의 데이터는 OpenStreetMap Foundation(OSMF)의 Open Data Common Open Database License(ODbL)에 따라 사용 가능합니다. 자세한 정보는 [OpenStreetMap 저작권 및 라이센스](http://www.openstreetmap.org/copyright){: new_window}를 참조하십시오.

## 정적 맵 데이터
{: #static_map_data_query}

제품의 주요 기능 중 하나는 사용자의 애플리케이션과 함께 사용할 수 있는 자세한 도로 정보를 검색하는 기능입니다. 링크 조회 REST API 인터페이스를 사용하여 링크 ID로 정적 맵 도로 속성 데이터를 조회하십시오. {{site.data.keyword.iotmapinsights_short}}의 [맵 매칭 기능](#map_matching)을 사용하여 필요한 링크 ID 매개변수를 식별하십시오.

리턴되는 데이터에는 요청된 링크 ID에 대한 다음 정보가 포함됩니다.

- 도로 유형
- 도로 길이
- 자세한 형태 지점(shape point)의 배열
- 인접 노드 및 인접 링크에 대한 정보

세부 연계 도로 정보를 조회함으로써 사용자의 애플리케이션은 리턴된 인접 링크 정보를 지능적으로 사용하여 연계 도로망을 순회할 수 있습니다.

## 동적 이벤트 데이터
{: #dynamic_event_data}

정적 맵 데이터와 별도로, 교통 정체 및 도로 공사와 같은 동적 이벤트가 필요에 의해 도로의 실제 상태에 포함됩니다. {{site.data.keyword.iotmapinsights_short}}을 사용하여 경로 계획 용도로 교통 이벤트를 작성하고, 관리하고, [영향을 받는 링크 검색](#link_search)과 통합하십시오.

### 이벤트 삽입 및 삭제
{: #inject_event}

{{site.data.keyword.iotmapinsights_short}} 서비스 이벤트 삽입 REST API를 사용하여 특정 연계 도로에 배치되는 맵 오브젝트 모델 양식의 교통 이벤트를 동적으로 삽입하고 제거하십시오. 각 이벤트에는 GPS 좌표, 시작 시간, 이벤트 유형, 이벤트 지속 기간 및 영향을 받는 도로 길이 등의 기본 속성이 포함됩니다.

이벤트 삭제 REST API 인터페이스를 사용하여 더 이상 사용되지 않는 맵의 이벤트를 제거하십시오.

### 이벤트 조회
{: #query_event}

이벤트 조회 REST API를 사용하여 특정 지리 영역의 모든 동적 이벤트에 대한 자세한 정보를 가져오십시오. 경도 및 위도 범위의 영역으로 조회하고 이벤트 속성을 포함하여 리턴되는 대상 이벤트의 수를 좁힐 수 있습니다.

## 지리공간 도구
{: #geospatial_tools}

{{site.data.keyword.iotmapinsights_short}} 지리공간 도구에서 제공되는 맵 매칭 및 경로 검색 기능으로 애플리케이션을 향상시키십시오.

### 맵 매칭
{: #map_matching}

사용자의 애플리케이션과 함께 맵 매칭 REST API 인터페이스를 사용하여 실제 디바이스 GPS 좌표를 [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 도로망 데이터에 맵핑해서 부정확한 GPS 데이터의 위치 정확성을 높이십시오. 또한 위치에 기반하여 도로 속성에 대한 정보를 수신할 수 있습니다. 맵 매칭 REST API를 사용하면 사용자의 애플리케이션이 원시 GPS 데이터 지점을 연계 도로의 일치된 지점에 맞출 수 있습니다.

맵 매칭 REST API 인터페이스는 한 지점의 경도 및 위도 GPS 좌표 데이터를 수신하여 맵 매칭된 지점을 리턴합니다. 맵 매칭된 지점은 특정 기간 내의 각 자동차에 대한 히스토리 데이터를 고려하여 분석되어 실시간으로 가장 가능성이 높은 지점을 발견합니다. 히스토리 위치 데이터가 없는 지점의 경우, 맵 매칭 인터페이스가 요청된 GPS 지점에서 가장 가까운 연계 도로 상의 지점을 리턴합니다.

### 경로 검색
{: #route_search}

지리공간 기능이 있는 애플리케이션의 기본 기능 중 하나는 두 지점 사이의 최단 경로를 찾는 기능입니다.  

{{site.data.keyword.iotmapinsights_short}} 서비스의 경로 검색 REST API 인터페이스는 시작 및 종료 지점 GPS 좌표 간의 최단 경로를 계산합니다. 수신된 좌표는 맵 매칭 기능을 사용하여 맵의 가장 가까운 링크에 일치되며 해당되는 맵 매칭된 지점 간의 최단 경로가 계산됩니다.

### 영향을 받는 링크 검색
{: #link_search}

도로에서 이벤트가 발생하는 경우, 다양한 연계 도로에 영향을 미칠 수 있습니다. REST API를 사용하여 영향을 받는 링크를 검색하고 자동차가 이벤트에 도달할 수 있는 연계 도로도 찾을 수 있습니다. 검색은 자동차에서 이벤트까지의 거리뿐만 아니라 연계 도로망의 토폴로지도 고려합니다.
