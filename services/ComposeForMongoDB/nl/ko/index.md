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

# Compose for MongoDB 시작하기
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}}에서는 MongoDB의 강력한 색인 작성, 조회, 집계, 폭넓은 드라이버 지원을 사용함으로써 많은 스타트업과 엔터프라이즈에서 찾는 JSON 데이터 저장소가 되었습니다. {{site.data.keyword.composeForMongoDB}}에서는 간단한 Auto-Scaling 배치 시스템을 제공합니다. 고가용성과 중복성, 자동화된 백업과 On-Demand의 중단 없는 백업, 모니터링 도구, 경보 시스템으로 통합, 성능 분석 보기 외의 여러 기능을 깔끔하고 단순한 사용자 인터페이스에서 제공합니다.
{:shortdesc}

**참고:** 2016년 9월 14일 이전에 프로비저닝되어 아직 사용 중인 Compose 서비스 인스턴스를 여전히 사용할 수 있으며 [https://www.compose.com/](https://www.compose.com)에서 해당 인스턴스에 직접 액세스할 수 있습니다. 이 시점 이후에 프로비저닝되는 Compose 서비스 인스턴스의 경우 Bluemix 계정을 사용하여 직접 액세스하고 사용할 수 있습니다. 

{{site.data.keyword.composeForMongoDB}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForMongoDB}} 인스턴스를 작성하십시오](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/). 

   서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 *사용 가능한 신임 정보* 섹션에 나열되어 있습니다. 

2. {{site.data.keyword.composeForMongoDB}} 서비스에 연결하십시오. 

   앱을 서비스에 연결하려면 서비스와 함께 작성된 [신임 정보](./credentials.html)를 사용하십시오. 샘플 앱에서는 Node.js를 사용하여 {{site.data.keyword.composeForMongoDB}} 서비스에 연결하는 방법을 시연합니다. 

   [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) 샘플 앱을 다운로드하고 readme 파일의 지시사항을 수행하십시오. 그런 다음 Bluemix의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하십시오. 
