---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
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

  앱을 서비스에 연결하려면 서비스와 함께 작성된 [신임 정보](./credentials.html)를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForElasticsearch}} 서비스에 연결하는 방법을 시연합니다. 

  [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하여 *예제* 색인의 컨텐츠를 표시하십시오. 
