---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IBM {{site.data.keyword.blockchain}} 시작하기
{: #gettingstartedtemplate}
마지막 업데이트 날짜: 2016년 10월 13일
{: .last-updated}

**주의:** 스타터 개발자 플랜(베타) 또는 고급 보안 비즈니스 네트워크 플랜(GA)을 사용하려면 먼저 [알아야 할 사항](needtoknow.html)에서 기술 및 지원 정보를 읽어야 합니다.
<br><br>

## 오퍼링 플랜 상태

스타터 개발자 플랜은 베타 릴리스이며 멀티 테넌트 개발 환경을 제공합니다. 고급 보안 비즈니스 네트워크 플랜은 2016년 10월 20일에 일반에게 공개되었습니다(GA 릴리스). 고급 보안 비즈니스 네트워크 플랜은 [IBM Secure Service Container](etn_ssc.html)를 사용한 코드 분리로 고급 보안, 단일 테넌트 LinuxONE on z 환경을 제공합니다.
<br><br>

## IBM Blockchain on Bluemix

Bluemix&reg;의 {{site.data.keyword.blockchainfull}} 서비스는 단추 클릭으로 4-노드 개발 및 테스트 블록체인 네트워크를 제공합니다. 개발자는 처음부터 블록체인 네트워크를 작성하는 대신 애플리케이션 작성과 체인코드 배치를 즉시 시작할 수 있습니다. IBM Blockchain on Bluemix 서비스는 Linux Foundation의 Hyperledger 프로젝트의 [Hyperledger Fabric v0.5](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview) 코드를 기반으로 구축된 피어 투 피어 권한 부여된 네트워크입니다.
{:shortdesc}

Blockchain 네트워크는 안전하고 효율적으로 디지털 자산을 교환하고 추적함을 물론 공유 원장의 모든 트랜잭션을 영구 기록하는 데 사용됩니다. 블록체인에 대한 세부사항은 [블록체인 정보](ibmblockchain_overview.html) 주제를 참조하십시오. 
<br><br>

## 네트워크 플랜 선택

두 IBM Blockchain on Bluemix 플랜, 즉 **스타터 개발자 네트워크** 또는 **고급 보안 비즈니스 네트워크** 간에 선택할 수 있습니다. 아래의 비교 차트를 사용하여 올바른 환경을 선택할 수 있습니다. 

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Bluemix 플랜:      | 스타터 개발자 네트워크       | 고급 보안 비즈니스 네트워크
| ------------------------- |:--------------------------:|:-----:|
| 상태:    | 베타     | GA |
| 용도:  |  개발 및 보안, 성능, 가용성의 레벨 테스트 |  엔터프라이즈 네트워크 시뮬레이션 및 보안, 성능, 가용성의 레벨 테스트 |
| 노드:    | 4 노드 + 인증 기관     | 4 노드 + 인증 기관 |
| [대시보드 모니터:](ibmblockchainmonitor.html) | 예 | 예 |
| 기밀 트랜잭션: | 예 | 예 |
| [합의:](etn_pbft.html) | PBFT | PBFT |
| 환경:     | 공유 멀티 테넌트 | 분리된 단일 테넌트 |
| [IBM Secure Service Container:](etn_ssc.html) | 아니오 | 예 |

<br>
## 네트워크 플랜 실행

다음 단계를 사용하여 블록체인 네트워크의 언바운드 서비스 인스턴스를 작성하고 배치하십시오. 네트워크에는 유효성 검증 노드 및 보안 서비스의 개발 환경이 포함되어 있으며, 체인코드를 배치하고 로그를 보며 애플리케이션을 빌드할 수 있도록 합니다. 

1. [{{site.data.keyword.blockchain}} 서비스 ](https://console.ng.bluemix.net/catalog/services/blockchain/) 페이지의 오른쪽 분할창에서 **서비스 추가** 양식을 완료하십시오. 
  - **영역:** **dev**를 선택하십시오. 
  - **앱:** **바인딩되지 않은 상태로 두기**를 선택하거나, **애플리케이션 선택**을 선택하여 Bluemix.org 애플리케이션 중 하나에 서비스를 바인드하십시오.
  - **서비스 이름:** 고유 이름 또는 값을 입력하십시오(예: **블록체인 테스트 Net123**). 
  - **신임 정보 이름:** 기본값을 유지하십시오. 
  - **선택한 플랜:** **스타터 개발자** 또는 **고급 보안**을 선택하십시오.
  - **작성** 단추를 클릭하십시오. 
2.  현재 위치는 새 서비스의 **서비스 대시보드** 화면입니다. 여기서 네트워크의 인스턴스를 **관리**할 수 있습니다. 블록체인 모니터를 사용하려면 **실행**을 클릭하십시오. 
3.  블록체인 모니터는 네트워크 세부사항, 라이브 로그, 현재 원장 상태, API 및 체인코드 템플리트를 표시합니다. 다음 기능에 대한 대시보드를 사용하십시오. 
  - 네트워크 피어의 발견 및 API 라우트에 액세스하십시오. 
  - 실행 중인 체인코드 컨테이너를 보십시오. 
  - 실시간 로그를 보고 체인코드의 문제점을 해결하십시오. 
  - 원장의 전체 상태를 보십시오. 
  - Swagger UI에 액세스하고 REST API를 통해 네트워크와 상호작용하십시오. 
  - 세 체인코드 예제 중 하나를 배치하십시오. 


# 관련 링크
{: #rellinks}
## 튜토리얼 및 샘플
{: #samples}
* [IBM Marbles 데모(GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM Commercial Paper 데모(GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [IBM Car Lease 데모(Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Art Auction 데모(Github)](https://github.com/ITPeople-Blockchain/auction)

## API 참조
{: #api}
* [Swagger UI](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [Hyperledger Fabric API(GitHub)](https://github.com/hyperledger/fabric/tree/master/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/master/sdk/node)

## 관련 링크
{: #general}
* [패브릭 코드](https://github.com/hyperledger/fabric)
* [백서](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [프로토콜 스펙 및 관련 문서](https://github.com/hyperledger/fabric/tree/master/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [Bluemix 서비스의 새로운 기능](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
