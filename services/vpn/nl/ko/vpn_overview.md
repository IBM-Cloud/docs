---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} 개요
{: #vpn_overview}  
*마지막 업데이트 날짜: 2016년 3월 17일*

{{site.data.keyword.vpn_full}}(VPN) 서비스는 IBM Bluemix&reg; 클라우드 환경에서 회사 데이터 센터와 사용자의 자원 사이에 보안 통신 채널을 제공합니다. 연결은 인터넷을 통해 설정됩니다.
{:shortdesc}

{{site.data.keyword.vpn_short}} 서비스는 다음과 같은 기능을 제공합니다.  
##보안 
IBM VPN 서비스는 산업 표준 IPSec(Internet Protocol Security) 프로토콜 스위트를 사용하여 회사 데이터 센터와 IBM Bluemix 클라우드 환경 간의 IP 통신을 인증하고 암호화합니다. IPSec은 네트워크 레벨의 피어 인증, 데이터 무결성 및 데이터 기밀성(암호화)을 제공합니다.

IBM VPN 서비스는 다음과 같은 IPSec 프로토콜을 지원 및 변환합니다.

* 인증 알고리즘:
	* HMAC-SHA1-96. 공유 키의 길이는 160비트(기본값)입니다.  
* 암호화 알고리즘:
	* 3DES-CBC. 공유 키의 길이는 192비트입니다.
	* AES-CBC. 공유 키의 길이는 128비트(기본값), 192비트, 256비트입니다.
* 인증 및 암호화 프로토콜:
	* AH(Authentication Header) 및 ESP(Encapsulating Security Payload) 프로토콜을 지원합니다. AH는 인증에만 사용됩니다. ESP는 인증과 암호화를 제공하는 데 사용됩니다.
* IKEv1 DH(Diffie-Hellman) 키 교환 그룹 2(기본값), 5, 14

IBM VPN 서비스는 IPSec 터널 모드를 지원합니다. 이 모드에서 IPSec은 전체 원래 IP 패킷을 보호합니다. IPSec은 패킷을 암호화하고, 패킷을 새 IP 패킷 내에 캡슐화하며, 새 패킷을 IPSec 피어로 전달합니다. 

IBM VPN 서비스는 Diffie-Hellman 키 교환 및 사전공유 키를 사용하여 두 피어 간의 연관을 보안합니다. 어느 한 쪽에서 사전공유 키를 제공하지 않으면 인증에 실패합니다. 
 
IBM VPN 서비스는 다음 IETF RFC를 준수합니다.

* IKEv1에 대해 RFC 2407, 2408, 2409
* IPv4 보안에 대해 RFC 4301   
* IPv4 AH에 대해 RFC 4302  
* IPv4 ESP(Encapsulating Security Payload)에 대해 RFC 4303  
* 인증에 대해 RFC 2104 HMAC 및 RFC 2404 HMAC-SHA-1-96  
* 암호화에 대해 RFC 2451 3DES-CBC, RFC 3602 AES128-CBC, AES192-CBC, AES256-CBC
##간편성
간편하고 직관적인 그래픽 인터페이스를 사용하여 IBM VPN 서비스를 작성할 수 있습니다. 사용 중인 게이트웨이 IP 주소와 데이터 센터 서브넷을 지정할 수 있습니다. 기본 IPSec 및 IKE 정책을 사용하거나 필요에 알맞도록 정책을 사용자 정의할 수 있습니다.  
##관리
그래픽 인터페이스, [명령행 인터페이스](../../cli/plugins/vpn/index.html) 또는 [API](https://new-console.ng.bluemix.net/apidocs/101)를 사용하여 IBM VPN 서비스를 관리할 수 있습니다.

