---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 디바이스 연결
{: #iotplatform_task}
마지막 업데이트 날짜: 2016년 9월 13일
{: .last-updated}

IoT 디바이스에서 데이터 수신을 시작하려면 {{site.data.keyword.iot_full}}에 연결해야 합니다. 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하려면 디바이스를 {{site.data.keyword.iot_short_notm}}에 등록한 다음 {{site.data.keyword.iot_short_notm}}에 연결하도록 등록 정보를 사용하여 디바이스를 구성해야 합니다.
{:shortdesc}

## 시작하기 전에
{: #byb}
 
연결 프로세스를 시작하기 전에 디바이스가 {{site.data.keyword.iot_short_notm}}과 통신하기 위한 다음 요구사항을 만족하는지 확인해야 합니다.

- 디바이스에서 [MQTT 형식](reference/mqtt/index.html)으로 디바이스 메시지를 전송하여 통신할 수 있어야 합니다.
- 디바이스 메시지는 {{site.data.keyword.iot_short_notm}} [메시지 페이로드](reference/mqtt/index.html#message-payload) 요구사항을 준수해야 합니다.

다음 단계를 완료하여 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하십시오.

## 1단계: {{site.data.keyword.iot_short_notm}}에 디바이스 등록  
{: #iotplatform_subtask1}

디바이스를 등록하려면 디바이스 유형으로 디바이스를 분류하고 디바이스에 이름을 제공하며 디바이스 정보를 제공해야 합니다. 그런 다음 연결 토큰을 제공하거나 {{site.data.keyword.iot_short_notm}}에서 생성된 토큰을 승인합니다.

{{site.data.keyword.iot_short_notm}} 대시보드에서 한 번에 하나씩 디바이스를 추가하거나 [{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/post_bulk_devices_add)를 사용하여 한 번에 하나 이상의 디바이스를 추가할 수 있습니다.

{{site.data.keyword.iot_short_notm}} 대시보드에서 디바이스를 추가하려면 다음을 수행하십시오.

1. {{site.data.keyword.Bluemix}} 대시보드에서 {{site.data.keyword.iot_short_notm}} 서비스 타일을 클릭하여 서비스 대시보드를 열거나 다음 URL을 사용하여 대시보드로 직접 이동합니다.

 `https://org_id.internetofthings.ibmcloud.com/dashboard/#/overview `

    여기서 *org_id*는 {{site.data.keyword.Bluemix}} 조직의 ID입니다.

2. 서비스 페이지에서 **대시보드 실행**을 클릭하여 {{site.data.keyword.iot_short_notm}} 조직 관리를 시작합니다.

3. 개요 대시보드의 메뉴 분할창에서 **디바이스**를 선택한 다음 **디바이스 추가**를 클릭합니다.
5. 추가할 디바이스의 디바이스 유형을 선택하거나 작성합니다.
{{site.data.keyword.iot_short_notm}}에 연결된 각 디바이스는 디바이스 유형과 연관되어야 합니다. 디바이스 유형은 공통 특성을 공유하는 디바이스 그룹입니다.
{{site.data.keyword.iot_short_notm}} 조직에 첫 번째 디바이스를 추가할 때 **디바이스 유형** 메뉴에 사용할 수 있는 디바이스 유형이 없습니다. 먼저 디바이스 유형을 작성해야 합니다.
 1. **디바이스 유형 작성**을 클릭합니다.
 2. `my_device_type`과 같은 이름과 디바이스 유형에 대한 설명을 입력합니다.
 3. 선택사항: 디바이스 유형 속성 및 메타데이터를 입력합니다.
 **팁:** 속성과 메타데이터는 나중에 추가하고 편집할 수 있습니다.
 4. **작성**을 클릭하여 새 디바이스 유형을 추가합니다.
10. **다음**을 클릭하여 선택한 디바이스 유형의 디바이스를 추가하는 프로세스를 시작합니다.
11. 디바이스 ID를 입력합니다. **팁:** 네트워크 연결 디바이스의 경우 구분하는 콜론이 없는 디바이스 MAC 주소 등이 될 수 있습니다.디바이스 ID는 {{site.data.keyword.iot_short_notm}} 대시보드에서 디바이스를 식별하는 데 사용하고 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하는 데도 필요한 매개변수입니다.
12. 선택사항: **추가 필드**를 클릭하여 일련 번호, 제조업체, 모델 등의 디바이스 정보를 추가합니다.
 **팁:** 이 정보는 나중에 추가하고 편집할 수 있습니다.
12. 선택사항: 디바이스 JSON 메타데이터를 입력합니다.
 **팁:** 디바이스 메타데이터는 나중에 추가하고 편집할 수 있습니다.
13. **다음**을 클릭하여 디바이스의 추가를 완료합니다.
14. 요약 정보가 올바른지 확인한 다음 **추가**를 클릭하여 연결을 추가합니다.
**팁:** 자동으로 생성된 인증 토큰을 승인하거나 인증 토큰을 직접 제공하는 옵션이 있습니다.
고유 토큰을 작성하도록 선택하는 경우 길이가 8 - 36자이며 대소문자가 혼합되어 있고, 숫자, 하이픈, 밑줄 또는 마침표가 포함되는지 확인합니다. 토큰에는 반복된 문자 시퀀스, 사전 단어, 사용자 이름 또는 기타 사전 정의된 시퀀스가 포함되지 않아야 합니다.
15. 디바이스 정보 페이지에서 다음 디바이스 정보를 복사하고 저장합니다.  
 - 조직 ID(예: `tubo8x`)
 - 디바이스 유형(예: `my_device_type`)
 - 디바이스 ID(예: `my_first_device`)
 - 인증 메소드(예: `token`)
 - 인증 토큰(예: `PtBVriRqIg4uh)_-Kl`)
  **팁:** {{site.data.keyword.iot_short_notm}}에 연결하도록 디바이스를 구성하는 데 조직 ID, 인증 토큰, 디바이스 유형 및 디바이스 ID가 필요합니다.  

축하합니다. 디바이스가 등록되었습니다. 이제 {{site.data.keyword.iot_short_notm}}에 연결하도록 디바이스를 구성할 수 있습니다.

## 2단계: {{site.data.keyword.iot_short_notm}}에 디바이스 연결
{: #iotplatform_subtask2}

{{site.data.keyword.iot_short_notm}}에 디바이스를 등록하고 나면 등록 정보를 사용하여 디바이스를 연결하고 디바이스 데이터 수신을 시작할 수 있습니다.

{{site.data.keyword.iot_short_notm}}에서는 여러 디바이스 유형을 지원합니다. 일반적으로 디바이스에 연결하는 기본 프로세스에는 다음 단계가 포함됩니다.
- MQTT 메시징에 사용할 디바이스를 설정하고 인증할 조직 ID, 인증 토큰, 디바이스 유형 및 디바이스 ID를 사용합니다.  
- MQTT 프로토콜을 사용하여 {{site.data.keyword.iot_short_notm}} 조직에 디바이스 메시지를 보냅니다.

**팁:** 일반적으로 사용되는 디바이스에 여러 연결 지침서를 사용할 수 있습니다. 지침서 목록은
IBM.com에서 사용 가능한 [디바이스 연결 지침서](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoT)를 참조하십시오.

디바이스에 연결할 때 다음 정보가 필요합니다.
- URL: *org_id*.messaging.internetofthings.ibmcloud.com
여기서 *org_id*는 {{site.data.keyword.iot_short_notm}} 조직의 ID입니다.
- 포트:
 - 1883
 - 8883(암호화됨)
 - 443(websockets)
- 디바이스 ID: d:*org_id*:*device_type*:*device_id*
이 매개변수 조합이 디바이스를 고유하게 식별합니다.
- 사용자 이름: use-token-auth
이 값은 사용자가 토큰 인증을 사용 중임을 표시합니다.
- 비밀번호: *Authentication token*
이 값은 사용자가 정의했거나 등록할 때 디바이스에 지정된 고유 토큰입니다.
- 이벤트 주제 형식: iot-2/evt/*event_id*/fmt/*format_string*
 여기서 *event_id*는 {{site.data.keyword.iot_short_notm}}에 표시된 이벤트 이름을 지정하고 *format_string*은 이벤트 형식(예: JSON)입니다.
- 메시지 형식: JSON
 {{site.data.keyword.iot_short_notm}}에서는 여러 형식을 지원합니다(예: JSON 및 텍스트).

디바이스 연결에 대한 자세한 정보는 기술 문서에서 [디바이스용 MQTT 연결](devices/mqtt.html)을 참조하십시오.
API 문서의 [연결](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Connectivity/post_device_types_deviceType_devices_deviceId_events_eventName) 섹션에는 필수 정보도 포함되어 있습니다.
