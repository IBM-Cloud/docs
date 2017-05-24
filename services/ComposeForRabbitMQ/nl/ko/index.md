---

copyright:
  years: 2016,2017
lastupdated: "2017-04-027"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Compose for RabbitMQ 시작하기
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ는 데이터와 애플리케이션 계층의 분리를 사용하여 애플리케이션과 데이터베이스 간 메시지를 비동기로 처리합니다. 개발자는 RabbitMQ를 사용하여 사용자 정의할 수 있는 지속성 레벨, 전달 설정, 확인된 문서가 있는 메시지를 라우트하고 추적하며 큐에 대기시킬 수 있습니다. {{site.data.keyword.composeForRabbitMQ_full}}를 사용하면 배치 모니터링, 단추를 클릭하여 실행하는 스케일링, 사용자 설정, 로그 파일 액세스와 같은 관리 기능을 갖춘 사용이 간편한 관리 인터페이스에 액세스할 수 있습니다.
{:shortdesc}

**참고:** 2016년 9월 14일 이전에 프로비저닝되어 아직 사용 중인 Compose 서비스 인스턴스를 여전히 사용할 수 있으며 [https://www.compose.com/](https://www.compose.com)에서 해당 인스턴스에 직접 액세스할 수 있습니다. 이 시점 이후에 프로비저닝되는 Compose 서비스 인스턴스의 경우 Bluemix 계정을 사용하여 직접 액세스하고 사용할 수 있습니다. 

{{site.data.keyword.composeForRabbitMQ}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForRabbitMQ}} 인스턴스를 작성하십시오](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/). 

  서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 *사용 가능한 신임 정보* 섹션에 나열되어 있습니다. 

2. {{site.data.keyword.composeForRabbitMQ}} 서비스에 연결하십시오. 

  앱을 서비스에 연결하려면 서비스와 함께 작성된 [신임 정보](./credentials.html)를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForRabbitMQ}} 서비스에 연결하는 방법을 시연합니다. 

  [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하십시오. 
