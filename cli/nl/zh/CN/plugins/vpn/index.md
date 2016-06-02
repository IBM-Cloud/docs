---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# IBM VPN CLI
*上次更新时间：2016 年 5 月 3 日*

您可以使用命令行界面 (CLI) 配置并管理 IBM® 虚拟专用网 (VPN) 服务。IBM VPN CLI 是与 Cloud Foundry CLI 插件搭配使用的插件。该插件可用于 Windows、MAC 和 Linux 操作系统。请确保使用适当的操作系统。

开始之前，请安装 Cloud Foundry CLI。请参阅 [Cloud Foundry 命令行界面](https://console.{DomainName}/docs/cli/downloads.html)以获取详细信息。 

##安装 IBM VPN CLI 插件
**注：**如果已安装 IBM VPN CLI 插件的先前版本，您必须先将其卸载。请使用以下命令： 

```
cf uninstall-plugin vpn
```  

**本地安装**

1. 从 [IBM Bluemix CLI 插件存储库](http://plugins.ng.bluemix.net)下载适用于您的平台的 IBM VPN 插件。
2. 使用以下命令安装 IBM VPN 插件：
**注：**切换到 VPN 插件的位置，或指定插件位置的路径。  

	**对于 MS Windows 操作系统：**

	```
	cf install-plugin vpn_windows64.exe
	```  

	**对于 Apple MAC 操作系统：**

	```
	cf install-plugin vpn_mac_os_amd64
	```  

	**对于 Linux 操作系统：**

	```
	cf install-plugin vpn_linuxamd64
	```  


**从 Bluemix 存储库安装**  

1. 将 Bluemix 存储库添加到 Cloud Foundry CLI 存储库中。请使用以下命令：

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. 运行以下命令：  

	```
	cf install-plugin vpn -r bluemix
	```
##IBM VPN 服务命令的列表

### cf vpn-create connection

创建 VPN 连接。

```
cf vpn-create connection <connection name> -g <gateway name> -k <preshared key> -subnets ["<subnet/mask>"] -cip <customer gateway IP address> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### 参数
{: #p1}

**connection name：**连接的名称。

**gateway name：**网关的名称。

**-k：**预共享密钥。

**subnet/mask：**CIDR 格式的远程子网地址。 

**customer gateway IP address：**VPN 隧道的远程端点 IP 地址。 

##### 可选参数：
{: #op1}

**-d：**指定参数的描述。

**-peer_id：**远程同级的标识。VPN 隧道的其他端点。

**-admin_state：**VPN 连接的状态。值：UP 或 DOWN。

**-dpd-action：**检测到同级无效时要执行的操作。值：hold、clear、disabled、restart 和 restart-by-peer。缺省值：hold

**-gateway_ip：**本地 VPN 隧道端点的 IP 地址。 

**-i：**发起者的状态。缺省值：bi-directional。

**-dpd-timeout：**终止会话之前的超时值（以秒为单位）。范围：6 - 86400 秒。缺省值：120 秒。保持活动的超时值必须大于保持活动的间隔值。

**-dpd-interval：**保持活动的时间间隔（以秒为单位）。按配置的时间间隔发送保持活动消息，以检查同级的活动状态。范围：5 - 86399 秒。缺省值：15 秒

**-ike：**IKE 策略的名称。

**-ipsec：**IPSec 策略的名称。


### cf vpn-create ike

创建 IKE 策略。

```
cf vpn-create ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 参数
{: #p2}

**policy name：**IKE 策略的名称。

**gateway name：**网关的名称。 

##### 可选参数：
{: #op2}

**-d：**指定参数的描述。

**-pfs：**Diffie-Hellman (DH) 组标识。值：Group2、Group5 和 Group14。缺省值：Group2 

**-e：**加密算法。值：aes-128、aes-192、aes-256 和 3des。缺省值：aes-128

**-lv：**IKE 安全性关联的生存期值。范围：60 - 86400 秒。缺省值：86400 秒


### cf vpn-create ipsec

创建 IPSec 策略。

```
cf vpn-create ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 参数
{: #p3}

**policy name：**IPSec 策略的名称。 

**gateway name：**网关的名称。 

##### 可选参数：
{: #op3}

**-d：**指定参数的描述。

**-pfs：**Diffie-Hellman (DH) 组标识。值：Group2、Group5 和 Group14。缺省值：Group2  

**-e：**加密算法。值：aes-128、aes-192、aes-256 和 3des。缺省值：aes-128

**-lv：**安全性关联的生存期值。范围：60 - 86400 秒。缺省值：3600 秒

### cf vpn-create gateway

创建 VPN 网关。

```
cf vpn-create gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### 参数
{: #p4}

**gateway name：**网关的名称。

**-t：**要对其启用服务的容器。值：allSingleContainers、allContainerGroups 和 allContainers。缺省值：无缺省值，您必须指定类型。 

#####可选参数：
{: #op4}

**-gateway_ip：**网关的 IP 地址。 

**-subnets：**CIDR 格式的子网地址。 

### cf vpn-show gateways

显示有关当前网关的信息。

```
cf vpn-show gateways
```
### cf vpn-show ikes

显示有关当前 IKE 连接的信息。

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

显示有关当前 IPSec 连接的信息。

```
cf vpn-show ipsecs
```
### cf vpn-show connections

显示有关当前所有连接的信息。

```
cf vpn-show connections
```
### cf vpn-show ike

显示有关 IKE 连接的信息。

```
cf vpn-show ike <policy name>
```
### cf vpn-show ipsec

显示有关 IPSec 连接的信息。

```
cf vpn-show ipsec <policy name>
```
### cf vpn-show gateway

显示有关网关的连接信息。

```
cf vpn-show gateway <gateway name>
```
### cf vpn-show connection

显示有关特定连接的所有信息。

```
cf vpn-show connection <connection name>
```
### cf vpn-delete

删除现有连接、策略或网关。

```
cf vpn-delete ike <policy name>
```

```
cf vpn-delete ipsec <policy name>
```

```
cf vpn-delete connection <connection name>
```

```
cf vpn-delete gateway <gateway name>
```


### cf vpn-update connection

更新现有 VPN 连接。

```
cf vpn-update connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### 参数
{: #p5}

**connection name：**连接的名称。


##### 可选参数：
{: #op5}

**gateway name：**网关的名称。

**customer gateway IP address：**VPN 隧道的远程端点 IP 地址。 

**subnet/mask：**CIDR 格式的子网地址。 

**-k：**预共享密钥。

**-d：**指定参数的描述。

**-peer_id：**远程同级的标识。VPN 隧道的其他端点。

**-admin_state：**VPN 连接的状态。值：UP 或 DOWN。

**-dpd-action：**检测到同级无效时要执行的操作。值：hold、clear、disabled、restart 和 restart-by-peer。缺省值：hold

**-gateway_ip：**本地 VPN 隧道端点的 IP 地址。 

**-i：**发起者的状态。缺省值：bi-directional。

**-dpd-timeout：**终止会话之前的超时值（以秒为单位）。范围：6 - 86400 秒。缺省值：120 秒

**-dpd-interval：**保持活动的时间间隔（以秒为单位）。按配置的时间间隔发送保持活动消息，以检查同级的活动状态。范围：5 - 86399 秒。缺省值：15 秒

**-ike：**IKE 策略的名称。

**-ipsec：**IPSec 策略的名称。


### cf vpn-update ike

更新 IKE 策略。

```
cf vpn-update ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 参数
{: #p6}

**policy name：**IKE 策略的名称。 

##### 可选参数：
{: #op6}

**gateway name：**网关的名称。 

**-d：**指定参数的描述。

**-pfs：**Diffie-Hellman (DH) 组标识。值：Group2、Group5 和 Group14。缺省值：Group2 

**-e：**加密算法。值：aes-128、aes-192、aes-256 和 3des。缺省值：aes-128

**-lv：**IKE 安全性关联的生存期值。范围：60 - 86400 秒。缺省值：86400 秒


### cf vpn-update ipsec

更新 IPSec 策略。

```
cf vpn-update ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 参数
{: #p7}

**policy name：**IPSec 策略的名称。


##### 可选参数：
{: #op7}

**gateway name：**网关的名称。

**-d：**指定参数的描述。

**-pfs：**Diffie-Hellman (DH) 组标识。值：Group2、Group5 和 Group14。缺省值：Group2 

**-e：**加密算法。值：aes-128、aes-192、aes-256 和 3des。缺省值：aes-128

**-lv：**安全性关联的生存期值。范围：60 - 86400 秒。缺省值：3600 秒

### cf vpn-update gateway

更新现有 VPN 网关。

```
cf vpn-update gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### 参数
{: #p8}

**gateway name：**网关的名称。

#####可选参数：
{: #op8}

**-t：**要对其启用服务的容器。值：allSingleContainers、allContainerGroups 和 allContainers。缺省值：无缺省值，您必须指定类型。

**-gateway_ip：**网关的 IP 地址。 

**-subnets：**CIDR 格式的子网地址。 

# 相关链接
## 常规  
{: #general}  
* [IBM VPN 服务](../../../services/vpn/index.html)
* [Cloud Foundry CLI](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
