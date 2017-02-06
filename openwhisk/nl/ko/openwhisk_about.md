---

 

copyright:

  years: 2016, 2017
lastupdated: "2016-08-02"
 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 정보

다음 절에서는 {{site.data.keyword.openwhisk}}에 대한 세부사항을 제공합니다.
{: shortdesc}

## {{site.data.keyword.openwhisk_short}}의 작동 방식
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}}는 이벤트 구동 컴퓨팅 플랫폼으로 Serverless 컴퓨팅 또는 FaaS(Function as a Service)라고도 하며 이벤트 또는 직접 호출에 대한 응답으로 코드를 실행합니다. 

다음 그림에서는 상위 레벨 {{site.data.keyword.openwhisk_short}} 아키텍처를 보여줍니다. 

![{{site.data.keyword.openwhisk_short}} 아키텍처](OpenWhisk.png)

이벤트 예로는 데이터베이스 레코드에 대한 변경, 특정 온도를 초과하는 IoT 센서 읽기, GitHub 저장소에 대한 새 코드 커미트 또는 웹 또는 모바일 앱으로부터의 단순 HTTP 요청 등이 있습니다. 외부 및 내부 이벤트 소스의 이벤트는 트리거를 채널로 사용하며 규칙은 조치가 이러한 이벤트에 대해 반응하도록 허용합니다.

조치는 JavaScript 또는 Swift 코드의 작은 스니펫이거나 Docker 컨테이너에 임베드된 사용자 정의 2진 코드입니다. {{site.data.keyword.openwhisk_short}}의 조치는 트리거가 실행될 때마다 즉시 배치되고 실행됩니다. 더 많은 트리거가 실행될수록 더 많은 조치가 호출됩니다. 트리거가 실행되지 않으면 조치 코드가 실행되지 않으므로 비용이 발생하지 않습니다.

조치를 트리거와 연관시키는 것 외에 {{site.data.keyword.openwhisk_short}} API, CLI 또는 iOS SDK를 사용하여 조치를 직접 호출할 수도 있습니다. 코드를 작성하지 않고 일련의 조치를 체인화할 수 있습니다. 시퀀스 내의 한 조치의 출력이 다음 조치의 입력으로 전달되어 체인 내의 각 조치가 순서대로 호출됩니다.

일반적인 장기 실행 가상 머신 또는 컨테이너를 사용하는 경우, 단일 인스턴스의 가동 중단에 대해 복원할 수 있도록 다중 VM 또는 컨테이너를 배치하는 것이 일반적인 관례입니다. 그러나 {{site.data.keyword.openwhisk_short}}에서는 복원 관련 비용 오버헤드 없이 대체 모델을 제공합니다. 조치의 On-Demand 실행은 실행 중인 조치의 수가 항상 트리거 비율과 일치하도록 내재적인 확장성 및 최적화된 활용도를 제공합니다. 또한 개발자는 이제 기본 서버, 스토리지, 네트워크, 운영 체제 인프라의 모니터링, 패치, 보안에 대해 걱정할 필요 없이 코드에만 집중할 수 있습니다. 

추가 서비스 및 이벤트 제공자와의 통합이 패키지에 추가될 수 있습니다. 패키지는 피드와 조치의 번들입니다. 피드는 트리거 이벤트를 실행하기 위해 외부 이벤트 소스를 구성하는 코드 조작입니다. 예를 들어, Cloudant 변경 피드로 작성된 트리거는 문서가 수정되거나 Cloudant 데이터베이스에 추가될 때마다 트리거를 실행하도록 서비스를 구성합니다. 패키지의 조치는 개발자가 이벤트 소스로 서비스를 사용할 수 있을 뿐 아니라 해당 서비스의 API도 호출할 수 있도록 서비스 제공자가 제공할 수 있는 재사용가능 로직을 나타냅니다. 

패키지의 기존 카탈로그는 유용한 기능으로 애플리케이션을 강화하고 에코시스템 내에서 외부 서비스에 액세스할 수 있는 빠른 방법을 제공합니다. {{site.data.keyword.openwhisk_short}} 사용 가능 외부 서비스의 예로는 Cloudant, The Weather Company, Slack 및 GitHub 등이 있습니다.


## 공통 유스 케이스
{: #openwhisk_use_cases}

{{site.data.keyword.openwhisk_short}}에서 제공하는 실행 모델은 다양한 유스 케이스를 지원합니다. 다음 절에는 일반적인 예가 있습니다.

### 애플리케이션을 마이크로서비스로 분해
{: #openwhisk_use_cases_decomp}

{{site.data.keyword.openwhisk_short}}의 모듈 형식 및 내재적인 확장 특성으로 인해 조치에서 로직의 세부 단위 조작을 구현하는 데 적합합니다. 예를 들어, {{site.data.keyword.openwhisk_short}}는 프론트 엔드 코드에서 로드 집중적이며 잠재적인 두드러지는(백그라운드) 태스크를 제거하고 해당 태스크를 조치로 구현하는 데 유용합니다.

### 모바일 백엔드
{: #openwhisk_use_cases_mobile_backend}

많은 모바일 애플리케이션이 서버 측 로직을 요구합니다. 일반적으로 모바일 개발자는 서버 측 로직 관리 경험이 없고 디바이스에서 실행 중인 앱에 집중하는 점을 고려하면 서버 측 백엔드로 {{site.data.keyword.openwhisk_short}}를 사용하는 것이 좋은 솔루션입니다. 또한 Swift에 대한 기본 제공 지원으로 인해 개발자가 기존 iOS 프로그래밍 기술을 재사용할 수 있습니다.

### 데이터 처리
{: #openwhisk_use_cases_data_proc}

이제 많은 양의 데이터를 사용할 수 있으므로 애플리케이션 개발에서 새 데이터를 처리하고 잠재적으로 이에 대해 반응할 수 있는 기능이 필요합니다. 이 요구사항에는 비구조적 문서, 이미지 또는 동영상 및 구조적 데이터베이스 레코드 처리 기능이 포함됩니다.

### IoT
{: #openwhisk_use_cases_iot}

IoT(Internet of Things) 시나리오는 주로 거의 센서 구동입니다. 예를 들어, 특정 온도를 초과하는 센서에 반응해야 하는 경우 {{site.data.keyword.openwhisk_short}}의 조치가 트리거될 수 있습니다. 
