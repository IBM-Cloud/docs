---

copyright:
  years: 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 시작하기
{: #gettingstartedtemplate}

**주의:** IBM Blockchain on Bluemix 플랜을 사용하기 전에 [면책사항](needtoknow.html)에 있는 기술 및 지원 정보를 읽어야 합니다.
{:shortdesc}

## IBM Blockchain on Bluemix

{{site.data.keyword.blockchainfull}} on Bluemix&reg; 서비스는 3개의 블록체인 네트워크 플랜으로 구성되어 있습니다. 최신 플랜 **HSBN(High Security Business Network) vNext Beta**는 Hyperledger Fabric v1.0 코드 기반으로 빌드되었으며 새 기능을 제공하기 위해 모듈 아키텍처를 활용합니다. IBM Blockchain on Bluemix 플랜은
개발자가 개인용 블록체인 네트워크를 디자인하고 구성하지 않고도 체인코드 애플리케이션을 즉시 쓰고 테스트할 수 있도록 지원합니다. 체인코드는 패브릭 블록체인 네트워크의 안전하고 효율적인 자산 교환이 이뤄지는 엔진이며 원장의 이러한 트랜잭션에 대한 영구적인 레코딩입니다. 

## 오퍼링 플랜

새로운 IBM Blockchain on Bluemix 가입자는 지금 **HSBN vNext Beta** 플랜에 등록접수할 수 있습니다. 이 최신 오퍼링은 차세대 보안, 무결성, 확장성 및 성능을 제공하는 Hyperledger Fabric v1.0 기반입니다. 표 1은 Bluemix 플랜에 대해 설명합니다. 

표 1: IBM Blockchain on Bluemix 플랜  

| Bluemix 플랜      | 상태       | 새 가입자 사용 가능  | Hyperledger Fabric 버전
| ------------------------- |:--------------------------:|:-----:|:-----:|
| **HSBN vNext Beta** (1)   | 베타     | 예 |  v1.0 |
| HSBN (2) |  GA |  예 |  v0.6 |
| 스타터 개발자 (3)    | 베타     | 예 | v0.6 |

(1) **HSBN(High Security Business Network) vNext Beta** 플랜은 Bluemix 조직에 가입하고 분산 블록체인 네트워크를 빌드하기 위한 손쉬운 메커니즘을 제공합니다.   
(2) **HSBN(High Security Business Network) GA** 플랜은 [IBM Secure Service Container](etn_ssc.html)를 사용하는 코드 분리 기능이 있는 보안이 강화된 단일 테넌트 LinuxONE on z Systems 환경을 제공합니다.   
(3) 스타터 개발자 베타 플랜은 다중 테넌트 개발 전용 환경을 제공합니다.   

## 오퍼링 플랜 세부사항

표 2에서는 IBM Blockchain on Bluemix 오퍼링 플랜에 대해 자세히 비교합니다. IBM Blockchain on Bluemix의 새로운 가입자는 **HSBN vNext Beta** 플랜을 선택해야 합니다. HSBN 및 스타터 개발자 플랜은 새 가입자는 사용할 수 없지만 IBM에 의해 계속 지원됩니다. 

표 2: IBM Blockchain on Bluemix 플랜 세부사항  

| Bluemix 플랜:      | 스타터 개발자 네트워크       | 고급 보안 비즈니스 네트워크       | HSBN(High Security Business Network) vNext Beta
| ------------------------- |:--------------------------:|:-----:|:-----:|
| 상태:    | 베타     | GA | 베타 |
| 용도:  |  개발 및 보안, 성능, 가용성의 레벨 테스트 |  엔터프라이즈 네트워크 시뮬레이션 및 보안, 성능, 가용성의 레벨 테스트 |  프로덕션 레벨 보안, 성능 및 가용성이 포함된 엔터프라이즈 비즈니스 네트워크 설정  |
| 노드:    | 4개 피어 + 인증 기관     | 4개 피어 + 인증 기관 | 네트워크 컴포넌트의 동적 관리 |
| 대시보드 모니터: | [예](ibmblockchainmonitor.html) | [예](ibmblockchainmonitor.html) | [예](v10_dashboard.html) |
| 환경:     | 공유 멀티 테넌트 | 분리된 단일 테넌트 | 다중 분리 레벨 |

# 관련 링크
{: #rellinks}
## 튜토리얼 및 샘플
{: #samples}
* [IBM Marbles 데모(GitHub)](https://github.com/IBM-Blockchain/marbles) - v0.6 & v1.0
* [IBM Commercial Paper 데모(GitHub)](https://github.com/IBM-Blockchain/cp-web#readme) - v0.6
* [IBM Car Lease 데모(Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) - v0.6
* [Art Auction 데모(Github)](https://github.com/ITPeople-Blockchain/auction) v0.6 - v1.0(로컬로 실행)

## API 참조
{: #api}
* [Hyperledger Fabric API(GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## 관련 링크
{: #general}
* [패브릭 코드](https://github.com/hyperledger/fabric)
* [패브릭 컴포저](https://fabric-composer.github.io/)
* [Fabric v1.0 문서](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [Fabric v0.6 문서](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Bluemix 서비스의 새로운 기능](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
