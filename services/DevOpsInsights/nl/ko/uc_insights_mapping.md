---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 보고서에 환경 맵핑
{: #uc_insights_mapping}

Delivery Insights에 표시되는 정보는 IBM UrbanCode Deploy 환경(*실제 환경*이라고도 함)의 콜렉션인 *논리 환경*별로 그룹화됩니다. 조직에 적합한 방식으로 사용자의 환경을 논리 환경으로 그룹화할 수 있습니다.
{:shortdesc}

## 논리 환경

Delivery Insights는 IBM UrbanCode Deploy 환경을 하나 이상의 논리 환경으로 그룹화합니다. 이 방식으로 조직에 적합한 그룹으로 환경을 수집할 수 있습니다. 예를 들어 여러 애플리케이션에 맞는 여러 프로덕션 환경이 있으면 이 모든 환경을 하나의 논리 환경으로 그룹화하고 이 모든 환경의 메트릭을 단일 프로덕션 환경 대시보드로 결합할 수 있습니다. IBM UrbanCode Deploy 서버에 적합한 방식으로 환경을 그룹화할 수 있도록 검색 문자열별로 맵핑을 수행합니다.

## 기본 논리 환경

기본적으로 보고서에는 문자열을 사용하여 IBM UrbanCode Deploy 환경과 일치되는 논리 환경이 포함됩니다. 예를 들어, 이름에 "dev"가 포함된 모든 환경이 DEV 논리 환경에 맵핑되고 이름에 "prod"가 포함된 모든 환경이 PROD 논리 환경에 맵핑됩니다.

![기본 논리 환경](images/uc_insights_mapping.gif)

## 환경을 논리 환경에 맵핑

수동으로 실제 환경을 논리 환경에 맵핑하거나 패턴을 사용하여 동적으로 실제 환경을 논리 환경에 연관시킬 수 있습니다.

패턴을 사용하여 실제 환경을 논리 환경에 맵핑하려면 다음 단계를 따르십시오.

1. {{site.data.keyword.DRA_short}}에서 **Delivery Insights > 맵 환경**을 클릭하십시오.
1. 기존 논리 환경을 클릭하거나 **논리 환경 추가**를 클릭하십시오.
1. 논리 환경 설정의 **패턴**에서 **패턴 추가**를 클릭하십시오.
1. 환경 이름의 패턴을 지정하십시오. 별표(*)를 와일드카드로 사용할 수 있습니다. 예를 들어, `env` 패턴은 `env1`, `env2` 및 `env` 환경과 일치합니다.
1. 논리 환경에 원하는 환경이 포함되어 있는지 확인하십시오.

수동으로 환경을 논리 환경에 맵핑하려면 **수동으로 추가**를 클릭하고 추가 또는 제거할 환경을 선택하십시오.

![DevOps Connect에서 통합 설정](images/uc_insights_mapping_manually.gif)

이제 환경을 논리 환경에 맵핑했으므로 해당 논리 환경에서 수집한 보고서 정보를 볼 수 있습니다.
