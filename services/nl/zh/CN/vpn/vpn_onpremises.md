---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 内部部署配置示例
{:#onpremises}
*上次更新时间：2016 年 3 月 17 日*

内部部署 VPN 网关与 {{site.data.keyword.vpn_short}} 网关相连。您可能需要修改所用的内部部署网关的配置。
{:shortdesc}

* [使用 strongSwan 配置 IBM VPN](vpn_onpremises.html#strongswan)
* [使用 Vyatta 配置 IBM VPN](vpn_onpremises.html#vyatta)
* [使用 SoftLayer Gateway Appliance Service (GaaS) 配置 IBM VPN](vpn_onpremises.html#gaas)
* [使用 Cisco ASA 配置 IBM VPN](vpn_onpremises.html#cisco)

##使用 strongSwan 配置 IBM VPN 服务
{: #strongswan} 

IBM VPN 设置使用以下示例配置：

* 单个容器子网：172.31.0.0/16
* 容器组子网：172.30.0.0/16
* IBM VPN 网关 IP 地址：134.168.8.164

内部部署 strongSwan 设置使用以下示例配置：

* VPN 网关 IP 地址（客户网关 IP）：169.55.254.166
* 与端点相连的子网地址（客户子网）：10.121.33.192/26 

###要搭配使用 IBM VPN 服务与 strongSwan，请按如下所示进行配置：

1. [配置网关](index.html#gateway)。  
2. [配置站点连接](index.html#site)。  
3. 配置 strongSwan。
	**注：**以下示例基于 Ubuntu 14.10。  
	1. 安装 strongSwan：
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

	2. 配置 IPSec：  
		* 编辑文件：/etc/ipsec.conf
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

		* 添加文件：/etc/ipsec.all.conf
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

		* 编辑文件：/etc/ipsec.secrets 
 
			```  
			root@rdmnm:~# more   /etc/ipsec.secrets  
				  : PSK "567890"
			```
			{: codeblock}

	3. 重新启动 IPSec：

		```
		root@rdmnm:~# ipsec restart
		```  
		{: codeblock}

	4. 验证配置：
		* 在 strongSwan 服务器上运行以下命令来验证 IPSec 状态：

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

		* 在 IBM Bluemix 服务仪表板上验证 IBM VPN IPSec 连接状态。在 **VPN 站点连接**部分，状态字段应显示为 **ACTIVE**。

	5. 如果需要，请检查 strongSwan syslog：

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

##使用 Vyatta 配置 IBM VPN 服务
{: #vyatta} 

IBM VPN 设置使用以下示例配置：

* 单个容器子网：172.31.0.0/16
* 容器组子网：172.30.0.0/16
* IBM VPN 网关 IP 地址：129.41.255.27

内部部署 Vyatta 设置使用以下示例配置：

* VPN 网关 IP 地址（客户网关 IP）：173.192.83.82
* 与端点相连的子网地址（客户子网）：192.168.201.0/24 

###要搭配使用 IBM VPN 服务与 Vyatta，请按如下所示进行配置：

1. [配置网关](index.html#gateway)。
2. [配置站点连接](index.html#site)。 
3. 配置 Vyatta。  

	1. 使用 SSH 登录到 Vyatta 设备：
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

	2. 输入配置方式：
		```
		vyatta@vyatta: configure
		vyatta@vyatta#
		```  
		{: codeblock}

	3. 配置绑定接口的 IP 地址：
		```
		Set interface bonding bond0 address 192.168.201.2/24
		Set interface bonding bond1 address 173.192.83.82/29
		```  
		{: codeblock}

	4. 在 bond1 上启用 VPN：
		```
		set vpn ipsec ipsec-interfaces interface bond1
		```  
		{: codeblock}

	5. 配置 IKE 组：
		```
		set vpn ipsec ike-group bm-ike lifetime 28800  
		set vpn ipsec ike-group bm-ike proposal 1 dh-group 2  
		set vpn ipsec ike-group bm-ike proposal 1 encryption aes128  
		set vpn ipsec ike-group bm-ike proposal 1 hash sha1  
		```  
		{: codeblock}

	6. 配置 ESP 组：
		```
		set vpn ipsec esp-group bm-esp compression disable  
		set vpn ipsec esp-group bm-esp lifetime 3600  
		set vpn ipsec esp-group bm-esp mode tunnel  
		set vpn ipsec esp-group bm-esp pfs dh-group2  
		set vpn ipsec esp-group bm-esp proposal 2 encryption aes128  
		set vpn ipsec esp-group bm-esp proposal 2 hash sha1  
		```  
		{: codeblock}

	7. 与远程站点建立连接：
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
		其中：  
			129.41.255.27 是 IBM 网关：  
			172.31.0.0/16 是 IBM 网关后面的容器子网。
		```
		{: screen}

	8. 落实并确认配置：
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

	9. 验证配置：
		```
		vyatta@vpn:~$ show vpn  ipsec status  
		```
		{: codeblock}

		```
		IPSec 进程运行的 PID：5633  
		  
		1 个活动 IPsec 隧道  
		  
		IPsec 接口：  
		        bond1   （接口上没有任何 IP 静态配置为任何 VPN 同级的本地 IP）  
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

	10. 检查 IBM VPN 服务连接状态：

		在 IBM Bluemix 服务仪表板上验证 IBM VPN IPSec 连接状态。在 **VPN 站点连接**部分，状态字段应显示为 **ACTIVE**。

	11. 如果需要，请检查 Vyatta syslog：
		
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

##使用 SoftLayer Gateway Appliance Service (GaaS) 配置 IBM VPN 服务
{: #gaas} 

IBM VPN 设置使用以下示例配置：

* 单个容器子网：172.31.0.0/16
* 容器组子网：172.30.0.0/16
* IBM VPN 网关 IP 地址：134.168.0.244

内部部署 SoftLayer GaaS 设置使用以下示例配置：

* VPN 网关 IP 地址（客户网关 IP）：75.126.122.46
* 与端点相连的子网地址（客户子网）：10.86.88.128/26
* 预共享密钥字符串：567890 

###要搭配使用 IBM VPN 服务与 SoftLayer GaaS，请按如下所示进行配置：

1. 配置 SoftLayer GaaS：

	1. 打开 [https://gateway-as-a-service.com/gaas/ui/](https://gateway-as-a-service.com/gaas/ui/)。  
	2. 使用您的 SoftLayer 帐户凭证登录。这将显示**管理网关**页面。 
	3. 针对您要配置的网关，选择**管理隧道**操作。这将显示**管理网关隧道配置**页面。 
	4. 选择**添加隧道**。后续页面会要求您提供网关和网络详细信息。 
	5. 请不要更改缺省网关和网络配置。选择**下一步**。
	6. 将 **VLAN 类型**设置为专用于内部部署子网。选择**下一步**。  
	7. 按如下所示编辑网络配置详细信息：  
		* 内部部署网关上的公共 IP 地址：输入 IBM VPN 网关公共 IP 地址。  
		* 内部部署子网：输入 IBM VPN 网关子网。  
		* 删除 GRE 隧道子网地址。   
		* 选择**高级 IPSec 配置**。按如下所示进行配置：  
			* IPSec 加密：aes-128  
			* Diffie-Hellman 组：2  
			* ESP - 完全正向安全性：启用  
			* 预共享密钥：输入配置 IBM VPN 时使用的预共享密钥。  
		* 选择**下一步**。
	8. 选择防火墙区域和选项**高级防火墙配置**。选择**下一步**。  
	9. 选中复选框以同意覆盖网关配置。
	10. 选择**下一步**。  
	11. 选择**完成**。这将显示**查看暂挂请求**页面。   
	12. 选择**详细信息**按钮，以查看请求状态。这将显示**查看请求详细信息**页面。 
	13. 等待所有配置参数的状态显示为完成。  
2. [配置网关](index.html#gateway)。
3. [配置站点连接](index.html#site)。
4. 验证配置。
	1. 在 Vyatta 上运行以下命令来验证 IPSec 连接状态：
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

	2. 在 IBM Bluemix 服务仪表板上验证 IBM VPN IPSec 连接状态。在 **VPN 站点连接**部分，状态字段应显示为 **ACTIVE**。  
5. 如果需要，请检查 Vyatta syslog：  

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

##使用 Cisco ASA 配置 IBM VPN 服务
{: #cisco}

IBM VPN 设置使用以下示例配置：

* 单个容器子网：172.31.0.0/16
* 容器组子网：172.30.0.0/16
* IBM VPN 网关 IP 地址：134.168.6.5

内部部署设置使用以下示例配置：

* VPN 网关 IP 地址（客户网关 IP）：62.95.35.53
* 与端点相连的子网地址（客户子网）：10.2.0.0/16

###要搭配使用 IBM VPN 服务与 Cisco ASA，请按如下所示进行配置：

1. [配置网关](index.html#gateway)。
2. [配置站点连接](index.html#site)。
3. 配置 Cisco ASA。请参阅以下配置示例：
		
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

