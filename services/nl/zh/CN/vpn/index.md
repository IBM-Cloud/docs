---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} 入门
{: #vpn}  
*上次更新时间：2016 年 5 月 9 日*

Bluemix&reg; 的 {{site.data.keyword.vpn_full}} 服务可用于安全访问 IBM Bluemix 云环境中的 IBM Containers（Docker 容器）。您可以将 IBM Bluemix 云环境用作公司数据中心的扩展。此外，还可以使用 IBM VPN 服务与 SoftLayer 服务器进行连接。
{:shortdesc}

开始之前，请确保 IBM Docker 容器可供使用。请参阅 [IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html)，以获取有关如何创建和管理 IBM Containers 的详细信息。  

要开始使用，请选择 Bluemix 仪表板上的**虚拟专用网**服务实例磁贴。完成以下步骤：

1. 通过选择**创建网关**来配置 {{site.data.keyword.vpn_short}} 网关。这将创建缺省网关。如果需要，请如以下步骤中所示编辑网关配置。
{: #gateway}  

  1. 选择**编辑**。  
  2. 指定网关名称。  
  3. 选择要使用 VPN 服务的容器和容器组。
	**注：**会预先选择容器和容器组专用子网，以便您可以通过 VPN 连接进行访问。
  4. 选择**保存**。  

 可以使用缺省 IKE 和 IPSec 策略，也可以配置定制策略。如果要使用缺省策略，请跳至步骤 4。

2. 通过选择 **IKE 和 IPSec 策略**选项卡来配置 IKE 策略。
  1. 选择**添加新项**。  
  2. 指定以下详细信息：
	* **名称**：IKE 策略的名称
	* **授权算法**：sha1；不能更改  
	* **加密算法**：从下拉列表中进行选择。值：aes-128（缺省值）、aes-192、aes-256 和 3des
	* **密钥生存期**：IKE 安全性关联的生存期值（以秒为单位）。范围：60-86400。缺省值：86400
	* **PFS**：Diffie-Hellman (DH) 组标识。值：Group2、Group5 和 Group14。缺省值：Group2
	* **协商方式**：Main；不能更改
	* **版本**：IKEV1；不能更改
  3. 选择**保存**。

3. 配置 IPSec 策略：
  1. 选择**添加新项**。  
  2. 指定以下详细信息：
  	* **名称**：IPSec 策略的名称  
  	* **授权算法**：sha1；不能更改  
  	* **加密算法**：从下拉列表中进行选择。值：aes-128（缺省值）、aes-192、aes-256 和 3des
  	* **密钥生存期**：安全性关联的生存期值（以秒为单位）。范围：60-86400。缺省值：3600
  	* **PFS**：Diffie-Hellman (DH) 组标识。值：Group2、Group5 和 Group14。缺省值：Group2
  	* **变换协议**：ESP；不能更改
  	* **封装方式**：隧道；不能更改
  3. 选择**保存**。  

4. 提供用于在数据中心或 SoftLayer 服务器 VPN 网关与 IBM VPN 网关之间建立连接的详细信息。
{: #site}  

  1. 选择**网关设备**选项卡。
  2. 在**站点连接**部分中选择**创建连接**。
  3. 指定以下站点连接详细信息：  
  	* **名称**：连接的名称  
  	* **描述**：连接的描述（可选）  
  	* **预共享密钥字符串**：要用于认证的预共享密钥
  	* **管理状态**：VPN 连接的状态。从下拉列表中进行选择：UP 或 DOWN。缺省值：UP  
  	* **客户网关 IP**：VPN 隧道的远程端点 IP 地址  
  	* **客户子网**：CIDR 格式的远程子网地址。选择加号可添加其他子网。
  4. （可选）配置以下**高级设置**参数：  
  	* **IKE 策略**：选择 IKE 策略。  
  	* **保持活动时间间隔**：保持活动的时间间隔（以秒为单位）。按配置的时间间隔发送保持活动消息，以检查同级的活动状态。缺省值：15。范围：5-86399。
  	* **检测到失效同级时的操作**：检测到同级无效时要执行的操作。
     值： 
  		* hold（缺省值）：安全性关联 (SA) 暂停 
  		* clear：已删除 SA
  		* disabled：已禁用 SA
  		* restart：已重新协商 SA
  		* restart-by-peer：已重新协商具有失效同级的所有 SA  
  	* **IPSec 策略**：选择 IPSec 策略。
  	* **保持活动超时**：终止会话之前的超时值（以秒为单位）。缺省值：120。范围：6-86400。保持活动的超时值必须大于保持活动的间隔值。
  5. 选择**保存**。

  **注：**正在建立连接时，连接状态显示为***暂挂创建***。看到此状态时，请刷新屏幕若干次，直到看到连接活动状态。

**重要信息：**如果是使用 Web 应用程序，那么必须将 Web 应用程序绑定到要使用的 Docker 容器。此绑定对于通过 IPSec VPN 隧道传递流量是必需的。

**重要信息：**IBM VPN 服务当前在以响应者方式运行。要启动 VPN 连接，数据包必须从 IBM VPN 网关流出到内部部署数据中心或 SoftLayer 服务器。一旦建立 VPN 连接后，流量即可在 VPN 连接的端点之间向任一方向流动。

 
# 相关链接
## 样本 
{: #samples}  
* [内部部署 strongSwan Gateway 配置示例](vpn_onpremises.html#strongswan){: new_window}
* [内部部署 Vyatta Gateway 配置示例](vpn_onpremises.html#vyatta){: new_window}
* [内部部署 SoftLayer Gateway Appliance Service (GaaS) 配置示例](vpn_onpremises.html#gaas){: new_window}
* [内部部署 Cisco ASA 配置示例](vpn_onpremises.html#cisco){: new_window}

## API  
{: #api}  
* [IBM VPN RESTful API](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## 常规  
{: #general}  
* [IBM VPN 命令行界面](../../cli/plugins/vpn/index.html){: new_window}
* [IBM VPN 常见问题解答](vpn_faq.html#vpn_faq){: new_window}
* [IBM Bluemix 价格表](https://console.{DomainName}/pricing/){: new_window}
* [IBM Bluemix 先决条件](https://developer.ibm.com/bluemix/support/#prereqs)
