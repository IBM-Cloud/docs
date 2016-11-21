---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 알아야 할 사항
{: #etn_overview}
마지막 업데이트 날짜: 2016년 10월 13일
{: .last-updated}

**주의:** IBM Blockchain on Bluemix 플랜인 스타터 개발자(베타) 또는 고급 보안 비즈니스 네트워크(GA)를 사용하기 전에 다음 정보를 검토해야 합니다.
<br><br>

## IBM 지원 설명

IBM은 오랫동안 혁신의 선두에 있었으며 최신 IBM Blockchain 오퍼링을 통해 여전히 그 역할을 하고 있습니다. 블록체인은 빠르게 발전하고 있는 기술로서, 금융부터 물류까지 여러 업종을 파괴적으로 변화시킬 것으로 예상됩니다. 다양한 조기 도입 프로그램을 통해 IBM 고객과 비즈니스 파트너는 이미 블록체인의 향방에 영향을 미치고 있습니다. IBM Blockchain on Bluemix는 이와 같은 프로그램 중 하나입니다. **다른 새 기술의 경우와 같이 IBM Blockchain on Bluemix 사용자는 신속하고 근본적인 변화에 대비해야 합니다**.  
{:shortdesc}

IBM Blockchain을 뒷받침하는 아키텍처는 Linux Foundation의 Hyperledger 프로젝트입니다. Hyperledger Fabric은 현재 개발 중인 *인큐베이션* 상태의 오픈 소스 프로젝트입니다. 각 오픈 소스 커뮤니티의 기여를 통해 Hyperledger Fabric이 더욱 강력해질 수 있지만 적용에 어려움이 있을 수 있습니다. *인큐베이션* 주기 동안 고객은 Hyperledger Fabric v0.5를 사용하여 네트워크 테스트 및 시뮬레이션을 진행할 수 있지만 **IBM은 Hyperledger Fabric v0.5 블록체인 네트워크에서 직접 금융 자산을 운용하지 말 것을 경고합니다**.  
<br>

## 오픈 소스 설명

IBM Blockchain on Bluemix(스타터 개발자 플랜 및 고급 보안 비즈니스 네트워크 플랜)는 Linux Foundation의 Hyperledger Fabric v0.5 오픈 소스 코드를 사용합니다. IBM을 포함한 Hyperledger 프로젝트 멤버는 커뮤니티에 의해 검토, 검사되고 테스트된 후에 코드를 패브릭에 기고합니다. Hyperledger Fabric v0.5는 현재 *인큐베이션* 상태입니다. *인큐베이션* 상태 및 Hyperledger 프로젝트의 전체 라이프사이클에 대한 세부사항은 https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle 페이지를 참조하십시오.
<br><br>

## 체인코드 지원 설명

IBM Blockchain은 블록체인 네트워크에서 데이터 일관성 및 무결성에 대한 위험성을 야기하는 [비결정적 체인코드](ibmblockchain_tutorials.html#ndcc)를 지원하지 않습니다. IBM Blockchain on Bluemix 네트워크에 새 체인코드를 배치하기 전에 [비결정적 체인코드](ibmblockchain_tutorials.html#ndcc)의 세부사항을 검토하십시오.

[비결정적 체인코드](ibmblockchain_tutorials.html#ndcc) 외에 다음 코딩 방식은 IBM Blockchain 네트워크에서 지원되지 않습니다.

1. 반복에 연관 배열 사용(Go에서 순서가 무작위로 지정됨)
2. KVS 테이블에서 항목 목록 읽기(순서가 보장되지 않음)
3. 스레드에 대해 안전하지 않은 체인코드 작성(조회와 호출을 동시에 호출할 수 있음)
4. 체인코드에서 원장 상태 변수를 글로벌 메모리 또는 캐시 스토리지로 대체
5. 체인코드에서 직접 데이터베이스와 같은 외부 서비스에 액세스
6. 비결정성을 야기시킬 수 있는 글로벌 변수 또는 라이브러리 사용(예: “random” 또는 "time" 사용)
<br><br>

## 도움 받기

IBM Blockchain on Bluemix 네트워크에 대한 지원 및 도움은 [지원 받기](ibmblockchain_support.html)를 참조하십시오.
