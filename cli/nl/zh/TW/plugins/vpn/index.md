---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# IBM VPN CLI
*前次更新：2016 年 5 月 3 日*

您可以使用指令行介面 (CLI) 來配置和管理 IBM® Virtual Private Network (VPN) 服務。IBM VPN CLI 是與 Cloud Foundry CLI 外掛程式搭配使用的外掛程式。該外掛程式可用於 Windows、MAC 和 Linux 作業系統。請確定您使用適當的作業系統。

開始之前，請安裝 Cloud Foundry CLI。如需詳細資料，請參閱 [Cloud Foundry 指令行介面](https://console.{DomainName}/docs/cli/downloads.html)。 

##安裝 IBM VPN CLI 外掛程式
**附註：**如果已安裝舊版 IBM VPN CLI 外掛程式，您必須先將其解除安裝。請使用以下指令： 

```
cf uninstall-plugin vpn
```  

**本端安裝**

1. 從 [IBM Bluemix CLI 外掛程式儲存庫](http://plugins.ng.bluemix.net)下載適用於您平台的 IBM VPN 外掛程式。
2. 使用下列指令安裝 IBM VPN 外掛程式：
**附註：**切換到 VPN 外掛程式的位置，或指定外掛程式位置的路徑。  

	**MS Windows 作業系統：**

	```
	cf install-plugin vpn_windows64.exe
	```  

	**Apple MAC 作業系統：**

	```
	cf install-plugin vpn_mac_os_amd64
	```  

	**Linux 作業系統：**

	```
	cf install-plugin vpn_linuxamd64
	```  


**從 Bluemix 儲存庫安裝**  

1. 將 Bluemix 儲存庫新增至 Cloud Foundry CLI 儲存庫。請使用下列指令：

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. 執行下列指令：  

	```
	cf install-plugin vpn -r bluemix
	```
##IBM VPN 服務指令的清單

### cf vpn-create connection

建立 VPN 連線。

```
cf vpn-create connection <connection name> -g <gateway name> -k <preshared key> -subnets ["<subnet/mask>"] -cip <customer gateway IP address> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### 參數
{: #p1}

**connection name：**
連線的名稱。

**gateway name：**
閘道的名稱。

**-k：**
預先共用金鑰。

**subnet/mask：**
CIDR 格式的遠端子網路位址。 

**customer gateway IP address：**
VPN 通道的遠端端點 IP 位址。 

##### 選用參數：
{: #op1}

**-d：**所指定參數的說明。

**-peer_id：**遠端對等節點的 ID。VPN 通道的其他端點。

**-admin_state：**VPN 連線的狀態。值：UP 或 DOWN。

**-dpd-action：**偵測到對等節點為停用時所要採取的動作。值：hold、clear、disabled、restart 和 restart-by-peer。預設值：hold

**-gateway_ip：**本端 VPN 通道端點的 IP 位址。 

**-i：**起始器的狀態。預設值：bi-directional。

**-dpd-timeout：**逾時值（以秒為單位），在此期間之後會終止階段作業。範圍：6 - 86400 秒。預設值：120 秒。保留作用中逾時值必須高於保留作用中間隔值。

**-dpd-interval：**保留作用中間隔（以秒為單位）。依配置的間隔傳送保留作用中訊息，以檢查對等節點是否活躍。範圍：5 - 86399 秒。預設值：15 秒

**-ike：**IKE 原則的名稱。

**-ipsec：**IPSec 原則的名稱。


### cf vpn-create ike

建立 IKE 原則。

```
cf vpn-create ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 參數
{: #p2}

**policy name：**
IKE 原則的名稱。

**gateway name：**
閘道的名稱。 

##### 選用參數：
{: #op2}

**-d：**所指定參數的說明。

**-pfs：**Diffie-Hellman (DH) 群組 ID。值：Group2、Group5 和 Group14。預設值：Group2 

**-e：**加密演算法。值：aes-128、aes-192、aes-256 和 3des。預設值：aes-128

**-lv：**IKE 安全關聯的生命期限值。範圍：60 - 86400 秒。預設值：86400 秒


### cf vpn-create ipsec

建立 IPSec 原則。

```
cf vpn-create ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 參數
{: #p3}

**policy name：**
IPSec 原則的名稱。 

**gateway name：**
閘道的名稱。 

##### 選用參數：
{: #op3}

**-d：**所指定參數的說明。

**-pfs：**Diffie-Hellman (DH) 群組 ID。值：Group2、Group5 和 Group14。預設值：Group2  

**-e：**加密演算法。值：aes-128、aes-192、aes-256 和 3des。預設值：aes-128

**-lv：**安全關聯的生命期限值。範圍：60 - 86400 秒。預設值：3600 秒

### cf vpn-create gateway

建立 VPN 閘道。

```
cf vpn-create gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### 參數
{: #p4}

**gateway name：**
閘道的名稱。

**-t：**您要啟用服務的儲存器。值：allSingleContainers、allContainerGroups 和 allContainers。預設值：無預設值；您必須指定類型。 

#####選用參數：
{: #op4}

**-gateway_ip：**
閘道的 IP 位址。 

**-subnets：**
CIDR 格式的子網路位址。 

### cf vpn-show gateways

顯示現行閘道的相關資訊。

```
cf vpn-show gateways
```
### cf vpn-show ikes

顯示現行 IKE 連線的相關資訊。

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

顯示現行 IPSec 連線的相關資訊。

```
cf vpn-show ipsecs
```
### cf vpn-show connections

顯示所有現行連線的相關資訊。

```
cf vpn-show connections
```
### cf vpn-show ike

顯示 IKE 連線的相關資訊。

```
cf vpn-show ike <policy name>
```
### cf vpn-show ipsec

顯示 IPSec 連線的相關資訊。

```
cf vpn-show ipsec <policy name>
```
### cf vpn-show gateway

顯示閘道的連線資訊。

```
cf vpn-show gateway <gateway name>
```
### cf vpn-show connection

顯示特定連線的所有資訊。

```
cf vpn-show connection <connection name>
```
### cf vpn-delete

刪除現有連線、原則或閘道。

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

更新現有 VPN 連線。

```
cf vpn-update connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### 參數
{: #p5}

**connection name：**
連線的名稱。


##### 選用參數：
{: #op5}

**gateway name：**
閘道的名稱。

**customer gateway IP address：**
VPN 通道的遠端端點 IP 位址。 

**subnet/mask：**
CIDR 格式的子網路位址。 

**-k：**
預先共用金鑰。

**-d：**所指定參數的說明。

**-peer_id：**遠端對等節點的 ID。VPN 通道的其他端點。

**-admin_state：**VPN 連線的狀態。值：UP 或 DOWN。

**-dpd-action：**偵測到對等節點為停用時所要採取的動作。值：hold、clear、disabled、restart 和 restart-by-peer。預設值：hold

**-gateway_ip：**本端 VPN 通道端點的 IP 位址。 

**-i：**起始器的狀態。預設值：bi-directional。

**-dpd-timeout：**逾時值（以秒為單位），在此期間之後會終止階段作業。範圍：6 - 86400 秒。預設值：120 秒

**-dpd-interval：**保留作用中間隔（以秒為單位）。依配置的間隔傳送保留作用中訊息，以檢查對等節點是否活躍。範圍：5 - 86399 秒。預設值：15 秒

**-ike：**IKE 原則的名稱。

**-ipsec：**IPSec 原則的名稱。


### cf vpn-update ike

更新 IKE 原則。

```
cf vpn-update ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 參數
{: #p6}

**policy name：**
IKE 原則的名稱。 

##### 選用參數：
{: #op6}

**gateway name：**閘道的名稱。 

**-d：**所指定參數的說明。

**-pfs：**Diffie-Hellman (DH) 群組 ID。值：Group2、Group5 和 Group14。預設值：Group2 

**-e：**加密演算法。值：aes-128、aes-192、aes-256 和 3des。預設值：aes-128

**-lv：**IKE 安全關聯的生命期限值。範圍：60 - 86400 秒。預設值：86400 秒


### cf vpn-update ipsec

更新 IPSec 原則。

```
cf vpn-update ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 參數
{: #p7}

**policy name：**
IPSec 原則的名稱。


##### 選用參數：
{: #op7}

**gateway name：**
閘道的名稱。

**-d：**所指定參數的說明。

**-pfs：**Diffie-Hellman (DH) 群組 ID。值：Group2、Group5 和 Group14。預設值：Group2 

**-e：**加密演算法。值：aes-128、aes-192、aes-256 和 3des。預設值：aes-128

**-lv：**安全關聯的生命期限值。範圍：60 - 86400 秒。預設值：3600 秒

### cf vpn-update gateway

更新現有 VPN 閘道。

```
cf vpn-update gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### 參數
{: #p8}

**gateway name：**
閘道的名稱。

#####選用參數：
{: #op8}

**-t：**您要啟用服務的儲存器。值：allSingleContainers、allContainerGroups 和 allContainers。預設值：無預設值；您必須指定類型。

**-gateway_ip：**
閘道的 IP 位址。 

**-subnets：**
CIDR 格式的子網路位址。 

# 相關鏈結
## 一般  
{: #general}  
* [IBM VPN 服務](../../../services/vpn/index.html)
* [Cloud Foundry CLI](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
