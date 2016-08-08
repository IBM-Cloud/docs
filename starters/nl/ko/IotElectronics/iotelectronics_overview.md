---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.iotelectronics}} 정보
{: #iotelectronics_about}
*마지막 업데이트 날짜: 2016년 6월 11일*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}}는 사용자 앱이 연결된 어플라이언스, 센서 및 게이트웨이로 수집되는 데이터와 통신하고 이를 이용하도록 하는 완전히 통합된 IoT 프로덕션 인스턴스입니다.
{:shortdesc}

{{site.data.keyword.iotelectronics}}는 {{site.data.keyword.iot_full}} 서비스를 사용하여 사용자가 개발하는 애플리케이션으로 스마트 전자식 어플라이언스를 연결합니다. 또한 이는 어플라이언스에서 데이터를 분석하고 파악하는 데 도움이 되도록 {{site.data.keyword.iot_full}}을 사용합니다. 규칙을 설정하여 주의가 필요한 조건을 식별하고 자동화된 응답을 정의할 수 있습니다(예: 이메일 전송, Node-RED 워크플로우 실행 또는 웹 서비스에 연결).  

## 스타터 찾기

{{site.data.keyword.Bluemix_notm}} 카탈로그의 [표준 유형 섹션](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/)에서 {{site.data.keyword.iotelectronics}} 스타터를 찾을 수 있습니다.  

## {{site.data.keyword.iotelectronics}}로 수행할 수 있는 항목
{: #Features_iote}
시뮬레이션된 어플라이언스 및 데이터를 사용하여 {{site.data.keyword.iotelectronics}} 솔루션의 기능을 신속히 탐색하십시오.

### 시뮬레이션된 어플라이언스 연결
시뮬레이션된 어플라이언스를 작성하고 플랫폼에 연결하여 스트리밍 라이브 데이터를 확인하십시오. 웹 기반 앱을 사용하여 어플라이언스가 명령을 수신하고 오퍼레이션을 수행하는 방식을 시뮬레이션하십시오. 실패를 모방하여 주의사항 및 경보를 생성하십시오.

### 샘플 이용자 모바일 앱 시도
iOS 전화기를 사용하여 어플라이언스 소유자가 어플라이언스와 상호작용할 수 있는 방법을 확인하십시오. 어플라이언스에 명령을 전송하고 플랫폼 및 {{site.data.keyword.Bluemix_notm}}를 사용하여 어플라이언스에서 업데이트를 수신하십시오. 실패 이벤트를 모방하고 모바일 앱에서 결과를 보십시오.

### 사용자 자체 전자식 디바이스 연결
클라우드에 안전하게 사용자 자체 디바이스를 연결하고 사용자 자체 앱의 사용자 정의를 시작하십시오. 확인된 예제 및 레시피의 세트가 사용 가능하여 개념 증명, 테스팅 및 실험에 대해 수정하고 사용할 수 있습니다.

## {{site.data.keyword.iotelectronics}} 스타터의 항목
{: #whatsInStarter}
스타터 표준 유형은 통합된 {{site.data.keyword.iotelectronics}} 솔루션을 배치합니다. 모든 컴포넌트가 사용자에 대해 자동으로 바인드되고 배치됩니다. 스타터 앱을 통해 사용자는 시뮬레이션된 어플라이언스 및 데이터를 사용하여 솔루션의 기능을 신속히 탐색합니다. 샘플 모바일 앱은 이용자가 등록하고 경보를 수신하며 연결된 어플라이언스를 제어할 수 있는 방법을 사용자에게 표시합니다. 사용자 자체 애플리케이션을 작성하고 사용자 자체 어플라이언스에서 데이터를 수집하는 데 시작점으로 샘플을 사용할 수 있습니다. 다음 서비스 및 애플리케이션이 솔루션에 포함됩니다.

![{{site.data.keyword.iotelectronics}} 아키텍처](images/IoT4E_architecture.svg "{{site.data.keyword.iotelectronics}} 아키텍처")

**{{site.data.keyword.iotelectronics}} 서비스**는 사용자 및 디바이스 등록 및 알림을 지원합니다.

**{{site.data.keyword.iot_full}}**을 통해 사용자 앱은 연결된 디바이스, 센서 및 게이트웨이로 수집되는 데이터와 통신하고 이를 사용합니다.

<!-- **{{site.data.keyword.iotrtinsights_full}}** enables you to enrich and monitor data from your devices, visualize what's happening now, and respond to emerging conditions by using automated actions. -->

**{{site.data.keyword.amafull}}**는 모바일 앱의 사용자가 기존의 소셜 계정을 사용하여 로그인할 수 있도록 하며 백엔드 시스템과의 통신이 안전한지 확인합니다.

**{{site.data.keyword.sdk4nodefull}}**에서는 사용자가 서버측 JavaScript&reg; 앱을 개발하고 배치하며 확장할 수 있도록 하며 향상된 성능, 보안 및 서비스 가능성을 제공합니다.

**샘플 모바일 앱**을 통해 사용자는 상태를 보고 iOS 전화기로 시뮬레이션된 어플라이언스와 통신합니다. [모바일 앱 사용](iotelectronics_config_mobile.html)에서 모바일 앱을 가져오는 방법을 찾으십시오.

# 관련 링크
{: #rellinks}
## 컴포넌트
{: #general}
* [{{site.data.keyword.iot_short}} 문서](https://new-console.ng.bluemix.net/docs/services/IoT/index.html#gettingstartedtemplate)
* [{{site.data.keyword.amafull}} 문서](https://new-console.ng.bluemix.net/docs/services/mobileaccess/index.html)
* [{{site.data.keyword.sdk4nodefull}} 문서](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)


## API 문서
{: #api}
*  [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)  
*  [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)
