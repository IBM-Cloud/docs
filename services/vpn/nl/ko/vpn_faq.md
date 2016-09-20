---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} FAQ
{: #vpn_faq}
*마지막 업데이트 날짜: 2016년 3월 17일*

다음은 자주 묻는 질문입니다.
{:shortdesc}

1. IBM Lab에서 IBM VPN 서비스와 상호 운용성이 있다고 인증한 써드파티 벤더의 디바이스는 무엇입니까?

	IBM Lab은 IBM VPN 서비스와의 상호 운용성에 대해 다음과 같은 VPN 게이트웨이 디바이스를 테스트했습니다.

	* Cisco Adaptive Security Appliance(ASA) 소프트웨어 버전 8.2(1). [구성 예 참조](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7. [구성 예 참조](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic. [구성 예 참조](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic. [구성 예 참조](vpn_onpremises.html#strongswan){: new_window}

	또한 기타 벤더의 IPSec 표준과 호환되는 VPN 게이트웨이 디바이스도 IBM VPN 서비스와 원활하게 작동합니다.

2. 피어 장애를 발견하는 주기는 어느 정도입니까?
 
	장애가 있는 피어는 구성된 keepalive 제한시간 값에 따라 발견됩니다. 기본 설정은 60초입니다.

3. VPN 서비스당 작성할 수 있는 VPN 게이트웨이와 연결의 수는 몇 개입니까?
 
	Bluemix 영역에서는 VPN 서비스당 하나의 VPN 게이트웨이 어플라이언스를 작성할 수 있습니다. VPN 게이트웨이당 최대 16개의 연결을 다른 대상으로 정의할 수 있습니다. 

4. IBM VPN 서비스와 Bluemix Secure Gateway 서비스를 언제 사용해야 합니까?

	두 서비스는 Bluemix 자원과 사내 구축형 데이터 센터 간의 보안 연결을 제공하는 데 사용됩니다. 

	임의의 두 엔드포인트 간에 연결을 해야 하는 경우에는 IBM VPN 서비스를 사용하십시오. VPN 서비스는 사내 구축형 네트워크 및 IBM Bluemix 클라우드 환경 간 안전한 Layer 3 IPSec 연결을 구성합니다. IBM 컨테이너(Docker 컨테이너)에 안전하게 액세스하는 데만 IBM VPN 서비스를 사용할 수 있습니다. 

	Bluemix의 특정 애플리케이션 엔드포인트에서 사내 구축형 데이터 센터 내부의 다른 엔드포인트에 보안 연결을 하려는 경우 Bluemix Secure Gateway 서비스를 사용하십시오. 

5. 개인용 IP 주소를 사용하여 IBM Bluemix 클라우드 환경 내부의 가상 서버 및 내 컨테이너에 액세스하도록 IBM VPN 서비스를 사용할 수 있습니까?
 
	현재 IBM VPN 서비스는 Bluemix 컨테이너에 액세스하는 데만 사용 가능합니다.

6. Bluemix 조직 레벨에서 IBM VPN 서비스를 정의할 수 있습니까?

	현재 IBM VPN 서비스는 Bluemix 영역 레벨에만 사용 가능합니다. Bluemix 조직에 여러 개의 영역이 있으면 각 영역에 대해 별도 VPN 서비스를 정의할 수 있습니다.

7. IBM VPN 서비스를 SoftLayer GaaS(Gateway Appliance Service)와 연결하는 방법은 무엇입니까?

	IPSec 터널을 빌드하여 IBM VPN 서비스 및 SoftLayer GaaS 간의 보안 통신을 설정할 수 있습니다. [구성 예를 참조하십시오.](vpn_onpremises.html#gaas){: new_window}
