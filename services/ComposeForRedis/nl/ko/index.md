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

# {{site.data.keyword.composeForRedis}} 시작하기
{: #getting-started-with-compose-for-redis}

Redis는 오픈 소스인 인메모리 키-값 저장소입니다. Redis의 값은 단순 문자열, 해시, 목록, 집합 또는 강력한 비트맵, hyperloglog, 지리공간 색인입니다. Redis는 애플리케이션 캐시 또는 응답이 빠른 데이터 저장소로 이상적입니다. {{site.data.keyword.composeForRedis_full}}에서는 고가용성과 온디스크 지속성을 확보할 수 있도록 미리 조정된 구성을 제공하며 이는 모두 추가 보안 기능을 사용해 잠겨 있습니다.
{:shortdesc}

**참고:** 2016년 9월 14일 이전에 프로비저닝되어 아직 사용 중인 Compose 서비스 인스턴스를 여전히 사용할 수 있으며 [https://www.compose.com/](https://www.compose.com)에서 해당 인스턴스에 직접 액세스할 수 있습니다. 이 시점 이후에 프로비저닝되는 Compose 서비스 인스턴스의 경우 Bluemix 계정을 사용하여 직접 액세스하고 사용할 수 있습니다. 

{{site.data.keyword.composeForRedis}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForRedis}} 인스턴스를 작성하십시오](https://console.ng.bluemix.net/catalog/services/compose-for-redis/). 

  서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 *사용 가능한 신임 정보* 섹션에 나열되어 있습니다. 

2. {{site.data.keyword.composeForRedis}} 서비스에 연결하십시오. 

  앱을 서비스에 연결하려면 서비스와 함께 작성되는 신임 정보를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForRedis}} 서비스에 연결하는 방법을 시연합니다. 

  [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하십시오. 

## 사용 가능한 신임 정보

필드 이름 |설명
----------|-----------
`uri`|서비스에 연결하는 데 사용할 URI로 스키마(redis:), 관리 사용자 이름과 비밀번호, 서버의 호스트 이름, 연결할 포트 번호를 포함합니다.
`uri_cli`|데이터베이스 인스턴스에 연결하는 `redis-cli` 명령행입니다.
`deployment_id`|Compose에서 작성된 서비스의 내부 ID입니다.
`db_type`|서비스에서 제공하는 데이터베이스의 유형입니다. 이 경우 `redis`입니다.
`이름`|데이터베이스 배치 이름입니다.
{: caption="Table 1. {{site.data.keyword.composeForRedis}} credentials" caption-side="top"}

# 관련 링크
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 문서](https://www.compose.com/articles/){:new_window}

## 튜토리얼 및 샘플
{: #samples}
* [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs){:new_window}

## 관련 링크
{: #general}
* [Compose 도움말](https://help.compose.com/docs){:new_window}
