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

# Compose for ScyllaDB 시작하기
{: #getting-started-with-compose-for-scylladb}

ScyllaDB는 Cassandra 와이드 컬럼 분산 데이터베이스를 위치 내에서 대체합니다. ScyllaDB는 벤치마크에서 성능을 10배 향상시킬 수 있는 더 효율적인 자원 사용을 위해 Cassandra의 Java가 아니라 C++로 작성됩니다. Cassandra 도구 및 데이터 파일과의 호환성을 유지하는 외에도 ScyllaDB는 자체 튜닝 기능을 추가합니다. {{site.data.keyword.composeForScyllaDB_full}}는 ScyllaDB의 기능을 확장하여 ScyllaDB를 관리하고 고가용성 및 중복성 외에도 자동화된 백업을 제공하는 사용하기 쉬운 자동 확장 배치 시스템을 제공합니다.{:shortdesc}

**참고:** {{site.data.keyword.composeForScyllaDB_full}}에서는 Compose UI에 대한 액세스를 제공하지 않습니다. 세부사항은 [Compose on Bluemix 지원](https://help.compose.com/docs/bluemix-compose-support)을 참조하십시오.

{{site.data.keyword.composeForScyllaDB}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForScyllaDB}} 인스턴스를 작성](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/)하십시오.

   서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 "사용 가능한 신임 정보" 섹션에 나열됩니다.

2. {{site.data.keyword.composeForScyllaDB}} 서비스에 연결하십시오. 

   애플리케이션을 서비스에 연결하려면 서비스와 함께 작성되는 신임 정보를 사용하십시오. 

   [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) 샘플 애플리케이션을 다운로드하고 readme 파일의 지시사항을 따르십시오. 그런 다음 Bluemix 콘솔의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하십시오.

   샘플 애플리케이션에서는 Node.js를 사용하여 {{site.data.keyword.composeForScyllaDB}} 서비스에 연결하는 방법을 시연합니다. 


## 사용 가능한 신임 정보

필드 이름 |설명
----------|-----------
`db_type`|서비스에서 제공하는 데이터베이스의 유형입니다. 이 경우 `scylla`입니다.
`uri_cli_1`|데이터베이스 인스턴스에 연결하는 대체 `cqlsh` 쉘 명령행입니다.
`maps`|다양한 드라이버에서 내부 IP 주소를 ScyllaDB 데이터베이스의 외부 DNS 이름과 연관시키는 데 필요한 정보를 제공하는 ScyllaDB 연결 맵입니다.
`이름`|데이터베이스 배치 이름입니다.
`uri_cli`|데이터베이스 인스턴스에 연결하는 `cqlsh` 쉘 명령행입니다.
`uri_direct_2`|서비스에 연결하는 데 사용할 수 있는 대체 URI입니다. `uri`에 따라 형식화됩니다.
`uri_direct_1`|서비스에 연결하는 데 사용할 수 있는 대체 URI입니다. `uri`에 따라 형식화됩니다.
`ca_certificate_base64`|애플리케이션이 적합한 서버에 연결되었는지 확인하는 데 사용되는 자체 서명된 인증서입니다. 인증서는 base64로 인코딩됩니다.
`deployment_id`|Compose에서 작성된 서비스의 내부 ID입니다.
`uri_cli_2`|데이터베이스 인스턴스에 연결하는 대체 `cqlsh` 쉘 명령행입니다.
`uri`|서비스에 연결할 때 사용하는 URI로서, 스키마(`scylla:`), 비밀번호, 서버의 호스트 이름, 연결할 포트 이름 및 데이터베이스 이름이 포함됩니다.
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} credentials" caption-side="top"}


# 관련 링크
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 문서](https://www.compose.com/articles/){:new_window}

## 튜토리얼 및 샘플
{: #samples}
* [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs){:new_window}

## 관련 링크
{: #general}
* [Compose 도움말](https://help.compose.com/docs){:new_window}
