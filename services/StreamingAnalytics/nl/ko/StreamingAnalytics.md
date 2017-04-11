---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 정보
{: #about}

{{site.data.keyword.streaminganalyticsfull}}를 사용하여 {{site.data.keyword.Bluemix_short}} 애플리케이션의 일부로 작동 중인 데이터에 대해 실시간 분석을 수행할 수 있습니다.
{:shortdesc}

{{site.data.keyword.streaminganalyticsshort}}는 실시간으로 다양한 유형의 데이터 소스에서 도착하는 정보를 삽입, 분석, 상관시키기 위해 사용할 수 있는 고급 분석 플랫폼인 {{site.data.keyword.streamsshort}}에서 제공합니다. {{site.data.keyword.streaminganalyticsshort}} 서비스의 인스턴스를 작성하면 {{site.data.keyword.streamsshort}} 애플리케이션을 실행할 준비가 된 {{site.data.keyword.Bluemix_short}} 클라우드에서 자체 {{site.data.keyword.streamsshort}} 인스턴스를 실행할 수 있습니다. 

{{site.data.keyword.streaminganalyticsshort}}의 새로운 기능 [서비스에 대한 빠른 소개](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}를 확인하십시오. 자체 애플리케이션으로 작업을 더 수행하려면 {{site.data.keyword.streamsshort}} 개발 환경이 있어야 하고 SPL 클라우드 가능이어야 합니다.

{{site.data.keyword.streaminganalyticsshort}} 서비스는 클라우드에서 데이터를 배치, 분석, 모니터할 수 있게 하는 다음 기능을 제공합니다. 

**대화식 및 프로그램 방식 서비스의 사용:**

[{{site.data.keyword.streaminganalyticsshort}} 콘솔](/docs/services/StreamingAnalytics/c_streams_console.html)을 통해 대화식으로 또는 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}를 통해 프로그래밍 방식으로 서비스를 사용할 수 있습니다.

**SPL 및 Java 애플리케이션 배치 및 모니터링:**

SPL({{site.data.keyword.streamsfull}} Processing Language)은 스트림 처리 애플리케이션을 작성하는 데 사용되는 프로그래밍 언어입니다. {{site.data.keyword.streamsshort}} 애플리케이션을 SPL 또는 Java로 쓸 수 있습니다. {{site.data.keyword.streaminganalyticsshort}}를 사용하여 [이러한 애플리케이션을 배치하고 모니터](/docs/services/StreamingAnalytics/t_deploytocloud.html)하십시오.  

**{{site.data.keyword.streamsshort}} 연산자와의 호환성:**

{{site.data.keyword.streamsshort}} 연산자([{{site.data.keyword.streamsshort}} Processing Language(SPL) 표준 툴킷)는 모두 다음과 호환 가능](/docs/services/StreamingAnalytics/c_beta_adapters.html)해야 합니다. {{site.data.keyword.streaminganalyticsshort}}

## {{site.data.keyword.streaminganalyticsfull}} 책임

### 클라이언트 책임

클라이언트는 다음 사항에 대해 책임을 집니다. 

* IBM의 초기 {{site.data.keyword.streamsshort}} 구성 유지 및 해당 인스턴스에서 실행 중인 {{site.data.keyword.streamsshort}} 작업의 모니터링, 구성 및 관리. 클라이언트는 인스턴스를 시작 및 중지하고 인스턴스에서 jobskeywordnning을 시작 및 중지하는 유연성을 가집니다.
* 데이터를 분석하고 이를 통해 통찰력을 얻기 위해 필요 또는 필수인 프로그램 및 애플리케이션 개발. 클라이언트는 또한 그러한 개발된 프로그램이나 애플리케이션의 품질과 성능에 대해 책임을 집니다. 프로그램은 {{site.data.keyword.streamsshort}} 토폴로지 기능을 사용하여 SPL, Java, 또는 기타 지원되는 언어로 개발될 수 있습니다. {{site.data.keyword.streaminganalyticsshort}}에 사용된 것과 동일한 운영 체제에서 {{site.data.keyword.streamsshort}} Developer Edition 또는 {{site.data.keyword.streamsshort}} Quick Start Edition 중 하나를 사용하여 컴파일되어야 합니다. 
* 링크([https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window})를 정기적으로 확인하여 스케줄된 비중단 또는 중단 다운타임 파악.  
* 연속성을 보장하기 위해 비즈니스 요구사항에 따라 모든 데이터, 메타데이터, 구성 파일, 환경 매개변수 백업.
* 데이터 센터 또는 포드(pod) 장애, 서버 장애 또는 하드 디스크 고장이나 소프트웨어 실패 등 모든 유형의 장애가 발생할 경우 연속성을 보장하기 위해 백업으로부터 데이터, 메타데이터, 구성 파일, 환경 매개변수 복원.

### IBM의 책임

{{site.data.keyword.streaminganalyticsfull}}의 일부로 IBM은 다음을 수행합니다. 

* 고객 인스턴스에 대한 서버, 스토리지, 네트워킹 인프라의 제공 및 관리. 
* 노드의 수를 선택하고 해당 노드에서 {{site.data.keyword.streamsshort}}의 초기 구성 제공.
* 보호 및 고립을 위해 인터넷 페이싱과 내부 방화벽을 위한 인프라 제공 및 관리. 
* {{site.data.keyword.streaminganalyticsfull}}에서 다음 컴포넌트의 모니터링 및 관리.
	* 네트워크 컴포넌트
	* 서버 및 관련 로컬 스토리지
	* 인프라 운영 체제
	* {{site.data.keyword.streamsshort}} 관리 서비스
	* {{site.data.keyword.streamsshort}} 인스턴스 
* 인프라 운영 체제 및 {{site.data.keyword.streamsshort}}에 대한 보안 패치를 비롯하여 유지보수 패치 제공.
* 시스템 중단이 필요하지 않은 정기 유지보수(“비중단” 유지보수) 및 일부 시스템 중단과 재시작이 필요할 수 있는 유지보수의 수행. 이러한 “중단” 유지보수는 [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}에 공개된 스케줄된 시간에 수행됩니다. 
* 스케줄된 유지보수 시간의 변경은 적절한 통지와 함께 게시됩니다.  
