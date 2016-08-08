---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iot_short_notm}} 스타터 시작하기
{: #gettingstartedtemplate}
<!-- Provide and appropriate ID above -->
*마지막 업데이트 날짜: 2016년 6월 27일*
{: .last-updated}

{{site.data.keyword.iot_short_notm}} 스타터 표준 유형을 사용하여 {{site.data.keyword.iot_full}}을 시작하십시오. 스타터를 사용하면 사용자가 디바이스를 신속히 시뮬레이션하고 카드를 작성하며 데이터를 생성하고 {{site.data.keyword.iot_short_notm}} 대시보드의 데이터 분석 및 표시를 시작할 수 있습니다.
{: shortdesc}

스타터는 다음 서비스를 자동으로 배치하고 연결합니다.

{{site.data.keyword.iot_short_notm}} - 플랫폼이 게이트웨이 디바이스, 디바이스 관리 및 강력한 애플리케이션 액세스 권한을 포함하는 다용도 IoT 툴킷을 사용자에게 제공합니다. {{site.data.keyword.iot_short_notm}}을 사용하여, 사용자는 연결된 디바이스 데이터를 수집하고 조직에서 실시간 데이터의 분석을 수행할 수 있습니다.

{{site.data.keyword.sdk4nodefull}} - Node-RED가 실행하는 런타임 환경을 작성합니다.

{{site.data.keyword.cloudantfull}} - Node-RED가 메타데이터를 저장하는 데이터베이스입니다.

## {{site.data.keyword.iot_short_notm}} 정보
{: #about_iotplatform}
{{site.data.keyword.iot_short_notm}}에서는 사용자가 분석 애플리케이션, 시각화 대시보드 및 모바일 IoT 앱을 신속히 구성하는 데 도움이 되도록 IoT 디바이스와 데이터에 대한 강력한 애플리케이션 액세스 권한을 제공합니다.
{{site.data.keyword.iot_short_notm}}을 통해 사용자는 강력한 디바이스 관리 오퍼레이션을 수행하고 디바이스 데이터를 저장하여 이에 액세스하며 광범위한 디바이스 및 게이트웨이 디바이스를 연결할 수 있습니다. {{site.data.keyword.iot_short_notm}}에서는 MQTT 및 TLS를 사용하여 디바이스에서 오가는 보안 통신을 제공합니다.

## Node-RED 정보
{: #about_nodered}
Node-RED는 새롭고 흥미로운 방법으로 하드웨어 디바이스, API 및 온라인 서비스를 함께 연결하는 도구입니다. Node-RED를 사용하여 {{site.data.keyword.iot_short_notm}} 서비스에 시뮬레이션된 데이터를 보내는 시뮬레이션된 온도조절기를 작성할 수 있습니다. 카드를 작성하여 {{site.data.keyword.iot_short_notm}} 대시보드에서 실시간 데이터를 표시할 수 있습니다. 자세한 정보는 [Node-RED 문서](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)를 참조하십시오.

## 돌아보기
{: #gettingaround}
다음 단계를 수행하여, 브라우저에서 3개의 서로 다른 탭을 사용합니다.
  1. *{{site.data.keyword.Bluemix_notm}} 대시보드* - {{site.data.keyword.Bluemix_notm}} 대시보드를 사용하여 배치 상태를 보고 문서를 읽으며 대시보드를 실행하십시오.
  2. *{{site.data.keyword.iot_short_notm}} 대시보드* - 대시보드를 사용하여 이 서비스에 대해 작업하십시오. 대시보드를 사용하여 디바이스 유형을 정의하고 디바이스를 등록하며 수신 센서 데이터를 모니터하고 데이터 시각화 카드를 작성하며 라이브 데이터 시각화를 봅니다.
  3. *Node-RED* - node.js 웹 애플리케이션으로 실행하여, 디바이스 시뮬레이터 플로우를 구성하여 실행하고 기타 플로우에 대해 작업하여 {{site.data.keyword.iot_short_notm}}에서 데이터를 처리합니다.

## {{site.data.keyword.iot_short_notm}}의 시뮬레이션된 디바이스 정의
{: #definingsimdev}
디바이스를 {{site.data.keyword.iot_short_notm}}에 등록:
  1.	{{site.data.keyword.Bluemix_notm}}에서, 배치된 애플리케이션의 개요 탭으로 이동하십시오.
  2.	연결 섹션 또는 탭에서 {{site.data.keyword.iot_short_notm}} 상자를 클릭하십시오.
  3.	실행 대시보드를 클릭하여 새 브라우저 창에서 {{site.data.keyword.iot_short_notm}} 대시보드를 여십시오.
  4.	디바이스를 선택하십시오.
  5.	디바이스 추가를 클릭하십시오.
  6.	디바이스 추가 대화 상자에서 디바이스 유형 작성을 클릭하십시오.
  7.	디바이스 유형 작성 대화 상자에서 디바이스 유형 작성을 클릭하십시오.
  8. 디바이스 유형에 대해 설명적 이름 및 설명을 입력하십시오(예: 온도조절기).
  9.	건너뛰기: 템플리트 정의
  10.	메타데이터를 건너뛰십시오.
  11.	작성을 클릭하여 새 디바이스 유형을 추가하십시오.
  12.	다음을 클릭하여 디바이스를 추가하십시오(디바이스 유형 선택이 사전에 선택됨).
  13.	디바이스 ID를 입력하십시오(예: LivingRoomThermo1).
  14.	건너뛰기: 디바이스 메타데이터 입력
  15.	다음을 클릭하여 자동 생성된 인증 토큰과 함께 디바이스 연결을 추가하십시오.
  16.	요약 정보가 올바른지 확인한 후 추가를 클릭하여 연결을 추가하십시오.
  17.	열리는 디바이스 정보 페이지에서, 디바이스 정보를 복사하고 저장하십시오.
      -	조직 ID
      -	디바이스 유형
      -	디바이스 ID
      - 인증 메소드
      - 인증 토큰

**팁**: 다음 몇몇 단계에서 조직 ID, 디바이스 유형 및 디바이스 ID가 있어야 Node-RED 애플리케이션의 구성을 마무리하여 연결을 완료할 수 있습니다.

## Node-RED 디바이스 시뮬레이터 구성 및 실행
{: #confignodered}
Node-RED 디바이스 시뮬레이터를 구성하십시오. 디바이스 시뮬레이터를 사용하여 MQTT 디바이스 메시지를 {{site.data.keyword.iot_short_notm}}에 전송하십시오. 디바이스 시뮬레이터는 {{site.data.keyword.iot_short_notm}}에 온도 및 습도 정보를 보냅니다.

1. Bluemix 대시보드에서, **앱 보기**를 선택하거나 링크(예: http:// myIoTApp.mybluemix.net)를 클릭하여 Node-RED를 여십시오.
2.	**Node-RED 플로우 편집기로 이동**을 클릭하여 편집기를 여십시오.
3.	디바이스 시뮬레이터 플로우에서 파란색 {{site.data.keyword.iot_short_notm}}에 **전송** 노드를 두 번 클릭하십시오.
  1.	인증 = Bluemix 서비스인지 확인하십시오.
  2.	등록한 디바이스에서 디바이스 유형을 붙여넣으십시오.
  3.	등록한 디바이스에서 디바이스 ID를 붙여넣으십시오.
  4.	확인을 클릭하십시오.
4.	Node-RED 플로우 편집기의 오른쪽 상단 구석에서 **배치**를 클릭하십시오.
5.	Node-RED 온도 모니터 플로우를 구성하십시오.
  1.	디바이스 시뮬레이터 플로우에서 파란색 IBM IoT 앱 인 노드를 두 번 클릭하십시오.
  2.	Bluemix 서비스로 인증을 변경하십시오.
  3.	디바이스 유형, 디바이스 ID, 이벤트 및 형식에 대해 모두 선택하십시오.
  4.	확인을 클릭하십시오.
6.	Node-RED 플로우 편집기의 오른쪽 상단 구석에서 **배치**를 클릭하십시오.
7.	디바이스 연결을 유효성 검증하십시오.
  1.	다른 브라우저 탭 또는 창에서, {{site.data.keyword.iot_short_notm}} 대시보드로 돌아가십시오.
  2.	디바이스를 선택하고 사용자가 추가한 디바이스의 이름 또는 LivingRoomThermo1을 클릭하십시오(다른 경우).
  디바이스 정보 페이지가 열립니다. 이 보기를 통해 사용자가 디바이스의 연결 상태를 볼 수 있습니다. 디바이스 상태는 연결 끊김입니다.
  3.	Node-RED 플로우 편집기로 되돌아가서, 회색의 데이터 전송 노드에서 단추를 클릭하여 자산 페이로드를 생성하십시오.
  페이로드에는 다음 데이터 점이 포함됩니다.
  ```
  {"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
  ```
  4.	오른쪽 분할창의 디버그 탭에서, 메시지가 작성되었는지 확인하십시오.
  5.	{{site.data.keyword.iot_short_notm}} 디바이스 정보 페이지에서, 센서 정보 섹션에 디바이스에서 수신된 동일한 데이터 점이 표시되는지 확인하십시오.

8.	샘플 IoT 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하여 디바이스 데이터를 보십시오.

## 라이브 데이터를 표시하기 위해 {{site.data.keyword.iot_short_notm}}에서 카드 작성
{: #createcards}
카드를 작성하려면 다음 태스크를 수행하십시오.

### 3초마다 데이터 자동 생성
1. Node-RED 탭에서, 데이터 전송 노드를 두 번 클릭하십시오.
2.	3초마다 간격으로 반복을 설정하십시오.
3.	배치하십시오.

### 대시보드에서 새 카드 작성
1. {{site.data.keyword.iot_short_notm}} 대시보드 브라우저 탭으로 이동하십시오.
2. BOARDS를 선택하십시오.
3. 새 보드 작성을 클릭하십시오.
4. 이에 홈 환경과 같은 이름을 제공하십시오.
5. 작성하십시오.
6. 새 카드 추가를 클릭하십시오(온도의 경우).
   1.	디바이스에서 실시간 차트를 선택하십시오.
   2.	카드 소스 데이터, 디바이스 "LivingRoomThermo1"을 검사한 후 다음을 클릭하십시오.
   3. 새 데이터 세트를 연결하십시오.
       - 이름: 온도
       - 이벤트: 업데이트
       - 특성: 임시
       - 유형: Float
       - 단위: °C
       - 정밀도: 2
       - 최소값: 0
       - 최대값: 50
       - 다음
  4. 카드 미리보기
       - L 선택
       - 다음
  5. 카드 정보
       - 제목: 온도
  6.	제출하십시오.
  7.	온도 카드가 대시보드에 나타나고 라이브 온도 데이터의 그래프를 포함합니다.
7.	새 카드 추가를 클릭하십시오(습도의 경우).
  1.	디바이스에서 추가 표시를 선택하십시오.
  2.	게이지를 선택하십시오.
  3.	카드 소스 데이터, 디바이스를 검사한 후 다음을 클릭하십시오.
  4.	새 데이터 세트를 연결하십시오.
       -	이름: 습도
       -	이벤트: 업데이트
       -	특성: 습도
       -	유형: Float
       -	단위: "% 상대 습도"
       -	정밀도: 1
       -	최소값: 10
       -	최대값: 95
       -	다음
  5.	카드 미리보기
       -	설정
          -	하위 임계값: 40 정도
          -	중간: 양호
          -	상위 임계값: 50% 정도
       -	M 선택
       -	다음
  6.	카드 정보
       -	제목: 습도
  7.	제출하십시오.
  8.	습도 카드가 대시보드에 나타나고 라이브 습도 데이터를 표시하는 게이지를 포함합니다.
8.	새 카드 추가를 클릭하십시오(위치의 경우).
  1.	디바이스에서 추가 표시를 선택하십시오.
  2.	값을 선택하십시오.
  3.	카드 소스 데이터, 디바이스 "LivingRoomThermo1"을 검사한 후 다음을 클릭하십시오.
  4.	새 데이터 세트를 연결하십시오.
       -	이름: 위도
       -	이벤트: 업데이트
       -	특성: 위치.위도
       -	유형: Float
       -	단위: "°N"
       -	정밀도: 2
       -	최소값: -180
       -	최대값: 180
  5. 새 데이터 세트를 연결하십시오.
       -	이름: 경도
       -	이벤트: 업데이트
       -	특성: 위치.경도
       -	유형: Float
       -	단위: "°E"
       -	정밀도: 2
       -	최소값: -180
       -	최대값: 180
       -  다음
  6.	카드 미리보기
       -	L 선택
       -	다음
  7.	카드 정보
       -	제목: 위치
  8.	제출하십시오.
9.	Node-RED 플로우에서 생성된 시뮬레이터 데이터를 사용하여 실시간으로 새 카드 업데이트를 감시하십시오.
**참고**: Node-RED는 사용자가 중지할 때까지 데이터를 계속해서 전송합니다.
10.	Node-RED 플로우 편집기에서, 데이터 전송 노드를 반복: 없음으로 업데이트하십시오.
11.	배치하십시오.

## 다음 항목
{: #whatsnext}
시뮬레이션된 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 전송 중이므로, 사용자는 IoT 프로젝트에서 계속해서 반복할 수 있습니다.

1. [IoT 레시피를 검색하여](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) 실제 디바이스(예: 라스베리 파이)를 연결하고 {{site.data.keyword.iot_short_notm}}에 데이터를 전송하십시오.
2. [샘플 node.js 애플리케이션을 배치하여 디바이스 데이터를 시각화하십시오.](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)
3.	비밀번호가 Node-RED 플로우 편집기를 보호합니다. 기본적으로, 임의의 사용자가 플로우에 액세스하고 이를 수정하도록 편집기가 열려 있습니다. 편집기에서 암호 보호를 수행하려면 다음 태스크를 수행하십시오.
  1.	Bluemix 대시보드에서, 애플리케이션의 '환경 변수' 페이지를 선택하십시오.
  2.	다음 사용자 정의된 변수를 추가하십시오.
       -	NODE_RED_USERNAME - 편집기 보안을 위한 사용자 이름
       -	NODE_RED_PASSWORD - 편집기 보안을 위한 비밀번호
  3.	저장을 클릭하십시오.


# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}
* [디바이스 연결 레시피](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short}} 재생 조직](https://play.internetofthings.ibmcloud.com/){:new_window}
* [{{site.data.keyword.iot_short}}에 Intel Galileo 연결](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [ARM&reg; mbed&trade; IoT 스타터 킷 연결](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [{{site.data.keyword.iot_short}}에 라스베리 파이 연결](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API 참조
{: #api}
* [{{site.data.keyword.iot_short}} API 문서](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}


## 관련 링크
{: #general}
* [{{site.data.keyword.iot_short_notm}} 문서](https://www.bluemix.net/docs/services/IoT/iotplatform_overview.html){:new_window}
* [{{site.data.keyword.sdk4nodefull}} 스타터 문서](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html){:new_window}
