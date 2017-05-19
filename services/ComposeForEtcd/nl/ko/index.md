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

# Compose for etcd 시작하기
{: #getting-started-with-compose-for-etcd}

etcd는 분산 서버 구성 관리를 위해 서버 클러스터를 조정하고 관리하는 데 필요한 항상 올바른 데이터를 보유하는 키-값 저장소입니다. etcd에서는 RAFT 컨센서스 알고리즘을 사용하여 클러스터에서 데이터 일관성을 보장합니다. etcd는 클러스터의 모든 노드가 동일한 방법으로 동일한 결과에 도달하도록 데이터에 대해 조작이 수행되는 순서를 강제 적용합니다. {{site.data.keyword.composeForEtcd_full}}는 etcd에 저장된 구성 데이터의 자동 백업을 추가합니다. 사용자는 직관적인 관리 인터페이스를 사용하여 간편하게 배치를 모니터하고 스케일링하며 관리할 수 있습니다.
{:shortdesc}

**참고:** 2016년 9월 14일 이전에 프로비저닝되어 아직 사용 중인 Compose 서비스 인스턴스를 여전히 사용할 수 있으며 [https://www.compose.com/](https://www.compose.com)에서 해당 인스턴스에 직접 액세스할 수 있습니다. 이 시점 이후에 프로비저닝되는 Compose 서비스 인스턴스의 경우 Bluemix 계정을 사용하여 직접 액세스하고 사용할 수 있습니다. 

{{site.data.keyword.composeForEtcd}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForEtcd}} 인스턴스를 작성하십시오](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/). 

  서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 *사용 가능한 신임 정보* 섹션에 나열되어 있습니다. 

2. {{site.data.keyword.composeForEtcd}} 서비스에 연결하십시오. 

앱을 서비스에 연결하려면 서비스와 함께 작성된 [신임 정보](./credentials.html)를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForEtcd}} 서비스에 연결하는 방법을 시연합니다. 

[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하여 *예제*의 컨텐츠를 표시하십시오. 
