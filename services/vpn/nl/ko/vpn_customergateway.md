---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 데이터 센터 또는 SoftLayer 서버에서 게이트웨이 구성
{: #vpn_yourdatacenter}
*마지막 업데이트 날짜: 2016년 3월 17일*

{{site.data.keyword.vpn_short}} 서비스와의 보안 연결을 구성하려면 데이터 센터 또는 SoftLayer 서버에 IPSec VPN 게이트웨이가 필요합니다. 데이터 센터 또는 SoftLayer 서버에서 다음과 같이 VPN 게이트웨이를 구성해야 합니다.

* VPN 게이트웨이가 NAT(Network Address Translation) 뒤에 있는 경우에만 VPN 게이트웨이에서 NAT 순회를 사용하십시오. 
* IBM VPN 서비스 구성에 사용한 것과 동일한 사전공유 키를 사용하십시오.
* 다음 서브넷을 원격 서브넷으로 추가하십시오.
	* IBM Bluemix 영역에서 단일 컨테이너를 작성한 경우 172.31.0.0/16을 추가하십시오.
	* IBM Bluemix 영역에서 컨테이너 그룹을 작성한 경우 172.30.0.0/16을 추가하십시오.
	* IBM Bluemix 영역에서 단일 컨테이너와 컨테이너 그룹을 작성한 경우 172.31.0.0/16 및 172.30.0.0/16을 추가하십시오.
* 암호화, 인증 및 PFS 그룹 설정이 IBM VPN 게이트웨이 및 사용자의 VPN 게이트웨이에서 동일한지 확인하십시오.
