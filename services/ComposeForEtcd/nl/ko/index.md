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

# {{site.data.keyword.composeForEtcd}} 시작하기
{: #getting-started-with-compose-for-etcd}

etcd는 분산 서버 구성 관리를 위해 서버 클러스터를 조정하고 관리하는 데 필요한 항상 올바른 데이터를 보유하는 키-값 저장소입니다. etcd에서는 RAFT 컨센서스 알고리즘을 사용하여 클러스터에서 데이터 일관성을 보장합니다. etcd는 클러스터의 모든 노드가 동일한 방법으로 동일한 결과에 도달하도록 데이터에 대해 조작이 수행되는 순서를 강제 적용합니다. {{site.data.keyword.composeForEtcd_full}}는 etcd에 저장된 구성 데이터의 자동 백업을 추가합니다. 사용자는 직관적인 관리 인터페이스를 사용하여 간편하게 배치를 모니터하고 스케일링하며 관리할 수 있습니다.
{:shortdesc}

**참고:** 2016년 9월 14일 이전에 프로비저닝되어 아직 사용 중인 Compose 서비스 인스턴스를 여전히 사용할 수 있으며 [https://www.compose.com/](https://www.compose.com)에서 해당 인스턴스에 직접 액세스할 수 있습니다. 이 시점 이후에 프로비저닝되는 Compose 서비스 인스턴스의 경우 Bluemix 계정을 사용하여 직접 액세스하고 사용할 수 있습니다. 

{{site.data.keyword.composeForEtcd}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForEtcd}} 인스턴스를 작성하십시오](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/). 

  서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 *사용 가능한 신임 정보* 섹션에 나열되어 있습니다. 

2. {{site.data.keyword.composeForEtcd}} 서비스에 연결하십시오. 

앱을 서비스에 연결하려면 서비스와 함께 작성되는 신임 정보를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForEtcd}} 서비스에 연결하는 방법을 시연합니다. 

[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하여 *예제*의 컨텐츠를 표시하십시오. 

## 사용 가능한 신임 정보

필드 이름 |설명
----------|-----------
`ca_certificate_base64`|앱이 적합한 서버에 연결되었는지 확인하는 데 사용되는 자체 서명된 인증서입니다. 인증서는 base64로 인코딩됩니다. You must decode the key before using it, as shown in the sample app.
`deployment_id`|Compose에서 작성된 서비스의 내부 ID입니다.
`db_type`|서비스에서 제공하는 데이터베이스의 유형입니다. 이 경우 `etcd`입니다.
`이름`|데이터베이스 배치 이름입니다.
`uri`|서비스에 연결할 때 사용할 URI입니다. `uri`는 스키마(`amqps:`), 관리 사용자 이름과 비밀번호, 서버의 호스트 이름, 연결할 포트 번호, vhost의 이름을 포함합니다.

{: caption="Table 1. {{site.data.keyword.composeForEtcd}} credentials" caption-side="top"}

# 관련 링크
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose 문서](https://www.compose.com/articles/){:new_window}

## 튜토리얼 및 샘플
{: #samples}
* [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs){:new_window}

## 관련 링크
{: #general}
* [Compose 도움말](https://help.compose.com/docs){:new_window}
