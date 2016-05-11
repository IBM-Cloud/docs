---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 사내 구축형 구성 예
{:#onpremises}
*마지막 업데이트 날짜: 2016년 3월 17일*

사내 구축형 VPN 게이트웨이는 {{site.data.keyword.vpn_short}} 게이트웨이와 연결됩니다. 사용 중인 사내 구축형 게이트웨이의 구성을 수정해야 할 수도 있습니다.
{:shortdesc}

* [strongSwan과 함께 IBM VPN 구성](vpn_onpremises.html#strongswan)
* [Vyatta와 함께 IBM VPN 구성](vpn_onpremises.html#vyatta)
* [SoftLayer GaaS(Gateway Appliance Service)와 함께 IBM VPN 구성](vpn_onpremises.html#gaas)
* [Cisco ASA와 함께 IBM VPN 구성](vpn_onpremises.html#cisco)

##strongSwan과 함께 IBM VPN 서비스 구성
{: #strongswan} 

IBM VPN 설정에서는 다음과 같은 예의 구성을 사용합니다.

* 단일 컨테이너 서브넷: 172.31.0.0/16
* 컨테이너 그룹 서브넷: 172.30.0.0/16
* IBM VPN 게이트웨이 IP 주소: 134.168.8.164

사내 구축형 strongSwan 설정에서는 다음과 같은 예의 구성을 사용합니다.

* VPN 게이트웨이 IP 주소(고객 게이트웨이 IP): 169.55.254.166
* 엔드포인트가 연결되는 서브넷 주소(고객 서브넷): 10.121.33.192/26 

###strongSwan과 함께 IBM VPN 서비스를 사용하려면 다음과 같이 구성하십시오.

1. [게이트웨이를 구성하십시오](index.html#gateway).  
2. [사이트 연결을 구성하십시오](index.html#site).  
3. strongSwan을 구성하십시오.
	**참고:** 다음 예는 Ubuntu 14.10을 기반으로 합니다.  
	1. strongSwan을 설치하십시오.
		```
		root@rdmnm:~# sudo apt-get install strongswan  
		root@rdmnm:~# ipsec version  
		```
		{: codeblock}
		
		```
		Linux strongSwan U5.1.2/K3.13.0-55-generic  
		Institute for Internet Technologies and Applications  
		University of Applied Sciences Rapperswil, Switzerland  
		See 'ipsec --copyright' for copyright information.		
		```  
		{: screen}

	2. IPSec을 구성하십시오.  
		* /etc/ipsec.conf 파일을 편집하십시오.
			```
			root@rdmnm:~# more /etc/ipsec.conf  
						
			config setup
					  
			conn %default  
			 ikelifetime=60m  
			 keylife=20m  
			 rekeymargin=3m  
			 keyingtries=1  
			 mobike=no  
			 keyexchange=ikev1  
			 dpdaction=clear  
			 dpddelay=2s  
			include /etc/ipsec.all.conf  
			```
			{: codeblock}

		* /etc/ipsec.all.conf 파일을 추가하십시오.
			```
			root@rdmnm:~# more /etc/ipsec.all.conf  
							
			conn all  
			  auto=add  
			  esp=aes128-sha1-modp1024!  
			  ike=aes128-sha1-modp1024!  
			  right=134.168.8.164  
			  left=169.55.254.166  
			  leftauth=psk  
			  rightauth=psk  
			  rightsubnet=172.31.0.0/16,172.30.0.0/16  
			  leftsubnet=10.121.33.0/24  
			  rightid=%any  
			  leftid=169.55.254.166  
			  ikelifetime=3600s  
			  aggressive=no  
			  keyexchange=ikev1  
			  lifetime=3600s  
			  dpddelay=30s  
			  dpdaction=hold  
			  dpdtimeout=120s  
			```
			{: codeblock}

		* /etc/ipsec.secrets 파일을 편집하십시오. 
 
			```  
			root@rdmnm:~# more   /etc/ipsec.secrets  
				  : PSK "567890"
			```
			{: codeblock}

	3. IPSec을 다시 시작하십시오.

		```
		root@rdmnm:~# ipsec restart
		```  
		{: codeblock}

	4. 구성을 확인하십시오.
		* strongswan 서버에서 다음 명령을 실행하여 IPSec 상태를 확인하십시오.

			```  
			root@rdmnm:~# ipsec status
			```
			{: codeblock}

			```
			Security Associations (1 up, 0 connecting):
			         all[1914]: ESTABLISHED 48 minutes ago, 169.55.254.166[169.55.254.166]...134.168.8.164[134.168.8.164]
			         all{20}:  INSTALLED, TUNNEL, ESP in UDP SPIs: cb9c3056_i 1595f835_o
			         all{20}:   10.121.33.0/24 === 172.30.0.0/16 
			         all{19}:  INSTALLED, TUNNEL, ESP in UDP SPIs: c6e4ed78_i 8765e42d_o
			         all{19}:   10.121.33.0/24 === 172.31.0.0/16
			```
			{: screen}

		* IBM Bluemix 서비스 대시보드에서 IBM VPN IPSec 연결 상태를 확인하십시오. **VPN 사이트 연결** 섹션에서 상태 필드가 **ACTIVE**로 표시되어야 합니다.

	5. 필요한 경우, strongSwan syslog를 확인하십시오.

		```
		tail -f /var/log/syslog
		```
		{: codeblock}
		
		```
		Nov 25 08:03:40 rdmnm charon: 12[IKE] received draft-ietf-ipsec-nat-t-ike-03 vendor ID
		Nov 25 08:03:40 rdmnm charon: 12[IKE] received draft-ietf-ipsec-nat-t-ike-02\n vendor ID
		Nov 25 08:03:40 rdmnm charon: 12[IKE] received draft-ietf-ipsec-nat-t-ike-02 vendor ID
		Nov 25 08:03:40 rdmnm charon: 12[IKE] received draft-ietf-ipsec-nat-t-ike-00 vendor ID
		Nov 25 08:03:40 rdmnm charon: 12[IKE] 129.41.253.120 is initiating a Main Mode IKE_SA
		```
		{: screen}  

##Vyatta와 함께 IBM VPN 서비스 구성
{: #vyatta} 

IBM VPN 설정에서는 다음과 같은 예의 구성을 사용합니다.

* 단일 컨테이너 서브넷: 172.31.0.0/16
* 컨테이너 그룹 서브넷: 172.30.0.0/16
* IBM VPN 게이트웨이 IP 주소: 129.41.255.27

사내 구축형 Vyatta 설정에서는 다음과 같은 예의 구성을 사용합니다.

* VPN 게이트웨이 IP 주소(고객 게이트웨이 IP): 173.192.83.82
* 엔드포인트가 연결되는 서브넷 주소(고객 서브넷): 192.168.201.0/24 

###Vyatta와 함께 IBM VPN 서비스를 사용하려면 다음과 같이 구성하십시오.

1. [게이트웨이를 구성하십시오](index.html#gateway).
2. [사이트 연결을 구성하십시오](index.html#site). 
3. Vyatta를 구성하십시오.  

	1. SSH를 사용하여 Vyatta 어플라이언스에 로그인하십시오.
		```
		ssh vyatta@173.192.83.82  
		vyatta@vpn:~$ show version  
		```
		{: codeblock}
		
		```
		Version:      VSE6.7R7  
		Description:  Brocade Vyatta 5415 vRouter 6.7 R7  
		Copyright:    2006-2015 Vyatta, Inc.  
		Built by:     autobuild@vyatta.com  
		Built on:     Thu Mar 26 23:12:48 UTC 2015  
		Build ID:     1503262314-56309bf  
		System type:  Intel 64bit  
		Boot via:     image  
		HW model:     X9SCI/X9SCA  
		HW S/N:       0123456789  
		HW UUID:      002590D2-A0A8-0607-0025-90D2A0A80E0F  
		Uptime:       20:12:17 up 2 days, 23:28,  2 users,  load average: 0.33, 0.27, 0.24  
		```  
		{: screen}

	2. 구성 모드로 들어가십시오.
		```
		vyatta@vyatta: configure
		vyatta@vyatta#
		```  
		{: codeblock}

	3. 인터페이스 결합 IP 주소를 구성하십시오.
		```
		Set interface bonding bond0 address 192.168.201.2/24
		Set interface bonding bond1 address 173.192.83.82/29
		```  
		{: codeblock}

	4. bond1에서 VPN을 사용으로 설정하십시오.
		```
		set vpn ipsec ipsec-interfaces interface bond1
		```  
		{: codeblock}

	5. IKE 그룹을 구성하십시오.
		```
		set vpn ipsec ike-group bm-ike lifetime 28800  
		set vpn ipsec ike-group bm-ike proposal 1 dh-group 2  
		set vpn ipsec ike-group bm-ike proposal 1 encryption aes128  
		set vpn ipsec ike-group bm-ike proposal 1 hash sha1  
		```  
		{: codeblock}

	6. ESP 그룹을 구성하십시오.
		```
		set vpn ipsec esp-group bm-esp compression disable  
		set vpn ipsec esp-group bm-esp lifetime 3600  
		set vpn ipsec esp-group bm-esp mode tunnel  
		set vpn ipsec esp-group bm-esp pfs dh-group2  
		set vpn ipsec esp-group bm-esp proposal 2 encryption aes128  
		set vpn ipsec esp-group bm-esp proposal 2 hash sha1  
		```  
		{: codeblock}

	7. 원격 사이트와의 연결을 설정하십시오.
		```
		set vpn ipsec site-to-site peer 129.41.255.27 authentication id 173.192.83.82  
		set vpn ipsec site-to-site peer 129.41.255.27 authentication remote-id 129.41.255.27  
		set vpn ipsec site-to-site peer 129.41.255.27 authentication mode pre-shared-secret  
		set vpn ipsec site-to-site peer 129.41.255.27 authentication pre-shared-secret 567890  
		set vpn ipsec site-to-site peer 129.41.255.27 connection-type response  
		set vpn ipsec site-to-site peer 129.41.255.27 default-esp-group bm-esp  
		set vpn ipsec site-to-site peer 129.41.255.27 ike-group bm-ike  
		set vpn ipsec site-to-site peer 129.41.255.27 local-address any  
		set vpn ipsec site-to-site peer 129.41.255.27 tunnel 1 local prefix 192.168.201.0/24  
		set vpn ipsec site-to-site peer 129.41.255.27 tunnel 1 remote prefix 172.31.0.0/16  
		```
		{: codeblock}

		```
		여기서  
			129.41.255.27은 IBM 게이트웨이입니다.  
			172.31.0.0/16은 IBM 게이트웨이 뒤에 있는 컨테이너 서브넷입니다.
		```
		{: screen}

	8. 구성을 커미트 및 확인하십시오.
		```  
		vyatta@vpn# show vpn  
		```
		{: codeblock}

		```
		 ipsec {
		     esp-group bm-esp {
		         compression disable
		         lifetime 3600
		         mode tunnel
		         pfs dh-group2
		         proposal 2 {
		             encryption aes128
		             hash sha1
		         }
		     }
		     ike-group bm-ike {
		         lifetime 28800
		         proposal 1 {
		             dh-group 2
		             encryption aes128
		             hash sha1
		         }
		     }
		     ipsec-interfaces {
		         interface bond1
		     }
		     nat-networks {
		     }
		     site-to-site {
		         peer 129.41.255.27 {
		             authentication {
		                 id 173.192.83.82
		                 mode pre-shared-secret
		                 pre-shared-secret 567890
		                 remote-id 129.41.255.27
		             }
		             connection-type initiate
		             default-esp-group bm-esp
		             ike-group bm-ike
		             local-address any
		             tunnel 1 {
		                 local {
		                     prefix 192.168.201.0/24
		                 }
		                 remote {
		                     prefix 172.31.0.0/16
		                 }
		             }
		         }
		     }
		 }
		[edit]
		```
		{: screen}

		```
		vyatta@vpn# commit
		vyatta@vpn# confirm   
		```
		{: codeblock}

	9. 구성을 검증하십시오.
		```
		vyatta@vpn:~$ show vpn  ipsec status  
		```
		{: codeblock}

		```
		IPSec Process Running PID: 5633  
		  
		1 Active IPsec Tunnels  
		  
		IPsec Interfaces :  
		        bond1   (no IP on interface statically configured as local-ip for any VPN peer)  
		```
		{: screen}

		```
		vyatta@vpn:~$ show vpn  ipsec policy  
		```
		{: codeblock}

		```
		src 192.168.201.0/24 dst 172.31.0.0/16   
		        dir out priority 1891 ptype main  
		        tmpl src 173.192.83.82 dst 129.41.255.27  
		                proto esp reqid 16384 mode tunnel  
		src 172.31.0.0/16 dst 192.168.201.0/24  
		        dir fwd priority 1891 ptype main  
		        tmpl src 129.41.255.27 dst 173.192.83.82  
			                proto esp reqid 16384 mode tunnel  
		src 172.31.0.0/16 dst 192.168.201.0/24  
		        dir in priority 1891 ptype main   
		        tmpl src 129.41.255.27 dst 173.192.83.82  
		                proto esp reqid 16384 mode tunnel  
		src ::/0 dst ::/0  
		        socket out priority 0 ptype main  
		src ::/0 dst ::/0  
		        socket in priority 0 ptype main  
		src ::/0 dst ::/0  
		        socket out priority 0 ptype main  
		src ::/0 dst ::/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main   
		vyatta@vpn:~$   
		```
		{: screen}

		```
		vyatta@vpn:~$ show vpn ipsec sa   
		```
		{: codeblock}

		```
		Peer ID / IP							Local ID / IP               
		------------  							-------------
		129.41.255.27                           173.192.83.82                          
		  
		Tunnel  State  Bytes Out/In   Encrypt  Hash  NAT-T  A-Time  L-Time  Proto
		------  -----  -------------  -------  ----  -----  ------  ------  -----
		1       up     0.0/0.0        aes128   sha1  no     1359    3600    all  
		```  
		{: screen}

	10. IBM VPN 서비스 연결 상태를 확인하십시오.

		IBM Bluemix 서비스 대시보드에서 IBM VPN IPSec 연결 상태를 확인하십시오. **VPN 사이트 연결** 섹션에서 상태 필드가 **ACTIVE**로 표시되어야 합니다.

	11. 필요한 경우 Vyatta syslog를 확인하십시오.
		
		```
		vyatta@vpn# run show log vpn ipsec 
		```
		{: codeblock}

		```
		Nov 19 00:26:07 vpn pluto[5876]: failed to load pkcs11 module '/usr/lib/opensc-pkcs11.so'
		Nov 19 00:26:07 vpn pluto[5876]: including NAT-Traversal patch (Version 0.6c) [disabled]
		Nov 19 00:26:07 vpn pluto[5876]: loaded plugins: test-vectors curl ldap aes des sha1 sha2 md5 random x509 pkcs1 pgp dnskey pem openssl gmp hmac xauth attr kernel-netlink resolve 
		Nov 19 00:26:07 vpn pluto[5876]: fe80::200:5eff:fe00:101
		Nov 19 00:26:07 vpn pluto[5876]: 10.41.203.130
		Nov 19 00:26:07 vpn pluto[5876]: bond0v1
		Nov 19 00:26:07 vpn pluto[5876]: fe80::200:5eff:fe00:101
		Nov 19 00:26:07 vpn pluto[5876]: 173.192.83.86
		```
		{: screen}  

##SoftLayer GaaS(Gateway Appliance Service)와 함께 IBM VPN 서비스 구성
{: #gaas} 

IBM VPN 설정에서는 다음과 같은 예의 구성을 사용합니다.

* 단일 컨테이너 서브넷: 172.31.0.0/16
* 컨테이너 그룹 서브넷: 172.30.0.0/16
* IBM VPN 게이트웨이 IP 주소: 134.168.0.244

사내 구축형 SoftLayer GaaS 설정에서는 다음과 같은 예의 구성을 사용합니다.

* VPN 게이트웨이 IP 주소(고객 게이트웨이 IP): 75.126.122.46
* 엔드포인트가 연결되는 서브넷 주소(고객 서브넷): 10.86.88.128/26
* 사전공유 키 문자열: 567890 

###SoftLayer GaaS와 함께 IBM VPN 서비스를 사용하려면 다음과 같이 구성하십시오.

1. SoftLayer GaaS를 구성하십시오.

	1. [https://gateway-as-a-service.com/gaas/ui/](https://gateway-as-a-service.com/gaas/ui/)를 여십시오.  
	2. SoftLayer 계정 신임 정보를 사용하여 로그인하십시오. **게이트웨이 관리** 페이지가 표시됩니다. 
	3. 구성할 게이트웨이에 대해 **터널 관리** 조치를 선택하십시오. **게이트웨이 터널 구성 관리** 페이지가 표시됩니다. 
	4. **터널 추가**를 선택하십시오. 후속 페이지에서 게이트웨이 및 네트워크 세부사항이 필요합니다. 
	5. 기본 게이트웨이와 네트워크 구성을 변경하지 마십시오. **다음**을 선택하십시오.
	6. 사내 구축형 서브넷의 경우 **VLAN 유형**을 개인용으로 설정하십시오. **다음**을 선택하십시오.  
	7. 네트워크 구성 세부사항을 다음과 같이 편집하십시오.  
		* 사내 구축형 게이트웨이의 공용 IP 주소: IBM VPN 게이트웨이 공용 IP 주소를 입력하십시오.  
		* 사내 구축형 서브넷: IBM VPN 게이트웨이 서브넷을 입력하십시오.  
		* GRE 터널 서브넷 주소를 삭제하십시오.   
		* **고급 IPSec 구성**을 선택하십시오. 다음과 같이 구성하십시오.  
			* IPSec 암호화: aes-128  
			* Diffie-Hellman 그룹: 2  
			* ESP - PFS(Perfect Forward Security): 사용  
			* 사전공유 시크릿: IBM VPN 구성 시 사용한 사전공유 비밀 키를 입력하십시오.  
		* **다음**을 선택하십시오.
	8. 방화벽 구역과 **고급 방화벽 구성** 옵션을 선택하십시오. **다음**을 선택하십시오.  
	9. 게이트웨이 구성 겹쳐쓰기에 동의하는 선택란을 선택하십시오.
	10. **다음**을 선택하십시오.  
	11. **완료**를 선택하십시오. **미해결 요청 보기** 페이지가 표시됩니다.   
	12. 요청 상태를 보려면 **세부사항** 단추를 선택하십시오. **요청 세부사항 보기** 페이지가 표시됩니다. 
	13. 모든 구성 매개변수의 상태가 완료로 표시될 때까지 기다리십시오.  
2. [게이트웨이를 구성하십시오](index.html#gateway).
3. [사이트 연결을 구성하십시오](index.html#site).
4. 구성을 검증하십시오.
	1. Vyatta에서 다음 명령을 실행하여 IPSec 연결 상태를 확인하십시오.
		```
		vyatta@gateway# run show vpn ipsec sa
		```
		{: codeblock}

		```
		Peer ID / IP                            Local ID / IP               
		------------                            -------------
		134.168.0.224                           75.126.122.46                          
		
		    Tunnel  State  Bytes Out/In   Encrypt  Hash  NAT-T  A-Time  L-Time  Proto
		    ------  -----  -------------  -------  ----  -----  ------  ------  -----
		    1       up     0.0/0.0        aes128   sha1  yes    978     3600    all
		    2       up     0.0/0.0        aes128   sha1  yes    768     3600    all

		[edit]
		```
		{: screen}

		```
		vyatta@gateway# run show vpn ipsec policy 
		```
		{: codeblock}

		```
		src 10.86.88.128/26 dst 172.31.0.0/16 
		        dir out priority 1883 ptype main 
		        tmpl src 75.126.122.46 dst 134.168.0.224
		                proto esp reqid 16384 mode tunnel
		src 172.31.0.0/16 dst 10.86.88.128/26 
		        dir fwd priority 1883 ptype main 
		        tmpl src 134.168.0.224 dst 75.126.122.46
		                proto esp reqid 16384 mode tunnel
		src 172.31.0.0/16 dst 10.86.88.128/26 
		        dir in priority 1883 ptype main 
		        tmpl src 134.168.0.224 dst 75.126.122.46
		                proto esp reqid 16384 mode tunnel
		src 10.86.88.128/26 dst 172.30.0.0/16 
		        dir out priority 1883 ptype main 
		        tmpl src 75.126.122.46 dst 134.168.0.224
		                proto esp reqid 16388 mode tunnel
		src 172.30.0.0/16 dst 10.86.88.128/26 
		        dir fwd priority 1883 ptype main 
		        tmpl src 134.168.0.224 dst 75.126.122.46
		                proto esp reqid 16388 mode tunnel
		src 172.30.0.0/16 dst 10.86.88.128/26 
		        dir in priority 1883 ptype main 
		        tmpl src 134.168.0.224 dst 75.126.122.46
		                proto esp reqid 16388 mode tunnel
		src ::/0 dst ::/0 
		        socket out priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket in priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket out priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket in priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket out priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket in priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket out priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket in priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main
		```
		{: screen}

		```
		vyatta@gateway# run ping 172.31.0.1 interface 10.86.88.129
		```
		{: codeblock}

		```
		PING 172.31.0.1 (172.31.0.1) from 10.86.88.129 : 56(84) bytes of data.
		64 bytes from 172.31.0.1: icmp_req=1 ttl=64 time=1.99 ms
		64 bytes from 172.31.0.1: icmp_req=2 ttl=64 time=1.79 ms
		^C
		--- 172.31.0.1 ping statistics ---
		2 packets transmitted, 2 received, 0% packet loss, time 1001ms
		rtt min/avg/max/mdev = 1.794/1.896/1.998/0.102 ms
		```
		{: screen}

	2. IBM Bluemix 서비스 대시보드에서 IBM VPN IPSec 연결 상태를 확인하십시오. **VPN 사이트 연결** 섹션에서 상태 필드가 **ACTIVE**로 표시되어야 합니다.  
5. 필요한 경우 Vyatta syslog를 확인하십시오.  

	```
	vyatta@gateway# tail -f /var/log/messages 
	```
	{: codeblock}

	```
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-1" #1: Peer ID is ID_IPV4_ADDR: '134.168.0.224'
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-1" #1: ISAKMP SA established
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-2" #5: initiating Quick Mode PSK+ENCRYPT+TUNNEL+PFS+UP {using isakmp#1}
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-1" #6: initiating Quick Mode PSK+ENCRYPT+TUNNEL+PFS+UP {using isakmp#1}
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-2" #5: sent QI2, IPsec SA established {ESP=>0x03d9db46 <0xcb02ea03 NATOA=0.0.0.0}
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-1" #6: sent QI2, IPsec SA established {ESP=>0x21605ff5 <0xc69ae517 NATOA=0.0.0.0}
	Dec  4 08:03:33 gateway Keepalived_vrrp: Warning: Failed to connect to the agentx master agent ([NIL]): 
	Dec  4 08:04:34 gateway Keepalived_vrrp: last message repeated 9 times
	Dec  4 08:05:34 gateway Keepalived_vrrp: last message repeated 8 times
	Dec  4 08:06:34 gateway Keepalived_vrrp: last message repeated 8 times
	```
	{: screen}

##Cisco ASA와 함께 IBM VPN 서비스 구성
{: #cisco}

IBM VPN 설정에서는 다음과 같은 예의 구성을 사용합니다.

* 단일 컨테이너 서브넷: 172.31.0.0/16
* 컨테이너 그룹 서브넷: 172.30.0.0/16
* IBM VPN 게이트웨이 IP 주소: 134.168.6.5

사내 구축형 설정에서는 다음과 같은 예의 구성을 사용합니다.

* VPN 게이트웨이 IP 주소(고객 게이트웨이 IP): 62.95.35.53
* 엔드포인트가 연결되는 서브넷 주소(고객 서브넷): 10.2.0.0/16

###Cisco ASA와 함께 IBM VPN 서비스를 사용하려면 다음과 같이 구성하십시오.

1. [게이트웨이를 구성하십시오](index.html#gateway).
2. [사이트 연결을 구성하십시오](index.html#site).
3. Cisco ASA를 구성하십시오. 다음 구성 예를 참조하십시오.
		
		object network 10.2-network 
		 subnet 10.2.0.0 255.255.0.0
		http 10.2.0.0 255.255.0.0 inside
		ssh 10.2.0.0 255.255.0.0 inside
		
		interface Ethernet0/0
		 nameif outside
		 security-level 0
		 ip address 62.95.35.53 255.255.255.248 
		
		object network A_62.95.35.53 
		 host 62.95.35.53
		
		access-list out-in extended permit gre any host 62.95.35.53 
		access-list out-in extended permit tcp any host 62.95.35.53 eq pptp 
		access-list outside_1_cryptomap extended permit ip object 10.2-network 
		object network NETWORK_OBJ_172.31.0.0_16 
		 subnet 172.31.0.0 255.255.0.0
		object network Bluemix31 
		 subnet 172.31.0.0 255.255.0.0
		 description Bluemix 172.31.0.0 VPN 
		
		nat (inside,outside) source static 10.2-network 10.2-network destination static NETWORK_OBJ_172.31.0.0_16 NETWORK_OBJ_172.31.0.0_16
		nat (outside,inside) source static NETWORK_OBJ_172.31.0.0_16 NETWORK_OBJ_172.31.0.0_16 destination static 10.2-network 10.2-network
		
		crypto ipsec transform-set ESP-AES-256-MD5 esp-aes-256 esp-md5-hmac 
		crypto ipsec security-association lifetime seconds 28800
		crypto ipsec security-association lifetime kilobytes 4608000
		crypto map outside_map0 1 set transform-set ESP-AES-128-SHA
		crypto map outside_map 1 match address outside_1_cryptomap
		crypto map outside_map 1 set pfs group5
		crypto map outside_map 1 set peer 134.168.6.5 
		crypto map outside_map 1 set transform-set ESP-AES-128-SHA
		crypto map outside_map 1 set nat-t-disable
		crypto map outside_map interface outside
		crypto isakmp identity address
		crypto isakmp enable outside
		crypto isakmp policy 1
		 authentication pre-share
		 encryption aes
		 hash sha
		 group 1
		 lifetime 86400
		
		group-policy IPsec internal
		group-policy IPsec attributes
		 vpn-tunnel-protocol IPSec l2tp-ipsec 
		
		tunnel-group 134.168.6.5 type ipsec-l2l
		tunnel-group 134.168.6.5 general-attributes
		 default-group-policy IPsec
		tunnel-group 134.168.6.5 ipsec-attributes
		 pre-shared-key bluemix

