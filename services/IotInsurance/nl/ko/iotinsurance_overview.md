---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# {{site.data.keyword.iotinsurance_short}} 정보
{: #about_servicename}
마지막 업데이트 날짜: 2016년 9월 12일
{: .last-updated}

{{site.data.keyword.iotinsurance_full}}는 보험 계약자의 전체 컨텍스트 데이터를 수집하고 분석하여 개인별 맞춤 위험성 평가, 실시간 보호, 정책 비용 감소를 제공하는 통합 IoT 프로덕션 인스턴스입니다.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}}에서는 위치, 날씨, 교통, 전반적인 건강상태 같은 정보를 비롯하여 보험 계약자의 자산과 상황에 대한 전체 컨텍스트 보기를 제공합니다. 보험자는 이와 같은 정보를 심층 분석하여 보험 계약자에게 개인별 맞춤 위험성 평가와 실시간 보호를 제공할 수 있습니다. 보험 계약자에게는 조기 경보, 개인별 맞춤 조언, 간소화된 청구 처리와 정산의 형태로 위험을 피할 수 있는 이점이 있습니다. 보험자에게는 청구 방지를 사용하고 자동화를 처리함으로써 고객 만족, 고객 로열티, 비용 감소와 같은 이점이 있습니다. 

## 프로세스 플로우
{: #processFlow}
보험 제공업체의 {{site.data.keyword.Bluemix_notm}} 서비스 브로커에 인스턴스가 있습니다. 보험자의 고객 집에는 센서가 있으며 이는 센서 제공업체의 클라우드에 연결되어 있습니다. 주택 소유자는 모바일 디바이스를 사용하여 {{site.data.keyword.iotinsurance_short}}에서 센서 데이터를 수신하도록 {{site.data.keyword.iotinsurance_short}} 서비스에 권한을 부여합니다. {{site.data.keyword.iotinsurance_short}} 서비스는 센서 제공업체의 클라우드에 연결하여 각 사용자의 데이터를 가져와 IoT 서버에 보냅니다. 센서에 보험자 실드에 지정된 매개변수가 고객의 집에서 충족되지 않는 것으로 표시되는 경우 보험자 대시보드와 고객의 디바이스에 알림이 전송됩니다. 

## 컴포넌트
{: #components}

### 보험 대시보드
{: #insurance_dashboard}
보험 대시보드는 보험 회사 사용자(예: 에이전트)에게 고객의 보험 가입 자산 상태에 대한 전체 보기를 제공합니다. 보험 회사 사용자는 국가, 시/도 또는 계정 레벨에서 실드와 이벤트를 볼 수 있습니다. 

샘플 보험 대시보드에는 시뮬레이션된 데이터가 로드되어 사용자가 수집하고 분석할 수 있는 정보 유형의 예를 표시합니다. 

### 모바일 스타터 앱
{: #mobileapp}
모바일 스타터 앱에서는 보험 계약자(예: 주택 소유자)가 {{site.data.keyword.iotinsurance_short}}가 센서에서 계약자의 집으로 보내는 정보를 보고 응답할 수 있습니다. 

주택 소유자는 모바일 디바이스를 사용하여 센서 제공업체의 클라우드에 연결해 데이터를 주고받을 수 있도록 서비스에 권한을 부여합니다. 예를 들어, 센서가 누수를 발견하면 주택 소유자가 모바일 스타터 앱에서 알림을 수신합니다. 자세한 정보는 [모바일 스타터 앱 설치 및 연결](index.html#iot4i_mobile})을 참조하십시오. 

### REST API
{: #rest_api}
REST API는 모바일 스타터 앱, 보험 대시보드, 실드 엔진, 위해 제어기에서 사용됩니다. 사용자는 REST API를 사용하여 디바이스, 실드, 조치 사이에 존재하는 연관을 확인할 수 있습니다. 프로그래머는 이 API를 사용하여 새 사용자 작성, 이벤트 데이터 생성, 새 실드 작성과 등록, 이벤트 데이터 페치를 수행할 수 있습니다. 

사용자가 서비스 콘솔에서 액세스하는 API는 {{site.data.keyword.iotinsurance_short}}의 인스턴스에 적합하게 사용자 정의됩니다. 

API 페이지에서 다음을 수행할 수 있습니다.   
  - 사용 가능한 모든 API 호출과 연관 문서를 볼 수 있습니다. 
  - 개별 API를 호출할 수 있습니다. 모든 정보를 표시할 API 호출을 선택한 후 **사용해보기**를 클릭하십시오. 

공통 시나리오를 시작하는 데 유용한 API 예제가 제공됩니다. 자세한 정보는 [{{site.data.keyword.iotinsurance_short}} API 예제](https://github.ibm.com/Iot4i/iot4i-api-examples)를 참조하십시오. 

### 클라우드 제공업체
{: #cloudprovider}
사용자는 Transformer 컴포넌트에 센서 클라우드 데이터에 액세스하고 기록된 데이터를 처리할 수 있는 권한을 부여해야 합니다. 모바일 스타터 앱을 사용하여 권한을 부여합니다. 현재 지원되는 클라우드 공급업체는 Wink뿐입니다. 

### Transformer
{: #transformer}
Transformer는 클라우드 서버 API에서 새 정보를 요청하여 {{site.data.keyword.iotinsurance_short}}의 데이터와 일치하도록 변환합니다. 그런 다음 데이터는 나머지 {{site.data.keyword.iotinsurance_short}} 구현에서 사용할 수 있도록 공개됩니다. 

### 분석 엔진
{: #analytics_engine}
이벤트에 저장된 정보를 기반으로 분석 엔진에서 누수 같은 위해 발생 여부를 판별합니다. 위해가 식별되면 위해 제어기에 전달됩니다. 조치 엔진에는 데이터베이스의 데이터가 표시되어 실드에 지정된 정보를 기반으로 수행할 조치를 판별합니다. 

{{site.data.keyword.iotinsurance_short}} API를 사용하여 JavaScript에서 새 실드를 작성할 수 있습니다. 

### 실드
{: #shields}
실드는 고객이 보험 제공업체에게서 제공받는 특정 보호입니다. 예를 들어, 주택 소유자는 화재, 수해, 도난, 기타 위해로부터 보호하기 위해 주택에 대한 보험을 구매합니다. {{site.data.keyword.iotinsurance_short}} 솔루션에는 침수에 대한 기본 제공 실드가 있습니다. 주택에 침수와 관련된 사건이 발생하면 고객이 경보를 수신하고 응답할 수 있습니다. 개발자는 REST API를 사용하여 실드를 추가할 수 있습니다.
실드는 {{site.data.keyword.iotinsurance_short}} 분석 엔진에서 실행됩니다. 분석 엔진은 위해 유형(예: *침수 발견*), 위해를 전송한 센서의 사용자 계정, 계정과 연관된 실드를 식별합니다. 해당 정보를 기반으로 조치를 수행할 수 있습니다. 
