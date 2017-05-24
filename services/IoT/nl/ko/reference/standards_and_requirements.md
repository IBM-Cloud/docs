---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# 표준 및 요구사항
{: #standards_and_requirements}

{{site.data.keyword.iot_full}}에서는 메시징과 일반 디바이스 및 애플리케이션 개발을 위한 다수의 표준 및 요구사항을 지원합니다.
{:shortdesc}


<!-- ## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} supports the following versions of the Hyperledger fabric:
- 0.5

## Python
{: #python}

Support for MQTT over SSL requires at least Python v2.7.9 or v3.4, and OpenSSL v1.0.1.
-->

## MQTT
{: #mqtt}

{{site.data.keyword.iot_short_notm}}에서는 다음 버전의 MQTT 메시징 프로토콜을 지원합니다.

MQTT 버전 | 참고
--- | --- | ---
[3.1.1 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.oasis-open.org/standards#mqttv3.1.1){: new_window}(권장)  | <ul><li>OASIS Standard.<li>ISO 표준(ISO/IEC PRF 20922) <li>V3.1과 비교하여 프로토콜의 정의가 보다 정밀하므로 다양한 클라이언트와 서버 간의 상호 운용성이 개선됩니다. <li>MQTT 클라이언트 ID(ClientId)의 최대 길이는 V3.1에서 부여한 23자 한계에서 256자로 증가됩니다. </br>{{site.data.keyword.iot_short_notm}} 서비스에는 종종 더 긴 클라이언트 ID가 필요합니다. </br>긴 클라이언트 ID는 MQTT 프로토콜 버전과 상관없이 지원됩니다. 단, 일부 V3.1 클라이언트 라이브러리에서는 ClientId 값의 길이를 검사하여 23자 한계를 적용합니다.</ul>
3.1 | MQTT V3.1은 현재 가장 광범위하게 사용되는 프로토콜 버전입니다.

{{site.data.keyword.iot_short_notm}}에서는 MQTT 표준에서 허용하는 모든 컨텐츠를 지원합니다. MQTT에서는 모든 데이터를 사용할 수 있으므로 이미지, 임의 인코딩 체계로 된 텍스트, 암호화된 데이터 및 2진 형식의 거의 모든 데이터 유형을 전송할 수 있습니다. MQTT 표준에 대한 자세한 정보는 다음 리소스를 참조하십시오.
- [MQTT.org ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://mqtt.org/){: new_window}
- [HiveMQ: MQTT 소개 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt){: new_window}

{{site.data.keyword.iot_short_notm}}에서의 특정 유스 케이스와 관련된 메시지 페이로드 크기 한계 및 형식 제한사항에 대해서는 [MQTT 메시징](mqtt/index.html)을 참조하십시오.
