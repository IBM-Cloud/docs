---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} 시작하기
{: #vpn}  
*마지막 업데이트 날짜: 2016년 3월 9일*

Bluemix&reg;용 {{site.data.keyword.vpn_full}} 서비스는 IBM Bluemix 클라우드 환경 내의 IBM Containers(Docker 컨테이너)에 안전하게 액세스하려고 사용할 수 있습니다. 회사 데이터 센터의 확장으로서 IBM Bluemix 클라우드 환경을 사용할 수 있습니다. IBM VPN 서비스를 사용하여 SoftLayer 서버와 연결할 수도 있습니다.
{:shortdesc}

시작하기 전에 IBM Docker 컨테이너를 사용할 준비가 되었는지 확인하십시오. IBM Containers의 작성 및 관리 방법에 대한 자세한 정보는 [IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html)를 참조하십시오.  

시작하려면 Bluemix 대시보드에서 **가상 사설망(VPN)** 서비스 인스턴스 타일을 선택하십시오. 다음 단계를 완료하십시오.

1. **게이트웨이 작성**을 선택하여 {{site.data.keyword.vpn_short}} 게이트웨이를 구성하십시오. 기본 게이트웨이가 작성됩니다. 필요하면 다음 단계에 표시된 것처럼 게이트웨이 구성을 편집하십시오.
{: #gateway}  

  1. **편집**을 선택하십시오.  
  2. 게이트웨이 이름을 지정하십시오.  
  3. VPN 서비스를 사용하려는 컨테이너 또는 컨테이너 그룹을 선택하십시오.
 **참고:** VPN 연결을 통해 컨테이너 및 컨테이너 그룹 개인용 서브넷에 액세스할 수 있도록 컨테이너 및 컨테이너 그룹 개인용 서브넷을 미리 선택합니다.
  4. **저장**을 선택하십시오.  

 기본 IKE 및 IPSec 정책을 사용하거나 사용자 정의 정책을 구성할 수 있습니다. 기본 정책을 사용하려면 4단계로 건너뛰십시오.

2. **IKE & IPSec 정책** 탭을 선택하여 IKE 정책을 구성하십시오.
  1. **새로 추가**를 선택하십시오.  
  2. 다음 세부사항을 지정하십시오.
	* **이름**: IKE 정책의 이름
	* **권한 알고리즘**: sha1이며 변경할 수 없음  
	* **암호화 알고리즘**: 드롭 다운에서 선택하십시오. 값: aes-128(기본값), aes-192, aes-256, 3des
	* **키 수명**: IKE SA(Security Association)의 수명 값(초). 범위: 60-86400. 기본값: 86400
	* **PFS**: DH(Diffie-Hellman) 그룹 ID. 값: Group2, Group5, Group14. 기본값: Group2
	* **협상 모드**: Main이며 변경할 수 없음
	* **버전**: IKEV1이며 변경할 수 없음
  3. **저장**을 선택하십시오.

3. IPSec 정책을 구성하십시오.
  1. **새로 추가**를 선택하십시오.  
  2. 다음 세부사항을 지정하십시오.
  	* **이름**: IPSec 정책의 이름  
  	* **권한 알고리즘**: sha1이며 변경할 수 없음  
  	* **암호화 알고리즘**: 드롭 다운에서 선택하십시오. 값: aes-128(기본값), aes-192, aes-256, 3des
  	* **키 수명**: SA(Security Association)의 수명 값(초). 범위: 60-86400. 기본값: 3600
  	* **PFS**: DH(Diffie-Hellman) 그룹 ID. 값: Group2, Group5, Group14. 기본값: Group2
  	* **변환 프로토콜**: ESP이며 변경할 수 없음
  	* **캡슐화 모드**: Tunnel이며 변경할 수 없음
  3. **저장**을 선택하십시오.  

4. 데이터 센터 또는 SoftLayer 서버 VPN 게이트웨이와 IBM VPN 게이트웨이 간의 연결을 설정하는 세부사항을 제공하십시오.
{: #site}  

  1. **게이트웨이 어플라이언스** 탭을 선택하십시오.
  2. **사이트 연결** 섹션에서 **연결 작성**을 선택하십시오.
  3. 다음 사이트 연결 세부사항을 지정하십시오.  
  	* **이름**: 연결 이름  
  	* **설명**: 연결에 대한 설명(선택사항)  
  	* **사전공유 키 문자열**: 인증에 사용될 사전공유 (시크릿) 키
  	* **관리 상태**: VPN 연결 상태. 드롭 다운에서 UP 또는 DOWN을 선택하십시오. 기본값: UP  
  	* **고객 게이트웨이 IP**: VPN 터널의 원격 엔드포인트 IP 주소  
  	* **고객 서브넷**: CIDR 형식의 원격 서브넷 주소. 다른 서브넷을 추가하려면 더하기 부호를 선택하십시오.
  4. (선택사항) 다음 **고급 설정** 매개변수를 구성하십시오.  
  	* **IKE 정책**: IKE 정책을 선택하십시오.  
  	* **활성 상태 지속 간격**: 활성 상태 지속 간격(초). 구성된 간격으로 활성 상태 지속 메시지를 보내 피어의 활성 여부를 확인합니다. 기본값: 15. 범위: 5-86399
  	* **작동 중지된 피어에 대한 조치**: 피어가 작동 중지로 발견되는 경우 수행해야 하는 조치.
     값: 
  		* hold(기본값): SA(Security Association)가 보류됨 
  		* clear: SA가 삭제됨
  		* disabled: SA를 사용 안함
  		* restart: SA가 재협상됨
  		* restart-by-peer: 작동 중지된 피어의 모든 SA가 재협상됨  
  	* **IPSec 정책**: IPSec 정책을 선택하십시오.
  	* **활성 상태 지속 제한시간**: 세션이 종료되는 제한시간 값(초). 기본값: 120. 범위: 6-86400. 활성 상태 지속 제한시간 값은 활성 상태 지속 간격 값보다 커야 합니다.
  5. **저장**을 선택하십시오.

  **참고:** 연결 중인 경우 연결 상태는 ***작성 보류 중***으로 표시됩니다. 이 상태가 표시되는 경우 연결 활성 상태를 보려면 화면을 몇 번 새로 고치십시오.

**중요:** 웹 애플리케이션을 사용 중인 경우 사용하고 있는 Docker 컨테이너에 웹 애플리케이션을 바인드해야 합니다. 트래픽이 IPSec VPN 터널을 통과하려면 이 바인딩이 필요합니다.

**중요:** IBM VPN 서비스는 현재 응답자 모드에서 작동합니다. VPN 연결을 시작하려면 데이터 패킷이 IBM VPN 게이트웨이에서 사내 구축형 데이터 센터 또는 SoftLayer 서버로 이동해야 합니다. VPN 연결이 설정되면 트래픽은 VPN 연결의 엔드포인트 간에 어느 한 방향으로 이동할 수 있습니다.

 
# 재링크
## 샘플 
{: #samples}  
* [사내 구축형 strongSwan 게이트웨이 구성 예](vpn_onpremises.html#strongswan){: new_window}
* [사내 구축형 Vyatta 게이트웨이 구성 예](vpn_onpremises.html#vyatta){: new_window}
* [사내 구축형 SoftLayer GaaS(Gateway Appliance Service) 구성 예](vpn_onpremises.html#gaas){: new_window}
* [사내 구축형 Cisco ASA 구성 예](vpn_onpremises.html#cisco){: new_window}

## api  
{: #api}  
* [IBM VPN RESTful API](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## 일반  
{: #general}  
* [IBM VPN 명령행 인터페이스](../../cli/plugins/vpn/index.html){: new_window}
* [IBM VPN FAQ](vpn_faq.html#vpn_faq){: new_window}
* [IBM Bluemix 가격 책정 시트](https://console.{DomainName}/pricing/){: new_window}
* [IBM Bluemix 필수 소프트웨어](https://developer.ibm.com/bluemix/support/#prereqs)
