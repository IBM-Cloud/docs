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

# 사용 가능한 신임 정보
{: #available-credentials}

앱을 서비스에 연결하려면 서비스와 함께 작성되는 신임 정보를 사용하십시오. [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) 샘플 앱은 Node.js를 사용하여 신임 정보로 {{site.data.keyword.composeForPostgreSQL}} 서비스에 연결하는 방법을 보여줍니다. 

필드 이름 |설명
----------|-----------
`uri`|서비스에 연결할 때 사용할 URI입니다. 스키마(`postgres:`), 관리 사용자 이름과 비밀번호, 서버의 호스트 이름, 연결할 포트 번호, 데이터베이스 이름, SSL 연결을 사용할 "?ssl=true"를 포함합니다.
`uri_cli`|데이터베이스 인스턴스에 연결하는 `psql` 쉘 명령행입니다.
`ca_certificate_base64`|애플리케이션이 적합한 서버에 연결되었는지 확인하는 데 사용되는 자체 서명된 인증서입니다. base64로 인코딩되어 있습니다. 샘플 애플리케이션에 표시된 대로 사용하기 전에 키를 디코딩해야 합니다.
`deployment_id`|Compose에서 작성된 서비스의 내부 ID입니다.
`db_type`|서비스에서 제공하는 데이터베이스의 유형입니다. 이 경우 `postgresql`입니다.
`name`|데이터베이스 배치 이름입니다.
{: caption="표 1. Compose for PostgreSQL 신임 정보" caption-side="top"}
