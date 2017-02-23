----

copyright:
  years: 2015, 2016, 2017

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}}에서 디바이스 개발
{: #device_dev_index}

마지막 업데이트 날짜: 2016년 11월 26일
{: .last-updated}

디바이스는 인터넷에 연결되어 있으며 클라우드에 전송하거나 이로부터 수신할 데이터가 있는 모든 대상입니다. 디바이스를 사용하여 이벤트 정보(예: 센서 측정값)를 클라우드에 전송하고 클라우드의 애플리케이션에서 명령을 받을 수 있습니다. 

디바이스는 이벤트를 사용하여 {{site.data.keyword.iot_short_notm}}에 데이터를 공개합니다. 디바이스는 이벤트의 컨텐츠를 제어하며 전송된 각 이벤트마다 이름을 지정합니다. 이벤트가 {{site.data.keyword.iot_short_notm}}에 의해 디바이스에서 수신되는 경우, 이벤트가 수신된 연결의 신임 정보는 어떤 디바이스에서 이벤트가 전송되었는지를 판별하는 데 사용됩니다. 이 아키텍처는 디바이스가 다른 디바이스로 위장하지 못하도록 방지합니다. 

디바이스를 포함하여 핵심 개념에 대한 자세한 정보는 [Watson IoT Platform 정보](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts)를 참조하십시오. 


# {{site.data.keyword.iot_short_notm}}에 디바이스 연결
{: #device_connect}
HTTP 또는 MQTT 프로토콜을 사용하여 {{site.data.keyword.iot_short_notm}}에 디바이스를 연결할 수 있습니다. 요청-응답 시나리오를 구성하려면 HTTP를 사용하십시오(예: 누군가 구매를 실행하고 수신확인을 받는 경우). 이벤트 시나리오를 구성하려면 MQTT를 사용하십시오(예: 누군가 초인종을 누르면 모바일 디바이스에서 경보가 트리거되도록 하는 경우). 

{{site.data.keyword.iot_full}}에 연결할 수 있으려면 디바이스를 조직에 등록해야 합니다. {{site.data.keyword.iot_short_notm}}에 안전하게 연결하려면 Bluemix 계정에 등록하고 자체 {{site.data.keyword.iot_short_notm}} 조직을 작성해야 합니다. 그리고 이 조직의 ID를 사용하여 디바이스를 등록할 수 있습니다. 등록된 디바이스는 고유 디바이스 ID(예: MAC 주소)와 해당 디바이스에만 허용된 인증 토큰으로 {{site.data.keyword.iot_short_notm}}에게 자신을 식별합니다. 일단 안전하게 연결되면 Bluemix를 사용하여 자체 애플리케이션을 빌드하십시오. Node-RED를 사용하여 애플리케이션을 함께 연결하십시오. 

등록 없이 디바이스를 연결하려면(예: 개념 증명을 실행하기 위해) 특수 조직 ID `QuickStart`를 사용하여 이를 수행할 수 있습니다. `QuickStart`는 클라우드에서 실행되는 {{site.data.keyword.iot_short_notm}}의 공용 샌드박스 인스턴스입니다. 안전하게 연결할 필요가 없으면 `QuickStart`를 사용하여 디바이스 연결을 테스트하고 {{site.data.keyword.iot_short_notm}}에서 시험해 보십시오. 시험이 완료되면 TLS 및 인증 토큰을 사용하여 디바이스를 안전하게 자신의 특정 조직 ID 인스턴스에 다시 연결하십시오. 

HTTP 프로토콜을 사용하여 {{site.data.keyword.iot_short_notm}}에 디바이스 연결에 대한 자세한 정보는 [디바이스용 HTTP REST API](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html)를 참조하십시오.
MQTT 프로토콜을 사용하여 {{site.data.keyword.iot_short_notm}}에 디바이스 연결에 대한 자세한 정보는 [디바이스용 MQTT 연결](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html)을 참조하십시오. 

# 디바이스 개발 시작하기
{: #get_started}
{{site.data.keyword.iot_short_notm}}에 이미 사용되는 디바이스가 있으면 간단하게 이를 사용하여 시작할 수 있습니다. 

아직 사용되는 디바이스가 없으면 [developerWorks](https://developer.ibm.com/recipes/)에서 사용 가능한 레시피를 확인하십시오. 기존 레시피를 찾아보고 디바이스에 해당되는 레시피가 있는지 여부를 확인하십시오. 레시피를 사용하면 개발을 시작하는 데 도움이 됩니다. 원하는 경우에는 자체 레시피를 공개할 수도 있습니다. 

특정 디바이스에 대한 레시피를 찾을 수 없는 경우, IBM은 사용자가 시작하는 데 사용할 수 있는 다수의 프로그래밍 안내서와 API를 제공합니다. 이러한 안내서에는 디바이스와 애플리케이션을 통합하고 이를 {{site.data.keyword.iot_short_notm}}에 연결하기 위한 코드를 빌드하고 개발하는 데 도움이 될 수 있는 클라이언트 라이브러리, 샘플 및 정보가 포함되어 있습니다. 현재 다음 프로그래밍 안내서를 사용할 수 있습니다. 

- Java
- Node.js
- Embedded C
- ARM mBed C++
- Python
- C#
- Node-RED

사용 가능한  프로그래밍 안내서에 대한 링크 및 자세한 정보는 [{{site.data.keyword.iot_short_notm}} 개발용 클라이언트 라이브러리](../iot_platform_client_lib.html)를 참조하십시오. 

적합한 {{site.data.keyword.iot_short_notm}} 프로그래밍 안내서를 찾을 수 없으면, 자체 프로그램을 작성하고 MQTT 또는 HTTP 프로토콜을 사용하여 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결할 수 있습니다. 

MQTT는 OASIS 표준 조직에서 관리하며 ISO에서 국제적으로 인정하는 개방형 표준입니다. 자세한 정보는 [OASIS MQTT(Message Queuing Telemetry Transport)](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt)를 참조하십시오. 

다음 환경을 포함하여 많은 서로 다른 시스템에 대해 매우 다양한 MQTT 클라이언트 라이브러리를 사용할 수 있습니다. 
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

MQTT에 대한 자세한 정보는 [MQTT 메시징](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3)을 참조하십시오. 
