---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iotelectronics}} 정보
{: #iotelectronics_about}

{{site.data.keyword.iotelectronics_full}}는 사용자 앱이 연결된 어플라이언스, 센서 및 게이트웨이로 수집되는 데이터와 통신하고 이를 이용하도록 하는 완전히 통합된 IoT 프로덕션 인스턴스입니다.
{:shortdesc}

{{site.data.keyword.iotelectronics}}는 {{site.data.keyword.iot_full}} 서비스를 사용하여 스마트 전자식 어플라이언스를 사용자가 개발하는 애플리케이션과 연결합니다. 또한 어플라이언스의 데이터를 분석하고 이해하는 데 도움이 되도록 {{site.data.keyword.iot_short_notm}}을 사용합니다. 규칙을 설정하여 주의가 필요한 상태를 식별하고 자동화된 응답을 정의할 수 있습니다(예: 이메일 전송, Node-RED 워크플로우 실행 또는 웹 서비스에 연결). 

## 스타터 찾기
{: #iot4eFindingStarter}
{{site.data.keyword.Bluemix_notm}} 카탈로그의 [표준 유형 섹션](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/)에서 {{site.data.keyword.iotelectronics}} 스타터를 찾을 수 있습니다. 

## {{site.data.keyword.iotelectronics}}를 사용하여 수행할 수 있는 작업
{: #Features_iote}
시뮬레이션된 어플라이언스 및 데이터를 사용하여 {{site.data.keyword.iotelectronics}} 솔루션의 기능을 빠르게 탐색할 수 있습니다. 

### 시뮬레이션된 어플라이언스 연결
시뮬레이션된 어플라이언스를 작성하고 플랫폼에 연결하여 스트리밍 라이브 데이터를 확인합니다. 웹 기반 앱을 사용하여 어플라이언스가 어떻게 명령을 수신하고 오퍼레이션을 수행하는지 시뮬레이션합니다. 고장 원인을 참고하여 주의사항 및 경보를 생성하십시오. 시연을 위해 {{site.data.keyword.iotelectronics}} 스타터에서는 세탁기를 시뮬레이션된 어플라이언스로 사용합니다. 사용자는 모든 유형의 스마트 전자 기기를 연결할 수 있습니다. 

### 샘플 소비자 모바일 앱 시도
iOS 또는 Android 모바일 디바이스를 사용하여 어플라이언스 소유자가 어떻게 어플라이언스와 상호작용할 수 있는지 확인합니다. 어플라이언스에 명령을 전송하고 플랫폼 및 {{site.data.keyword.Bluemix_notm}}를 사용하여 어플라이언스에서 업데이트를 수신합니다. 고장 상황을 가정하여 모바일 앱에서 결과를 확인합니다.

### 사용자 소유의 전자식 어플라이언스 연결
사용자 소유의 어플라이언스를 클라우드에 안전하게 연결하고 사용자 소유 앱의 사용자 정의를 시작합니다. 검증된 예제 및 구성 요소 세트가 사용 가능하며 개념 증명, 테스트 및 실험을 위해 이를 사용하고 수정할 수 있습니다. 

## {{site.data.keyword.iotelectronics}} 스타터에 포함된 내용
{: #whatsInStarter}
스타터 표준 유형은 통합 {{site.data.keyword.iotelectronics}} 솔루션을 배치합니다. 모든 컴포넌트가 자동으로 바인드되고 배치됩니다. 스타터 앱을 통해 사용자는 시뮬레이션된 어플라이언스 및 데이터를 사용하여 솔루션의 기능을 빠르게 탐색할 수 있습니다. 샘플 모바일 앱에서는 소비자가 어떻게 등록하고, 경보를 수신하며, 연결된 어플라이언스를 제어하는지를 보여줍니다. 고유 애플리케이션을 작성하고 고유 어플라이언스에서 데이터를 수집하기 위한 시작점으로 샘플을 사용할 수 있습니다. 다음 서비스 및 애플리케이션이 솔루션에 포함되어 있습니다. 

![{{site.data.keyword.iotelectronics}} 아키텍처. 이 다이어그램에 대해서는 주제의 본문에 설명되어 있습니다. ](images/IoT4E_architecture.svg "{{site.data.keyword.iotelectronics}} 아키텍처")

{{site.data.keyword.iotelectronics}} 스타터는 {{site.data.keyword.iotelectronics}} 서비스와 API를 사용하여 {{site.data.keyword.iot_short_notm}}에 연결합니다. 스타터 앱 및 샘플 모바일 앱은 {{site.data.keyword.iotelectronics}} 서비스와 통신합니다. 다음 컴포넌트가 스타터에 포함되어 있습니다. 

**{{site.data.keyword.iotelectronics}} 서비스**는 사용자 및 어플라이언스 등록과 알림을 지원합니다. 

**{{site.data.keyword.iot_full}}**을 통해 앱은 연결된 어플라이언스, 센서 및 게이트웨이와 통신하고 여기서 수집한 데이터를 사용할 수 있습니다. 

**{{site.data.keyword.sdk4nodefull}}**를 통해 서버 측 JavaScript&reg; 앱을 개발, 배치 및 확장할 수 있으며 사용자에게 향상된 성능, 보안 및 서비스 가능성을 제공합니다. 

**샘플 모바일 앱**을 통해 사용자는 스마트폰이나 태블릿과 같은 모바일 디바이스를 사용하여 시뮬레이션된 어플라이언스의 상태를 확인하고 통신할 수 있습니다. 모바일 앱을 가져오는 방법은 [모바일 앱 사용](iotelectronics_config_mobile.html)을 참조하십시오. 
