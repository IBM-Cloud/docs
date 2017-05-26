---

copyright:

years: 2015, 2017

lastupdated: "2017-03-16"


---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 게이트웨이 연결
{: #IoT_connectGateway}

게이트웨이에 연결된 디바이스에서 데이터 수신을 시작할 수 있으려면 {{site.data.keyword.iot_full}}에 게이트웨이를 연결해야 합니다. {{site.data.keyword.iot_short_notm}}에 게이트웨이를 연결하려면 게이트웨이 디바이스 유형을 작성하고 게이트웨이를 {{site.data.keyword.iot_short_notm}}에 등록해야 합니다. 그러면 등록 정보를 사용하여 게이트웨이를 {{site.data.keyword.iot_short_notm}}에 연결할 수 있습니다.
{:shortdesc}

게이트웨이는 {{site.data.keyword.iot_short_notm}}의 특수화된 디바이스 클래스입니다. 게이트웨이는 다른 디바이스를 위한 {{site.data.keyword.iot_short_notm}}의 액세스 지점으로 사용됩니다.


## 시작하기 전에
{: #Prerequisites}

일반 디바이스와 비교해 볼 때 게이트웨이 디바이스에는 추가 권한이 있으며 다음 기능을 수행할 수 있습니다.
- {{site.data.keyword.iot_short_notm}}에 새 디바이스를 등록합니다.
- 직접 연결된 디바이스와 같이 고유 센서 데이터를 전송 및 수신합니다.
- 연결된 디바이스 대신 데이터를 전송 및 수신합니다.
- 디바이스 관리하고 연결된 디바이스도 관리할 수 있도록 디바이스 관리 에이전트를 실행합니다.  
게이트웨이 개발자 정보는 [게이트웨이용 MQTT 연결](mqtt.html)을 참조하십시오.

게이트웨이 디바이스에서 전송 중인 데이터에 대해 에지 분석을 수행하는 데도 게이트웨이를 사용할 수 있습니다. 자세한 정보는 [에지 분석](../edge_analytics.html) 및 [Edge Analytics Agent 설치](#edge)를 참조하십시오.

## 1단계: {{site.data.keyword.iot_short_notm}}에 게이트웨이 등록  
{: #register_gateway}

게이트웨이를 등록하려면 게이트웨이 유형으로 디바이스를 분류하고 게이트웨이에 이름을 제공하며 게이트웨이 정보를 제공해야 합니다. 그런 다음 연결 토큰을 제공하거나 {{site.data.keyword.iot_short_notm}}에서 생성된 토큰을 승인합니다.


**팁:** {{site.data.keyword.iot_short_notm}} 대시보드에서 한 번에 하나씩 게이트웨이를 추가하거나 [조직 관리 API ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration/post_bulk_devices_add){: new_window}를 사용하여 하나 이상의 게이트웨이를 한 번에 추가할 수 있습니다. 

{{site.data.keyword.iot_short_notm}} 대시보드에서 게이트웨이를 추가하려면 다음을 수행하십시오.

1. {{site.data.keyword.iot_short_notm}} 대시보드에서 **디바이스**를 선택합니다.
2. **디바이스 추가**를 클릭합니다.
3. 추가할 디바이스의 디바이스 유형을 선택하거나 작성합니다.  
{{site.data.keyword.iot_short_notm}}에 연결된 각 디바이스는 디바이스 유형과 연관되어야 합니다. 디바이스 유형은 공통 특성을 공유하는 디바이스 그룹입니다.  
 1. **디바이스 유형 작성**을 클릭한 다음 **게이트웨이 유형 작성**을 클릭합니다.
 2. 디바이스 유형 이름(예: `my_gateway_type`)과 게이트웨이 유형에 대한 설명을 입력합니다.    
 **중요:** 디바이스 유형 이름은 36자 이하여야 하며 다음 문자만 포함할 수 있습니다.
 <ul>
  <li>영숫자 문자(a-z, A-Z, 0-9)</li>
  <li>하이픈(-)</li>
  <li>밑줄(&lowbar;)</li>
  <li>마침표(.)</li>
  </ul>3. 선택사항: 게이트웨이 유형 속성 및 메타데이터를 입력합니다.     
 **팁:** 속성과 메타데이터는 나중에 추가하고 편집할 수 있습니다.
 4. **작성**을 클릭하여 새 게이트웨이 유형을 추가합니다.
10. **다음**을 클릭하여 선택한 게이트웨이 유형의 게이트웨이 디바이스를 추가하는 프로세스를 시작합니다.
11. 디바이스 ID(예: `my_gateway_device`)를 입력합니다.  
디바이스 ID는 {{site.data.keyword.iot_short_notm}} 대시보드에서 게이트웨이 디바이스를 식별하는 데 사용하고 게이트웨이 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하는 데도 필요한 매개변수입니다.  
**중요:** 디바이스 ID는 36자 이하여야 하며 다음 문자만 포함할 수 있습니다.
 <ul>
 <li>영숫자 문자(a-z, A-Z, 0-9)</li>
 <li>하이픈(-)</li>
 <li>밑줄(&lowbar;)</li>
 <li>마침표(.)</li>  
 </ul>
 **팁:** 네트워크 연결 디바이스의 경우 디바이스 ID는 예를 들어, 구분하는 콜론이 없는 디바이스 MAC 주소일 수 있습니다.  
12. 선택사항: **추가 필드**를 클릭하여 일련 번호, 제조업체, 모델 등의 게이트웨이 디바이스 정보를 추가합니다.  
 **팁:** 이 정보는 나중에 추가하고 편집할 수 있습니다.
12. 선택사항: 디바이스 JSON 메타데이터를 입력합니다.  
 **팁:** 디바이스 메타데이터는 나중에 추가하고 편집할 수 있습니다.
13. **다음**을 클릭하여 게이트웨이 디바이스의 추가를 완료합니다.
14. 요약 정보가 올바른지 확인한 다음 **추가**를 클릭하여 게이트웨이 디바이스를 추가합니다.  
**팁:** 자동으로 생성된 인증 토큰을 승인하거나 인증 토큰을 직접 제공하는 옵션이 있습니다. 고유 토큰을 작성하도록 선택하는 경우 길이가 8 - 36자이며 대소문자가 혼합되어 있고, 숫자, 하이픈, 밑줄 또는 마침표가 포함되는지 확인합니다. 토큰에는 반복된 문자 시퀀스, 사전 단어, 사용자 이름 또는 기타 사전 정의된 시퀀스가 포함되지 않아야 합니다.
15. 디바이스 정보 페이지에서 다음 디바이스 정보를 복사하고 저장합니다.  
 - 조직 ID(예: `tubo8x`)
 - 디바이스 유형(예: `my_gateway_type`)
 - 디바이스 ID **팁:** 네트워크 연결 디바이스의 경우 디바이스 ID는 예를 들어, 구분하는 콜론이 없는 디바이스 MAC 주소일 수 있습니다.
 - 인증 메소드(예: `token`)
 - 인증 토큰(예: `PtBVriRqIg4uh)_-Kl`)  
  **팁:** {{site.data.keyword.iot_short_notm}}에 연결하도록 디바이스를 구성하려면 조직 ID, 인증 토큰, 디바이스 유형 및 디바이스 ID가 필요합니다.   

축하합니다. 게이트웨이 디바이스가 등록되었습니다. 이제 {{site.data.keyword.iot_short_notm}}에 연결하도록 게이트웨이 디바이스를 구성할 수 있습니다.

게이트웨이를 등록하는 데 필요한 플로우를 보여주는 단계별 지시사항은 [IBM Watson IoT Platform에 게이트웨이 등록 방법 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/how-to-register-gateways-in-ibm-watson-iot-platform/){:new_window} 레시피를 참조하십시오. 

## 2단계: {{site.data.keyword.iot_short_notm}}에 게이트웨이 연결
{: #connect_gateway}

{{site.data.keyword.iot_short_notm}}에 게이트웨이를 등록하고 나면 등록 정보를 사용하여 게이트웨이를 {{site.data.keyword.iot_short_notm}}에 연결하고 게이트웨이에 연결된 디바이스에서 데이터 수신을 시작하십시오.

{{site.data.keyword.iot_short_notm}}에 게이트웨이를 연결하는 데 관한 정보는 [게이트웨이용 MQTT 연결](mqtt.html)을 참조하십시오.

**팁:** {{site.data.keyword.iot_short_notm}}에 디바이스를 연결하는 데 사용할 수 있는 지침서는 다양합니다. 레시피의 목록은 IBM.com에서 사용 가능한
[디바이스 연결 레시피 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}를 참조하십시오. 


## 3단계: 게이트웨이를 통해 디바이스 연결
{: #gateway_devices}

게이트웨이가 디바이스에서 메시지를 공개하면 게이트웨이에 연결된 디바이스가 자동으로 {{site.data.keyword.iot_short_notm}}에 연결됩니다. 게이트웨이에서 아직 존재하지 않는 디바이스 유형 및 디바이스 ID 조합에 대한 메시지를 공개하면 디바이스 유형과 디바이스 자체가 모두 자동으로 작성됩니다.

디바이스 자동 등록 및 연결된 디바이스의 데이터 공개 및 수신에 대한 정보는 [게이트웨이용 MQTT 연결](mqtt.html)을 참조하십시오.


디바이스가 게이트웨이에 연결되면 {{site.data.keyword.iot_short_notm}} 조직의 대시보드에 표시됩니다.

세부 플로우 및 관련 설명은 [게이트웨이로서 Watson IoT에 Raspberry Pi 연결 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-as-a-gateway-to-watson-iot-using-node-red/){:new_window} 레시피를 참조하십시오. 

**참고:** {{site.data.keyword.iot_short_notm}} 대시보드에서 {{site.data.keyword.iot_short_notm}}에 직접 연결된 디바이스와 게이트웨이는 현재 연결되었음을 표시하는 상태 아이콘을 표시합니다. 대시보드에는 게이트웨이에 연결된 디바이스에 대한 정보가 없으므로 게이트웨이를 통해 간접적으로 연결된 디바이스는 연결이 끊김으로 표시됩니다.


## EAA(Edge Analytics Agent) 설치
{: #edge}

EAA(Edge Analytics Agent)는 스트리밍 엔진 위에서 구축된 소프트웨어 컴포넌트이며, 이 엔진은 {{site.data.keyword.iot_short_notm}} 대시보드에서 에지 분석 규칙을 업로드하고 관리함으로써 게이트웨이에서 에지 분석 조작을 수행하는 에지 처리를 위해 최적화되어 있습니다. 에지 분석에 대한 자세한 정보는 [에지 분석](../edge_analytics.html)을 참조하십시오.

### EAA 설치
{: #eaa_install}

게이트웨이에 EAA를 설치하려면 다음을 수행하십시오.
1. {{site.data.keyword.iot_short}} 대시보드에서 **규칙**으로 이동하십시오. 
2. **Edge Agent 다운로드**를 클릭하여 [IBM Edge Analytics 커뮤니티 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){:new_window}로 이동하십시오. 
3. **파일** 섹션으로 이동하여 게이트웨이 유형에 적합한 압축 디렉토리를 다운로드하십시오.   
Edge Analytics 솔루션은 Java를 지원하는 디바이스에 대한 SDK로 또는 Cisco 게이트웨이 디바이스에 대한 DSLink로 사용 가능합니다. 
4. 게이트웨이에서 EAA 소프트웨어 컴포넌트를 설치하고 구성하는 방법에 대한 정보는 다음 정보를 참조하십시오. 
 - SDK  
 커뮤니티에서 사용 가능한 PDF, Readme 파일 및 비디오 링크를 참조하십시오.   
 [SDK용 Edge Recipe - 시작하기(SDK) ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/getting-started-with-the-ibm-edge-analytics-sdk-in-watson-iot-platform/){:new_window} 레시피. 
 - DSLink  
 [Watson IoT Platform에서 Edge Analytics 시작하기 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=19472){:new_window} 레시피. 

### EAA 구성 설정
{: #eaa_configuration}

EAA config.properties 파일을 사용하여 기본 소프트웨어 구성 매개변수를 설정할 수 있습니다.

EAA 구성을 업데이트합니다.
1. EAA가 실행 중인 게이트웨이 시스템에서 EAA config.properties 파일을 찾습니다.  
예:
`../dglux-server/dslinks/ibm-watson-iot-edge-analytics-dslink-java-0.0.1/config.properties`
2. 설정 편집을 시작하기 전에 파일의 백업 사본을 작성합니다.
3. 편집할 config.properties 파일을 엽니다.
4. 환경에 맞게 구성 매개변수를 편집합니다.
 <dl>
 <dt>DataDirectSendEnable</dt>
 <dd>BOOLEAN (true|false)</br>
 TRUE(기본값) - {{site.data.keyword.iot_short_notm}}에 모든 데이터를 보냅니다.</br>
 FALSE - 엔진에 규칙이 설정된 경우 데이터만 {{site.data.keyword.iot_short_notm}}에 보냅니다.</dd>
 <dt>MonitorInterval</dt>
 <dd>INTEGER (milliseconds)</br>
 새 모니터링 메시지를 {{site.data.keyword.iot_short_notm}}에 보내기 전의 시간(밀리초)입니다. </br>
 모니터 메트릭을 더 자주 보고하려면 값을 작게 설정하십시오. {{site.data.keyword.iot_short_notm}}에 대한 자세한 모니터링 정보를 원하면 값을 크기 설정하십시오. </br>
 기본값: 60000    </br>
 권장 범위: [1000, 360000]</dd>
 <dt>MonitorLogDesample</dt>
 <dd>INTEGER  </br>
 {{site.data.keyword.iot_short_notm}}에 보낸 모니터링 메시지 수와 로컬 로그에 입력된 메시지 수 사이의 샘플링 해제 비율입니다. 예를 들어 `MonitorLogDesample`이 10으로 설정되면 {{site.data.keyword.iot_short_notm}}에 전송된 10개의 메시지마다 단 하나의 로컬 로그 항목이 작성됩니다. </br>수가 크면 로컬 로그가 작게 유지됩니다. 수가 작으면 로컬 로그가 더 자세하게 됩니다.</br>
 기본값: 10</br>
 권장 범위: [1, 100]</dd>
 <dt>MemoryAlertThreshold</dt>
 <dd>INTEGER (Megabytes)</br>
 {{site.data.keyword.iot_short_notm}} 진단 로그에 메모리 경고 로그 메시지를 보내는 사용 가능한 JVM 힙 메모리 임계값입니다. 경보는 모니터링을 통해 구동됩니다. </br>값이 작으면 {{site.data.keyword.iot_short_notm}}에 전송되는 경보 메시지 수가 줄어듭니다. 수가 크면 EAA 서버에서 메모리 문제가 발생하는 경우 조기에 경고를 표시합니다. </br>**팁:** [클라우드 분석](../cloud_analytics.html) 규칙을 사용하여 메모리 문제를 경보할 이메일 알림 등의 경보 조치를 구성할 수 있습니다. 규칙을 빌드하는 데 사용할 수 있는 특성에 대한 정보는 [Edge Analytics Agent 진단 메트릭](../edge_analytics.html#eaa_metrics)을 참조하십시오.</br>
 기본값: 10</br>
 권장 범위: [10 또는 총 메모리, 200의 5% ]</dd>
 </dl>
5. 편집한 파일을 저장한 다음 EAA를 다시 시작합니다.

샘플 EAA config.properties 파일
```
#######################################################################
# Engine Parameters
#######################################################################
# DataDirectSendEnable
#                    - BOOLEAN(true|false) Set to true to forward all
#                      the data; Set to false to disable data direct
#                      send to IOTP when there is no rule set in the
#                      engine.
#                      DEFAULT: true
#######################################################################
DataDirectSendEnable=true

#######################################################################
# Monitoring Parameters
#######################################################################
# MonitorInterval    - INTEGER Time interval in milliseconds before a  
#                      new monitoring message is generated. Set it to a
#                      small value to report the monitor metrics more
#                      frequently. Set it to a big value to have more
#                      detailed monitoring information on IoTP.
#                      DEFAULT: 60000    RECOMMEND: [1000, 360000]
# MonitorLogDesample - INTEGER The de-sampling ratio of the number of
#                      monitoring messages sent to IOTP vs. local log,
#                      i.e. number of monitoring messages N where
#                      EAA would output only one to the Info log for
#                      every N messages. Set it big to keep the size
#                      of the log small. Set it small to have detailed
#                      monitoring information in local log.
#                      DEFAULT: 10       RECOMMEND: [1, 100]
# MemoryAlertThreshold
#                    - INTEGER the free JVM heap memory in megabyte under
#                      which a log message would be generated and send to
#                      IOTP diagnosis log. The alert is driven by the
#                      monitoring. Set it small to eliminate unnecessary
#                      alert message on IoTP. Set it big to receive early
#                      alert when the system is likely to crash. Set to
#                      Min(Max(10MB, 5% of the total memory), 200MB) is
#                      recommended.
#                      DEFAULT: 10       RECOMMEND: [10, 200]
#######################################################################

MonitorInterval=60000
MonitorLogDesample=10
MemoryAlertThreshold=10
```
