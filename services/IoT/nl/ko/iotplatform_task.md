---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 디바이스 연결
{: #iotplatform_task}

IoT 디바이스에서 데이터 수신을 시작하려면 {{site.data.keyword.iot_full}}에 연결해야 합니다. 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하려면 디바이스를 {{site.data.keyword.iot_short_notm}}에 등록한 다음 {{site.data.keyword.iot_short_notm}}에 연결하도록 등록 정보를 사용하여 디바이스를 구성해야 합니다.
{:shortdesc}

## 시작하기 전에
{: #byb}

연결 프로세스를 시작하기 전에 디바이스가 {{site.data.keyword.iot_short_notm}}과 통신하기 위한 다음 요구사항을 만족하는지 확인해야 합니다.

- 디바이스가 HTTP 또는 MQTT 프로토콜을 사용하여 통신할 수 있어야 합니다. 
- 디바이스 메시지가 {{site.data.keyword.iot_short_notm}} 메시지 페이로드 요구사항을 준수해야 합니다. 

자세한 정보는 [Watson IoT Platform에서 디바이스 개발](https://console.ng.bluemix.net/docs/services/IoT/devices/device_dev_index.html)을 참조하십시오. 

다음 단계를 완료하여 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하십시오.

## 1단계: {{site.data.keyword.iot_short_notm}}에 디바이스 등록  
{: #iotplatform_subtask1}

디바이스를 등록하려면 디바이스 유형으로 디바이스를 분류하고 디바이스에 이름을 제공하며 디바이스 정보를 제공해야 합니다. 그런 다음 연결 토큰을 제공하거나 {{site.data.keyword.iot_short_notm}}에서 생성된 토큰을 승인합니다.

{{site.data.keyword.iot_short_notm}} 대시보드에서 한 번에 하나씩 디바이스를 추가하거나 [{{site.data.keyword.iot_short_notm}} API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration){: new_window}를 사용하여 하나 이상의 디바이스를 한 번에 추가할 수 있습니다. 

{{site.data.keyword.iot_short_notm}} 대시보드에서 디바이스를 추가하려면 다음을 수행하십시오.

1. {{site.data.keyword.Bluemix}} 대시보드의 {{site.data.keyword.iot_short_notm}} 서비스 타일을 클릭하십시오. 

2. 서비스 페이지에서 {{site.data.keyword.iot_short_notm}} 조직에 대한 관리를 시작하려면 **시작**을 클릭하십시오. 

  {{site.data.keyword.iot_short_notm}} 웹 콘솔은 새 브라우저 탭에서 다음 URL을 엽니다. 

 ```
 https://org_id.internetofthings.ibmcloud.com/dashboard/#/overview
 ```

    여기서 *org_id*는 [{{site.data.keyword.iot_short_notm}} 조직 ](iotplatform_overview.html#organizations){: new_window}의 ID입니다. 

3. 개요 대시보드의 메뉴 분할창에서 **디바이스**를 선택한 다음 **디바이스 추가**를 클릭합니다.
5. 추가할 디바이스의 디바이스 유형을 선택하거나 작성합니다.  
{{site.data.keyword.iot_short_notm}}에 연결된 각 디바이스는 디바이스 유형과 연관되어야 합니다. 디바이스 유형은 공통 특성을 공유하는 디바이스 그룹입니다.  
{{site.data.keyword.iot_short_notm}} 조직에 첫 번째 디바이스를 추가할 때 **디바이스 유형** 메뉴에 사용할 수 있는 디바이스 유형이 없습니다. 먼저 디바이스 유형을 작성해야 합니다.
 1. **디바이스 유형 작성**을 클릭합니다.
 2. 디바이스 유형 이름(예: `my_device_type`)과 디바이스 유형에 대한 설명을 입력합니다.   
 **중요:** 디바이스 유형 이름은 36자 이하여야 하며 다음 문자만 포함할 수 있습니다.
 <ul>
  <li>영숫자 문자(a-z, A-Z, 0-9)</li>
  <li>하이픈(-)</li>
  <li>밑줄(&lowbar;)</li>
  <li>마침표(.)</li>
  </ul>
 3. 선택사항: 디바이스 유형 속성 및 메타데이터를 입력합니다.    
 **팁:** 속성과 메타데이터는 나중에 추가하고 편집할 수 있습니다.
 4. **작성**을 클릭하여 새 디바이스 유형을 추가합니다.
10. **다음**을 클릭하여 선택한 디바이스 유형의 디바이스를 추가하는 프로세스를 시작합니다.
11. 디바이스 ID(예: `my_first_device`)를 입력합니다.  
디바이스 ID는 {{site.data.keyword.iot_short_notm}} 대시보드에서 디바이스를 식별하는 데 사용하고 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하는 데도 필요한 매개변수입니다.  
**중요:** 디바이스 ID는 36자 이하여야 하며 다음 문자만 포함할 수 있습니다.
 <ul>
 <li>영숫자 문자(a-z, A-Z, 0-9)</li>
 <li>하이픈(-)</li>
 <li>밑줄(&lowbar;)</li>
 <li>마침표(.)</li>  
 </ul>
 **팁:** 네트워크 연결 디바이스의 경우 디바이스 ID는 예를 들어, 구분하는 콜론이 없는 디바이스 MAC 주소일 수 있습니다.  
12. 선택사항: **추가 필드**를 클릭하여 일련 번호, 제조업체, 모델 등의 디바이스 정보를 추가합니다.  
 **팁:** 이 정보는 나중에 추가하고 편집할 수 있습니다.
12. 선택사항: 디바이스 JSON 메타데이터를 입력합니다.  
 **팁:** 디바이스 메타데이터는 나중에 추가하고 편집할 수 있습니다.
13. **다음**을 클릭하여 디바이스의 추가를 완료합니다.
14. 요약 정보가 올바른지 확인한 다음 **추가**를 클릭하여 연결을 추가합니다.  
**팁:** 자동으로 생성된 인증 토큰을 승인하거나 인증 토큰을 직접 제공하는 옵션이 있습니다.  
고유 토큰을 작성하도록 선택하는 경우 길이는 8 - 36자이고 영숫자 문자와 다음 특수 문자로만 구성되어야 합니다. 
 - 하이픈(-)
 - 밑줄(&lowbar;)
 - 느낌표(!)
 - 앰퍼샌드(&)
 - at 기호(@)
 - 물음표(?)
 - 별표(\*)
 - 더하기 부호(+)
 - 마침표(.)
 - 오른쪽 및 왼쪽 소괄호  

 **중요:** 토큰에는 반복된 문자 시퀀스, 사전 단어, 사용자 이름 또는 기타 사전 정의된 시퀀스가 포함되지 않아야 합니다.
15. 디바이스 정보 페이지에서 다음 디바이스 정보를 복사하고 저장합니다.  
 - 조직 ID(예: `tubo8x`)
 - 디바이스 유형(예: `my_device_type`)
 - 디바이스 ID(예: `my_first_device`)
 - 인증 메소드(예: `token`)
 - 인증 토큰(예: `PtBVriRqIg4uh)_-Kl`)  
  **팁:** {{site.data.keyword.iot_short_notm}}에 연결하도록 디바이스를 구성하려면 조직 ID, 인증 토큰, 디바이스 유형 및 디바이스 ID가 필요합니다.   

축하합니다. 디바이스가 등록되었습니다. 이제 {{site.data.keyword.iot_short_notm}}에 연결하도록 디바이스를 구성할 수 있습니다.

## 2단계: {{site.data.keyword.iot_short_notm}}에 디바이스 연결
{: #iotplatform_subtask2}

{{site.data.keyword.iot_short_notm}}에 디바이스를 등록하고 나면 등록 정보를 사용하여 디바이스를 연결하고 디바이스 데이터 수신을 시작할 수 있습니다.

{{site.data.keyword.iot_short_notm}}에서는 여러 디바이스 유형을 지원합니다. 일반적으로 디바이스에 연결하는 기본 프로세스에는 다음 단계가 포함됩니다.
- MQTT 메시징에 사용할 디바이스를 설정하고 인증할 조직 ID, 인증 토큰, 디바이스 유형 및 디바이스 ID를 사용합니다.  
- MQTT 프로토콜을 사용하여 {{site.data.keyword.iot_short_notm}} 조직에 디바이스 메시지를 보냅니다.

**팁:** 일반적으로 사용되는 디바이스에 여러 연결 지침서를 사용할 수 있습니다. 레시피의 목록은 IBM.com에서 사용 가능한
[디바이스 연결 레시피 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){: new_window}를 참조하십시오. 

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

[조직 관리 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} API 문서에도 필수 정보가 포함되어 있습니다. 

## 디바이스 연결에 대한 레시피

다음 레시피는 디바이스를 등록하고 Watson IoT Platform에 연결하는 데 사용되는 전체 플로우를 설명합니다. 

- [디바이스를 IBM Watson IoT Platform에 등록하는 방법 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/how-to-register-devices-in-ibm-iot-foundation/){: new_window}

- [Node-RED를 사용하여 디바이스로서 Watson IoT에 Raspberry Pi 연결 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/){: new_window}

- [IBM Watson IoT Platform에 Arduino Uno 디바이스 연결 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/connect-an-arduino-uno-device-to-the-ibm-internet-of-things-foundation/){: new_window}

- [Node-RED를 사용하여 Watson IoT에 Sense HAT 연결 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/connecting-a-sense-hat-to-watson-iot-using-node-red/){: new_window}

- [디바이스로서 Watson IoT Platform에 Windows IoT Core가 포함된 Raspberry Pi 연결 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-with-windows-iot-core-as-a-device-to-watson-iot-using-node-red/){: new_window}
