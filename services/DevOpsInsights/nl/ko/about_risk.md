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

# Deployment Risk 정보

{{site.data.keyword.DRA_short}}에서는 배치, 특히 위험성에 대한 풍부한 정보를 제공합니다. 이 정보를 사용하면 정책과 게이트를 사용하여 Delivery Pipeline에서 품질 보호를 자동화할 수 있습니다.
{:shortdesc}

도구 체인에서 {{site.data.keyword.DRA_short}}를 연 다음 **Deployment Risk**를 클릭하십시오. 여기에서 스테이징 및 프로덕션 환경에서 애플리케이션의 개요를 가져오고 코드 적용 범위, 테스트 성능 및 보안 보고서를 이해하도록 드릴다운할 수 있습니다. 이러한 대시보드는 파이프라인의 {{site.data.keyword.DRA_short}} 테스트에 있는 최신 정보로 자동으로 채워집니다. 

정책과 게이트를 통해 도구 체인에 품질 표준을 적용하는 데 Deployment Risk를 사용할 수 있습니다. 정책은 규칙 세트로 구성되며, 게이트가 정책을 적용합니다. 예를 들어, 단위 테스트와 테스트 적용 범위 표준을 만족시키는 빌드가 필요한 "단위 테스트 및 테스트 적용 범위" 정책을 작성할 수 있습니다. 그런 다음 정책을 나타내는 게이트를 Continuous Delivery 프로세스에 추가합니다. 정책을 만족하지 않는 빌드가 해당 게이트에서 중지됩니다. 

## 통합 정보

Deployment Risk는 {{site.data.keyword.contdelivery_full}}의 일부인 {{site.data.keyword.deliverypipeline}} 및 Jenkins 프로젝트와 통합됩니다. 대략적으로 이 둘을 사용하는 지시사항은 비슷합니다.   

{{site.data.keyword.deliverypipeline}}을 사용하는 경우 다음 단계를 따르십시오.

1. 관리할 {{site.data.keyword.DRA_short}}의 [정책 및 규칙을 작성](risk_policies.html)하십시오.
2. {{site.data.keyword.DRA_short}}와 통합할 [파이프라인의 단계를 준비](risk_cd.html)하십시오.
3. 파이프라인에서 {{site.data.keyword.DRA_short}}에 결과를 업로드하는 [테스트 작업을 작성하거나 편집](risk_cd.html)하십시오.
4. 해당 결과와 정책을 기반으로 승격 의사결정을 하는 파이프라인에 [게이트를 추가](risk_cd.html)하십시오.
5. 파이프라인을 실행하고 [결과 보기](results.html)를 수행하십시오.

Jenkins를 사용하는 경우 다음 단계를 따르십시오.

1. 관리할 {{site.data.keyword.DRA_short}}의 [정책 및 규칙을 작성](risk_policies.html)하십시오.
2. [Jenkins 플러그인을 설치 및 구성](risk_jenkins.html)하십시오.
3. [플러그인 지시사항에 설명된 대로 테스트 작업과 게이트를 작성](risk_jenkins.html)하십시오. 분석을 위해 테스트를 통해 결과를 {{site.data.keyword.DRA_short}}에 업로드하고, 게이트에서 해당 결과를 사용하여 승격 의사결정을 내립니다.
4. 프로젝트를 실행하고 [결과 보기](results.html)를 수행하십시오. 

코드를 빌드하고 배치하는 방법과 상관없이 결과는 동일합니다. 표준에 맞는 빌드는 Deployment Risk 게이트를 통과하고 표준을 만족하지 않는 빌드는 중지됩니다. 

## 전제조건
{: #prerequisites}

Deployment Risk에는 [{{site.data.keyword.DRA_short}} 시작하기](/docs/services/DevOpsInsights/index.html)에 설명된 내용 이상의 구성이 필요합니다.

Deployment Risk를 사용하려면 다음 두 가지가 필요합니다.

* {{site.data.keyword.deliverypipeline}} 또는 Jenkins 프로젝트의 인스턴스
* 프로젝트를 평가하는 데 사용할 테스트
