---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 데디케이티드 및 로컬의 CF 앱에 대한 로깅
{: #hybrid_apps_logs_ov}

{{site.data.keyword.Bluemix_dedicated_notm}} 및 {{site.data.keyword.Bluemix_local_notm}}에서 Cloud Foundry 앱은 기본 제공 로깅과 함께 제공됩니다. {{site.data.keyword.Bluemix_notm}} 콘솔의 앱에서 수집되는 데이터를 검토할 수 있습니다.
{:shortdesc}

Cloud Foundry 앱은 Cloud Foundry 로그 작성기(loggregator)를 사용하여 앱의 외부에서 로그를 모니터링하고 전달합니다. 앱의 외부에서 에이전트를 설치할 필요가 없습니다. 

## 하드웨어 요구사항


| **요구사항** |    **1개 노드**     | **3개의 고가용성 노드** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| 메모리 | 80GB | 240GB |
| 로컬 스토리지 | 2.98TB | 8.94TB |
{: caption="표 2. {{site.data.keyword.Bluemix_local_notm}}의 로깅 하드웨어 요구사항" caption-side="top"}

## 설정

{{site.data.keyword.Bluemix_dedicated_notm}} 및 {{site.data.keyword.Bluemix_local_notm}}에서 모든 앱에 대한 로그는 기본적으로 활성입니다. 표준 로그를 읽는 방법에 대한 정보를 보려면 [Cloud Foundry에서 실행 중인 앱 로깅](../logging_cf_apps.html#logging_bluemix_cf_apps)을 참조하십시오. 또한 고급 로깅은 {{site.data.keyword.Bluemix_dedicated_notm}} 및 {{site.data.keyword.Bluemix_local_notm}} 환경에서 사용할 수 있습니다. 

* {{site.data.keyword.Bluemix_dedicated_notm}} 및 {{site.data.keyword.Bluemix_local_notm}} 환경에서 고급 로깅이 사용 가능한지 확인하려면 [로그 보기](#hybrid_apps_logs_dash)의 단계를 따르십시오. **고급 보기** 단추가 없는 경우 이 기능을 사용할 수 없습니다. 

* 사용자 환경에 고급 로깅을 추가하려면 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 또는 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 문서의 단계를 수행하십시오.

## 로그 보유

{{site.data.keyword.Bluemix_dedicated_notm}} 및 {{site.data.keyword.Bluemix_local_notm}} Cloud Foundry 앱에서 로그 데이터가 기본적으로 30일 동안 저장됩니다.

## 데디케이티드 및 로컬의 Cloud Foundry 앱에 대한 로그 보기
{: #hybrid_apps_logs_dash}

{{site.data.keyword.Bluemix_dedicated_notm}} 및 {{site.data.keyword.Bluemix_local_notm}}에서 실행 중인 앱에 대한 로그를 검토할 수 있습니다.
{:shortdesc}

앱 로그를 보려면 다음 단계를 수행하십시오.
1. 실행 중인 앱을 선택하십시오. 
2. **로그**를 클릭하십시오. **로그** 보기의 실행 중인 앱에서 로그를 볼 수 있습니다. 
4. **고급 보기** 단추를 클릭하십시오. **고급 보기**는 로그 및 시간소인이 있는 데이터를 사용하여 사용자 정의 시각화를 작성하는 시각화 도구인 Kibana를 사용하여 로그에 대한 자세한 보기를 보여줍니다. 고급 보기 사용에 대한 자세한 정보는 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 문서를 참조하십시오.

다음으로, Kibana 대시보드를 사용자 정의할 수 있습니다. 자세한 정보는 [Kibana에서 로그 분석](../logging_view_kibana3.html#analyzing_logs_Kibana3)을 참조하십시오.
