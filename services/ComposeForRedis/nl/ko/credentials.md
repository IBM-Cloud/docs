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

앱을 서비스에 연결하려면 서비스와 함께 작성되는 신임 정보를 사용하십시오. [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) 샘플 앱은 Node.js를 사용하여 신임 정보로 {{site.data.keyword.composeForRedis}} 서비스에 연결하는 방법을 보여줍니다. 

필드 이름 |설명
----------|-----------
`uri`|서비스에 연결하는 데 사용할 URI로 스키마(redis:), 관리 사용자 이름과 비밀번호, 서버의 호스트 이름, 연결할 포트 번호를 포함합니다.
`uri_cli`|데이터베이스 인스턴스에 연결하는 `redis-cli` 명령행입니다.
`deployment_id`|Compose에서 작성된 서비스의 내부 ID입니다.
`db_type`|서비스에서 제공하는 데이터베이스의 유형입니다. 이 경우 `redis`입니다.
`name`|데이터베이스 배치 이름입니다.
{: caption="표 1. Compose for Redis 신임 정보" caption-side="top"}
