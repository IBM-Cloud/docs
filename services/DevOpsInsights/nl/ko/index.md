---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.DRA_short}}(시범) 시작하기
{: #gettingstarted}

{{site.data.keyword.DRA_full}}를 사용하여 빌드 및 배치 위험성을 식별하십시오.
{:shortdesc}

{{site.data.keyword.DRA_short}}는 단위 테스트, 기능 테스트, 코드 적용 범위 도구를 집계하고 분석하여 코드가 배치 프로세스에 지정된 게이트의 사전 정의된 정책을 충족하는지 파악합니다. 코드가 정책을 충분히 준수하지 못하는 경우, 위험한 변경이 릴리스되지 않도록 배치가 정지됩니다. {{site.data.keyword.DRA_short}}를 Continuous Delivery 환경의 안전망으로 사용할 수 있는데 이를 통해 시간 경과에 따라 품질 표준을 구현 및 개선하고 프로젝트 상황을 파악하는 데이터 시각화 도구로 사용할 수 있습니다. 

{{site.data.keyword.DRA_short}}는 시범 오퍼링이며 있는 그대로 개발 및 실험 용도로만 제공됩니다. {{site.data.keyword.DRA_short}}를 사용하려면 {{site.data.keyword.deliverypipeline}}을 사용하는 도구 체인에 추가하십시오. 

{: #catalog}
{{site.data.keyword.DRA_short}} UI에 액세스하려면 기존 도구 체인에서 다음 단계를 완료하십시오. 

1. **도구 추가** 단추를 클릭하십시오. 

2. **{{site.data.keyword.DRA_short}}**를 클릭하십시오. 

3. **통합 작성**을 클릭하십시오. 

4. **{{site.data.keyword.DRA_short}}** 타일을 클릭하십시오. 

5. 나머지 태스크로 설정을 완료하십시오. 

	1. [{{site.data.keyword.deliverypipeline}} 통합을 구성하십시오.](./pipeline_integration.html)
	2. 파이프라인을 실행하고 [{{site.data.keyword.deliverypipeline}} 대시보드를 검토](./pipeline_decision_reports.html)하십시오.
	3. 관리할 {{site.data.keyword.DRA_short}}의 [정책을 정의](./create_criteria.html)하십시오. 
	4. 파이프라인을 다시 실행하여 프로젝트가 정책을 패스하는지 확인하십시오. 


# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}

* [분석을 사용하여 배치 성공 가능성에 관하여 조언하기](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## 관련 링크
{: #general}

* [도구 체인 시작하기](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Delivery Pipeline 시작하기](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [IBM Bluemix 가격 책정 시트](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [IBM Bluemix 전제조건](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
