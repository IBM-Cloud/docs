---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 면책사항
{: #etn_overview}

**주의:** IBM Blockchain on Bluemix 플랜을 사용하기 전에 다음 정보를 검토해야 합니다. 

## IBM 지원 설명

IBM은 오랜 시간 혁신의 선두 자리에 있었으며 IBM Blockchain on Bluemix 오퍼링 플랜을 통해 여전히 그 역할을 지속하고 있습니다. 블록체인은 빠르게 발전하고 있는 기술로서, 금융부터 물류 공급망까지 여러 업종을 파괴적으로 변화시킬 것으로 예상됩니다. 다양한 조기 도입 프로그램을 통해 IBM 고객 및 비즈니스 파트너는 산업용 솔루션으로서 블록체인을 활발하게 이용해 오고 있습니다. IBM Blockchain on Bluemix는 이와 같은 프로그램 중 하나입니다. **다른 새 기술의 경우와 같이 IBM Blockchain on Bluemix 사용자는 신속하고 근본적인 변화의 가능성에 대해 인지하고 있어야 합니다. **  
{:shortdesc}

IBM Blockchain을 뒷받침하는 아키텍처는 Linux Foundation의 Hyperledger 패브릭 프로젝트입니다. 패브릭은 현재 *활성* 상태이며 지속적으로 개발하는 중입니다. 각 오픈 소스 커뮤니티의 기여를 통해 Hyperledger Fabric이 향상되지만 적용에 어려움이 있을 수 있습니다. *활성* 프로젝트 주기 동안 고객은 네트워크 테스트 및 시뮬레이션을 위해 Hyperledger Fabric v1.0을 사용할 수 있습니다. **IBM은 Hyperledger Fabric 블록체인 네트워크에서 금융 자산 또는 가치있는 모든 자산을 직접 정의하거나 교환하는 것에 대해 경고하고 있습니다**.  

## 오픈 소스 설명

**HSBN(High Security Business Network) vNext Beta** 플랜은 Linux Foundation의 Hyperledger Fabric v1.0 오픈 소스 코드 기반입니다. 스타터 개발자 및 HSBN(High Security Business Network) 플랜은 Hyperledger Fabric v0.6 코드 기반입니다. IBM을 포함한 Hyperledger 프로젝트 멤버는 커뮤니티에 의해 검토, 조사 및 테스트된 후에 소스 코드에 계속 기고합니다. Hyperledger Fabric v1.0은 현재 *활성*이며 *활성* 상태 및 Hyperledger 프로젝트의 전체 라이프사이클에 대한 세부사항은 https://wiki.hyperledger.org/community/project-lifecycle에서 사용 가능합니다.   

## 체인코드 지원 설명

다음 코딩 방식은 IBM Blockchain 네트워크에서 지원되지 않습니다. 

1. 반복에 연관 배열 사용(Go에서 순서가 무작위로 지정됨)
2. KVS 테이블에서 항목 목록 읽기(순서가 보장되지 않음)
3. 스레드에 대해 안전하지 않은 체인코드 작성(조회와 호출을 동시에 호출할 수 있음)
4. 체인코드에서 원장 상태 변수를 글로벌 메모리 또는 캐시 스토리지로 대체
5. 체인코드에서 직접 데이터베이스와 같은 외부 서비스에 액세스
6. 비결정성을 야기시킬 수 있는 글로벌 변수 또는 라이브러리 사용(예: "random" 또는 "time" 사용)
7. GetRows를 사용한 반복  

또한 HSBN 및 스타터 플랜(Hyperledger Fabric v0.6)은 데이터 일관성 및 무결성에 대한 위험이 발생할 수 있는 비결정적 체인코드를 지원하지 않습니다. 세부사항은 [비결정적 체인코드](nondeterministic.html)를 참조하십시오. 
