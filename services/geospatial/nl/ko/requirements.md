---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#서비스 요구사항
{: #requirements}


##MQTT 디바이스 메시지 요구사항

* MQTT 메시지 브로커는 하나 이상의 MQTT 주제에 대한 디바이스 메시지를 JSON 형식으로 제공해야 합니다. 
* 디바이스 메시지는 여러 속성을 포함할 수 있지만 다음 세 가지 속성은 항상 필수입니다. 
	* 디바이스를 고유하게 식별하는 속성
	* 현재 디바이스 위치의 위도를 지정하는 속성
	* 현재 디바이스 위치의 경도를 지정하는 속성
* 지원되는 두 가지 메시지 모드는 다음과 같습니다. 
	* MQTT 메시지는 단일 디바이스에 대한 정보가 있는 JSON 오브젝트를 포함할 수 있습니다. 
	* MQTT 메시지는 디바이스 세트에 대한 정보가 있는 JSON 오브젝트 배열을 포함할 수 있습니다. 

##MQTT 이벤트 및 서비스 구성

애플리케이션은 MQTT 메시지를 구독하고 해당 [REST API](https://console.ng.bluemix.net/apidocs/246)를 통해 {{site.data.keyword.geospatialshort_Geospatial}}를 제어합니다. 다음 조치는 REST API 호출을 통해 사용할 수 있습니다. 

* 서비스를 구성하고 시작합니다. 
* 모니터할 지리적 지역을 추가하고 제거합니다. 
* 서비스 상태 및 현재 정의된 지역의 세트에 대한 정보를 검색합니다. 
* 서비스를 중지합니다. 
* 이미 구성된 서비스를 다시 시작합니다. 

