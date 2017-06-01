---



copyright:

  years: 2015, 2017

lastupdated: "2017-05-03"

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_dedicated_notm}}
{: #dedicated}


{{site.data.keyword.Bluemix}}는 애플리케이션을 빌드, 실행 및 관리하기 위한 개방형 표준, 클라우드 기반 플랫폼입니다. {{site.data.keyword.Bluemix_dedicated_notm}}를 사용하면, {{site.data.keyword.Bluemix_notm}} 퍼블릭 환경과 자체 네트워크 모두에 안전하게 연결되어 있는 자체 전용 SoftLayer 환경에서 {{site.data.keyword.Bluemix_notm}}&mdash;의 강력한 성능과 단순성을 이용할 수 있습니다.
{:shortdesc}

모든 {{site.data.keyword.Bluemix_notm}} 데디케이티드 배치에는 추가 비용 없이 VPN, 사설 VLAN(Virtual 로컬 Area Network), 방화벽, LDAP을 통한 연결, 기존 온프레미스 데이터베이스 및 앱을 활용하는 능력, 연중 무휴 온사이트 보안, 데디케이티드 하드웨어, 표준 지원 등 여러 혜택과 기능이 포함됩니다.

기본적으로 개인용 {{site.data.keyword.Bluemix_notm}} 인스턴스는 회사 네트워크에서만 액세스할 수 있습니다. 예를 들어, 인터넷 또는 모바일 디바이스, 데디케이티드 데이터베이스에서 직접 {{site.data.keyword.Bluemix_notm}} 환경에 액세스할 수 있도록 해야 하는 경우 추가 네트워크 보안 컴포넌트가 필요하며 이를 위해서는 추가 비용이 발생합니다.

{{site.data.keyword.Bluemix_dedicated_notm}}은 {{site.data.keyword.Bluemix_notm}} 런타임 및 64GB의 컴퓨팅 리소스 메모리가 모두 포함되어 제공됩니다.

또한 포함되거나 선택적으로 구입할 수 있는 서비스 및 컴포넌트 세트가 있습니다. 다음 표를 검토하여 포함되는 항목과 선택적으로 구입 가능한 항목을 확인하십시오.

| **유형**        | **이름**            | **설명** |
|-----------------|-------------------|-------------------|
|포함 | [{{site.data.keyword.Bluemix_notm}} 런타임](/docs/cfapps/runtimes.html) | 시스템 및 운영 체제를 설정하고 관리할 필요 없이 신속하게 앱을 시작하고 실행하려면 런타임을 사용하십시오. 모든 {{site.data.keyword.Bluemix_notm}} 런타임은 {{site.data.keyword.Bluemix_dedicated_notm}} 인스턴스에서 사용 가능합니다.|
| 포함 | [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html) | 정책에 따라 애플리케이션의 컴퓨팅 용량을 동적으로 늘리거나 줄입니다. 이 서비스를 사용하면 {{site.data.keyword.Bluemix_dedicated_notm}} 환경에서 무제한 사용이 가능합니다. 참고: Auto-Scaling은 현재 Cloud Foundry 런타임에서만 작동합니다. |
|선택사항 | [{{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect/index.html) | {{site.data.keyword.apiconnect_long}}는 {{site.data.keyword.APIM}}와 IBM StrongLoop를 API 및 마이크로서비스를 작성, 실행, 관리 및 적용하기 위한 포괄적 솔루션을 제공하는 단일 오퍼링으로 통합합니다. |
|선택사항 | [{{site.data.keyword.rules_short}}](/docs/services/rules/rules.html) | {{site.data.keyword.rules_short}}는 자주 발생하는 반복 가능한 규칙 기반 비즈니스 의사결정을 자동화하고 실행하기 위한 포괄적 환경을 제공합니다. 또한 이를 통해 IT 기술의 필요성을 줄여 비즈니스 사용자 또는 개발자가 저비용으로 신속하게 의사결정을 모델링하고 테스트할 수 있습니다. |
|선택사항 | [{{site.data.keyword.cloudant}}](/docs/services/Cloudant/index.html#Cloudant) | {{site.data.keyword.cloudant}}에서는 항상 작동 상태인 완전히 관리되는 NoSQL JSON 데이터 계층에 대한 액세스를 제공합니다. 이 서비스는 CouchDB와 호환 가능하며, 모바일 및 웹 애플리케이션 모델을 위한 사용이 간편한 HTTP 인터페이스를 통해 액세스할 수 있습니다. |
|선택사항 | [{{site.data.keyword.containershort}}](/docs/containers/container_index.html) | {{site.data.keyword.Bluemix_dedicated_notm}}에서 Docker 컨테이너를 실행합니다. 컨테이너는 앱에서 실행해야 하는 모든 요소를 포함하는 가상 소프트웨어 오브젝트입니다. 컨테이너는 리소스 격리와 할당의 이점이 있으며 가상 머신 등보다 휴대가 간편하고 효율적입니다. 하드웨어 요구사항에 대한 정보는 [{{site.data.keyword.Bluemix_dedicated_notm}} 및 Bluemix 로컬의 IBM {{site.data.keyword.containershort}}](/docs/containers/container_ov.html#container_dl)를 참조하십시오.|
| 선택사항 | [{{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html) | {{site.data.keyword.contdelivery_short}} 데디케이티드를 사용하여 빌드, 단위 테스트, 배치 등을 자동화합니다. 풍부한 웹 기반 IDE을 통해 코드를 편집하고 푸시하십시오. 개발, 배치 및 오퍼레이션 태스크를 지원하는 도구 통합을 가능하게 하는 도구 체인을 작성합니다. |
| 선택사항 | [{{site.data.keyword.dashdbshort}}](/docs/services/dashDB/dashDB.html) | IBM {{site.data.keyword.dashdbshort}} for Analytics는 전체 관리되는 SQL 클라우드 데이터베이스 서비스이고, 데이터 웨어하우스와 분석 워크로드를 위해 최적화되어 있습니다. IBM {{site.data.keyword.dashdbshort}} for Transactions는 전체 관리되는 SQL 클라우드 데이터베이스 서비스이고 일반적인 용도, 웹 앱 및 트랜잭션 워크로드를 위해 최적화되어 있습니다. |
| 선택사항 | [{{site.data.keyword.datacshort}}](/docs/services/DataCache/index.html#data_cache) | 이 서비스는 앱에 대한 분산 캐싱 시나리오를 지원하는 인메모리 데이터 그리드를 제공합니다. 50GB의 인메모리 캐시가 포함됩니다. |
| 선택사항 | [Dedicated GitHub Enterprise](/docs/services/ghededicated/index.html) | {{site.data.keyword.ghe_long}}는 IBM 클라우드에 호스팅되고 완전하게 관리되는 GitHub Enterprise 버전이며 개발자가 선호하는 소셜 경험을 제공합니다. 이 서비스는 현재 {{site.data.keyword.Bluemix_dedicated_notm}} 환경에서만 사용할 수 있습니다.  |
| 선택사항(베타) | [Logging](/docs/monitoringandlogging/cfapps_ml_logs_dedicated_ov.html#container_ml_logs_dedicated_ov) | Kibana의 검색 가능한 로그 및 대시보드와 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스의 Cloud Foundry 앱에 대한 로그를 제공합니다. |
| 선택사항 | [{{site.data.keyword.messagehub}}](/docs/services/MessageHub/index.html#messagehub) | {{site.data.keyword.messagehub}}는 온프레미스와 오프프레미스 기술을 통합하는 확장 가능하고 처리량이 많은 분산 메시지 버스입니다. {{site.data.keyword.messagehub}}는 빠르고 확장 가능하고 내구성 강한 실시간 메시징 엔진인 Apache Kafka를 기반으로 합니다. |
|선택사항 | [{{site.data.keyword.mobilepush}}](/docs/services/mobilepush/index.html) | {{site.data.keyword.mobilepush}}는 iOS 및 Android 디바이스에 알림을 보내는 데 사용할 수 있는 서비스입니다. 알림은 모든 애플리케이션 사용자와 태그를 사용하는 특정 디바이스 및 사용자 세트를 대상으로 할 수 있습니다. 디바이스, 태그 및 구독을 관리할 수 있습니다. SDK(Software Development Kit) 및 REST(Representational State Transfer) API(Application Program Interface)를 사용하여 클라이언트 애플리케이션을 추가적으로 개발할 수도 있습니다.|
|선택사항 | [{{site.data.keyword.SecureGateway}}](/docs/services/SecureGateway/secure_gateway.html) | {{site.data.keyword.SecureGateway}} 서비스는 온프레미스 또는 클라우드를 통해 {{site.data.keyword.Bluemix_notm}} 애플리케이션을 원격 위치에 연결하는 안전한 방법을 제공합니다.  |
|선택사항 | [{{site.data.keyword.sescashort}}](/docs/services/SessionCache/index.html#session_cache) | 증가된 중복성을 위해 {{site.data.keyword.sescashort}}에서는 캐시에 저장된 세션의 복제본을 제공합니다. 따라서 등화 관제 또는 가동 중단의 상황에서도 클라이언트 애플리케이션은 캐시의 세션에 계속 액세스할 수 있습니다. 이 서비스는 웹 및 모바일 애플리케이션에 대한 세션 캐싱 시나리오를 지원합니다. |
| 선택사항 | [{{site.data.keyword.iot_short}}](/docs/services/IoT/index.html) | 이 서비스를 사용하여 앱은 연결된 디바이스, 센서 및 게이트웨이와 통신하고 여기서 수집한 데이터를 이용할 수 있습니다. 기본 오퍼링은 1.6TB의 데이터 교환과 100,000개의 동시 연결된 디바이스 또는 애플리케이션의 용량을 지닌 데디케이티드 환경 내에서 {{site.data.keyword.iot_short}}의 개인용 버전 실행을 허용합니다. |
| 선택사항 | [{{site.data.keyword.appserver_short}}](/docs/services/ApplicationServeronCloud/index.html) | IBM {{site.data.keyword.appserver_short}} for IBM {{site.data.keyword.Bluemix_notm}}는 {{site.data.keyword.Bluemix_notm}}의 호스팅 클라우드 환경에서 사전 구성된 {{site.data.keyword.appserver_short}} Liberty, 기존 네트워크 배치 또는 기존 WebSphere Java EE 인스턴스를 빠르게 설정할 수 있는 편리한 서비스입니다.  |
{: caption="표 1. 전용 서비스" caption-side="top"}
{: #table01}



리소스 및 서비스의 용량을 스케일링하고 확장하기 위해 구매할 수 있는 선택적 컴포넌트가 있습니다. 영업 팀에 문의하면 이 컴포넌트를 구입할 수 있습니다. 영업 담당자의 연락처 정보를 보려면 [담당자](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs)로 이동하십시오. 서비스에 대한 플랜을 늘리기 위해 카탈로그의 서비스 타일에서 플랜을 선택할 수 있습니다.

| **이름**            | **설명** |
|-------------------|-------------------|
|데디케이티드 {{site.data.keyword.apiconnect_short}} Professional 500만 API 호출 | 부서별 API 프로젝트 방향으로 대상 지정된 월간 500만 API 호출의 용량을 지닌 데디케이티드 환경 내의 {{site.data.keyword.apiconnect_short}}의 개인용 버전 실행을 허용하는 환경입니다.  |
|데디케이티드 {{site.data.keyword.apiconnect_short}} Professional 10만 API 호출 증가 | 매월 10만 API 호출의 추가 용량을 제공하는 {{site.data.keyword.apiconnect_short}} Professional 환경의 확장입니다.  |
|데디케이티드 {{site.data.keyword.apiconnect_short}} Enterprise 2,500만 API 호출 | 엔터프라이즈 전체 API 프로젝트 방향으로 대상 지정된 월간 2,500만 API 호출의 용량을 지닌 데디케이티드 환경 내의 {{site.data.keyword.apiconnect_short}}의 개인용 버전 실행을 허용하는 환경입니다.  |
|데디케이티드 {{site.data.keyword.apiconnect_short}} Enterprise 10만 API 호출 증가 | 매월 10만 API 호출의 추가 용량을 제공하는 {{site.data.keyword.apiconnect_short}} Enterprise 환경의 확장입니다.  |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.rules_short}} 1백만 규칙 의사결정 | 규칙 의사결정은 규칙 실행 서버에서 규칙 세트를 호출한 결과입니다. 청구 기간 중에 실행되거나 처리된 총 규칙 의사 결정 수(가장 가까운 백만 단위로 반올림됨)를 커버하려면 충분한 인타이틀먼트를 확보해야 합니다. 클라우드 서비스에서 측정되는 규칙 의사결정은 의사결정을 얻기 위해 규칙 실행 서버로 이루어진 호출입니다. 클라우드 서비스의 전용 배치에서 합의된 용량은 관련 비용 메트릭으로 측정됩니다. {{site.data.keyword.Bluemix_dedicated_notm}} 플랫폼의 {{site.data.keyword.rules_short}} 서비스 기본 영역 할당량은 16GB이며, 규칙 의사결정을 실행하기 위해 각각 1GB인 인스턴스를 10개까지 호출할 수 있습니다. 사용 한계를 초과하면 이 초과 사용을 위해 추가 용량을 구매해야 합니다. |
|데디케이티드 {{site.data.keyword.cloudant}} 1.6TB 용량 증가 | 1.6TB 디자인 용량의 데디케이티드 환경 내에서 {{site.data.keyword.cloudantfull}}의 개인용 버전 실행을 포함합니다.  |
|데디케이티드 {{site.data.keyword.datacshort}} 및 {{site.data.keyword.sescashort}} 50GB 용량 증가 | 최대 50GB 누적 용량까지 {{site.data.keyword.datacshort}} 및 {{site.data.keyword.sescashort}} 인스턴스의 배치 및 실행을 허용하는 환경입니다. |
|{{site.data.keyword.contdelivery_short}} 데디케이티드 인스턴스 | 전용 환경에서 실행되는 개인용 버전의 {{site.data.keyword.contdelivery_short}}입니다. 용량은 {{site.data.keyword.contdelivery_short}} 데디케이티드 권한 부여된 사용자 인타이틀먼트로 결정됩니다. |
|{{site.data.keyword.contdelivery_short}} 데디케이티드 권한 부여된 사용자 | 지정된 {{site.data.keyword.contdelivery_short}} 데디케이티드 환경 사용을 위해 권한 부여된 사용자에게 액세스 권한을 부여합니다. {{site.data.keyword.contdelivery_short}} 서비스 인스턴스를 포함하는 {{site.data.keyword.Bluemix_notm}} 조직에 속한 모든 사용자에게 권한이 부여되어야 합니다. |
|데디케이티드 {{site.data.keyword.dashdbshort}} Enterprise 64.1 | 64GB RAM, 16 vCPU의 데디케이티드 서버에서 서비스 인스턴스당 하나의 데이터베이스. 일반 압축을 기반으로 최대 1TB의 사전 로드 데이터에 권장됩니다.  |
|데디케이티드 {{site.data.keyword.dashdbshort}} Enterprise 256.4 | 256GB RAM, 32 코어의 데디케이티드 베어메탈 서버에서 서비스 인스턴스당 하나의 데이터베이스. 일반 압축을 기반으로 최대 4TB의 사전 로드 데이터에 권장됩니다. |
|데디케이티드 {{site.data.keyword.dashdbshort}} Enterprise 256.12  | 256GB RAM, 32 코어의 데디케이티드 베어메탈 서버에서 서비스 인스턴스당 하나의 데이터베이스. 일반 압축을 기반으로 최대 12TB의 사전 로드 데이터에 권장됩니다. 이는 데이터 볼륨이 크며 인메모리 속도로 조회를 실행할 필요가 없는 환경에 적합한 스토리지 고밀도 플랜입니다. |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.dashdbshort}} Enterprise for Transactions 2.8.500 | 8GB RAM과 데이터 및 로그를 위한 500GB의 영역으로 OLTP(Online Transaction Processing) 워크로드를 지원하는 데디케이티드 인스턴스입니다. |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.dashdbshort}} Enterprise for Transactions 12.128.1400 | 128GB RAM과 데이터 및 로그를 위한 1.4TB SSD 스토리지로 OLTP(Online Transaction Processing) 워크로드를 지원하는 데디케이티드 인스턴스입니다. |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.dashdbshort}} Enterprise for Transactions High Availability 2.8.500 | 8GB RAM과 데이터 및 로그를 위한 500GB의 영역으로 OLTP(Online Transaction Processing) 워크로드를 지원하는 데디케이티드 인스턴스이며 여기에는 고가용성을 위한 추가 대기 서버가 포함됩니다. |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.dashdbshort}} Enterprise for Transactions High Availability 12.128.1400 | 128GB RAM과 데이터 및 로그를 위한 1.4TB SSD 스토리지로 OLTP(Online Transaction Processing) 워크로드를 지원하는 데디케이티드 인스턴스이며 여기에는 고가용성을 위한 추가 대기 서버가 포함됩니다. |
|{{site.data.keyword.Bluemix_dedicated_notm}} 커뮤니티 서비스  | 각 커뮤니티 서비스마다 총 50개 인스턴스까지 커뮤니티 서비스의 배치 및 실행을 허용하는 환경입니다.  |
|{{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.cloudant}} 클러스터 인스턴스 | 이 선택적 컴포넌트에는 사용자가 인프라 제공을 담당하는 3노드 클러스터가 포함되며 스토리지 및 컴퓨팅 용량은 사용자의 특정 요구에 맞게 결정될 수 있습니다. {{site.data.keyword.cloudant}}에서는 항상 작동 상태인 완전히 관리되는 NoSQL JSON 데이터 계층에 대한 액세스를 제공합니다. 이 서비스는 CouchDB와 호환 가능하며, 모바일 및 웹 애플리케이션 모델을 위한 사용이 간편한 HTTP 인터페이스를 통해 액세스할 수 있습니다. |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.messagehub}} | 파티션(100개 파티션으로 제함됨)당 최대 10GB의 발행/구독 메시징을 제공하는 환경입니다.   |
|IBM Bluemix 데디케이티드 {{site.data.keyword.mobilepushshort}} | 초당 300개의 요청을 승인하는 기능으로 {{site.data.keyword.mobilepushshort}} 인스턴스의 배치 및 실행을 허용하는 환경입니다. |
|{{site.data.keyword.iot_short}} 데디케이티드 증분 증가 | 0.5TB의 데이터 교환과 100,000개의 동시 연결된 디바이스 또는 애플리케이션의 용량을 지닌 데디케이티드 환경 내에서 {{site.data.keyword.iot_short}}의 개인용 버전 실행을 허용하는 환경 증가입니다. |
|IBM {{site.data.keyword.appserver_short}} for {{site.data.keyword.Bluemix_notm}} - 데디케이티드 소형| 매월 64개 vCore, 128GB RAM 및 1TB HDD가 제공되는 {{site.data.keyword.Bluemix_notm}}의 호스팅 클라우드 환경에 사전 구성된 {{site.data.keyword.appserver_short}} Liberty, 기존 네트워크 배치 또는 기존 WebSphere Java EE 인스턴스.  |
|IBM {{site.data.keyword.appserver_short}} for {{site.data.keyword.Bluemix_notm}} - 데디케이티드 중형| 매월 128개 vCore, 256GB RAM 및 2TB HDD가 제공되는 {{site.data.keyword.Bluemix_notm}}의 호스팅 클라우드 환경에 사전 구성된 {{site.data.keyword.appserver_short}} Liberty, 기존 네트워크 배치 또는 기존 WebSphere Java EE 인스턴스.  |
|IBM {{site.data.keyword.appserver_short}} for {{site.data.keyword.Bluemix_notm}} - 데디케이티드 대형| 매월 256개 vCore, 512GB RAM 및 4TB HDD가 제공되는 {{site.data.keyword.Bluemix_notm}}의 호스팅 클라우드 환경에 사전 구성된 {{site.data.keyword.appserver_short}} Liberty, 기존 네트워크 배치 또는 기존 WebSphere Java EE 인스턴스.  |
|IBM {{site.data.keyword.appserver_short}} for {{site.data.keyword.Bluemix_notm}} - 데디케이티드| 매월 HDD Expansion 및 1TB가 제공되는 {{site.data.keyword.Bluemix_notm}}의 호스팅 클라우드 환경에 사전 구성된 {{site.data.keyword.appserver_short}} Liberty, 기존 네트워크 배치 또는 기존 WebSphere Java EE 인스턴스.  |
{: caption="표 2. 구매할 수 있는 선택적 서비스 컴포넌트" caption-side="top"}
{: #table02}



| **이름**            | **설명** |
|-------------------|-------------------|
|데디케이티드 런타임 16GB 용량 증가  | 추가 16GB 런타임 용량을 제공하는 런타임 환경의 확장입니다. |
|데디케이티드 Direct Link 1Gbps 용량 | 최대 1Gbps의 데이터 전송을 위해 디자인된 해당 {{site.data.keyword.BluSoftlayer}} 네트워크 PoP(Point of Presence)에 직접 연결된 데디케이티드 네트워크 링크입니다. |
|데디케이티드 Direct Link 10Gbps 용량 | 최대 10Gbps의 데이터 전송을 위해 디자인된 해당 {{site.data.keyword.BluSoftlayer}} 네트워크 PoP(Point of Presence)에 직접 연결된 데디케이티드 네트워크 링크입니다. |
|IBM Bluemix 데디케이티드 하드웨어 방화벽 - 고가용성 | 데디케이티드 환경 내의 동일한 VLAN에서 단일, 다중 또는 모든 서버를 보호하기 위해 구성된 중복 1Gbps 하드웨어 방화벽입니다. |
{: caption="표 3. 구매할 수 있는 선택적 플랫폼 추가 기능 컴포넌트" caption-side="top"}
{: #table03}

**참고**: {{site.data.keyword.Bluemix_dedicated_notm}} 컴포넌트는 특정 구성 용량(예: 기가바이트 또는 초당 트랜잭션)을 표시할 수 있습니다. 클라우드 서비스의 구성에 대한 사실상의 실제 용량이 수많은 요인에 따라 다양하므로, 사실상의 실제 용량은 구성된 용량보다 크거나 작을 수 있습니다.

### 신디케이트된(각 클라우드 형태 간 동일하게 연동된) 카탈로그
{: #catalogdedicated}

{{site.data.keyword.Bluemix_dedicated_notm}}에는 퍼블릭, 데디케이티드 및 로컬 배치의 승인된 서비스를 한데 모으는 개인용 카탈로그가 있습니다. 이 {{site.data.keyword.Bluemix_notm}} 카탈로그를 통해 사용자 소유의 서비스를 공개하고 서비스에 대한 액세스를 관리할 수도 있습니다. 데이터에 대한 개인정보 보호정책 및 보안 기준에 따라 사용자 비즈니스의 요구사항을 충족해야 하는 공용 서비스를 결정하는 옵션이 있습니다.

데디케이티드 환경에 대한 서비스의 개인용 인스턴스가 있으면 카탈로그에 서비스 이름과 함께 "데디케이티드" 태그가 표시됩니다. 마찬가지로, 사용자 정의 서비스인 경우(즉, 서비스 브로커를 사용하여 작성한 경우)에는 서비스 이름과 함께 "사용자 정의"가 나열됩니다. "데디케이티드" 또는 "사용자 정의" 태그 없이 나열된 기타 모든 서비스는 {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 신디케이션을 사용하여 사용할 수 있습니다. 신디케이트된(각 클라우드 형태 간 동일하게 연동된) 카탈로그는 공용 및 개인 서비스로 구성되는 하이브리드 애플리케이션을 작성하는 기능을 제공합니다. 

|서비스	|미국 남부 지역에서 사용 가능	|유럽 영국 지역에서 사용 가능 |오스트레일리아 시드니 지역에서 사용 가능|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.alchemyapishort}} 		|예	   	|예  		|예|
|{{site.data.keyword.alertnotificationshort}}	|예		|예		|예	|
|{{site.data.keyword.apiconnect_short}}         |예            |예            |예  |
|{{site.data.keyword.appseccloudshort}}		|예		|예		|예 |
|{{site.data.keyword.apiconnect_short}} 	|예   	 	|예  	 	|예   |
|Automated Accessibility Checker |예       |예    |예   |
|{{site.data.keyword.rules_short}}		|예		|예		|예 |
|{{site.data.keyword.cloudant}}			|예		|예		|예 |
|{{site.data.keyword.iotmapinsights_short}}    |예  |예  |예  |
|{{site.data.keyword.conversationshort}}  |예  |예  |예  |
|{{site.data.keyword.dashdbshort}}		|예		|예		|예 |
|{{site.data.keyword.dataworks_short}}		|예		|예		|아니오|
|{{site.data.keyword.DB2OnCloud_short}}		|예		|예		|예 |
|Digital Content Checker |예  |예  |예  |
|{{site.data.keyword.documentconversionshort}}	|예		|예		|예|
|{{site.data.keyword.iotdriverinsights_short}}  |예 |예  |예  |
|{{site.data.keyword.geospatialshort_Geospatial}}	|예	|예		|예 |
|{{site.data.keyword.GlobalizationPipeline_short}}	|예		| 예		| 예 |
|{{site.data.keyword.identitymixershort}}		|예		|예		|예|
|{{site.data.keyword.iot4auto_short}} |예   |예  |예  |
|{{site.data.keyword.iotelectronics}}  |예  |예  |아니오 |
|{{site.data.keyword.iotinsurance_short}} |아니오   |아니오   |예  |
|{{site.data.keyword.twittershort}}		|예		|예		|예|
|{{site.data.keyword.languagetranslationshort}}	|예		|예		|예 |
|{{site.data.keyword.languagetranslatorshort}} |예  |예  |예  |
|{{site.data.keyword.dwl_short}}  |예  |예  |아니오  |
|{{site.data.keyword.eventhubshort}}		|예		|아니오		|아니오|
|{{site.data.keyword.messagehub}}		|예		|예		|아니오|
|{{site.data.keyword.manda}}			|예		|예		|예 |
|{{site.data.keyword.amashort}}			|예		|예		|예 |
|{{site.data.keyword.mqa}}			|예		|예		|예 |
|{{site.data.keyword.mql}}			|아니오		|아니오		|예 |
|{{site.data.keyword.nlclassifierlshort}} 	|예 		|예 		|예|
|{{site.data.keyword.personalityinsightsshort}}	|예		|예		|예|
|{{site.data.keyword.pm_short}}			|예		|예		|아니오 |
|{{site.data.keyword.mobilepush}}		|예		|예		|예 |
|{{site.data.keyword.retrieveandrankshort}}	|예 		|예 		|예|
|{{site.data.keyword.runbook_short}}		|예		|예		|예|
|{{site.data.keyword.SecureGateway}}		|예		|예		|예 |
|{{site.data.keyword.ssofull}}			|예		|아니오		|아니오|
|{{site.data.keyword.speechtotextshort}}	|예 		|예	 	|예|
|{{site.data.keyword.streaminganalyticsshort}}	|예		|예		|예 |
|{{site.data.keyword.texttospeechshort}} 	|예 		|예	 	|예|
|{{site.data.keyword.toneanalyzershort}} 	|예 		|예 		|예|
|{{site.data.keyword.tradeoffanalyticsshort}}	|예		|예		|예|
|{{site.data.keyword.visualrecognitionshort}}	|예 		|예	 	|예|
|{{site.data.keyword.iot_short}}		|예		|예		|아니오|
|{{site.data.keyword.weather_short}}		|예		|예		|예|
|{{site.data.keyword.workloadscheduler}}	|예		|예		|예 |
{: caption="표 4. 지역별 Bluemix 공용에서 신디케이션에 사용 가능한 서비스" caption-side="top"}
{: #table04}

**참고**: 표에 써드파티 서비스가 포함되어 있지 않습니다. 써드파티 서비스 옵션에 대한 데디케이티드 카탈로그를 확인하십시오. 



## {{site.data.keyword.Bluemix_dedicated_notm}} 아키텍처
{: #dedicatedarch}

{{site.data.keyword.Bluemix_dedicated_notm}}를 전 세계의 [{{site.data.keyword.IBM_notm}} SoftLayer 데이터 센터 ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://www.softlayer.com/data-centers){: new_window}에 배치할 수 있습니다. {{site.data.keyword.IBM_notm}} SoftLayer는 고성능 클라우드 인프라를 제공합니다. 각 데이터 센터에서는 연중 무휴 하루 24시간 보안 및 엄격한 제어를 수행합니다. 

각 {{site.data.keyword.Bluemix_dedicated_notm}} 배치는 자체 사설 네트워크에서 {{site.data.keyword.IBM_notm}} SoftLayer 데디케이티드 하드웨어에 연결된 단일 엔터프라이즈에만 사용됩니다. {{site.data.keyword.Bluemix_dedicated_notm}} 환경은 인프라, 운영 및 물리적 보안이라는 면에서 퍼블릭 {{site.data.keyword.Bluemix_notm}}와 보안 표준이 동일합니다. 그러나 데디케이티드 {{site.data.keyword.Bluemix_notm}}에 대한 개발자 액세스는 LDAP 정책에 의해 제어되며, 이 정책은 환경을 설정할 때 {{site.data.keyword.Bluemix_notm}} 팀에서 구성할 수 있습니다. 데디케이티드 환경 내에서는 사용자 역할 및 권한을 관리할 수 있습니다. 세부사항은 [관리자 및 권한 관리](/docs/admin/index.html#oc_useradmin)를 참조하십시오. 다음 그림은 기본 {{site.data.keyword.Bluemix_dedicated_notm}} 배치의 논리적 아키텍처를 보여줍니다.

![{{site.data.keyword.Bluemix_dedicated_notm}}](images/bm_dedicated_arch.png "{{site.data.keyword.Bluemix_dedicated_notm}} 기본 아키텍처")

그림 1. 자세한 {{site.data.keyword.Bluemix_dedicated_notm}} 다이어그램 기본 아키텍처
{: #figure01}

이전 아키텍처 다이어그램에서 설명된 중요한 아키텍처 컴포넌트에는 다음 사항이 포함되어 있습니다.

<dl>
<dt>{{site.data.keyword.IBM_notm}} 클라우드</dt>
<dd>
{{site.data.keyword.IBM_notm}} Cloud 환경 전체에는 다음과 같은 중요한 네트워킹 환경이 포함되어 있습니다.
<ul>
<li>{{site.data.keyword.Bluemix_dedicated_notm}}</li>
<li>{{site.data.keyword.Bluemix_notm}} 퍼블릭</li>
<li>{{site.data.keyword.IBM_notm}} 운영 센터</li>
</ul>
</dd>
<dt>{{site.data.keyword.Bluemix_dedicated_notm}}</dt>
<dd>
최소한, 여기에는 Cloud Foundry 컴포넌트과 일부 데디케이티드 애플리케이션 서비스가 있습니다. {{site.data.keyword.Bluemix_notm}}는 Cloud Foundry와 {{site.data.keyword.containerlong}} 기반 컴퓨팅 환경을 모두 제공합니다. 엔터프라이즈에는 이러한 컴퓨팅 환경 중 하나 또는 둘 모두가 구성되어 있을 수 있습니다. <br>
엔터프라이즈는 추가 데디케이티드 애플리케이션 서비스를 추가할 수 있습니다. <br>
추가할 수 있는 추가 서비스와 컴퓨팅 기능은 [표 2](#table02)를 참조하십시오.
</dd>
<dt>{{site.data.keyword.Bluemix_notm}} 퍼블릭</dt>
<dd>
{{site.data.keyword.Bluemix_dedicated_notm}}에는 {{site.data.keyword.Bluemix_notm}} 퍼블릭 지역에 대한 아웃바운드 연결이 있을 수 있습니다. 이는 데디케이티드 카탈로그에 퍼블릭 서비스의 신디케이션을 제공합니다. {{site.data.keyword.Bluemix_notm}} 퍼블릭 서비스 신디케이션은 개발자가 엔터프라이즈의 {{site.data.keyword.Bluemix_dedicated_notm}}에서 호스팅되는 애플리케이션을 빌드하고 {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 실행되는 서비스에 액세스하는 데 편리한 방법을 제공합니다. [신디케이트된 카탈로그 절의 표4](#catalogdedicated)에 표시된 {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 신디케이트할 수 있는 서비스 목록.
</dd>
<dt>{{site.data.keyword.IBM_notm}} 운영 센터</dt>
<dd>
{{site.data.keyword.IBM_notm}}은 사용자가 혁신적인 애플리케이션을 빌드하는 작업에 집중할 수 있도록 데디케이티드 플랫폼과 데디케이티드 서비스를 관리하고 모니터하며 유지보수합니다. {{site.data.keyword.IBM_notm}} Operations Support Services(OSS) 팀은 {{site.data.keyword.IBM_notm}}의 운영 네트워크에서 VPN 터널 연결을 사용하여 오퍼레이션을 수행합니다.
</dd>
<dt>엔터프라이즈</dt>
<dd>
엔터프라이즈 네트워크 환경에는 {{site.data.keyword.Bluemix_dedicated_notm}}에 대한 보안 사설 양방향 네트워크 링크가 있습니다. {{site.data.keyword.Bluemix_dedicated_notm}}에서 호스팅되는 애플리케이션은 이 링크를 통해 데이터 소스 및 엔터프라이즈 서비스를 포함하여 엔터프라이즈의 서비스 및 리소스에 액세스할 수 있습니다. 또한 {{site.data.keyword.Bluemix_dedicated_notm}}는 이 네트워크 링크를 통해 엔터프라이즈의 개발자와 관리자의 인증에 LDAP을 사용할 수 있습니다. <br>
<br>
보안 사설 네트워크 링크를 작성하기 위한 몇 가지 옵션이 있습니다. 엔터프라이즈를 위한 최적의 네트워킹 옵션에 대해 IBM 기술 전문가에게 문의하십시오. <br>
<br>
{{site.data.keyword.Bluemix_dedicated_notm}}에서 엔터프라이즈 네트워크로의 기본 연결에는 가상 사설망(VPN)을 사용합니다. {{site.data.keyword.Bluemix_dedicated_notm}}에는 고가용성을 위해 구성된 데디케이티드 1 Gbps Vyatta VPN 종료가 있습니다.
<br>
[그림 1](#figure01)에 표시된 대로 {{site.data.keyword.Bluemix_dedicated_notm}}용 기본 아키텍처에는 인터넷에서 직접 유입되는 인바운드 네트워크 트래픽이 없습니다. 엔터프라이즈가 {{site.data.keyword.Bluemix_dedicated_notm}}에서 호스팅된 애플리케이션에 인터넷으로 액세스하려는 경우, 엔터프라이즈 네트워크를 통해 액세스를 구성해야 합니다.
</dd>
</dl>


## {{site.data.keyword.Bluemix_dedicated_notm}} 설정
{: #setupdedicated}

{{site.data.keyword.Bluemix_dedicated_notm}}는 {{site.data.keyword.Bluemix_notm}} 퍼블릭 오퍼링의 개인용 버전을 제공하도록 디자인되었습니다. {{site.data.keyword.Bluemix_notm}} 서비스 및 런타임을 사용하여 IBM이 호스팅하는 {{site.data.keyword.BluSoftlayer}} 계정의 컴퓨팅 요구사항을 지원할 수 있습니다.

IBM은 비밀번호로 보호되는 로그인을 사용하여 {{site.data.keyword.Bluemix_dedicated_notm}}에 대한 액세스를 제공합니다. 서비스, 런타임 및 연관된 리소스에 액세스하고 {{site.data.keyword.Bluemix_notm}} 앱을 배치 및 제거할 수 있습니다. IBM이 다수의 {{site.data.keyword.BluSoftlayer}} 위치를 활용하여 {{site.data.keyword.Bluemix_dedicated_notm}}를 제공하기 때문에 사용자는 자신에게 가까운 위치에서 개인용 버전을 가져올 수 있습니다.

{{site.data.keyword.Bluemix_notm}}의 개인용 버전 설정:

<ol>
<li>시작하려면 IBM 지정 계정 담당자에게 문의하거나 <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}에 문의 <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>하십시오. </li>
<li>{{site.data.keyword.Bluemix_dedicated_notm}} 인스턴스의 사용 요금에 관해 IBM과 함께 작업하십시오. 매월 발생하는 요금은 사용하고자 하는 데디케이티드 서비스 및 모든 {{site.data.keyword.Bluemix_notm}} 퍼블릭 서비스에 대한 구독을 기반으로 합니다. 그런 다음 해당 구독 계약과 더불어 사용하는 모든 항목에 대한 송장을 수령하십시오.</li>
<li>{{site.data.keyword.Bluemix_dedicated_notm}} 인스턴스 설정의 각 단계(Phase)마다 최종 기한을 식별하십시오. 각 단계 및 관련 태스크에 대한 자세한 정보는 <a href="/docs/dedicated/index.html#rolesresponsibilities">{{site.data.keyword.Bluemix_dedicated_notm}} 역할 및 책임</a>을 참조하십시오.</li>
<li>데디케이티드 인스턴스에 대한 <a href="http://www.softlayer.com/data-centers" target="_blank">{{site.data.keyword.BluSoftlayer}} 데이터 센터 위치 <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 선택합니다. 그러면 데디케이티드 플랫폼 및 계정이 작성됩니다. 계정에 대해, 데디케이티드 인스턴스를 시작하고 실행하기 위해 필요한 역할을 담당할 조직의 직원을 식별하십시오. 사용자가 지정하는 역할에 대한 자세한 정보는 <a href="/docs/dedicated/index.html#rolesresponsibilities">{{site.data.keyword.Bluemix_dedicated_notm}} 역할 및 책임</a>을 참조하십시오.
</li>
<li>기업 네트워크 및 {{site.data.keyword.Bluemix_dedicated_notm}} 인스턴스 간의 네트워크 연결을 정의하고 설정하십시오.	방화벽 및 침입 방지 기능이 포함된 필수 네트워크 보안 어플라이언스가 있으며 이 옵션과 연관된 비용이 있습니다.
	<ol type="a">
	<li>IBM은 데디케이티드 인스턴스에 대한 모니터링 및 보안 인프라를 설치합니다.</li>
	<li>IBM은 선택된 단일 테넌트 데디케이티드 서비스를 설치합니다.</li>
	<li>IP 주소 또는 방화벽과 같은 항목에 대해 네트워크 구성 및 엔드포인트를 제공하고 {{site.data.keyword.Bluemix_notm}}로의 통합을 위한 LDAP에 액세스하십시오.</li>
	</ol>
</li>
<li>환경에서 관리 팀의 역할을 식별하고 지정하십시오.
	<ol type="a">
	<li>IBM은 제공된 내용을 기반으로 네트워크 액세스 및 LDAP을 구성합니다. 관리 액세스 권한이 지정된 담당자에게 부여됩니다. 지원 및 청구에 대한 담당자도 지정해야 합니다.</li>
	<li>IBM은 데디케이티드 서비스를 표시하기 위해 데디케이티드 환경에 신디케이트된(각 클라우드 형태 간 동일하게 연동된) 카탈로그를 설정합니다. 신디케이트된(각 클라우드 형태 간 동일하게 연동된) 카탈로그에는 {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 사용 가능하며 여기에서 신디케이트된 추가 서비스도 포함됩니다. 데이터에 대한 개인정보 보호정책 및 보안 기준에 따라 사용자 비즈니스의 요구사항을 충족해야 하는 공용 서비스를 결정하는 옵션이 있습니다.</li>
	<li>네트워크 및 방화벽 구성과 LDAP 엔드포인트 및 액세스를 유효성 검증하십시오.</li>
	</ol>
</li>
</ol>

사용자 환경에 처음 배치하고 구성하기 위해서는 다음 목록과 비슷하게 프로세스가 진행되어야 합니다. 각 태스크를 책임지는 담당자에 대한 자세한 정보는 [역할 및 책임](index.html#rolesresponsibilities)을 참조하십시오.

<ol>
<li>데디케이티드 인스턴스를 호스팅하는 데 사용할 데이터 센터를 선택합니다. 데이터 센터 옵션에 대한 정보는 <a href="http://www.softlayer.com/data-centers" target="_blank">{{site.data.keyword.BluSoftlayer}} 데이터 센터 위치 <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오. </li>
<li>배치에 필요한 도메인 이름 및 사용할 ID를 지정합니다. {{site.data.keyword.Bluemix_notm}} 인스턴스를 설정하면 3개 도메인을 사용하게 됩니다. <code>*mycompany*.*region*.bluemix.net</code> 및 <code>*mycompany*.*region*.mybluemix.net</code>에 대한 접두부를 선택합니다. 그런 다음, 세 번째 도메인의 전체 이름을 선택합니다.<br />
<p>사용자 정의 도메인은 필요한 만큼 선택할 수 있습니다. 그러나, 사용자 정의 도메인의 인증은 사용자 자신이 책임져야 합니다. 사용자 정의 도메인 작성에 대한 자세한 정보는 <a href="/docs/manageapps/updapps.html#domain">사용자 정의 도메인 작성 및 사용</a>을 참조하십시오.</p></li>
<li>{{site.data.keyword.Bluemix_notm}} 퍼블릭에서 사용자 회사를 나타내는 데 사용되는 공용 계정의 소유자를 식별합니다. 이 계정은 신디케이트된 서비스의 사용량을 추적하는 데 사용됩니다.</li>
<li>데이터 센터에 대한 보안 연결의 유형을 선택합니다. {{site.data.keyword.Bluemix_notm}} VPN, {{site.data.keyword.Bluemix_notm}} Direct Link 및 AT&T Net Bond에서 선택할 수 있습니다.</li>
<li>공용 인터넷에서 데디케이티드 환경에 제한 없이 액세스할 수 있는지 결정합니다.</li>
<li>사용할 인증의 유형을 선택합니다. IBM ID 또는 Active Directory 중에서 선택할 수 있습니다. IBM ID의 사용과 등록에 대한 정보는 <a href="https://www.ibm.com/account/profile/us?page=regfaqhelp#4">Help and FAQ</a> 페이지를 참조하십시오.
</li>
<li>환경에서 관리 팀의 역할을 식별하고 지정합니다. 사용자가 지정해야 하는 역할에 대한 자세한 정보는 <a href="/docs/dedicated/index.html#rolesresponsibilities">{{site.data.keyword.Bluemix_dedicated_notm}} 역할 및 책임</a>을 참조하십시오. </li>
<li>IBM이 탄력적 런타임, 콘솔, 관리 기능 및 모니터링을 포함하는 코어 플랫폼을 배치합니다.</li>
<li>IBM이 환경에 대한 사용자의 관리 액세스 권한을 구성합니다.</li>
<li>경보에 대응하기 위해 IBM 운영 팀에서 모니터링하는 데디케이티드 인스턴스의 사용을 시작할 수 있습니다.</li>
</ol>

{{site.data.keyword.Bluemix_notm}} 인스턴스를 설정하고 나면 관리 페이지를 사용하여 {{site.data.keyword.Bluemix_notm}} 인스턴스를 모니터링하고 관리할 수 있습니다. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 로컬 및 데디케이티드 관리](../admin/index.html#mng)를 참조하십시오. 업그레이드 및 유지보수에 대한 자세한 정보는 [데디케이티드 인스턴스 유지보수](index.html#maintaindedicated)를 참조하십시오.

##역할 및 책임
{: #rolesresponsibilities}

{{site.data.keyword.Bluemix_dedicated_notm}} 계정을 설정하는 경우, 인스턴스를 시작하고 실행하기 위해 필요한 역할을 담당할 조직의 직원을 식별하십시오.

###역할

다음 목록은 사용자가 지정하는 고객 역할 및 책임을 보여줍니다.

<dl>
<dt>**조달 담당자**</dt>
<dd>프로젝트의 특정 측면에 관해 작업하는 조직의 적합한 직원 식별을 포함하여, {{site.data.keyword.Bluemix_dedicated_notm}} 환경의 설정에 관해 IBM 담당자와 함께 작업합니다. 이 역할에 지정된 사용자는 프로젝트 관리 역할을 맡아 패턴 선택, 상업적 배열 및 고객 리소스에 대한 액세스 배열을 감독합니다. 이 조달 담당자는 데디케이티드 인스턴스를 설정하고 배치 프로세스를 추적하기 위한 전체 담당자입니다.</dd>
<dt>**규제 준수 담당자**</dt>
<dd>IBM 담당자와 함께 작업하여 보안 요구사항을 충족하는 토폴로지 및 배치 옵션을 선택합니다. 이 역할에 지정된 사용자는 규제 준수를 달성하는 배치 패턴을 결정하기 위해 IBM 규제 준수 컨설턴트와 함께 작업합니다.</dd>
<dt>**네트워크 전문가**</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 배치의 네트워크 플랜에 관해 IBM 담당자와 함께 작업합니다. 이 역할에 지정된 사용자는 IBM에서 요구하는 필수 네트워킹 스펙을 검토하고 IBM과 함께 구현 플랜에 대한 작업을 수행합니다. 설치 및 검증 단계의 끝에서 이 역할에 지정된 사용자는 네트워크 구성이 기업 표준 규제를 준수함을 승인합니다.</dd>
<dt>**DevOps 담당자**</dt>
<dd>IBM 담당자와 함께 작업하여 {{site.data.keyword.Bluemix_notm}} 플랫폼, 서비스 및 런타임에 필요한 유지보수 업데이트를 계획하고 적용합니다. 이 역할에 지정된 사용자는 {{site.data.keyword.Bluemix_dedicated_notm}} 인스턴스의 구성과 관련해서도 IBM 담당자와 함께 작업합니다. </dd>
<dt>운영 담당자</dt>
<dd>환경이 시작되고 실행되면 필요에 따라 IBM 지원 팀과 함께 작업합니다. 관리 콘솔에 대해 수퍼유저 액세스 권한이 있는 사용자로, Bluemix 환경에 대한 유지보수 업데이트를 승인하고 스케줄링할 수 있으며 중요한 인시던트가 발생하는 경우에 항상 지원 가능한 인원입니다. 이 역할에 지정된 사용자는 Bluemix 환경에 대한 기술적 지식이 있어야 하며 예를 들어, 네트워킹 또는 보안을 포함하여 영향을 받는 영역에서 전문적인 스킬을 갖춘 회사 내 다른 직원들에게 연락할 수 있는 위치에 있어야 합니다. </dd>
</dl>

고객 담당자는 IBM 전문가와 공동 작업을 통해 사용자가 항상 필요한 지원을 받을 수 있도록 보장합니다. 프리미엄 지원 계층으로 업그레이드하여 계정 전용 CSM(Client Success Manager)과 함께 작업할 수 있습니다. 여러 지원 계층에 대한 자세한 정보는 [지원 문의](../support/index.html#contacting-support)를 참조하십시오. CSM은 다음 유형의 태스크를 완료합니다.

<ul>
<li>{{site.data.keyword.Bluemix_dedicated_notm}} 환경을 신속하게 채택할 수 있게 합니다. </li>
<li>자급을 개선하기 위한 교육 및 인에이블먼트 자료를 제공합니다.</li>
<li>사용자와 사용자가 이용하는 {{site.data.keyword.Bluemix_notm}} 개발, 지원 및 서비스 사이에서 장기적인 관계를 수립합니다.</li>
</ul>

{{site.data.keyword.Bluemix_notm}} 인스턴스와 관련하여 사용자와 협력하는 {{site.data.keyword.Bluemix_notm}} 지원 및 운영 팀은 다음과 같은 이유로만 사용자의 로컬 환경에 액세스합니다.

<ul>
<li>경보에 대한 응답 및 운영 유지보수 수행</li>
<li>지원 티켓에 보고된 문제점 재연</li>
</ul>

### 책임

환경 설정에서부터 지속적 유지보수에 이르기까지 다양한 태스크를 완료해야 합니다. 다음 표에서는 도입/인식(Inception), 진행 및 완료 단계에서 태스크 완료를 위한 소유자와 필수 태스크를 보여줍니다.

도입/인식(Inception) 단계(Phase)는 {{site.data.keyword.Bluemix_dedicated_notm}} 환경을 설정하는 데 사용됩니다. 이 단계의 1차 목표에는 다음이 포함됩니다.

- 재무 계약을 검토하고 전달을 위한 마일스톤 날짜를 설정합니다.
- {{site.data.keyword.Bluemix_notm}} 플랫폼을 작성하고 런타임 및 서비스에 대한 액세스를 제공합니다.
- 기업 네트워크 및 {{site.data.keyword.Bluemix_notm}} 오퍼레이션 간의 네트워크 연결을 정의하고 설정합니다.
- 관리 팀에 대한 역할을 식별하고 지정합니다.

| **태스크** | **태스크 세부사항** | **책임자** |
|----------|------------------|-----------------------|
|규제 준수 표준 설정 | 환경에 필요한 정부, 산업 및 개인 기업 표준을 식별합니다. | 고객 |
|보안 및 규제 준수 통합 플랜 작성 | 보안 규제 준수를 달성하는 데 필요한 비용, 스케줄 및 리소스를 포함하는 보안 및 통합 플랜을 작성합니다. | IBM |
|규제 준수 플랜 승인 | 규제 준수 플랜을 승인합니다. | 고객 |
|환경에 대한 크기 작성 |  	플랫폼에서 작성된 앱을 지원하는 데 필요한 초기 DEA 및 서비스 프로비저닝뿐 아니라 고가용성 및 재해 복구 목표를 고려하여 사전 정의된 선택사항을 토대로 환경의 크기를 작성합니다. 사용자와 IBM이 공동으로 필요한 데이터베이스, 신디케이트된 고객 카탈로그에 제공되는 서비스 등을 정의합니다. | IBM 및 고객 책임 공유 |
|아키텍처 선택 | 고가용성 및 재해 복구 요구사항을 고려하여 사전 정의된 선택사항을 토대로 아키텍처를 선택합니다. | IBM |
|재해 복구 목표 정의 | 환경에 대한 재해 복구 요구사항을 정의합니다. | 고객 |
|재해 복구 플랜 작성 | 재해 복구 플랜을 상의하여 정의합니다. IBM은 재해 복구 모델을 작성하고 사용자의 피드백 제공 및 플랜 승인 지점에서 사용자와 상의합니다. | IBM 및 고객 책임 공유 |
|백업 및 복구 플랜 작성 | 온오프 사이트 백업 분배를 위한 요구사항과 빈도를 정의하는 백업 및 복구 플랜을 작성합니다. IBM은 패브릭 컴포넌트, IBM 서비스, 사용자 역할을 포함하는 서비스 메타데이터 등을 백업합니다. 사용자는 사용자에게 책임이 있는 애플리케이션 고유 데이터를 백업합니다. | IBM 및 고객 책임 공유 |
|이벤트 발견 및 문제점 판별을 위한 식별 도구 | {{site.data.keyword.Bluemix_notm}} 플랫폼 레벨에서 이벤트 발견 및 문제점 판별에 사용되는 IBM 및 써드파티 도구를 식별합니다. | IBM |
|확대 플랜 정의 | 모니터링 컴포넌트를 통해 발견된 이벤트를 선별하고 해결하는 단계적 확대 플랜을 정의합니다. | IBM |
|인프라, 플랫폼 및 지원 계약에 서명 | 환경에 대한 재무 조건을 포함하여 구독 계약에 서명합니다. 지원 구독에 서명합니다. | 고객 |
|환경 조달 | {{site.data.keyword.Bluemix_notm}}을 호스팅하는 코어 및 서비스 VLAN과, Data Power 및 {{site.data.keyword.Bluemix_notm}} Firewall을 호스팅하는 베어 메탈 서비스 등 컴퓨팅 리소스, 네트워크 및 스토리지를 조달합니다. VPN 터널을 허용하는 인프라를 제공합니다. | IBM |
|패브릭, 애플리케이션, 모니터링 및 관리 컴포넌트 설치 | 패브릭 컴포넌트(예: BOSH Director, 클라우드 제어기, 상태 관리자, 메시징, 라우터, DEA 및 서비스 제공자)와, 단계적 확대 및 문제점 발견 플랜에 정의된 모니터링 컴포넌트를 설치하고 구성하며 확인합니다. | IBM |
|보안 컴포넌트 설치 및 구성 | 모니터링 및 단계적 확대 플랜에 연결된 보안 컴포넌트(예: IBM QRadar, 신임 정보 저장소, 침입 방지 시스템, IBM BigFix, IBM Security Privileged Identity Management)를 설치하고 구성합니다. | IBM |
|사용자 정의 컴포넌트 설치 및 구성 |  	{{site.data.keyword.Bluemix_notm}} 제품 및 서비스 범위의 외부에 상주하는 사용자 정의 컴포넌트를 설치하고 구성합니다. | 고객 |
|초기 네트워크 구성 설정 | 방화벽, DataPower, Fortigate 및 DNS 등 초기 네트워크 구성을 설정합니다. | IBM |
|{{site.data.keyword.Bluemix_notm}} 파이프라인 연결 | {{site.data.keyword.Bluemix_notm}} 지속적 통합 및 지속적 딜리버리 파이프라인을 IBM 저장소에 연결합니다. | IBM |
|외부 솔루션 컴포넌트 사용자 정의 | 재해 복구 시나리오에 대비해 로드 밸런서를 사용자 정의합니다. | 고객 |
|VPN 솔루션 설치 | 양방향 VPN 솔루션을 설치합니다. | IBM |
|로그인 서버 구성 | 기업 LDAP에 사용할 로그인 서버를 구성합니다. | IBM |
|보안, 규제 준수 및 감사 제어를 위한 상태 추적  | 모든 도구와 프로세스가 식별된 규제 준수 수준에 도달하는 시점까지 상태를 추적합니다. | 고객 |
|실제 인프라 검토 | 위협에 대비한 솔루션 컴포넌트를 호스팅하는 실제 구내와 데이터 센터를 보호하기 위한 보안 제어를 검토합니다. | 고객 |
|모니터링 소프트웨어 검사 | 단계적 확대 및 문제점 판별 플랜에 정의된 대로 모니터링 및 관리 컴포넌트를 검사합니다. | 고객 |
|OS 검사 | 운영 체제 이미지가 규제 준수 표준에 부합하는지 검사합니다. IBM이 OS 이미지에 대한 액세스 권한을 제공합니다. | IBM 및 고객 책임 공유 |
{: caption="표 5. 도입/인식(Inception) 단계(Phase) 태스크" caption-side="top"}


다음은 진행 단계입니다. 진행 단계에서 사용자와 IBM 클라우드 사이의 지속적 협력 관계를 기술합니다. 이 단계의 1차 목표에는 다음이 포함됩니다.

- 용량을 검토하여 필요한 조정을 합니다.
- 유지보수 및 플랫폼 개선 방안을 검토합니다.
- 문제점 해결 및 근본 원인 분석을 위한 활동을 조정합니다.

| **태스크** | **태스크 세부사항** | **책임자** |
|----------|------------------|-----------------------|
|주간 용량 보고서 검토 | 주간 용량 보고서를 검토하고 필요 시 정정 조치를 수행합니다. | 고객 |
|월별 예측 작성 | 정보를 수집하여 용량 및 사용량에 대한 월별 예측을 작성합니다. | IBM 및 고객 책임 공유 |
|용량 예측 검토 | 용량 예측은 예상되는 앱의 새 배치뿐 아니라 용량에 영향을 줄 수 있는 외부 이벤트와 관련되므로 이를 검토합니다. IBM과 함께 예측 및 플랜을 검토합니다. | IBM 및 고객 책임 공유 |
|예측 검토 | 용량에 영향을 줄 수 있는 외부 이벤트와 관련되므로 용량 예측을 검토합니다. | 고객 |
|용량 조정 |  변경이 필요할 때 용량을 추가하거나 제거합니다. | IBM |
|다음 업데이트 및 유지보수 공개 | IBM 컴포넌트의 필수 유지보수를 위한 문서를 작성합니다. | IBM |
|유지보수 수행 | IBM과 공동 작업하여 21일 기간 내에서 필수 유지보수를 스케줄합니다. 사용자는 21일 기간에서 작업이 없는 날짜를 제공할 수 있으며 IBM은 이에 따라 유지보수를 스케줄하도록 작업합니다. | IBM 및 고객 책임 공유 |
|프로비저닝 장애 해결 | 카탈로그에 배치된 고객 작성 서비스의 프로비지닝 장애(발생하는 경우)를 수정합니다. | IBM |
|네트워크 및 IP 스캔 수행 | 네트워크 및 IP 스캔을 일별 및 월별로 수행합니다. | IBM 및 고객 책임 공유 |
|감사 로그에 대한 액세스 권한 제공 | 모든 보안 및 관리 감사 로그에 대한 액세스 권한을 제공합니다.   | IBM 및 고객 책임 공유 |
|테스트 수행 | 운영 테스트 및 써드파티 침투 테스트에 대해 정기적 키 제어를 수행합니다. | IBM 및 고객 책임 공유 |
|상태 보고, 감사 조정 및 규제 준수 미팅  | 규제 준수 검토 상태 미팅에서 상태 보고, 외부 감사 조정 및 표시를 완료합니다. | IBM |
|채용 및 비즈니스 수요 검증 | 고객 환경에 액세스하는 IBM 담당자를 위해 분기별 채용 검증 및 지속적 비즈니스 수요에 대한 검증을 완료합니다. | IBM |
|보안 취약점 해결 | 플랫폼에서 보고된 보안 취약점을 해결합니다. | IBM |
{: caption="표 6. 진행 단계(Phase) 태스크" caption-side="top"}

최종 완료 단계는 사용자와 IBM {{site.data.keyword.Bluemix_notm}} 사이의 관계 종료를 나타냅니다. 이 단계의 1차 태스크에는 다음이 포함됩니다.

* 재무 계약 종료
* 모든 네트워크 연결 제거
* 인프라 재사용


| **태스크** | **태스크 세부사항** | **책임자** |
|----------|------------------|-----------------------|
|재무 계약 종료 | 재무 계약의 종료를 논의하고 합의합니다. | IBM 및 고객 책임 공유 |
|환경에 대한 커미션 해지 | 환경에 대한 액세스 권한과 신임 정보를 종료합니다. | IBM 및 고객 책임 공유 |
|고객 네트워크 연결 제거 | IBM과 고객 환경 사이의 네트워크 연결을 제거합니다. | IBM 및 고객 책임 공유 |
|인프라 재사용 | {{site.data.keyword.BluSoftlayer}}에서 정의한 프로세스에 기반하여 사용자 환경은 재사용됩니다. | IBM |
{: caption="표 7. 완료 단계(Phase) 태스크" caption-side="top"}

##데디케이티드 인스턴스 유지보수
{: #maintaindedicated}

IBM은 {{site.data.keyword.Bluemix_notm}} 런타임 및 서비스에 대해 적합하다고 판단하면 업데이트 및 수정사항을 유지보수하고 설치합니다. 유지보수 기간 중에는 서비스를 사용하지 못할 수 있습니다.또한 IBM은 {{site.data.keyword.Bluemix_notm}} 플랫폼에 대한 유지보수 업데이트를 스케줄하도록 사용자와 함께 작업합니다.

다음 유형의 유지보수가 {{site.data.keyword.Bluemix_dedicated_notm}}에 필요합니다.
<dl>
<dt>**서비스의 표준 유지보수**</dt>
<dd>해당 서비스는 사전 정의된 표준 유지보수 기간을 이용하며 서비스가 사용 불가능할 수 있습니다. IBM은 서비스 유지보수를 수행하는 데 고객 승인이 필요하지 않지만 서비스에 미치는 영향을 최소화하도록 시도합니다.<br />
<br />
IBM은 각 유지보수 기간에 대해 계획된 변경사항에 대한 브로드캐스트 메시지를 상태 페이지에 보냅니다.<br />
<br />
**중요**: 유지보수 기간 중에는 일부 서비스를 사용하지 못할 수도 있습니다.</dd>

<dt>**{{site.data.keyword.Bluemix_notm}} 플랫폼의 표준 유지보수**</dt>
<dd>유지보수 업데이트는 21일 기간 내에서 사용자와 IBM 간의 조정을 기반으로 적용됩니다. 사용자는 IBM에 사전 승인된 유지보수 기간 및 작업이 없는 특정 날짜 또는 시간을 제공하고 IBM은 사용자가 선택한 날짜 동안이나 날짜에 맞춰 업데이트를 스케줄하도록 작업합니다.
<p>
<p>**관리 > 시스템 정보**로 이동하여 스케줄 및 보류 중인 유지보수 업데이트를 확인하십시오. 사전 승인된 기간 설정, 사용 불가능한 날짜, 유지보수 업데이트 보기 또는 승인에 대한 자세한 정보는 <a href="/docs/admin/index.html#oc_schedulemaintenance">유지보수 업데이트</a>를 참조하십시오.</p></dd>
</dl>

**중요**: IBM은 필요에 따라 비상 유지보수를 적용할 수 있도록 서비스를 인터럽트할 수 있는 권한을 보유합니다. IBM은 스케줄된 유지보수 시간을 변경할 수 있지만 그러한 변경은 물론 비상 유지보수 정보에 대해서도 사용자에게 알려드릴 것입니다.

유지보수 업데이트 이후 문제가 보고되는 경우에는 IBM이 업데이트를 롤백하도록 허용하는 것이 최선인지 여부를 {{site.data.keyword.Bluemix_notm}} 지원 센터와 협의합니다. 협의가 이루어지면 IBM은 업데이트를 롤백하여 환경을 이전 단계로 복원합니다.

## {{site.data.keyword.Bluemix_dedicated_notm}}에 대한 인시던트 대응 및 지원
{: #incidentresponse}

### 고객이 발견한 문제

IBM 지원 센터 및 운영 센터의 주의가 필요한 문제를 식별하는 경우 몇 가지 다양한 방법을 사용하여 지원 센터에 문의할 수 있습니다. 지원 센터에 문의하는 방법에 대한 정보는 [지원 센터에 문의](../support/index.html#contacting-bluemix-support-local)를 참조하십시오. 문제에 따라 사용자 본인이나 IBM이 또는 사용자와 IBM이 협력하여 문제를 수정합니다.

### IBM이 발견한 중요 인시던트

중요 인시던트는 환경 또는 사용자에게 영향을 미치는 긴급하고 예상치 못한 서비스 가동 중단 및 안정성 문제입니다. IBM이 사용자의 환경 내에서 중요 인시던트를 발견하는 경우 **상태** 페이지의 알림을 통해 사용자에게 알립니다. 상태 페이지에서 플랫폼이나 사용하는 서비스에 대한 알려진 문제가 있는지 확인할 수도 있습니다. 상태 페이지에 대한 자세한 정보는 [상태 보기](../admin/index.html#oc_status)를 참조하십시오.

웹 훅을 지원하는 웹 서비스와 알림을 통합하려면 [알림 및 이벤트 구독](../admin/index.html#oc_eventsubscription)에서 알림 기능 확장 방법에 대한 정보를 참조하십시오.

![인시던트 대응 프로세스](../local/images/incidentresponseprocess.png "인시던트 대응 프로세스")

그림 2. 인시던트 응답 프로세스

문제에 따라 사용자 본인이나 IBM이 또는 사용자와 IBM이 협력하여 문제를 수정합니다. 인시던트에 관한 질문이 있거나 문제를 해결하는 데 IBM 담당자의 도움이 필요한 경우 지원 티켓을 열 수 있습니다. 지원 센터에 문의하는 방법에 대한 정보는 [지원 센터에 문의](/docs/support/index.html#contacting-bluemix-support-local)를 참조하십시오. 

**참고**: 심각도 1 지원 티켓은 연중 무휴로 모니터링됩니다. 기타 티켓은 일요일 GMT 오후 10:00부터 토요일 GMT 오전 12:00까지 처리됩니다. 지원 티켓의 심각도와 지원 관련 작업에 대한 자세한 정보는 <a href="/docs/support/index.html#contacting-bluemix-support-local">지원 센터에 문의</a>를 참조하십시오.


## {{site.data.keyword.Bluemix_dedicated_notm}}의 재해 복구
{: #dr}

{{site.data.keyword.Bluemix_short}} 데디케이티드의 재해 복구는 {{site.data.keyword.Bluemix_short}} 퍼블릭을 사용할 때 작동하는 방식과 유사하게 설정할 수 있습니다. {{site.data.keyword.Bluemix_short}} 퍼블릭은 다중 고장 안전 조치로 지속적으로 혁신 가능한 플랫폼을 제공하여 사용자 조직, 영역 및 앱이 항상 사용 가능하도록 합니다. 지리적으로 여러 위치에 앱을 배치하면 불시의 동시 다발성 하드웨어 또는 소프트웨어 컴포넌트 유실, 전체 데이터 센터의 유실로부터 보호되어 지속적으로 가용성이 보장되므로, 지리적으로 한 위치에서 자연 재해가 발생하여도 대체 위치의 Distributed {{site.data.keyword.Bluemix_notm}} 퍼블릭 앱 인스턴스는 사용 가능합니다.
{: shortdesc}

{{site.data.keyword.Bluemix_short}} 데디케이티드의 재해 복구는 사용자 앱의 지속적 가용성, 플랫폼의 내재적 고가용성, 장애 시 인스턴스 복구 능력 등을 통해 가능해집니다. 여러 지역에 앱을 배치하여 앱의 지속적 가용성을 보장하는 것은 사용자의 책임입니다. 고가용성은 Cloud Foundry 및 기타 컴포넌트에 포함된 기술을 통해 플랫폼 레벨에서 빌드됩니다. 또한 IBM과 협력하여 언제든 인스턴스 복원이 필요한 시점에 데이터를 적절히 백업할 수도 있습니다.

### {{site.data.keyword.Bluemix_dedicated_notm}}에 대한 지속적인 가용성 사용
{: #enabling}

기본적으로 {{site.data.keyword.Bluemix_notm}} 퍼블릭은 지리적으로 여러 위치에 배치됩니다. 그러나 글로벌하게 분산된 {{site.data.keyword.Bluemix_dedicated_notm}} 인스턴스를 사용하려면 다음을 수행해야 합니다.

* 개발자는 수동 또는 자동화된 프로세스를 통해 하나 이상의 지역에 앱을 배치해야 합니다. 자연 재해가 두 위치에 모두 영향을 줄 수 없도록 각 지역은 200km 이상 떨어져 있어야 합니다.
* 둘 이상의 서로 다른 지역에 있는 앱을 가리키도록 글로벌 로드 밸런서(예: Akamai 또는 Dyn)를 구성하십시오.

**참고**: 모든 {{site.data.keyword.Bluemix_notm}} 서비스가 지역 분산 배포를 지원하는 것은 아닙니다. 애플리케이션을 생성할 때 지역 분산을 원하는 경우 해당 애플리케이션에서 사용하는 서비스가 데이터 동기화를 핵심 기능으로 가지고 있는지도 확인해야 합니다.

#### 여러 지리적 위치에 {{site.data.keyword.Bluemix_dedicated_notm}} 앱 배치
{: #deploying}

두 번째 또는 더 많은 위치에 배치하려면 1차 지리적 위치에서 했던 것과 유사한 프로세스를 따라야 합니다.

1. 새 데디케이티드 환경이 애플리케이션의 추가 인스턴스를 호스팅할 수 있게 하십시오. 새 환경을 작성하려면 IBM 영업부에 문의하여 프로세스를 시작하십시오. 데디케이티드 인스턴스 설정에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_dedicated_notm}} 설정](/docs/dedicated/index.html#setupdedicated)을 참조하십시오. 각 환경에 액세스하려면 별도로 로그인해야 합니다. 가용성을 보장하려면 호스팅되는 각 환경의 실제 위치가 1차 위치와 200km 이상 떨어져 있어야 합니다.
2. 배치된 새 앱이 호스팅되는 고유 도메인 이름을 확보하십시오.  예를 들어, 원래 도메인이 *mycompany.caeast.bluemix.net*이면 새 도메인(예: *mycompany.cawest.bluemix.net*)을 사용하여 새 로컬 환경을 작성하고 새 도메인에 배치할 수 있습니다.
3. 원본 앱을 배치할 때마다 새 위치에도 배치하십시오. 배치에 대한 자세한 정보는 [앱 업로드](/docs/starters/upload_app.html)를 참조하십시오.


#### {{site.data.keyword.Bluemix_dedicated_notm}}에 대한 글로벌 로드 밸런서 사용
{: #glb}

글로벌 로드 밸런서는 지속적 가용성을 보장하여 재해 복구에 필요할 뿐만 아니라 여러 가지 추가적 이점도 있습니다.

* 기본적으로 사용자를 가장 인접한 지역의 {{site.data.keyword.Bluemix_notm}}에 라우트합니다.
* 성능에 기반하여 라우트합니다.
* 트래픽 비율을 새 애플리케이션 버전에 맞게 선택적으로 지정합니다.
* 지역 상태 점검을 토대로 사이트 장애 복구를 제공합니다.
* 애플리케이션 상태 점검을 토대로 사이트 장애 복구를 제공합니다.
* 엔드포인트 사이에서 가중 라우팅을 사용합니다.

Akamai 또는 Dyn과 같은 글로벌 로드 밸런서를 선택할 수 있습니다. Akamai를 글로벌 로드 밸런서로 사용하기 위한 자세한 정보는 [Global traffic management ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp "새 탭에서 열림"){: new_window}를 참조하십시오. Dyn을 글로벌 로드 밸런서로 사용하기 위한 자세한 정보는 [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}를 참조하십시오. 

### 고가용성
{: #ha}

지속적 가용성을 사용함을 물론, {{site.data.keyword.Bluemix_notm}}에서는 Cloud Foundry 및 기타 컴포넌트에 빌드된 기술을 사용하여 플랫폼에서 고가용성도 제공합니다.

이 기술에는 다음이 포함됩니다.

<dl>
<dt>Cloud Foundry의 DEA 확장성</dt>
<dd>Cloud Foundry <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">DEA(Droplet Execution Agent) <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 내부에서 실행되는 앱에 대한 상태 점검을 수행합니다. 앱이나 DEA 자체에 문제가 있는 경우 문제 해결을 위해 앱의 추가 인스턴스를 대체 DEA에 배치합니다. 자세한 정보는 <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configuring CF for High Availability with Redundancy <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.
<p>애플리케이션의 고가용성을 보장하려면 로드 밸런싱을 위한 충분한 컴퓨팅 리소스가 필요합니다. 또한 가능한 장애를 지원하기 위한 추가 컴퓨팅 리소스가 필요할 수도 있습니다. 장애에 준비하거나 앱 인스턴스에 대한 로드의 스파이크를 처리하기 위해 DEA 풀을 증가하여 사용자 환경을 스케일링해야 하는 경우에는 IBM 담당자와 공동 작업하여 추가 DEA를 주문하고 추가된 리소스를 지원하기 위한 적합한 하드웨어가 있는지 확인할 수 있습니다.
</p>
</dd>
<dt>{{site.data.keyword.BluSoftlayer}} 중복성</dt>
<dd>데디케이티드 환경에 {{site.data.keyword.BluSoftlayer}}가 있을 경우, 각 클라우드 스토리지 클러스터의 데이터가 여러 차례 기록되고 스토리지 클러스터는 드라이브 장애 시 자동 치료 기능을 갖도록 구성됩니다. 가상 서버에 문제가 있는 경우 {{site.data.keyword.BluSoftlayer}}는 다른 호스트에서 가상 서버를 다시 시작하려고 시도합니다.</dd>
<dt>메타데이터 백업</dt>
<dd>메타데이터는 {{site.data.keyword.BluSoftlayer}} EVault 백업을 사용하여 200km 이상 떨어진 위치에 백업됩니다.</dd>
</dl>

##데디케이티드 인스턴스 복원
{: #restorededicated}

{{site.data.keyword.Bluemix_dedicated_notm}} 설정, 메타데이터 및 구성은 환경에서 예상치 못한 가동 중단에 대처하기 위해 주기적으로 백업됩니다. 사용자에게 백업 책임이 있는 데이터에는 애플리케이션 데이터, 클라우드 데이터베이스 서비스 데이터 및 오브젝트 저장소가 있습니다.

시스템 메타데이터 및 구성을 포함하는 데이터 백업의 일부로서 IBM은 다음 태스크를 완료합니다.

<ul>
<li>모든 백업 사본의 암호화 및 암호화 키 관리</li>
<li>백업 활동의 모니터 및 관리</li>
<li>암호화된 백업 파일 제공</li>
<li>요청된 데이터의 복원</li>
<li>백업 및 수정사항 관리 운영 간의 스케줄링 충돌 관리</li>
</ul>

개인 데이터 보호가 중요하므로 파일이 데이터 센터 외부로 노출되지 않도록 백업 파일 관리를 처리할 때 여러분의 협력이 필요합니다. 특히, 다음 태스크를 완료해 주시기 바랍니다.

<ul>
<li>관리하는 다른 백업 데이터에 하듯이 암호화된 백업 데이터 사본을 오프사이트로 이동합니다.</li>
<li>복원이 필요한 경우 백업 파일을 IBM 운영자에게 제공합니다.</li>
</ul>

# rellinks
{: rellinks}
## general
{: general}
* [검색: {{site.data.keyword.Bluemix_dedicated_notm}}](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
* [{{site.data.keyword.Bluemix_notm}}의 새로운 기능](/docs/whatsnew/index.html)
* [{{site.data.keyword.Bluemix_notm}} 용어집](/docs/overview/glossary/index.html)
* [{{site.data.keyword.Bluemix_notm}} 로컬 및 {{site.data.keyword.Bluemix_dedicated_notm}} 관리](/docs/admin/index.html#mng)
* [지원 문의](/docs/support/index.html#getting-customer-support)
