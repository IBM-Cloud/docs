---

copyright:
years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 디바이스에서 The Weather Company의 데이터 사용
{: #weathercompany}

The Weather Company 통합을 통해 날씨 데이터를 기존 {{site.data.keyword.iot_short_notm}} 디바이스에 결합시킬 수 있습니다.
{:shortdesc}

API를 사용하여 업데이트 위치 요청이 작성되었거나 디바이스 관리 메시지를 사용하여 디바이스가 이미 해당 위치를 설정한 경우 The Weather Company의 날씨 데이터가 디바이스 세부사항 보기에 표시됩니다.

**중요:** 관리 디바이스만 고유 위치를 설정할 수 있습니다. 모든 비관리 디바이스에 API를 사용하여 수동으로 설정된 위치가 있어야 합니다. 디바이스 위치 설정에 대한 자세한 정보는 [위치 찾기 요청](../../devices/device_mgmt/index.html#update-location)을 참조하십시오.

### The Weather Company용 REST API
The Weather Company용 REST API에 액세스하려면 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![외부 링크 아이콘](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} 문서의 디바이스 위치 날씨 절을 참조하십시오. 

### 날씨 데이터 보기

디바이스 위치에 대해 검색된 날씨 데이터를 보려면 다음을 수행하십시오. 
1. **디바이스** 분할창에서 디바이스를 클릭하십시오. 
2. 상세 디바이스 보기에서 **확장기능** 섹션까지 아래로 화면이동하십시오.   
다음 날씨 데이터가 나열됩니다.
 - 현재 날씨.
 - 현재 온도.
 - 예상된 최대 및 최저 온도.
 - 상대 습도.
 - 기압.
 - 가시성.
 - 풍속.
 - 풍향.
 - 위도.
 - 경도.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
