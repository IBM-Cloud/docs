---



copyright:

  years: 2016, 2017

lastupdated: "2016-10-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# 데디케이티드 및 로컬의 Cloud Foundry 앱에 대한 모니터링 및 로깅
{: #dedicated_apps_ml_ov}


{{site.data.keyword.Bluemix_dedicated_notm}} 및 {{site.data.keyword.Bluemix_local_notm}}에서 Cloud Foundry 앱은 기본 제공 로깅과 함께 제공됩니다. {{site.data.keyword.Bluemix_notm}} 콘솔의 앱에서 수집되는 데이터를 검토할 수 있습니다.
{:shortdesc}

Cloud Foundry 앱은 Cloud Foundry 로그 작성기(loggregator)를 사용하여 앱의 외부에서 로그를 모니터링하고 전달합니다. 앱의 외부에서 에이전트를 설치할 필요가 없습니다. 

## 하드웨어 요구사항


| **요구사항** |    **1개 노드**     | **3개의 고가용성 노드** |
|-----------------|-------------------|-------------------|
vCPU | 19 | 57 |
메모리 | 80GB | 240GB |
로컬 스토리지 | 2.98TB | 8.94TB |
{: caption="표 1. {{site.data.keyword.Bluemix_local_notm}}의 로깅 하드웨어 요구사항" caption-side="top"}

## 설정

{{site.data.keyword.Bluemix}} 데디케이티드 및 {{site.data.keyword.Bluemix}} 로컬에서 모든 앱에 대한 로그는 기본적으로 활성입니다. 표준 로그 읽기에 대한 정보를 보려면 Cloud Foundry에서 실행되는 앱에 대한 로깅을 참조하십시오. 또한 고급 로깅은 {{site.data.keyword.Bluemix}} 데디케이티드 및 {{site.data.keyword.Bluemix}} 로컬 환경에서 사용 가능합니다.

## 로그 보유

{{site.data.keyword.Bluemix}} 데디케이티드 및 {{site.data.keyword.Bluemix}} 로컬 Cloud Foundry 앱에서 로그 데이터는 기본적으로 30일 동안 저장됩니다.

## {{site.data.keyword.Bluemix}} 데디케이티드 및 {{site.data.keyword.Bluemix}} 로컬에서 Cloud Foundry 앱에 대한 로그 보기
{: #dedicated_apps_ml_logs_dash}

{{site.data.keyword.Bluemix_notm}} 데디케이티드 및 {{site.data.keyword.Bluemix_notm}} 로컬에서 실행 중인 앱에 대한 로그를 검토할 수 있습니다.
{:shortdesc}

앱 로그를 보려면 다음 단계를 수행하십시오.
1. 실행 중인 앱을 선택하십시오. 
2. **로그**를 클릭하십시오. **로그** 보기의 실행 중인 앱에서 로그를 볼 수 있습니다. 
4. **고급 보기** 단추를 클릭하십시오. **고급 보기**는 로그 및 시간소인이 있는 데이터를 사용하여 사용자 정의 시각화를 작성하는 시각화 도구인 Kibana를 사용하여 로그에 대한 자세한 보기를 보여줍니다. 고급 보기 사용에 대한 자세한 정보는 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 문서를 참조하십시오.

다음으로, Kibana 대시보드를 사용자 정의할 수 있습니다. 자세한 정보는 [Kibana 대시보드에서 로그 표시 사용자 정의](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom)를 참조하십시오.

<!-- audience blue staging only end comment -->
