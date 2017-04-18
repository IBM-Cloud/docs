---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.composeForPostgreSQL}} 시작하기
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}}에서는 쉽게 사용자 정의할 수 있는 강력한 오픈 소스 오브젝트 관계형 데이터베이스를 제공합니다. Postgres를 사용하면 개발을 빠르고 간편하게 스케일링할 수 있습니다. C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP, ASP, Java 등 사용자가 편한 언어로 개발할 수 있습니다. 사용자는 JSON이 지원되는 풍부한 기능을 갖춘 엔터프라이즈 데이터베이스를 확보하여 SQL과 NoSQL 모두 잘 활용할 수 있습니다.
{:shortdesc}

**참고:** 2016년 9월 14일 이전에 프로비저닝되어 아직 사용 중인 Compose 서비스 인스턴스를 여전히 사용할 수 있으며 [https://www.compose.com/](https://www.compose.com)에서 해당 인스턴스에 직접 액세스할 수 있습니다. 이 시점 이후에 프로비저닝되는 Compose 서비스 인스턴스의 경우 Bluemix 계정을 사용하여 직접 액세스하고 사용할 수 있습니다. 

Compose for PostgreSQL을 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForPostgreSQL}} 인스턴스를 작성하십시오](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/). 

  서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 *사용 가능한 신임 정보* 섹션에 나열되어 있습니다. 

2. {{site.data.keyword.composeForPostgreSQL}} 서비스에 연결하십시오. 

  앱을 서비스에 연결하려면 서비스와 함께 작성되는 신임 정보를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForPostgreSQL}} 서비스에 연결하는 방법을 시연합니다. 

  [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하여 *예제* 테이블의 컨텐츠를 표시하십시오. 

## 사용 가능한 신임 정보

필드 이름 |설명
----------|-----------
`uri`|서비스에 연결할 때 사용할 URI입니다. 스키마(`postgres:`), 관리 사용자 이름과 비밀번호, 서버의 호스트 이름, 연결할 포트 번호, 데이터베이스 이름, SSL 연결을 사용할 "?ssl=true"를 포함합니다.
`uri_cli`|데이터베이스 인스턴스에 연결하는 `psql` 쉘 명령행입니다.
`ca_certificate_base64`|애플리케이션이 적합한 서버에 연결되었는지 확인하는 데 사용되는 자체 서명된 인증서입니다. base64로 인코딩되어 있습니다. 샘플 애플리케이션에 표시된 대로 사용하기 전에 키를 디코딩해야 합니다.
`deployment_id`|Compose에서 작성된 서비스의 내부 ID입니다.
`db_type`|서비스에서 제공하는 데이터베이스의 유형입니다. 이 경우 `postgresql`입니다.
`이름`|데이터베이스 배치 이름입니다.
{: caption="Table 1. {{site.data.keyword.composeForPostgreSQL}} credentials" caption-side="top"}

# 관련 링크
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 문서](https://www.compose.com/articles/){:new_window}

## 튜토리얼 및 샘플
{: #samples}
* [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs){:new_window}

## 관련 링크
{: #general}
* [Compose 도움말](https://help.compose.com/docs){:new_window}
