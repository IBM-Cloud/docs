---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 스타터 시작하기
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

{{site.data.keyword.iot_short_notm}} 스타터 GitHub 프로젝트를 사용하여 {{site.data.keyword.iot_full}}을 시작합니다. 스타터를 사용하면 디바이스를 빠르게 시뮬레이션하고 카드를 작성하며 데이터를 생성하고 {{site.data.keyword.iot_short_notm}} 대시보드에서 데이터 분석과 표시를 시작할 수 있습니다.   
{:shortdesc}

## 개요
{: #overview}  

스타터는 다음 서비스를 자동으로 배치하고 연결합니다. 
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>게이트웨이 관리, 디바이스 관리 및 애플리케이션 액세스가 포함된 IoT 웹 서비스. {{site.data.keyword.iot_short_notm}}을 사용하면 연결된 디바이스 데이터를 수집하고 조직의 실시간 데이터에 대한 분석을 실행할 수 있습니다. </dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>Node-RED가 실행되는 런타임 환경. </br>자세한 정보는 [{{site.data.keyword.sdk4nodefull}} 스타터 문서](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html)를 참조하십시오. </dd>
<dd>Node-RED는 새롭고 흥미로운 방식으로 하드웨어 디바이스, API 및 온라인 서비스를 함께 연결하는 도구입니다. Node-RED를 사용하여 {{site.data.keyword.iot_short_notm}} 서비스에 시뮬레이션된 데이터를 보내는 시뮬레이션된 온도조절기를 작성할 수 있습니다. 카드를 작성하여 {{site.data.keyword.iot_short_notm}} 대시보드에서 실시간 데이터를 표시할 수 있습니다. </br>자세한 정보는 [Node-RED 문서](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)를 참조하십시오.</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>Node-RED가 메타데이터를 저장하는 데이터베이스. </dd>
</dl>

## 시작하기 전에
{: #byb}  

- 필수 계정  
시작하려면 우선 [IBM Bluemix 계정](https://bluemix.net/registration)이 필요합니다. 

- 둘러보기  
다음의 프로세스에서 태스크 간에 보다 쉽게 이동하려면 브라우저의 서로 다른 탭에서 {{site.data.keyword.Bluemix_notm}} 대시보드, {{site.data.keyword.iot_short_notm}} 대시보드 및 Node-RED 애플리케이션을 여십시오. 
<dl>
<dt>*{{site.data.keyword.Bluemix_notm}} 대시보드*</dt>
<dd>배치 상태를 보고 문서를 읽으며 대시보드를 시작합니다. </dd>
<dt>*{{site.data.keyword.iot_short_notm}} 대시보드*</dt>
<dd>디바이스 유형을 정의하고 디바이스를 등록하며 수신 센서 데이터를 모니터하고 데이터 시각화 카드를 작성하며 라이브 데이터 시각화를 봅니다. </dd>
<dt>*Node-RED*</dt>
<dd>디바이스 시뮬레이터 플로우를 구성하고 실행하며, 기타 플로우 관련 작업을 수행하여 {{site.data.keyword.iot_short_notm}}의 데이터를 처리합니다. </dd>
</dl>

## 1단계: {{site.data.keyword.iot_short_notm}} 스타터 배치
{: #deployStarter}

다음 단계를 수행하여 스타터 샘플 애플리케이션을 배치하십시오. 

1. 스타터 애플리케이션을 배치하십시오. 
 1. <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a>를 클릭하여 Bluemix의 새 Continuous Delivery 도구 체인을 작성하십시오(Continuous Delivery를 통해).   
 **팁:** 명령행에서 배치하는 경우에는 GitHub의 IBM Watson IoT 조직에서 [{{site.data.keyword.iot_short_notm}} 스타터를 찾을 수](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter) 있습니다. 
 2. 프롬프트가 표시되면 IBM Bluemix에 로그인하십시오. 
 3. 필요하면 스타터 애플리케이션이 배치될 Bluemix 조직을 선택하십시오. 
 4. 도구 체인 이름을 유지하거나 필요하면 이를 업데이트하십시오. 이는 기본 앱 이름 및 앱 URL의 루트로서 사용됩니다(`<app-name>.mybluemix.net`). 
 5. **작성**을 클릭하십시오.   
**팁:** **Delivery Pipeline** 타일을 클릭하면 첫 번째 배치의 진행상태를 모니터할 수 있습니다. 
 6. 배치가 완료되면 **앱 보기**를 클릭하여 새 탭에서 새 Node-RED 애플리케이션을 여십시오. 
2. 스타터 앱 서비스를 찾으십시오. 
 1. Bluemix 메뉴에서 **대시보드**를 선택하십시오. 
 2. *모든 서비스* 아래에서 다음 서비스를 찾으십시오. 
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. *모든 앱* 아래에서 도구 체인을 찾으십시오. 
    - default-toolchain-{id}}


## 2단계: {{site.data.keyword.iot_short_notm}}에서 시뮬레이션된 디바이스 정의
{: #definingsimdev}

온도조절기를 사용하여 온도, 습도와 거실 위치를 모니터하는 시나리오를 시뮬레이션하려면 다음 단계를 완료하십시오. 

1.	{{site.data.keyword.iot_short_notm}} 대시보드를 시작하십시오. 
  1. Bluemix 대시보드의 *모든 서비스* 아래에서 {{site.data.keyword.iot_short_notm}} 인스턴스의 이름을 클릭하십시오.
**팁:** 인스턴스 이름에는 대개 `iotp-starter`가 포함됩니다. 
  2. **시작**을 클릭하여 새 브라우저 탭에서 {{site.data.keyword.iot_short_notm}} 대시보드를 여십시오.    
`All Boards` 페이지가 기본적으로 표시됩니다. 
2. 디바이스 유형을 작성하십시오. 
  1.	기본 메뉴에서 **디바이스**를 선택한 후에 **디바이스 추가**를 클릭하십시오. 
  2.	디바이스 추가 페이지에서 **디바이스 유형 작성**을 클릭하십시오. 
  3.	디바이스 유형 작성 페이지에서 **디바이스 유형 작성**을 클릭하십시오. 
  4. 디바이스 유형에 대해 고유 이름(예: `Thermostat`)을 입력하고 **다음**을 클릭하십시오. 
  5. 선택사항: 다음의 두 페이지에서 템플리트 및 메타데이터 정의는 선택사항이며, 각 페이지에서 **다음**을 클릭하여 아무 문제 없이 건너뛸 수 있습니다. 
  6.	**작성**을 클릭하여 디바이스 유형을 추가하십시오. 
3.	새로 작성된 디바이스 유형을 사용하는 디바이스를 추가하십시오. 
  1. 디바이스 추가 페이지에서, 방금 작성한 디바이스 유형이 디바이스 유형 목록에 표시됩니다. **다음**을 클릭하여 해당 디바이스 유형을 사용하는 디바이스를 추가하십시오. 
  2. 고유 디바이스 ID(예: `LivingRoomThermo1`)를 입력하십시오. 
  3. 선택사항: 디바이스 추가 페이지에서 설명 데이터를 제공하거나 다음 페이지에서 디바이스 메타데이터를 입력하는 것은 선택사항이며, 각 페이지에서 **다음**을 클릭하여 아무 문제 없이 해당 페이지를 건너뛸 수 있습니다. 
  4. 보안 페이지에서 **다음**을 클릭하여 디바이스의 인증 토큰을 생성하십시오. 
  5. 요약 페이지에서 정보가 올바른지 확인하고 **추가**를 클릭하여 디바이스를 추가하십시오. **이전**을 클릭하여 이전 페이지로 돌아가십시오. 
4.	디바이스 신임 정보 페이지에 표시된 정보를 기록해 두십시오.    
시뮬레이터를 구성하고 데이터를 표시하려면 다음 정보가 필요합니다. 
 - 조직 ID
 - 디바이스 유형
 - 디바이스 ID
 - 인증 방법
 - 인증 토큰

## 3단계: Node-RED 디바이스 시뮬레이터를 구성하고 실행하십시오.   
{: #confignodered}  
온도 및 습도 정보와 함께 MQTT 디바이스 메시지를 {{site.data.keyword.iot_short_notm}}에 전송하도록 Node-RED 디바이스 시뮬레이터를 구성하십시오. 

1. Node-RED 플로우 편집기를 시작하십시오. 
  1. Bluemix 대시보드의 *모든 앱* 아래에서 도구 체인의 이름을 클릭하십시오.   
**팁:** 도구 체인 이름에는 대개 `default-toolchain...`이 포함됩니다. 
  2. 도구 체인 대시보드에서 **라우트**를 클릭하고 라우트 링크를 선택하여 Node-RED 인스턴스를 여십시오.   
  2. **Node-RED 플로우 편집기로 이동**을 클릭하여 편집기를 여십시오. 
2. 디바이스를 배치하십시오. 
  1. 디바이스 시뮬레이터 플로우에서 파란색 **IBM IoT Platform에 전송** 노드를 두 번 클릭하십시오. 
  2. 인증이 **Bluemix 서비스**로 설정되었는지 확인하십시오. 
  3. 디바이스의 **디바이스 유형** 및 **디바이스 ID**를 입력하고 **완료**를 클릭하십시오. 
  4. **배치**를 클릭하여 디바이스를 배치하십시오. 
3. Node-RED 온도 모니터 플로우를 구성하십시오. 
  1. 디바이스 시뮬레이터 플로우에서 파란색 **IBM IoT 앱** 노드를 두 번 클릭하십시오. 
  2. 인증에서 **Bluemix 서비스**를 선택하십시오. 
  3.	디바이스 유형, 디바이스 ID, 이벤트 및 형식에 대해 **모두**를 선택하십시오. 
  4.	**완료**를 클릭하십시오.
  5.  **배치**를 클릭하여 모니터를 배치하십시오. 
4. 디바이스 연결의 유효성을 검증하십시오. 
  1.	{{site.data.keyword.iot_short_notm}} 대시보드를 여십시오.  
**팁:** {{site.data.keyword.iot_short_notm}} 대시보드가 아직 다른 탭에서 열리지 않았으면 {{site.data.keyword.Bluemix_notm}} 대시보드로 돌아가서 {{site.data.keyword.iot_short_notm}} 인스턴스의 이름을 클릭한 후에 **대시보드 시작**을 클릭하십시오. 
  2. 기본 메뉴에서 **디바이스**를 선택하십시오. 
  3. 추가한 디바이스의 이름을 클릭하십시오.    
디바이스 정보가 디바이스의 연결 상태를 표시합니다. 
  4.	Node-RED 플로우 편집기에서 **데이터 전송** 노드를 두 번 클릭하고 반복 값을 **간격**으로 설정한 후에 빈도를 매 `3`초로 설정하십시오. 
  5. **완료**를 클릭하십시오.
  6. **배치**를 클릭하여 변경사항을 배치하십시오.   
페이로드에는 다음 예제에 표시된 것과 같은 데이터 점이 포함되어 있습니다. 
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. 선택사항: 디버그 탭을 열어서 메시지를 작성 중인지 확인하십시오. 
    1. 표제 섹션에 있는 메뉴에서 **보기**를 선택하십시오. 
    2. **사이드바 표시**를 선택하십시오. 
    3. 디버그 탭을 클릭하여 메시지를 보십시오. 
  8. {{site.data.keyword.iot_short_notm}} 디바이스 정보 페이지의 센서 정보 섹션에서 디바이스의 데이터 점이 보이는지 확인하십시오. 


## 4단계: 라이브 데이터 표시를 위해 {{site.data.keyword.iot_short_notm}}에서 카드 작성  
{: #createcards}  
{{site.data.keyword.iot_short_notm}} 대시보드에서 디바이스 데이터를 표시할 수 있도록 보드 및 카드를 작성하십시오. 보드 및 카드에 대한 자세한 정보는 [보드 및 카드를 사용하여 실시간 데이터 시각화](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html)를 참조하십시오. 

1. 보드 작성
  1. {{site.data.keyword.iot_short_notm}} 대시보드를 여십시오.  
  **팁:** {{site.data.keyword.iot_short_notm}} 대시보드가 아직 다른 탭에서 열리지 않았으면 {{site.data.keyword.Bluemix_notm}} 대시보드로 돌아가서 {{site.data.keyword.iot_short_notm}} 인스턴스의 이름을 클릭한 후에 **대시보드 시작**을 클릭하십시오.   
  2. 시뮬레이션된 디바이스에 대한 카드를 포함하기 위한 보드를 작성하십시오. 
    1. 모든 보드 페이지가 아직 표시되지 않으면 {{site.data.keyword.iot_short_notm}} 대시보드 기본 메뉴에서 **보드**를 선택한 후에 **새 보드 작성**을 클릭하십시오. 
    2. 보드 이름(예: `Home Environment`)을 입력하고 **다음**을 클릭하십시오. 
    3. 다음 페이지에서 **제출**을 클릭하십시오.   
  3. 방금 작성한 보드를 클릭하여 이를 여십시오. 
2. 온도 표시를 위한 카드 작성
  1. **새 카드 추가**를 클릭한 후에 디바이스 섹션에서 **선형 차트** 카드 유형을 선택하십시오. 
  2. 디바이스 목록에서 디바이스를 선택한 후에 **다음**을 클릭하십시오. 
  3. **새 데이터 세트 연결**을 클릭하십시오. 
  4. 값 카드 작성 페이지에서 다음 값을 선택하거나 입력하고 **다음**을 클릭하십시오. 
    - 이벤트: 업데이트
    - 특성: temp
    - 이름: 온도
    - 유형: Float
    - 단위: °C
    - 정밀도: 2
    - 최소값: 0
    - 최대값: 50
  5. 카드 미리보기 페이지에서 선형 차트 크기에 대해 **L**을 선택하고 **다음**을 클릭하십시오. 
  6. 카드 정보 페이지에서 카드 이름을 **온도**로 변경하고 **제출**을 클릭하십시오.    
온도 카드가 대시보드에 나타나며 여기에 라이브 온도 데이터의 선형 차트가 포함됩니다. 
3. 습도 표시를 위한 카드 작성
  1. **새 카드 추가**를 클릭한 후에 디바이스 섹션에서 **게이지** 카드 유형을 선택하십시오. 
  2. 목록에서 디바이스를 선택한 후에 **다음**을 클릭하십시오. 
  3. **새 데이터 세트 연결**을 클릭하십시오. 
  4. 값 카드 작성 페이지에서 다음 값을 선택하거나 입력하고 **다음**을 클릭하십시오.
  이벤트: 업데이트
     - 특성: 습도
     - 이름: 습도
     - 유형: Float
     - 단위: %
     - 정밀도: 1
     - 최소값: 10
     - 최대값: 95
  5. 카드 미리보기 페이지에서 게이지 크기에 대해 **M**을 선택하고 **다음**을 클릭하십시오. 
  6. 카드 정보 페이지에서 카드 이름을 **습도**로 변경하고 **제출**을 클릭하십시오.    
습도 카드가 대시보드에 나타나며 여기에 라이브 습도 데이터를 표시하는 게이지가 포함됩니다.   

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## 다음에 수행할 작업  
{: #whats-next}  
이제 시뮬레이션된 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 전송하므로 사용자는 IoT 프로젝트에서 계속해서 반복할 수 있습니다. 
 - 카드가 node-RED 플로우에 의해 생성된 데이터를 표시하는지 지켜보십시오.   
Node-Red는 사용자가 중지할 때까지 데이터를 전송합니다. 시뮬레이션된 데이터를 중지하려면 다음 단계를 수행하십시오. 
    1.	Node-RED 플로우 편집기에서 회색 **데이터 전송** 노드를 두 번 클릭하고 반복 값을 **간격**으로 설정한 후에 빈도를 매 **3**초로 설정하십시오. 
    2. **완료**를 클릭하십시오.
    3. **배치**를 클릭하여 변경사항을 배치하십시오. 

 - 실제 디바이스를 연결하십시오.   
Raspberry Pi 등의 실제 디바이스를 연결하고 데이터를 {{site.data.keyword.iot_short_notm}}에 전송하려면 [IoT 레시피를 검색](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot)하십시오. 

 - 시각화 옵션을 탐색하십시오.   
[디바이스 데이터를 시각화하려면 샘플 node.js 애플리케이션을 배치](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)하십시오. 

 -	비밀번호는 Node-RED 플로우 편집기를 보호합니다.    
기본적으로는 편집기는 누구나 플로우에 액세스하고 이를 수정할 수 있도록 열립니다. 편집기를 비밀번호로 보호하려면 다음 태스크를 수행하십시오. 
    1.	{{site.data.keyword.Bluemix_notm}} 대시보드에서 스타터 애플리케이션의 이름을 클릭하여 애플리케이션 페이지를 여십시오. 
    2. **런타임**을 클릭하여 런타임 페이지를 표시하십시오. 
    3. **환경 변수**를 클릭하여 환경 변수 페이지를 표시하십시오. 
    4. **사용자 정의** 섹션에서 **추가**를 클릭한 후에 다음의 사용자 정의된 변수를 입력하십시오. 
         -	NODE_RED_USERNAME - 편집기를 보호하기 위한 사용자 이름
         -	NODE_RED_PASSWORD - 편집기를 보호하기 위한 비밀번호
    3.	**저장**을 클릭하십시오.
