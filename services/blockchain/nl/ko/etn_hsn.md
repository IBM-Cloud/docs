---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 고급 보안 비즈니스 네트워크
{: #etn_overview}


IBM Blockchain 고급 보안 비즈니스 네트워크는 격리된 고급 보안 환경에서 실행되며 바로 이 점이 다른 클라우드 호스팅 오퍼링과 구분되는 특징입니다. 운영 체제, 패브릭 및 노드는 모두 IBM Secure Service Container에 존재하며, 엔터프라이즈 고객이 z Systems 기술에서 기대하게 되는 수준의 보안성과 견고함을 제공합니다. IBM Secure Service Container는 피어 투 피어 통신을 위한 성능 최적화, 가용성, 확장성, 하드웨어 암호화, 변조 방지 암호화 키는 물론 보안 암호화된 VM도 제공합니다.   
{:shortdesc}

환경(LinuxONE on z)은 애플리케이션 컨테이너에서 실행 중인 멤버십 서비스가 사용되는 4-피어 네트워크 구현 PBFT로 구성되어 있습니다. 애플리케이션 컨테이너는 시스템 내에서 실행 중인 블록체인 소프트웨어, 체인코드 및 데이터를 보호합니다. 보안 부트 내의 블록체인 소프트웨어를 서명하고 인증하며 암호화할 수 있습니다. 그리고 일단 애플리케이션 컨테이너에 설치되면 변조 방지가 작동됩니다. 플랫폼의 루트 사용자와 시스템 관리자는 보안 컨테이너 컨텐츠에 액세스하거나 이를 볼 수 없습니다. LinuxONE on z는 FIPS 준수, 고급 평가 보증 등급(EAL) 보안, 고급 감사 가능 운영 환경 및 암호 최적화를 제공합니다.

보안 기능에 대한 세부사항은 [IBM Secure Service Container](etn_ssc.html) 섹션을 참조하십시오.
