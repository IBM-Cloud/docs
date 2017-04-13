---

copyright:
  years: 2017
lastupdated: "2017-03-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 애플리케이션 개발
{: #v10_dashboard}


marbles02 예제 체인코드 및 해당 Javascript 앱을 고유 비즈니스 솔루션 작성을 위한 템플리트로 사용하십시오.
{:shortdesc}


앱은 Node.js SDK API를 사용하여 프로비저닝된 네트워크 컴포넌트와 상호작용하며 궁극적으로 트랜잭션 요청이 있는 피어를 대상으로 합니다. 모니터의 **리소스** 화면에 있는 **서비스 신임 정보** 탭 내에서 피어에 대한 API 엔드포인트, 인증 기관 및 네트워크 순서 지정 서비스를 찾은 후 이러한 문자열을 앱과 함께 제공되는 구성 파일에 플러그하십시오. 그러나 네트워크에서 추가 피어를 대상으로 지정하려는 경우(조직에 속하지 않은 피어의 인증이 필요한 경우가 해당됨)에는 올바른 API가 있어야 한다는 점을 참고하십시오. 애플리케이션에 리턴되는 응답을 확인하기 위해 다른 조직에 대한 CA 인증서를 저장해야 할 수도 있습니다. 이 정보는 **리소스** 보기에 표시되지 않으므로 Bluemix 조직의 담당 관리자에게 문의하여 대역 외 오퍼레이션에서 이 데이터를 획득해야 합니다. 순서 지정 서비스 URL은 네트워크에서 공통이므로 이 컴포넌트에 대한 멤버 특정 정보가 필요하지 않습니다.   

소스 코드 및 전제조건은 [Marbles](https://github.com/IBM-Blockchain/marbles/tree/v3.0) GitHub 저장소를 방문하십시오. README에 따라 앱을 실행하십시오.   

[SDK 저장소](https://github.com/hyperledger/fabric-sdk-node)를 탐색하여 엔드-투-엔드 테스트로 실험을 진행하고 API에 대해 정확히 파악하십시오. 
