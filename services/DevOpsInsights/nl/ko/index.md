---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# DevOps Insights(베타) 시작하기
{: #gettingstarted}

{{site.data.keyword.DRA_full}}는 가장 활발하게 진행 중인 DevOps 프로젝트에 개발자, 팀 및 배치 분석을 적용합니다. 코드 베이스에서 위험성을 관리하고 Continuous Delivery 프로젝트에서 자동으로 품질 표준을 적용하기 위해 팀이 DevOps 및 개발자 관행을 준수하는 방법을 배우는 데 사용하십시오.
{:shortdesc}

{{site.data.keyword.DRA_short}}는 다음과 같은 여러 기능 그룹으로 구성됩니다.

   * Developer Insights에서는 프로젝트의 개발 성숙도를 탐색하는 포괄적인 방법을 제공합니다. 오류 발생 가능성이 높은 파일을 식별하고 프로젝트가 개발자 관행을 준수하는지 볼 수 있습니다. 

   * Team Dynamics에서는 소셜 코딩 분석을 사용하여 팀이 협업하는 방식을 배우고 작업을 향상시키는 방법을 파악할 수 있습니다.

   * Deployment Risk는 Continuous Delivery 안전망과 같습니다. 배치 프로세스의 지정된 게이트에서 단위 테스트, Funcitonal Test, 애플리케이션 스캔 및 코드 적용 범위 도구의 결과를 분석하고 위험한 변경사항을 릴리스하지 못하게 합니다.

   * Delivery Insights는 IBM UrbanCode Deploy 설치에 대한 배치 통계, 메트릭 및 기타 정보를 보여줍니다. 예를 들어 배치 기간, 성공 및 실패 차트를 보여주며 모두 논리적으로 그룹화된 환경별로 정렬합니다. [IBM UrbanCode Deploy와 DevOps Insights 통합](/docs/services/DevOpsInsights/uc_insights_overview.html)을 참조하십시오.

{{site.data.keyword.DRA_short}}는 Bluemix 개방형 도구 체인 카탈로그의 통합입니다. 도구 체인에 대한 자세한 정보는 [도구 체인 작업](/docs/services/ContinuousDelivery/toolchains_working.html)을 참조하십시오.

{{site.data.keyword.DRA_short}}를 사용하려면 도구 체인에 추가해야 합니다. 많은 도구 체인 템플리트에 이미 {{site.data.keyword.DRA_short}}가 포함되어 있습니다. {{site.data.keyword.DRA_short}}에 대한 정보를 확인하고 {{site.data.keyword.Bluemix_notm}} 대시보드에서 이를 포함하는 일부 도구 체인 템플리트에 액세스할 수 있도록 [{{site.data.keyword.Bluemix_notm}} 조직에 서비스로 추가](/docs/services/reqnsi.html)하십시오.  

## 도구 체인에 DevOps Insights 추가
{: #catalog}

{{site.data.keyword.DRA_short}}는 {{site.data.keyword.contdelivery_short}}의 일부입니다. 도구 통합 카탈로그에서 선택하여 도구 체인에 {{site.data.keyword.DRA_short}}를 추가할 수 있습니다.

{{site.data.keyword.DRA_short}}도 여러 도구 체인 템플리트의 일부입니다. {{site.data.keyword.DRA_short}}를 포함하는 템플리트에서 도구 체인을 작성하는 경우 {{site.data.keyword.DRA_short}}가 **고급**으로 설정되었는지 확인하십시오. 그런 다음 도구 체인을 작성하고 [Insights 사용](/docs/services/DevOpsInsights/index.html#using)으로 건너뛰십시오.

도구 체인에 {{site.data.keyword.DRA_short}}를 추가하려면 다음을 수행하십시오.

1. **도구에 추가**를 클릭하십시오.

2. **{{site.data.keyword.DRA_short}}**를 클릭하십시오. 

3. 모든 {{site.data.keyword.DRA_short}} 기능을 도구 체인에 추가하려면 **고급**을 선택하고 **Developer Insights 사용** 선택란을 선택합니다. Deployment Risk만 추가하려면 **기본값**을 선택하십시오. 

4. **통합 작성**을 클릭하십시오. 

{{site.data.keyword.DRA_short}}는 이제 도구 체인의 개요 페이지에서 사용할 수 있습니다.

## DevOps Insights 사용
{: #using}

도구 체인에 GitHub, GitLab 또는 JIRA가 포함되어 있으면 {{site.data.keyword.DRA_short}}에서 초기 데이터 수집 및 분석 후에 자동으로 코드 베이스와 팀에 대한 정보를 제공합니다. 도구 체인에 통합이 포함되지 않으면 통합 중 하나를 추가하고 다음 단계를 따르십시오.

1. 도구 체인의 개요 페이지에서 **{{site.data.keyword.DRA_short}}**를 클릭하십시오.

2. 왼쪽 탐색에서 **Team Dynamics** 또는 **Developer Insights**를 클릭한 다음 데이터 카테고리를 선택하십시오.

3. 데이터 카테고리에서 대시보드를 확인하여 프로젝트의 데이터를 탐색하십시오. 그래프에 대한 자세한 정보 또는 이 정보를 사용하여 수행할 수 있는 작업에 대해 알아보려면 **정보** 또는 **안내**를 클릭하십시오.

Team Dynamics 및 Developer Insights를 탐색한 다음 코드 품질을 적용할 수 있도록 [Deployment Risk를 구성](/docs/services/DevOpsInsights/insights_risk.html)하십시오. Deployment Risk는 {{site.data.keyword.contdelivery_short}} 파이프라인 및 Jenkins 둘 다와 호환 가능합니다.   

기본적으로 {{site.data.keyword.DRA_short}}에는 Developer Insights나 Team Dynamics가 포함되지 않습니다. 도구 체인을 구성한 다음 해당 기능에 도구 체인에 추가하려면 다음을 수행하십시오.

1. 도구 체인의 개요 페이지로 이동하십시오.
2. {{site.data.keyword.DRA_short}} 카드에서 **조치** 메뉴를 클릭하십시오.
3. **구성**을 클릭하십시오.
4. 유형으로는 **고급**을 선택한 다음 선택란을 선택하십시오.
5. **통합 저장**을 클릭하십시오.

구성을 저장하고 나면 Developer Insights와 Team Dynamics가 자동으로 저장소와 문제 추적 시스템을 스캔합니다.
