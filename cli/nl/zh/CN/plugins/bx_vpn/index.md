---



copyright:

  years: 2015，2017

lastupdated: "2016-06-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 的 VPN 插件

*版本：*1.4.0

您可以使用命令行界面 (CLI) 来配置和管理 {{site.data.keyword.vpn_full}} 服务。VPN CLI 插件提供两个版本：一个用于与 Cloud Foundry CLI 插件一起使用，另一个用于与 {{site.data.keyword.Bluemix}} CLI 插件一起使用。这两个版本的插件提供相同的功能。
{:shortdesc}

VPN 插件可用于 Windows、MAC 和 Linux 操作系统。请确保使用适合于您的插件。

以下指示信息适用于使用 {{site.data.keyword.Bluemix_notm}} CLI 插件。要将该插件与 Cloud Foundry (cf) CLI 插件一起使用，请参阅 [cf CLI 的 VPN CLI 插件](../vpn/index.html)。


以下信息列出了 Bluemix CLI 的 VPN 插件支持的所有命令，并包含命令名称、选项、用法、先决条件、描述和示例。请参阅[扩展 Bluemix 命令行界面](../../index.html#cli_bluemix_ext)，以了解如何安装 vpn 插件。

**注：***先决条件*列出使用命令前必须执行的操作。先决条件可能会包含以下一个或多个操作：
<dl>
<dt>**端点**</dt>
<dd>使用此命令之前，必须通过 `bluemix api` 设置 API 端点。</dd>
<dt>**登录**</dt>
<dd>使用此命令之前，必须使用 `bluemix login` 命令登录。</dd>
<dt>**目标**</dt>
<dd>使用此命令之前，必须使用 `bluemix target` 命令来设置组织和空间。</dd>
</dl>


## bluemix vpn connection-create
创建 VPN 连接。

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**先决条件**：端点、登录和目标

**命令选项**：

*CONNECTION_NAME*（必需）：连接的名称。

-g *GATEWAY_NAME*（必需）：网关的名称。

-k *PRESHARED_KEY*（必需）：预共享密钥。

-subnets "*SUBNET*/*MASK*"（必需）：CIDR 格式的远程子网地址。

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*（必需）：VPN 隧道的远程端点 IP 地址。

-d *DESCRIPTION*（可选）：所指定参数的描述。

-peer_id *PEER_ID*（可选）：远程同级的标识。VPN 隧道的另一个端点。

-admin_state *ADMIN_STATE*（可选）：VPN 连接的状态。有效值为 `UP` 或 `DOWN`。

-dpd-action *ACTION*（可选）：检测到同级无效时要执行的操作。有效值为 `hold`、`clear`、`disabled`、`restart` 或 `restart-by-peer`。缺省值为 `hold`。

-gateway_ip *IP_ADDRESS*（可选）：本地 VPN 隧道端点的 IP 地址。

-i *INITIATOR_STATE*（可选）：发起者的状态。缺省值为 `bi-directional`。

-dpd-timeout *VALUE*（可选）：终止会话之前的超时值（以秒为单位）。范围：6-86400 秒。缺省值为 `120` 秒。

-dpd-interval *VALUE*（可选）：保持活动时间间隔（以秒为单位）。按配置的时间间隔发送保持活动消息，以检查同级的活动性。范围：5-86399 秒。缺省值为 `15` 秒。

-ike *NAME*（可选）：IKE 策略的名称。

-ipsec *NAME*（可选）：IPSec 策略的名称。

**示例**：

创建名为 `my_connection` 的新 VPN 连接：

```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
创建 IKE 策略。

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**先决条件**：端点、登录和目标

**命令选项**：

*POLICY_NAME*（必需）：IKE 策略的名称。

-g *GATEWAY_NAME*（必需）：网关的名称。

-d *DESCRIPTION*（可选）：所指定参数的描述。

-pfs *GROUP*（可选）：Diffie-Hellman (DH) 组标识。有效值为 `Group2`、`Group5` 或 `Group14`。缺省值为 `Group2`。

-e *ENCRYPTION_ALGORITHM*（可选）：加密算法。有效值为 `aes-128`、`aes-192`、`aes-256` 或 `3des`。缺省值为 `aes-128`。

-lv *LIFETIME_VALUE*（可选）：IKE 安全性关联的生存期值。范围：60-86400 秒。缺省值为 `86400` 秒。

**示例**：

创建名为 `my_ike` 的新 IKE 策略：

```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
创建 IPSec 策略。

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**先决条件**：端点、登录和目标

**命令选项**：

*POLICY_NAME*（必需）：IPSec 策略的名称。

-g *GATEWAY_NAME*（必需）：网关的名称。

-d *DESCRIPTION*（可选）：所指定参数的描述。

-pfs *GROUP*（可选）：Diffie-Hellman (DH) 组标识。有效值为 `Group2`、`Group5` 或 `Group14`。缺省值为 `Group2`。

-e *ENCRYPTION_ALGORITHM*（可选）：加密算法。有效值为 `aes-128`、`aes-192`、`aes-256` 或 `3des`。缺省值为 `aes-128`。

-lv *LIFETIME_VALUE*（可选）：安全性关联的生存期值。范围：60-86400 秒。缺省值为 `3600` 秒。

**示例**：

创建名为 `my_policy` 的 IPSec 策略：

```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
创建 VPN 网关。

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**先决条件**：端点、登录和目标

**命令选项**：

*GATEWAY_NAME*（必需）：网关的名称。

-t *TYPE*（必需）：要对其启用服务的容器。有效值为 `allSingleContainers`、`allContainerGroups` 或 `allContainers`。没有缺省值；必须指定一种类型。

-gateway_ip *IP_ADDRESS*（可选）：网关的 IP 地址。

-subnets *SUBNET_ADDRESS*（可选）：CIDR 格式的子网地址。

**示例**：

创建名为 `my_gateway` 且类型为 `allContainerGroups` 的网关：

```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
显示有关所有当前连接的信息。

```
bluemix vpn connections
```

**先决条件**：端点、登录和目标


## bluemix vpn ikes
显示有关当前 IKE 连接的信息。

```
bluemix vpn ikes
```

**先决条件**：端点、登录和目标


## bluemix vpn ipsecs
显示有关当前 IPSec 连接的信息。

```
bluemix vpn ipsecs
```

**先决条件**：端点、登录和目标


## bluemix vpn gateways
显示有关当前网关的信息。

```
bluemix vpn gateways
```

**先决条件**：端点、登录和目标


## bluemix vpn connection
显示有关特定连接的所有信息。

```
bluemix vpn connection CONNECTION_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*CONNECTION_NAME*（必需）：要显示的连接的名称。


## bluemix vpn ike
显示有关 IKE 连接的信息。

```
bluemix vpn ike POLICY_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*POLICY_NAME*（必需）：要显示的 IKE 策略的名称。


## bluemix vpn ipsec
显示有关 IPSec 连接的信息。

```
bluemix vpn ipsec POLICY_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*POLICY_NAME*（必需）：要显示的 IPSec 策略的名称。


## bluemix vpn gateway
显示有关网关的连接信息。

```
bluemix vpn gateway GATEWAY_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*GATEWAY_NAME*（必需）：要显示的网关的名称。


## bluemix vpn connection-delete
删除现有连接。

```
bluemix vpn connection-delete CONNECTION_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*CONNECTION_NAME*（必需）：要删除的连接的名称。


## bluemix vpn ike-delete
删除现有 IKE 策略。

```
bluemix vpn ike-delete POLICY_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*POLICY_NAME*（必需）：要删除的 IKE 策略的名称。


## bluemix vpn ipsec-delete
删除现有 IPSec 策略。

```
bluemix vpn ipsec-delete POLICY_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*POLICY_NAME*（必需）：要删除的 IPSec 策略的名称。


## bluemix vpn gateway-delete
删除现有网关。

```
bluemix vpn gateway-delete GATEWAY_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*GATEWAY_NAME*（必需）：要删除的网关的名称。


## bluemix vpn connection-update
更新现有 VPN 连接。

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME] [-k PRESHARED_KEY] [-subnets "SUBNET/MASK"] [-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**先决条件**：端点、登录和目标

**命令选项**：

*CONNECTION_NAME*（必需）：连接的名称。

-g *GATEWAY_NAME*（可选）：网关的名称。

-k *PRESHARED_KEY*（可选）：预共享密钥。

-subnets "*SUBNET*/*MASK*"（可选）：CIDR 格式的子网地址。

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*（可选）：VPN 隧道的远程端点 IP 地址。

-d *DESCRIPTION*（可选）：所指定参数的描述。

-peer_id *PEER_ID*（可选）：远程同级的标识。VPN 隧道的另一个端点。

-admin_state *ADMIN_STATE*（可选）：VPN 连接的状态。有效值为 `UP` 或 `DOWN`。

-dpd-action *ACTION*（可选）：检测到同级无效时要执行的操作。有效值为 `hold`、`clear`、`disabled`、`restart` 或 `restart-by-peer`。

-gateway_ip *IP_ADDRESS*（可选）：本地 VPN 隧道端点的 IP 地址。

-i *INITIATOR_STATE*（可选）：发起者的状态。

-dpd-timeout *VALUE*（可选）：终止会话之前的超时值（以秒为单位）。范围：6-86400 秒。

-dpd-interval *VALUE*（可选）：保持活动时间间隔（以秒为单位）。按配置的时间间隔发送保持活动消息，以检查同级的活动性。范围：5-86399 秒。

-ike *NAME*（可选）：IKE 策略的名称。

-ipsec *NAME*（可选）：IPSec 策略的名称。


## bluemix vpn ike-update
更新 IKE 策略。

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**先决条件**：端点、登录和目标

**命令选项**：

*POLICY_NAME*（必需）：IKE 策略的名称。

-g *GATEWAY_NAME*（可选）：网关的名称。

-d *DESCRIPTION*（可选）：所指定参数的描述。

-pfs *GROUP*（可选）：Diffie-Hellman (DH) 组标识。有效值为 `Group2`、`Group5` 或 `Group14`。

-e *ENCRYPTION_ALGORITHM*（可选）：加密算法。有效值为 `aes-128`、`aes-192`、`aes-256` 或 `3des`。

-lv *LIFETIME_VALUE*（可选）：IKE 安全性关联的生存期值。范围：60-86400 秒。


## bluemix vpn ipsec-update
更新 IPSec 策略。

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**先决条件**：端点、登录和目标

**命令选项**：

*POLICY_NAME*（必需）：IPSec 策略的名称。

-g *GATEWAY_NAME*（可选）：网关的名称。

-d *DESCRIPTION*（可选）：所指定参数的描述。

-pfs *GROUP*（可选）：Diffie-Hellman (DH) 组标识。有效值为 `Group2`、`Group5` 或 `Group14`。

-e *ENCRYPTION_ALGORITHM*（可选）：加密算法。有效值为 `aes-128`、`aes-192`、`aes-256` 或 `3des`。

-lv *LIFETIME_VALUE*（可选）：安全性关联的生存期值。范围：60-86400 秒。


## bluemix vpn gateway-update
更新现有 VPN 网关。

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE] [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**先决条件**：端点、登录和目标

**命令选项**：

*GATEWAY_NAME*（必需）：网关的名称。

-t *TYPE*（可选）：要对其启用服务的容器。有效值为 `allSingleContainers`、`allContainerGroups` 或 `allContainers`。

-gateway_ip *IP_ADDRESS*（可选）：网关的 IP 地址。

-subnets *SUBNET_ADDRESS*（可选）：CIDR 格式的子网地址。
