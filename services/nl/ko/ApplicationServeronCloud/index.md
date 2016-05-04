---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM WebSphere Application Server for Bluemix 시작하기
{: #getting_started}

*마지막 업데이트 날짜: 2016년 4월 08일*

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}}는 Bluemix에 호스팅된 클라우드 환경에서 사전 구성된 WebSphere Application Server Liberty, Network Deployment 또는 일반적인 인스턴스에 대한 신속한 설정을 용이하게 해주는 서비스입니다.
{: shortdesc}

## WebSphere Application Server for Bluemix의 개요
{: #overview}

WebSphere Application Server for Bluemix에서는 이용자에게 사전 구성된 일반적인 WebSphere 및 Liberty Profile 서버를 제공합니다. 이는 게스트 운영 체제에 대한 루트 액세스 권한이
있는 가상 머신 게스트에서 호스팅됩니다. 서비스를 작성할 때 *Liberty*, *ND* 또는 *일반적인 WebSphere* 중에서 선택하십시오.

사용자에게 비슷한 WebSphere 관리 환경이 제공되며 기본 운영 체제에 대한
전체 액세스 권한이 있습니다. 기존 스크립트를 재사용하고 자체 프레임워크 또는 써드파티
프레임워크에서 작업하도록 필요에 따라 시스템을 약간 수정할 수 있습니다. 사내 구축형 WebSphere 구성과 마찬가지로 WebSphere Application Server Liberty, ND 또는 일반적인 서비스를 관리하도록 Admin Center와 Admin Console이 제공됩니다.

**참고**: WebSphere Application Server for Bluemix Network Deployment 플랜에 이제 더 많은 기능이 있습니다. 플랜은 둘 이상의 가상 머신이 있는 WebSphere Application Server Network Deployment 셀 환경으로 구성됩니다. 첫 번째 가상 머신에는 배치 관리자와
IBM HTTP Server가 포함되어 있고, 나머지 가상 머신에는 배치 관리자에 연합된 사용자 정의
노드(노드 에이전트)가 포함되어 있습니다. 기존 wsadmin 스크립트를 사용하여 WebSphere 구성을 작성하거나
WebSphere Admin Console을 사용하여 수동으로 환경을 구성하십시오. 해당 새 기능을
사용하면 고가용성, 장애 복구 및 확장성을 위한 클러스터형 환경을 설정할 수 있습니다. 클러스터링은
미들웨어 엔터프라이즈 애플리케이션의 중요한 요소이며, 이제 클라이언트에서 두 개 이상의
인스턴스에 있는 로드 밸런스 요청으로 토폴로지를 클러스터링하도록 선택할 수 있습니다.


WebSphere Application Server for Bluemix Liberty Core 플랜에도
더 많은 기능이 있습니다. 플랜에는 Liberty 프로파일(서버)의 그룹에 대한 관리 도메인이고
둘 이상의 가상 머신으로 구성된 Liberty Collective의 사용이 포함됩니다. 첫 번째
가상 머신에는 Liberty Collective의 제어점인 Collective Controller Liberty 서버를
포함합니다. Liberty Collective 외에도 이 가상 머신에는 웹 브라우저에서
애플리케이션에 액세스할 수 있는 IBM HTTP Server도 포함됩니다. 나머지
가상 머신은 통합 멤버가 있는(Liberty Profile 서버) 통합
호스트입니다. Liberty 제어기 서버에서는 Liberty Admin Center 기능도 사용됩니다.

다음 그림은 WebSphere Application Server for Bluemix Network Deployment 셀의 아키텍처 및 Liberty Collective 환경을 나타냅니다.

![그림1. Network Deployment 셀 및 Liberty Collective](images/CellCollectiveDiagram.gif)

## 운영 환경
{: #operational_environment}

IBM WebSphere Application Server for Bluemix는 이용자가 애플리케이션을 배치하도록 공유 환경에서 게스트(가상 머신)를 리턴하는 서비스입니다. VPN은
일반 포트 스캔 및 기타 원치 않는 네트워크 기반 공격으로부터 공용 서비스를 보호합니다.
그러나 서비스 인스턴스에 액세스하기 위해 사용하는 서비스 VPN이 여러 Bluemix 조직과 사용자 간에 공유될 수 있음에 유의하는 것이 중요합니다. 가상 머신은 IaaS 자원의 공유 풀에서 오는 계산, 메모리 및 I/O 자원을 제공합니다. 개인용 환경에서 애플리케이션을 실행하려는 경우, 전용 IBM WebSphere Application Server for Bluemix 오퍼링을 담당하는 IBM 영업 담당자에게 문의하십시오. 

공유 환경에서 가상 머신이 특정 계산, 메모리 및 I/O 자원을 실행하므로
서비스 구성이 다를 수 있습니다. 각 특정 서비스 인스턴스에 대한 구성은 IBM WebSphere Application Server for Bluemix 서비스 대시보드 및 포털을 통해 볼 수 있습니다.

**참고**: IBM WebSphere Application Server for Bluemix에서는 이제 해당 환경을 더 큰 가상 머신이 있는 올바른 크기로 만들도록 메모리 중심 애플리케이션이 있는 클라이언트에 대한 옵션을 제공합니다. 클라이언트는 최대 32GB RAM 가상 머신의 프로비저닝된 WebSphere Application Server 컴포넌트 또는 단일 시스템의 특정 자원 크기를 선택할 수 있습니다.

## 가격 책정 전략
{: #pricing_strategy}

IBM WebSphere Application Server for Bluemix에서는 가상 머신 인스턴스를 제공합니다. 이러한 인스턴스로 클라이언트는 단순 포털을 사용하여 애플리케이션 조정에 중요한 유연성이 있으며 일관성 있고, 반복 가능한 방식으로 엔터프라이즈 WebSphere Application Server 배치를 작성하고 관리합니다. 사용자는 호스팅된 클라우드 환경에서 사전 구성된 WebSphere Application Server Liberty, ND 또는 일반적인 가상 머신에서 시작해서 실행할 수 있습니다. 사용자는 기존 WebSphere Application Server 애플리케이션을 Bluemix로 마이그레이션하고 기본 OS 및 미들웨어의 전체 제어를 수행할 수 있습니다. 

IBM WebSphere Application Server for Bluemix는 다음과 같은 비용 메트릭에 따라 제공됩니다. 

*  *인스턴스-시간*: 인스턴스가 IBM WebSphere Application Server for Bluemix 서비스의 특정 구성에 대한 액세스로 정의됩니다. 클라이언트는 비용 청구 기간 중에 배치된 서비스의 각 인스턴스에 대한 각각의 전체 또는 부분 시간에 대해 청구됩니다. 각 인스턴스 시간은 매월 청구되며 인스턴스가 그 달의 일부만 사용된 경우에는 사용 비율로 비례 계산됩니다. 

예를 들어, ND 플랜을 사용하는 경우 하나의 인스턴스는 2GB RAM 및 12GB HD의 1vCPU와 동일합니다. 따라서 한 개의 제어 노드와 여덟 개의 사용자 정의 노드로 셀을 구성하려고 선택한 경우 아홉 개의 노드(인스턴스)에 대해 비용 청구됩니다.

**참고**: 사용자 정의 노드 또는 Liberty 호스트당 최소 비용 청구가 0.25 인스턴스 시간으로 설정됩니다. 위의 예제에서 최소 15분에 대해 구성된 하나의 제어 노드와 하나의 사용자 정의 노드가 (.25 * 인스턴스의 #)의 최소 비용 청구와 동일하게 됩니다.

# 관련 링크
## 일반
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [WebSphere Application Server 문서](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/as_ditamaps/was855_welcome_ndmp.html){: new_window}
* [WebSphere Application Server 일반적인 v9 Beta 문서](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
