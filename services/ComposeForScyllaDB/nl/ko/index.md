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

# Compose for ScyllaDB 시작하기
{: #getting-started-with-compose-for-scylladb}

ScyllaDB는 Cassandra 와이드 컬럼 분산 데이터베이스를 위치 내에서 대체합니다. ScyllaDB는 벤치마크에서 성능을 10배 향상시킬 수 있는 더 효율적인 리소스 사용을 위해 Cassandra의 Java가 아니라 C++로 작성됩니다. Cassandra 도구 및 데이터 파일과의 호환성을 유지하는 외에도 ScyllaDB는 자체 튜닝 기능을 추가합니다. {{site.data.keyword.composeForScyllaDB_full}}는 ScyllaDB의 기능을 확장하여 ScyllaDB를 관리하고 고가용성 및 중복성 외에도 자동화된 백업을 제공하는 사용하기 쉬운 자동 확장 배치 시스템을 제공합니다.{:shortdesc}

**참고:** {{site.data.keyword.composeForScyllaDB_full}}에서는 Compose UI에 대한 액세스를 제공하지 않습니다. 세부사항은 [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support)를 참조하십시오.

{{site.data.keyword.composeForScyllaDB}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForScyllaDB}} 인스턴스를 작성하십시오.](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/)

   서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 "사용 가능한 신임 정보" 섹션에 나열됩니다.

2. {{site.data.keyword.composeForScyllaDB}} 서비스에 연결하십시오. 

   애플리케이션을 서비스에 연결하려면 서비스와 함께 작성된 [신임 정보](./credentials.html)를 사용하십시오. 

   [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) 샘플 애플리케이션을 다운로드하고 readme 파일의 지시사항을 따르십시오. 그런 다음 Bluemix 콘솔의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하십시오.

   샘플 애플리케이션에서는 Node.js를 사용하여 {{site.data.keyword.composeForScyllaDB}} 서비스에 연결하는 방법을 시연합니다. 
