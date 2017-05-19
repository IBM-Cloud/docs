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

# Compose for RethinkDB 시작하기
{: #getting-started-with-compose-for-rethinkdb}

{{site.data.keyword.composeForRethinkDB}}에서는 통합된 관리 및 탐색 콘솔이 있는 JSON 문서 기반의 분산 데이터베이스를 제공합니다. RethinkDB에서는 ReQL 조회 언어를 사용하며 이는 함수 체인화를 중심으로 빌드되고 Java, JavaScript, Python, Ruby의 클라이언트 라이브러리에서 사용 가능합니다. ReQL을 사용하면 클러스터의 노드에서 분배된 결합, 하위 조회와 같은 RethinkDB 서버 측 기능을 사용할 수 있습니다. 또한 RethinkDB는 읽기 조회 성능을 향상시킬 수 있도록 2차 색인을 지원합니다. RethinkDB의 가장 강력한 기능인 changefeeds를 사용하면 여러 ReQL 조회를 실시간 피드로 변환할 수 있습니다.
{:shortdesc}

**참고:** 2016년 9월 14일 이전에 프로비저닝되어 아직 사용 중인 Compose 서비스 인스턴스를 여전히 사용할 수 있으며 [https://www.compose.com/](https://www.compose.com)에서 해당 인스턴스에 직접 액세스할 수 있습니다. 이 시점 이후에 프로비저닝되는 Compose 서비스 인스턴스의 경우 Bluemix 계정을 사용하여 직접 액세스하고 사용할 수 있습니다. 

{{site.data.keyword.composeForRethinkDB}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForRethinkDB}} 인스턴스를 작성하십시오](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/). 

  서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 *사용 가능한 신임 정보* 섹션에 나열되어 있습니다. 

2. {{site.data.keyword.composeForRethinkDB}} 서비스에 연결하십시오. 

   앱을 서비스에 연결하려면 서비스와 함께 작성된 [신임 정보](./credentials.html)를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForRethinkDB}} 서비스에 연결하는 방법을 시연합니다. 

   [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하십시오. 
