---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# z의 블록체인
{: #zblockchain}
마지막 업데이트 날짜: 2016년 7월 8일
{: .last-updated}



z/OS에서 Bluemix 데디케이티드 오퍼링의 블록체인 서비스를 사용하여 개인용 및 보안 디지털 자산을 작성할 수 있으며, 이는 권한 부여된 네트워크에서 빠르고 안전하게 거래될 수 있습니다. *(간략한 설명의 일부로서 추가 정보)*
{:shortdesc}


* 이 정도 양의 컨텐츠를 별도의 섹션으로 둘 필요가 있습니까? 혹은 이를 "정보" 아래의 임베디드 주제로서 두시겠습니까? 
* PBFT, 보안, 성능, 지원과 관련된 정보가 예상됩니다. 


## PBFT
{: #PBFT}

PBFT(Practical Byzantine Fault Tolerance)는 배치당 구성되고 플러그인될 수 있는 중요한 합의 프로토콜입니다. `obcpbft` 패키지는 중요한 [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT") 합의 프로토콜의 구현이며, 이는 *비잔틴*으로 작동하는 유효성 검증기의 임계값에도 불구하고 유효성 검증기 간의 합의를 제공합니다(즉, 악의적이거나 예측 불가능한 방식에 실패함). 기본 구성에서 PBFT 및 Sieve는 모두 최소한 *3t+1* 유효성 검증기(복제본)에서 실행되도록 설계되어 있으며, 최대 *t* 잠재적 결함(악의적 또는 *비잔틴* 포함) 복제본이 허용됩니다. 핵심 PBFT 기능에 대한 자세한 정보는 Linux Foundation의 Hyperledger 프로젝트의 [프로토콜 스펙](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) 섹션을 참조하십시오.  

[![미리보기](http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)](http://www.youtube.com/watch?v=EKa5Gh9whgU) 보기

*(사용자가 PBFT를 알아야 하는 실제 이유를 표시해야 합니다. z 지원의 블록체인에서 PBFT가 수행하는 역할 및 이 지원에 대한 해당 관계.)*


### 지원되는 실패 케이스
{: #failure}

*지원되는 실패 케이스 및 지원되지 않는 실패 케이스입니다.*

*(Barry Mosakowski/Raleigh/IBM 또는 Tuan Dang/Raleigh/IBM은 추가 세부사항을 제공할 수 있습니다.)*

### z/OS에서 데디케이티드 오퍼링의 가용성
{: #Availability}

*PBFT 테스트를 기반으로 하는 가용성 및 가용성에 대한 기대치입니다. *

*(추가 세부사항이 필요합니다.)*

### PBFT의 기본 기능 확인
{: #Test PBFT}

*(Gari의 입력입니다. 스크린샷을 포함하여 테스트 단계 수행 방법에 대한 Jason의 추가 세부사항이 필요합니다.)*

기본 PBFT 기능을 확인하려면 다음 단계를 수행하십시오. 

1. 네트워크에서 하나 이상의 피어에 대해 트랜잭션을 제출하십시오. 
2. 최소한 *2f+1*개(이 경우에는 3개)의 피어가 동일한 상태인지 확인하십시오. *(어떻게 확인합니까? 테스트 케이스 세부사항이 필요합니다.)*

  *REST API를 사용한 예제*
3. 대시보드에서 피어 4를 중지하는 단추를 클릭하십시오. *(피어 4를 중지하려면 대시보드의 "피어 중지" 기능을 사용하십시오. 세부 오퍼레이션을 설명하려면 테스트 케이스가 필요합니다.)*
4. 네트워크 처리가 계속되는지 확인하십시오. *(어떻게 확인합니까?)*
5. 대시보드에서 피어 3을 중지하는 단추를 클릭하십시오. 
6. 네트워크 처리가 중지 중인지 확인하십시오. 
7. 대시보드에서 피어 3을 다시 시작하는 단추를 클릭하십시오. 

피어 3이 캐치업하고 네트워크 처리가 계속되면 기능 PBFT 함수를 사용할 수 있습니다. 

**참고:**
* 피어 3을 다시 시작한 이후, 새 트랜잭션을 피어 3에 제출하기 전에 제한시간이 초과될 때까지 기다려야 합니다. 

* 네트워크 처리가 중지될 때 활성 피어에 전송되는 트랜잭션은 네트워크 처리가 계속된 후에 버퍼링되고 네트워크에 제출됩니다. 

## z의 블록체인에 대한 환경
{: #z environment}

z/OS의 Bluemix 데디케이티드 오퍼링에서 블록체인 서비스를 사용하려면, 사용자 환경이 다음 요구사항을 충족하는지 확인하십시오. 

* 멤버십 서비스에서 PBFT를 실행 중인 4-피어 네트워크. 멤버십 서비스에 대해 자세히 알아보려면 Linux Foundation의 Hyperledger 프로젝트의 [프로토콜 스펙](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) 섹션을 참조하십시오.  
* 공유 컴퓨터 또는 메모리가 없는 격리된 네트워크. 
* 네트워크 내의 격리된 피어. 
* 클라우드 시스템 관리자로부터 보호되는 시스템. 

블록체인 모니터는 블록체인 환경의 개요를 제공하며 네트워크에 대한 세부사항을 검색합니다. 블록체인 환경 및 이를 모니터하는 방법에 대해 자세히 알아보려면 [블록체인 모니터에서 체인코드 관리](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) 및 [블록체인의 튜토리얼 및 샘플 앱](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html)을 참조하십시오. 

## 보안

*문서에서 보안 정보를 제공하지 않습니까?*

## 성능

*문서에서 성능 정보를 제공하지 않습니까?*

## 고객 지원 받기

z/OS에서 Bluemix 데디케이티드 오퍼링의 블록체인 서비스에 문제점이 있으면 IBM Bluemix 문제점 해결 프로세스를 따르십시오. 도움을 받는 방법에 대한 자세한 정보는 [문제점 해결](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html)을 참조하십시오. 
