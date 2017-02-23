---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 기능 개요
{: #feature_overview}

{{site.data.keyword.iot_full}}은 다음 키 영역에서 빌드됩니다.

  1. 연결 - 디바이스를 연결하고 애플리케이션을 개발합니다.
  2. 정보 관리 - 디바이스 데이터를 저장하고 검토하며 {{site.data.keyword.iot_short_notm}}을 다른 서비스와 통합합니다.
  3. 분석 - {{site.data.keyword.iot_short_notm}} 대시보드를 사용하여 실시간 디바이스 데이터를 시각화합니다.
  4. 위험 관리 - 사용자와 애플리케이션에 대한 액세스 제어를 사용하여 보안 연결과 아키텍처를 구성합니다.

## 연결
{: #connect}

{{site.data.keyword.iot_short_notm}} 연결은 {{site.data.keyword.iot_short_notm}} 서비스의 시작점입니다. 디바이스 연결, 애플리케이션 작성, 디바이스 제어 및 써드파티 서비스와 통합은 모두 {{site.data.keyword.iot_short_notm}} 연결에서 사용 가능합니다.

### 게이트웨이 디바이스

게이트웨이가 없으면 인터넷에 연결할 수 없는 {{site.data.keyword.iot_short_notm}}에 디바이스를 연결하는 데 게이트웨이를 사용합니다. 게이트웨이는 디바이스의 모든 기능을 가지며 게이트웨이에 연결된 디바이스 대신 공개 및 구독을 수행할 수도 있습니다. 인터넷에 연결할 수 없는 센서 그룹은 게이트웨이 디바이스를 통해 해당 데이터를 게이트웨이에 전송하여 {{site.data.keyword.iot_short_notm}}에 연결할 수 있습니다. 자세한 정보는 [게이트웨이 개발](https://console.ng.bluemix.net/docs/services/IoT/gateways/gw_dev_index.html)을 참조하십시오.

### 디바이스 관리

디바이스 관리 기능은 디바이스 관리 API와 디바이스에 설치된 디바이스 관리 에이전트를 통해 제공됩니다. 디바이스 관리 에이전트가 있는 디바이스는 디바이스 관리 조치를 수행할 수 있으며, 이 조치는 기본 {{site.data.keyword.iot_short_notm}} 대시보드 또는 디바이스 관리 API를 통해 트리거할 수 있습니다. 디바이스 관리 조치에는 재부팅, 펌웨어 업데이트 다운로드 및 설치, 팩토리 설정으로 디바이스 재설정 등이 있습니다. 디바이스 관리는 사용자 정의 관리 조치를 포함하도록 확장할 수도 있습니다. 자세한 정보는 [디바이스 관리 문서](https://console.ng.bluemix.net/docs/services/IoT/devices/device_mgmt/index.html)를 참조하십시오. 

### 확장기능 및 서비스 통합

확장기능 및 서비스 통합을 통해 외부 서비스와 코어 서비스의 사용자 정의 확장기능을 모두 {{site.data.keyword.iot_short_notm}}의 인스턴스에 추가할 수 있습니다. {{site.data.keyword.iot_short_notm}}과 통합할 수 있는 외부 서비스에는 디바이스 위치에서 현재 날씨를 찾을 수 있는 The Weather Company 날씨 위치 서비스, Jasper SIM 데이터 및 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}이 포함됩니다. 써드파티 서비스 통합 및 확장기능에 대한 자세한 정보는 [외부 서비스 통합](https://console.ng.bluemix.net/docs/services/IoT/reference/extensions/index.html)을 참조하십시오.

---

## 정보 관리
{: #information_management}

{{site.data.keyword.iot_short_notm}} 정보 관리에서는 {{site.data.keyword.iot_short_notm}} 서비스에 도달한 후 디바이스에서 보낸 데이터를 제어합니다. 정보 관리에는 데이터 스토리지와 변환이 포함됩니다.

### 디바이스 마지막 이벤트 캐시

{{site.data.keyword.iot_short_notm}} 마지막 이벤트 캐시 API를 사용하면 디바이스에서 보낸 마지막 이벤트를 검색할 수 있습니다. 이 작업은 디바이스의 온라인 또는 오프라인 여부에 상관없이 작동하므로, 디바이스의 실제 위치나 사용 상태와 무관하게 디바이스 상태를 검색할 수 있습니다. 디바이스의 마지막 이벤트 데이터는 최대 365일 전에 발생한 특정 이벤트에 대해서만 검색할 수 있습니다.

### 디바이스 이벤트 데이터 저장

{{site.data.keyword.iot_short_notm}} 서비스의 디바이스 이벤트 데이터는 나중에 사용하도록 저장할 수 있습니다. 데이터 저장은 해당 데이터를 통해 이해하기 위해 통찰력 있는 분석을 수행하는 데 중요한 첫 번째 단계입니다. 예를 들어, 오랜 기간 동안 변경사항을 추적하고 Watson API 및 코그너티브 컴퓨팅 사용 등의 강력한 분석 도구와 사용하도록 데이터 세트를 저장할 수 있습니다.자세한 정보는 [{{site.data.keyword.cloudant_short_notm}} 히스토리언 서비스 연결](https://console.ng.bluemix.net/docs/services/IoT/cloudant_connector.html) 또는 [{{site.data.keyword.messagehub}} 히스토리언 서비스 연결](https://console.ng.bluemix.net/docs/services/IoT/message_hub.html)을 참조하십시오. 

---

## 분석
{: #analytics}

### 실시간 디바이스 데이터 시각화

대시보드 카드를 사용하여 실시간 디바이스 데이터를 시각화하고 표시할 수 있습니다. 대시보드 카드는 실시간으로 디바이스 데이터를 모니터하고 표시하므로, 키 디바이스 또는 디바이스 데이터를 계속 추적할 수 있습니다. 실시간 디바이스 데이터의 컨텍스트와 상태에 신속하게 액세스할 수 있도록 이러한 시각화는 기본 {{site.data.keyword.iot_short_notm}} 대시보드에 표시됩니다.자세한 정보는 [실시간 데이터 시각화](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html)를 참조하십시오.

### 에지 및 클라우드 분석

{{site.data.keyword.iot_short_notm}} 클라우드 분석을 사용하면 실시간 디바이스 데이터를 기반으로 하며 충족 시에 경보 및 선택적 조치를 트리거하는 규칙 조건을 지정합니다. 예를 들어, 디바이스를 떨어뜨리거나 디바이스의 온도가 급등할 때 경보가 사용자 디바이스의 대시보드로 전송되며 이메일이 관리자에게 발송되는지를 확인하는 규칙을 작성할 수 있습니다. 자세한 정보는 [클라우드 분석 문서](https://console.ng.bluemix.net/docs/services/IoT/cloud_analytics.html)를 참조하십시오.

에지 분석을 사용하여 클라우드에서 에지 분석 사용 게이트웨이로 분석 규칙 트리거 프로세스를 이동하면 디바이스 가까이에서 분석 처리를 수행하여 클라우드에 대한 디바이스 데이터 트래픽 양을 현저히 줄일 수 있습니다.
자세한 정보는 [에지 분석 문서](https://console.ng.bluemix.net/docs/services/IoT/edge_analytics.html)를 참조하십시오. 

---

## 위험 관리
{: #risk_management}

### 보안 연결 및 아키텍처

{{site.data.keyword.iot_short_notm}}의 아키텍처는 디바이스가 다른 디바이스로 위장하지 못하게 하므로 디바이스 데이터의 무결성을 유지보수합니다. 디바이스에서 사용자만 아는 클라이언트 ID와 인증 토큰의 조합을 사용하여 {{site.data.keyword.iot_short_notm}}에 연결합니다. 디바이스를 등록하거나 API 키가 생성되고 나면 신임 정보의 보안을 유지보수하기 위해 인증 토큰이 솔트(salt)되고 해시됩니다. 

위험 및 보안 관리 추가 기능을 사용하면 서버와 디바이스 간의 모든 연결점이 증명된 신임 정보로 인증되도록 {{site.data.keyword.iot_short_notm}} 보안을 향상시킬 수 있습니다. 이 추가 기능을 사용하는 경우에는 {{site.data.keyword.iot_short_notm}}에서 사용되는 사용자 ID 및 토큰 이외에 인증서 및 TLS(Transport Layer Security) 인증이 사용됩니다. 디바이스와 서버 간의 통신 중 서버 액세스 권한이 포함된 유효한 인증서가 없는 디바이스는 유효한 사용자 ID 및 암호를 사용하더라도 위험 및 보안 관리 추가 기능에 구성된 대로 액세스가 거부됩니다. 

---
