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

# Compose for MySQL 시작하기
{: #getting-started-with-compose-for-mysql}

ANSI SQL 99의 광범위한 서브세트와 다양한 고유 확장기능 세트(예: JSON 문서, 전체 텍스트 검색 및 업데이트 가능 보기)를 사용하여 MySQL에서는 개발자가 애플리케이션에서 이용할 수 있는 풍부한 팔레트를 제공합니다. 관리자가 MySQL과 함께 작동할 수 있는 다양한 데이터베이스 관리 도구도 찾을 수 있습니다. {{site.data.keyword.composeForMySQL_full}}에서는 MySQL의 기능을 확장하여 ScyllaDB를 관리하고 고가용성 및 중복성 외에도 자동화된 백업을 제공하는 사용하기 쉬운 자동 확장 배치 시스템을 제공합니다.{:shortdesc}

**참고:** {{site.data.keyword.composeForMySQL_full}}에서는 Compose UI에 대한 액세스를 제공하지 않습니다. 세부사항은 [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support)를 참조하십시오.

{{site.data.keyword.composeForMySQL}}를 시작하려면 다음 단계를 완료하십시오. 

1. [{{site.data.keyword.composeForMySQL}} 인스턴스를 작성하십시오.](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/)

   서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 "사용 가능한 신임 정보" 섹션에 나열됩니다.

2. {{site.data.keyword.composeForMySQL}} 서비스에 연결하십시오. 

  애플리케이션을 서비스에 연결하려면 서비스와 함께 작성된 [신임 정보](./credentials.html)를 사용하십시오. 

  [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) 샘플 애플리케이션을 다운로드하고 readme 파일의 지시사항을 따르십시오. 그런 다음 Bluemix 콘솔의 애플리케이션 세부사항 페이지에서 **앱 보기**를 클릭하십시오.

  샘플 애플리케이션에서는 Node.js를 사용하여 {{site.data.keyword.composeForMySQL}} 서비스에 연결하는 방법을 시연합니다. 
