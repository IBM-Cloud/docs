---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Compose for Elasticsearch 시작하기
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}}에서는 전체 텍스트 검색 엔진의 기능과 JSON 문서 데이터베이스의 인덱싱 장점을 함께 이용할 수 있습니다. 이들 기능을 함께 사용하면 대용량 데이터의 리치 데이터 분석을 수행할 수 있는 강력한 도구가 됩니다. Elasticsearch를 사용하면 근접한 일치 항목과 사용자가 놓칠 수 있는 잠재적인 위험이 있는지 데이터 세트를 조사할 수 있어 검색의 정확도에 대한 점수를 매길 수 있습니다.
{:shortdesc}

**참고:** 2016년 9월 14일 이전에 프로비저닝되어 아직 사용 중인 Compose 서비스 인스턴스를 여전히 사용할 수 있으며 [https://www.compose.com/](https://www.compose.com)에서 해당 인스턴스에 직접 액세스할 수 있습니다. 이 시점 이후에 프로비저닝되는 Compose 서비스 인스턴스의 경우 Bluemix 계정을 사용하여 직접 액세스하고 사용할 수 있습니다. 

{{site.data.keyword.composeForElasticsearch}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForElasticsearch}} 인스턴스를 작성하십시오](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/). 

  서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 *사용 가능한 신임 정보* 섹션에 나열되어 있습니다. 

2. {{site.data.keyword.composeForElasticsearch}} 서비스에 연결하십시오. 

  앱을 서비스에 연결하려면 서비스와 함께 작성되는 신임 정보를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForElasticsearch}} 서비스에 연결하는 방법을 시연합니다. 

  [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하여 *예제* 색인의 컨텐츠를 표시하십시오. 

## 사용 가능한 신임 정보

필드 이름 |설명
----------|-----------
`uri`|서비스에 연결할 때 사용할 URI입니다. 스키마(`https:`), 관리 사용자 이름과 비밀번호, 서버의 호스트 이름, 연결할 포트 번호를 포함합니다.
`uri_direct_1`|서비스에 연결할 때 사용할 수 있는 대체 URI입니다. `uri`에 따라 형식화됩니다.
`uri_health`|첫 번째 haproxy에서 클러스터 상태를 요청하는 `curl` 명령입니다.
`uri_health_1`|두 번째 haproxy에서 클러스터 상태를 요청하는 `curl` 명령입니다.
`ca_certificate_base64`|애플리케이션이 적합한 서버에 연결되었는지 확인하는 데 사용되는 자체 서명된 인증서입니다. base64로 인코딩되어 있습니다. 샘플 애플리케이션에 표시된 대로 사용하기 전에 키를 디코딩해야 합니다.
`deployment_id`|Compose에서 작성된 서비스의 내부 ID입니다.
`db_type`|서비스에서 제공하는 데이터베이스의 유형입니다. 이 경우 `elastic_search`입니다.
`이름`|데이터베이스 배치 이름입니다.
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**참고:** 두 `haproxy` 포털에서 Elasticsearch 클러스터에 대한 액세스를 제공합니다. `uri`와 `uri_direct_1` 모두 클러스터에 연결하는 데 사용할 수 있습니다. 애플리케이션에서 `uri`와 `uri_direct_1`을 서로 전환하여 연결 실패에 대한 응답을 관리하십시오. 

# 관련 링크
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 문서](https://www.compose.com/articles/){:new_window}

## 튜토리얼 및 샘플
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## 관련 링크
{: #general}
* [Compose 도움말](https://help.compose.com/docs){:new_window}
