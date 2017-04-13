---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 새로운 기능
{: #whatsnew}

**HSBN vNext Beta** 플랜은 [Hyperledger Fabric v1.0](https://www.hyperledger.org/){:new_window} 오픈 소스 코드 베이스의 안정적 커미트를 기반으로 빌드되었습니다. Hyperledger Fabric v1.0은 모듈 아키텍처를 구현하며 이 아키텍처는 엔터프라이즈 블록체인 네트워크 빌드를 위해 복원력이 높고 안전하고 사용자 정의 가능한 보안 플랫폼을 제공합니다.   
{: shortdesc}

**HSBN vNext Beta** 서비스는 단일 샌드박스 환경을 뛰어넘어 다양한 Bluemix 조직 전체로 확장되는 리소스 그룹이 포함된 분산 블록체인 네트워크를 제공하는 방향으로 발전하고 있습니다. 네트워크 아키텍처에 대한 자세한 정보는 [개요](v10_netoverview.html) 주제를 참조하십시오. 

## v1.0의 새 아키텍처
{:why}

Hyperledger Fabric 아키텍처는 보안, 확장성, 기밀성 및 성능에 초점을 맞춘 엔터프라이즈급 네트워크를 강화하도록 v1.0 버전에서 크게 발전했습니다. 피어는 **보증** 및 **커미트**라는 두 개의 고유 런타임으로 나뉘며 트랜잭션 순서 지정에 대한 책임은 별도의 컴포넌트로 추상화됩니다. 개인정보 보호정책 및 기밀성에 대한 우려는 데이터 분리를 제공하는 채널을 통해 해결됩니다. 원장은 피어 채널 기반에 존재하므로 쌍방, 다자간 또는 공용 트랜잭션의 다양한 조합을 지원하도록 네트워크를 사용자 정의할 수 있습니다. 

네트워크 토폴로지 및 상호작용에 대한 자세한 정보는 [Hyperledger 아키텍처 딥 다이브](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window} 섹션을 참조하십시오. 

## 추가 변경사항

HSBN vNext Beta 플랜에는 다음 변경사항도 포함됩니다. 
* [새 대시보드](v10_dashboard.html)를 통해 가입자는 블록체인 네트워크를 작성하고, 멤버를 초대하고, 다른 네트워크에 가입하고, 리소스 및 자산을 관리할 수 있습니다. 
* [v1.0용 새 Marbles 샘플 체인코드 애플리케이션](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window}은 최신 코드 베이스로 다양한 실험을 수행하도록 지원합니다. 
* Hyperledger Fabric v1.0의 새 [트랜잭션 플로우](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html)는 트랜잭션 프로세스 전체에서 다중 체크포인트를 구현하여 데이터 일관성 및 무결성을 보장합니다. 
