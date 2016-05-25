---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} 常见问题与解答
{: #vpn_faq}
*上次更新时间：2016 年 3 月 17 日*

下面列出了一些常见问题。
{:shortdesc}

1. IBM Lab 有哪些合格的第三方供应商设备与 IBM VPN 服务具有互操作性？

	IBM lab 测试出以下 VPN 网关设备与 IBM VPN 服务具有互操作性：

	* Cisco Adaptive Security Appliance (ASA) 软件 V8.2(1)。[请参阅配置示例](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7。[请参阅配置示例](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic。[请参阅配置示例](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic。[请参阅配置示例](vpn_onpremises.html#strongswan){: new_window}

	此外，其他任何供应商符合 IPSec 标准的 VPN 网关设备应该可以与 IBM VPN 服务良好运作。

2. 需要多长时间才能检测到同级故障？
 
	在已配置的保持活动超时值之后将检测到发生故障的同级。缺省设置是 60 秒。

3. 为每个 VPN 服务可创建多少个 VPN 网关和连接？
 
	在 Bluemix 空间中可以为每个 VPN 服务创建一个 VPN 网关设备。您可以为每个 VPN 网关定义最多 16 个不同目的地的连接。 

4. 何时应使用 IBM VPN 服务和 Bluemix Secure Gateway 服务？

	这两种服务都用于在 Bluemix 资源与内部部署数据中心之间提供安全连接。 

	当您需要确保任意两个端点之间具有连接时，请使用 IBM VPN 服务。VPN 服务在内部部署网络与 IBM Bluemix 云环境之间建立第 3 层 IPSec 安全连接。IBM VPN 服务仅可用于安全访问 IBM 容器（Docker 容器）。 

	如果想要在 Bluemix 中的特定应用程序端点与内部部署数据中心内的其他端点之间建立安全连接，请使用 Bluemix Secure Gateway 服务。 

5. 我是否可使用 IBM VPN 服务，在 IBM Bluemix 云环境中通过专用 IP 地址来访问我的容器和虚拟服务器？
 
	目前，IBM VPN 服务仅可用于访问 Bluemix 容器。

6. 我是否可定义 Bluemix 组织级别的 IBM VPN 服务？

	目前，IBM VPN 服务仅可用于 Bluemix 空间级别。如果您的 Bluemix 组织具有多个空间，那么可以为每个空间定义单独的 VPN 服务。

7. 我如何将 IBM VPN 服务与 SoftLayer Gateway Appliance Service (GaaS) 相连？

	通过构建 IPSec 隧道，可建立 IBM VPN 服务与 SoftLayer GaaS 之间的安全通信。[请参阅配置示例。](vpn_onpremises.html#gaas){: new_window}
