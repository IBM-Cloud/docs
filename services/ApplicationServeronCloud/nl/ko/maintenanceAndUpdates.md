---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 유지보수 및 VM 업데이트
{: #maintenance_and_vm_updates}

## 유지보수 전략
{: #maintenance_strategy}

IBM WebSphere Application Server for Bluemix는 현재 수정팩과 패치로 새 서비스 인스턴스가 작성될 수 있도록 정기적으로 업데이트됩니다. 미들웨어 관리 시
클라우드를 통해 새 서비스 인스턴스를 쉽고 빠르게 프로비저닝할 수 있습니다. 많은 소비자가
유지보수를 적용하려고 할 때 새 서비스 인스턴스로 업그레이드하려고 합니다. 장기 서비스
인스턴스를 보유하려는 해당 소비자의 경우 유지보수 저장소를 미들웨어 및 기본 운영
게스트에 사용할 수 있습니다. 사용자는 이러한 저장소를 사용하여 온프레미스와 마찬가지로 환경을
유지보수할 수 있습니다. 

## VM 업데이트

다음 섹션에서는 가상 머신 시스템 변경사항을 적용하는 방법에 대해 설명합니다.

다른 일반 RHEL 시스템과 같이 VM을 업데이트할 수 있습니다. Red Hat 패키지 관리자인
"Yum"을 사용하여 패키지와 같이 다른 여러 가지를 설치, 업데이트, 설치 제거 및 수행할 수
있습니다.

시스템은 IBM의 Red Hat Satellite 서버에서 이러한 업데이트를 수신하도록 설정됩니다. 이
위성은 Yum 패키지 관리자를 통해 Red Hat Network에서 안전한 패키지를
제공합니다. 

Satellite 서버는 IBM에서 관리하며 사용자의 시스템에서 수정할 수 없습니다. 

자세한 정보는 [Red Hat Enterprise Linux에서 패키지 업데이트 적용](https://access.redhat.com/articles/11258#rhel6){: new_window} 및 [Red Hat 패키지 관리자 Yum](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}을 참조하십시오. 
