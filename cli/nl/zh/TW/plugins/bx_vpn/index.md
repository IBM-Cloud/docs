---



copyright:

  years: 2015，2017

lastupdated: "2016-06-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 適用於 {{site.data.keyword.Bluemix_notm}} CLI 的 VPN 外掛程式

*版本：*1.4.0

您可以使用指令行介面 (CLI) 來配置及管理 {{site.data.keyword.vpn_full}} 服務。VPN CLI 外掛程式有兩個可用的版本：一個是與 Cloud Foundry CLI 外掛程式搭配使用，另一個是與 {{site.data.keyword.Bluemix}} CLI 外掛程式搭配使用。這兩個版本的外掛程式都提供相同的功能。
{:shortdesc}

VPN 外掛程式適用於 Windows、MAC 及 Linux 作業系統。請確定您是使用適用的版本。

下列指示適用於 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式。若要將此外掛程式與 Cloud Foundry (cf) CLI 外掛程式搭配使用，請參閱[適用於 cf CLI 的 VPN CLI 外掛程式](../vpn/index.html)。


下列資訊列出 Bluemix CLI VPN 外掛程式支援的所有指令，並且包括其名稱、選項、用法、必要條件、說明及範例。請參閱[延伸您的 Bluemix 指令行介面](../../index.html#cli_bluemix_ext)，以瞭解如何安裝 VPN 外掛程式。

**附註：***必要條件* 列出使用指令之前需要哪些動作。必要條件可能包括下列一個以上的動作：
<dl>
<dt>**端點**</dt>
<dd>必須透過 `bluemix api` 設定 API 端點後，才能使用此指令。</dd>
<dt>**登入**</dt>
<dd>需要使用 `bluemix login` 指令進行登入後，才能使用此指令。</dd>
<dt>**目標**</dt>
<dd>必須使用 `bluemix target` 指令來設定組織及空間後，才能使用此指令。</dd>
</dl>


## bluemix vpn connection-create
建立 VPN 連線。

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**必要條件**：端點、登入、目標

**指令選項**：

*CONNECTION_NAME*（必要）：連線的名稱。

-g *GATEWAY_NAME*（必要）：閘道的名稱。

-k *PRESHARED_KEY*（必要）：預先共用金鑰。

-subnets "*SUBNET*/*MASK*"（必要）：遠端子網路位址（CIDR 格式）。

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*（必要）：VPN 通道的遠端端點 IP 位址。

-d *DESCRIPTION*（選用）：指定參數的說明。

-peer_id *PEER_ID*（選用）：遠端對等節點的 ID。VPN 通道的其他端點。

-admin_state *ADMIN_STATE*（選用）：VPN 連線的狀態。有效值為 `UP` 或 `DOWN`。

-dpd-action *ACTION*（選用）：偵測到對等節點已停用時所要採取的動作。有效值為 `hold`、`clear`、`disabled`、`restart` 或 `restart-by-peer`。預設值為 `hold`。

-gateway_ip *IP_ADDRESS*（選用）：本端 VPN 通道端點的 IP 位址。

-i *INITIATOR_STATE*（選用）：起始器的狀態。預設值為 `bi-directional`。

-dpd-timeout *VALUE*（選用）：逾時值（秒），在此期間之後會終止階段作業。範圍：6 - 86400 秒。預設值為 `120` 秒。

-dpd-interval *VALUE*（選用）：保留作用中間隔（秒）。依配置的間隔傳送保留作用中訊息，以檢查對等節點是否活躍。範圍：5-86399 秒。預設值為 `15` 秒。

-ike *NAME*（選用）：IKE 原則的名稱。

-ipsec *NAME*（選用）：IPSec 原則的名稱。

**範例**：

建立名稱為 `my_connection` 的新 VPN 連線：

```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
建立 IKE 原則。

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**必要條件**：端點、登入、目標

**指令選項**：

*POLICY_NAME*（必要）：IKE 原則的名稱。

-g *GATEWAY_NAME*（必要）：閘道的名稱。

-d *DESCRIPTION*（選用）：指定參數的說明。

-pfs *GROUP*（選用）：Diffie-Hellman (DH) 群組 ID。有效值為 `Group2`、`Group5` 或 `Group14`。預設值為 `Group2`。

-e *ENCRYPTION_ALGORITHM*（選用）：加密演算法。有效值為 `aes-128`、`aes-192`、`aes-256` 或 `3des`。預設值為 `aes-128`。

-lv *LIFETIME_VALUE*（選用）：IKE 安全關聯的生命期限值。範圍：60 - 86400 秒。預設值為 `86400` 秒。

**範例**：

建立名稱為 `my_ike` 的新 IKE 原則：

```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
建立 IPSec 原則。

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**必要條件**：端點、登入、目標

**指令選項**：

*POLICY_NAME*（必要）：IPSec 原則的名稱。

-g *GATEWAY_NAME*（必要）：閘道的名稱。

-d *DESCRIPTION*（選用）：指定參數的說明。

-pfs *GROUP*（選用）：Diffie-Hellman (DH) 群組 ID。有效值為 `Group2`、`Group5` 或 `Group14`。預設值為 `Group2`。

-e *ENCRYPTION_ALGORITHM*（選用）：加密演算法。有效值為 `aes-128`、`aes-192`、`aes-256` 或 `3des`。預設值為 `aes-128`。

-lv *LIFETIME_VALUE*（選用）：安全關聯的生命期限值。範圍：60 - 86400 秒。預設值為 `3600` 秒。

**範例**：

建立名稱為 `my_policy` 的 IPSec 原則：

```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
建立 VPN 閘道。

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**必要條件**：端點、登入、目標

**指令選項**：

*GATEWAY_NAME*（必要）：閘道的名稱。

-t *TYPE*（必要）：您要啟用服務的容器。有效值為 `allSingleContainers`、`allContainerGroups` 或 `allContainers`。無預設值；您必須指定類型。

-gateway_ip *IP_ADDRESS*（選用）：閘道的 IP 位址。

-subnets *SUBNET_ADDRESS*（選用）：子網路位址（CIDR 格式）。

**範例**：

建立名稱為 `my_gateway` 且類型為 `allContainerGroups` 的閘道：

```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
顯示所有現行連線的相關資訊。

```
bluemix vpn connections
```

**必要條件**：端點、登入、目標


## bluemix vpn ikes
顯示現行 IKE 連線的相關資訊。

```
bluemix vpn ikes
```

**必要條件**：端點、登入、目標


## bluemix vpn ipsecs
顯示現行 IPSec 連線的相關資訊。

```
bluemix vpn ipsecs
```

**必要條件**：端點、登入、目標


## bluemix vpn gateways
顯示現行閘道的相關資訊。

```
bluemix vpn gateways
```

**必要條件**：端點、登入、目標


## bluemix vpn connection
顯示特定連線的所有資訊。

```
bluemix vpn connection CONNECTION_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*CONNECTION_NAME*（必要）：要顯示的連線名稱。


## bluemix vpn ike
顯示 IKE 連線的相關資訊。

```
bluemix vpn ike POLICY_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*POLICY_NAME*（必要）：要顯示的 IKE 原則名稱。


## bluemix vpn ipsec
顯示 IPSec 連線的相關資訊。

```
bluemix vpn ipsec POLICY_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*POLICY_NAME*（必要）：要顯示的 IPSec 原則名稱。


## bluemix vpn gateway
顯示閘道的連線資訊。

```
bluemix vpn gateway GATEWAY_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*GATEWAY_NAME*（必要）：要顯示的閘道名稱。


## bluemix vpn connection-delete
刪除現有連線。

```
bluemix vpn connection-delete CONNECTION_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*CONNECTION_NAME*（必要）：要刪除的連線名稱。


## bluemix vpn ike-delete
刪除現有 IKE 原則。

```
bluemix vpn ike-delete POLICY_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*POLICY_NAME*（必要）：要刪除的 IKE 原則名稱。


## bluemix vpn ipsec-delete
刪除現有 IPSec 原則。

```
bluemix vpn ipsec-delete POLICY_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*POLICY_NAME*（必要）：要刪除的 IPSec 原則名稱。


## bluemix vpn gateway-delete
刪除現有閘道。

```
bluemix vpn gateway-delete GATEWAY_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*GATEWAY_NAME*（必要）：要刪除的閘道名稱。


## bluemix vpn connection-update
更新現有 VPN 連線。

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME] [-k PRESHARED_KEY] [-subnets "SUBNET/MASK"] [-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**必要條件**：端點、登入、目標

**指令選項**：

*CONNECTION_NAME*（必要）：連線的名稱。

-g *GATEWAY_NAME*（選用）：閘道的名稱。

-k *PRESHARED_KEY*（選用）：預先共用金鑰。

-subnets "*SUBNET*/*MASK*"（選用）：子網路位址（CIDR 格式）。

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*（選用）：VPN 通道的遠端端點 IP 位址。

-d *DESCRIPTION*（選用）：指定參數的說明。

-peer_id *PEER_ID*（選用）：遠端對等節點的 ID。VPN 通道的其他端點。

-admin_state *ADMIN_STATE*（選用）：VPN 連線的狀態。有效值為 `UP` 或 `DOWN`。

-dpd-action *ACTION*（選用）：偵測到對等節點已停用時所要採取的動作。有效值為 `hold`、`clear`、`disabled`、`restart` 或 `restart-by-peer`。

-gateway_ip *IP_ADDRESS*（選用）：本端 VPN 通道端點的 IP 位址。

-i *INITIATOR_STATE*（選用）：起始器的狀態。

-dpd-timeout *VALUE*（選用）：逾時值（秒），在此期間之後會終止階段作業。範圍：6 - 86400 秒。

-dpd-interval *VALUE*（選用）：保留作用中間隔（秒）。依配置的間隔傳送保留作用中訊息，以檢查對等節點是否活躍。範圍：5-86399 秒。

-ike *NAME*（選用）：IKE 原則的名稱。

-ipsec *NAME*（選用）：IPSec 原則的名稱。


## bluemix vpn ike-update
更新 IKE 原則。

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**必要條件**：端點、登入、目標

**指令選項**：

*POLICY_NAME*（必要）：IKE 原則的名稱。

-g *GATEWAY_NAME*（選用）：閘道的名稱。

-d *DESCRIPTION*（選用）：指定參數的說明。

-pfs *GROUP*（選用）：Diffie-Hellman (DH) 群組 ID。有效值為 `Group2`、`Group5` 或 `Group14`。

-e *ENCRYPTION_ALGORITHM*（選用）：加密演算法。有效值為 `aes-128`、`aes-192`、`aes-256` 或 `3des`。

-lv *LIFETIME_VALUE*（選用）：IKE 安全關聯的生命期限值。範圍：60 - 86400 秒。


## bluemix vpn ipsec-update
更新 IPSec 原則。

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**必要條件**：端點、登入、目標

**指令選項**：

*POLICY_NAME*（必要）：IPSec 原則的名稱。

-g *GATEWAY_NAME*（選用）：閘道的名稱。

-d *DESCRIPTION*（選用）：指定參數的說明。

-pfs *GROUP*（選用）：Diffie-Hellman (DH) 群組 ID。有效值為 `Group2`、`Group5` 或 `Group14`。

-e *ENCRYPTION_ALGORITHM*（選用）：加密演算法。有效值為 `aes-128`、`aes-192`、`aes-256` 或 `3des`。

-lv *LIFETIME_VALUE*（選用）：安全關聯的生命期限值。範圍：60 - 86400 秒。


## bluemix vpn gateway-update
更新現有 VPN 閘道。

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE] [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**必要條件**：端點、登入、目標

**指令選項**：

*GATEWAY_NAME*（必要）：閘道的名稱。

-t *TYPE*（選用）：您要啟用服務的容器。有效值為 `allSingleContainers`、`allContainerGroups` 或 `allContainers`。

-gateway_ip *IP_ADDRESS*（選用）：閘道的 IP 位址。

-subnets *SUBNET_ADDRESS*（選用）：子網路位址（CIDR 格式）。
