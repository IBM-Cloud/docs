---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-4"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Continuous Delivery 정보  
{: #cd_about}  

{{site.data.keyword.contdelivery_full}}를 통해 DevOps 사례와 업계 최고의 도구를 사용하여 애플리케이션을 빌드하고 테스트하며 전달할 수 있습니다.
{:shortdesc}

{{site.data.keyword.contdelivery_short}} 서비스에서는 다음과 같이 DevOps 워크플로우를 지원합니다.

 * 개발, 배치 및 운영 태스크를 지원하는 도구 통합을 사용할 수 있도록 통합된 DevOps 오픈 [도구 체인](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window}을 작성할 수 있습니다. 

  도구 체인은 애플리케이션 개발, 빌드, 배치, 테스트, 관리를 수행하는 데 함께 사용할 수 있는 통합 도구 세트입니다. 개발과 운영을 반복하고 간편하게 관리할 수 있는 {{site.data.keyword.Bluemix_notm}} 서비스, 오픈 소스 도구, 써드파티 도구(예: GitHub, PagerDuty, Slack)를 포함하는 도구 체인을 작성할 수 있습니다.

 * 자동화된 [파이프라인](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window}을 사용하여 지속적 딜리버리를 제공합니다. 

  빌드, 단위 테스트, 배치 등을 자동화하십시오. 사용자 개입을 최소화하여 반복할 수 있는 방식으로 빌드, 테스트, 배치를 수행하십시오. 언제든 프로덕션으로 릴리스할 수 있게 준비하십시오.

 * [웹 기반 IDE](/docs/services/ContinuousDelivery/web_ide.html){: new_window}를 사용하여 어디서든 코드를 편집하고 푸시합니다. 

  GitHub에서 소스 제어 태스크의 작성, 편집, 실행, 디버그, 완료를 수행하십시오. 코드 편집에서 프로덕션으로 배치하는 작업으로 원활하게 이동하십시오.

 * [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window}를 통해 품질을 개선하십시오.

  코드를 개발하고 전달하는 팀의 원동력을 파악하십시오. 사용자가 애플리케이션과 상호작용하는 방법을 알아보십시오. 애플리케이션 운영을 관리하는 데 유용하도록 데이터를 검토하십시오.


## Bluemix 데디케이티드 및 Bluemix 퍼블릭의 도구 체인 가용성 비교
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} 퍼블릭은 사용자가 [http://bluemix.net ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window}에 의해 액세스되는 애플리케이션을 빌드, 실행 및 관리할 수 있는 오픈 표준의 클라우드 기반 플랫폼입니다. {{site.data.keyword.Bluemix_notm}} 데디케이티드는 {{site.data.keyword.Bluemix_notm}} 퍼블릭 환경과 사용자 네트워크 모두에 안전하게 연결된 데디케이티드 SoftLayer 환경에서 {{site.data.keyword.Bluemix_notm}}의 기능을 제공합니다. 회사의 {{site.data.keyword.Bluemix_notm}} 데디케이티드 환경에 {{site.data.keyword.Bluemix_notm}} 퍼블릭 사이트와 동일한 도구 통합이 포함되지 않을 수 있습니다. 

소스 코드 관리 및 문제 추적을 위해 {{site.data.keyword.Bluemix_notm}} 퍼블릭에서는 일반적으로 github.com을 사용합니다. {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 github.com을 사용할 수도 있지만, 이는 일반적으로 사용자의 회사에서 설치하거나 IBM에서 관리하는 {{site.data.keyword.ghe_short}}를 사용합니다. 

{{site.data.keyword.contdelivery_short}}는 {{site.data.keyword.Bluemix_notm}} 퍼블릭과 {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 사용 가능합니다. 도구 체인은 사용자가 {{site.data.keyword.contdelivery_short}}를 {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 또는 {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 사용하는지 여부에 따라 다릅니다. 

|도구 체인 |{{site.data.keyword.Bluemix_notm}} 퍼블릭	|{{site.data.keyword.Bluemix_notm}} 데디케이티드 |
|:----------|:------------------------------|:------------------|
|도구 통합 		|지원되는 도구 통합의 목록은 [도구 통합 구성](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}을 참조하십시오.  		|사용 가능한 도구 통합은 {{site.data.keyword.contdelivery_short}}가 사용자 환경에서 설정된 방법에 따라 다릅니다. 			|
|템플리트에서 도구 체인 작성		|[{{site.data.keyword.Bluemix_notm}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://console.ng.bluemix.net/devops){:new_window}에 로그인		|{{site.data.keyword.Bluemix_notm}}의 데디케이티드 환경에 로그인합니다. 			|
|앱에서 도구 체인 작성		|앱 스타터 코드로 채워진 새 GitHub 저장소에서 지속적 딜리버리를 위해 앱이 구성됩니다. 		|앱 스타터 코드로 채워진 새 GitHub 또는 GitHub Enterprise 저장소에서 지속적 딜리버리를 위해 앱이 구성됩니다. 		|  
|딜리버리 파이프라인 배치 지역		|모든 {{site.data.keyword.Bluemix_notm}} 퍼블릭 지역이 Cloud Foundry 배치 작업에 사용 가능합니다.  		|{{site.data.keyword.Bluemix_notm}} 데디케이티드 지역이 사용 가능합니다. 또한 동일한 고객 계정 내의 기타 데디케이티드 또는 로컬 지역도 특정 환경에서 {{site.data.keyword.contdelivery_short}}가 설정된 방법에 따라 사용이 가능합니다. 		|
|딜리버리 파이프라인 배치 작업		|모든 [작업 유형](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs)이 사용 가능합니다. 		|데디케이티드 환경에 설치되지 않은 {{site.data.keyword.Bluemix_notm}} 서비스에 의존하는 작업 유형은 사용 가능하지 않습니다. 예를 들어, 컨테이너 빌드 및 배치 작업 유형은 {{site.data.keyword.Bluemix_notm}} Container 서비스가 없는 환경에서는 사용 가능하지 않습니다. 	|
{: caption="Table 1. Differences between toolchains on {{site.data.keyword.Bluemix_notm}} 데디케이티드 및 {{site.data.keyword.Bluemix_notm}} 퍼블릭" caption-side="top"}


## 도구 체인 템플리트
{: #templates}

[도구 체인 작성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/create){: new_window}에 대한 시작점으로 템플리트를 사용할 수 있습니다. 도구 체인 템플리트에는 개발, 배치 및 운영 태스크를 지원하는 특정 도구 통합 세트가 포함되어 있습니다. 

**팁**: 회사의 {{site.data.keyword.Bluemix_notm}} 데디케이티드 환경에 {{site.data.keyword.Bluemix_notm}} 퍼블릭 사이트와 동일한 도구 체인 템플리트가 포함되어 있지 않을 수 있습니다. {{site.data.keyword.Bluemix_notm}} 퍼블릭 및 {{site.data.keyword.Bluemix_notm}} 데디케이티드 모두에서 사용 가능한 도구 체인 템플리트에 {{site.data.keyword.Bluemix_notm}} 데디케이티드의 다른 도구 통합 세트가 포함될 수 있습니다. 

일부 도구 체인 템플리트에는 {{site.data.keyword.contdelivery_short}} 서비스의 일부인 도구 통합이 포함되어 있습니다. 해당 서비스의 인스턴스가 아직 조직에 없는 경우, **작성**을 클릭하여 도구 체인을 작성하면 서비스가 무료로 자동으로 추가됩니다. 자세한 정보 및 이용 약관은 [Bluemix 카탈로그 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}을 참조하십시오. 

마이크로서비스 도구 체인 템플리트는 Cloudant 저장소에서 지원하는 카탈로그 및 주문 API로 앱을 배치합니다. 앱 배치의 일부로서 무료 Cloudant 서비스 인스턴스가 작성됩니다. 자세한 정보 및 이용 약관은 [Bluemix 카탈로그 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}을 참조하십시오. 

|템플리트 |설명	|
|:----------|:------------------------------|
|[Garage Method 클라우드 고유 튜토리얼 도구 체인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|이 도구 체인은 Garage Method에서 제공하는 DevOps 사례를 보여줍니다. 이 도구 체인은 지속적 딜리버리, 소스 제어, 테스트 자동화, 그리고 자동화된 모니터링 및 운영을 위해 사전 구성되어 있습니다. 이는 추가로 확장이 가능한 Node.js Express 4로 작성된 샘플 앱과 함께 제공됩니다.  		|
|[{{site.data.keyword.DRA_short}}를 사용하는 마이크로서비스 도구 체인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|이 클라우드 고유 도구 체인으로 사용자는 3개의 마이크로서비스(카탈로그 API, 주문 API, 그리고 두 API를 모두 호출하는 UI)로 구성된 온라인 저장소를 작성하는 샘플을 사용할 수 있습니다. 이 도구 체인은 지속적 딜리버리, 소스 제어, 기능 테스트, 문제 추적, 온라인 편집 및 경보 알림을 위해 사전 구성되어 있습니다.  		|
|[{{site.data.keyword.DRA_short}}를 사용하는 마이크로서비스 도구 체인(v2) ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|이 클라우드 고유 도구 체인으로 사용자는 3개의 마이크로서비스(카탈로그 API, 주문 API, 그리고 두 API를 모두 호출하는 UI)로 구성된 온라인 저장소를 작성하는 샘플을 사용할 수 있습니다. 이 도구 체인은 지속적 딜리버리, 소스 제어, 기능 테스트, 문제 추적, 온라인 편집 및 경보 알림을 위해 사전 구성되어 있습니다.  		|
|[보안 컨테이너 도구 체인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|이 도구 체인으로 사용자는 보안 Docker 컨테이너 앱을 개발하고 배치할 수 있습니다. 기본적으로 도구 체인은 샘플 Node.js "Hello World" 앱을 사용하지만, 사용자가 자신의 GitHub 저장소에 대신 링크할 수 있습니다. 이 도구 체인은 Vulnerability Advisor의 지속적 딜리버리, 소스 제어, 문제 추적 및 온라인 편집을 위해 사전 구성되어 있습니다.  		|
|[단순 Cloud Foundry 도구 체인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|이 도구 체인으로 사용자는 Cloud Foundry 앱을 개발하고 배치할 수 있습니다. 기본적으로 이 도구 체인은 샘플 Node.js "Hello world" 앱을 사용하지만, 사용자가 자신의 GitHub 저장소에 대신 링크할 수 있습니다. 이 도구 체인은 지속적 딜리버리, 소스 제어, 문제 추적 및 온라인 편집을 위해 사전 구성되어 있습니다.  		|
|[단순 Cloud Foundry 도구 체인(v2) ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|이 도구 체인으로 사용자는 Cloud Foundry 앱을 개발하고 배치할 수 있습니다. 기본적으로 이 도구 체인은 샘플 Node.js "Hello world" 앱을 IBM 호스팅 Git 저장소에 복제하며, 이는 수정이 가능합니다. 이 도구 체인은 지속적 딜리버리, 소스 제어, 문제 추적 및 온라인 편집을 위해 사전 구성되어 있습니다.  		|
|[{{site.data.keyword.DRA_short}}를 사용하는 단순 Cloud Foundry 도구 체인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|이 클라우드 고유 도구 체인으로 사용자는 {{site.data.keyword.DRA_short}}를 사용하여 단순 Cloud Foundry 앱의 배치를 게이트 처리할 수 있습니다. 기본적으로 이 도구 체인은 샘플 Node.js Weather 앱을 사용합니다. 또는 사용자가 자신의 GitHub 저장소에 링크할 수 있습니다.  		|
|[단순 컨테이너 도구 체인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|이 도구 체인으로 사용자는 Docker 컨테이너 앱을 개발하고 배치할 수 있습니다. 기본적으로 도구 체인은 샘플 Node.js "Hello World" 앱을 사용하지만, 사용자가 자신의 GitHub 저장소에 대신 링크할 수 있습니다. 이 도구 체인은 지속적 딜리버리, 소스 제어, 문제 추적 및 온라인 편집을 위해 사전 구성되어 있습니다.  		|
|[IBM UrbanCode Deploy를 사용하는 Delivery Insights ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|이 도구 체인으로 사용자는 IBM UrbanCode Deploy의 배치 메트릭을 볼 수 있습니다. 이 도구 체인을 사용하면 {{site.data.keyword.DRA_short}}의 설정 페이지에서 DevOps Connect를 다운로드하고 구성하여 IBM UrbanCode Deploy와 통신할 수 있습니다.  		|
|[GitHub 및 Jenkins를 사용하는 Deployment Risk Analytics ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|이 도구 체인으로 사용자는 지속적 통합 및 딜리버리를 위한 Jenkins 프로세스에 대한 통찰을 얻을 수 있습니다. Jenkins에서 작업을 실행할 때 {{site.data.keyword.DRA_short}}에 데이터를 전송하도록 Jenkins 서버를 구성할 수 있습니다. 또한 정책에 따라 배치를 차단할 수 있도록 품질 게이트를 구현할 수도 있습니다. 사용자는 {{site.data.keyword.DRA_short}}의 배치 위험성 대시보드에서 결과를 볼 수 있습니다. Jenkins에서 사용하는 소스 저장소를 표시하도록 GitHub 저장소를 구성하는 경우에는 변경 추적성을 사용할 수 있습니다.   		|
|[GitHub 및 JIRA를 사용하는 Developer Insights 및 Team Dynamics ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|이 도구 체인으로 사용자는 프로젝트의 개발 위험성을 탐색하고 소셜 코딩 분석을 사용하여 개발자 간의 상호작용 패턴을 파악할 수 있습니다. 사용자는 GitHub 문제, JIRA 문제 또는 둘 모두와 함께 GitHub 소스 코드를 분석할 수 있습니다. Developer Insights를 사용하면 오류 발생 가능성이 높은 파일을 식별하고 프로젝트가 DevOps 사례를 준수하는 방법을 파악할 수 있습니다. Team Dynamics의 소셜 코딩 분석이 팀 구성원 간의 상호작용 레벨을 식별하므로, 팀은 비생산적인 사례를 수정할 수 있습니다.  		|
|[사용자 자체 도구 체인 빌드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|이 도구 체인에는 사전 구성된 도구가 없습니다. 도구 체인에 이미 익숙한 경우 사용자 자체 도구 체인을 설정할 수 있습니다.  		|
{: caption="Table 2. Toolchain templates" caption-side="top"}
