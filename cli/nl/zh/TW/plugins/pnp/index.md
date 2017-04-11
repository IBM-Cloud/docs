---

copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Bluemix CLI 的專用網路對等作業外掛程式
{: #private_network_cli}

使用專用網路對等作業指令行介面 (CLI)，以配置及管理兩個 {{site.data.keyword.Bluemix}} 空間之間的專用網路對等作業。IBM Containers（Docker 容器）支援專用網路對等作業。Bluemix 空間可以位在相同地區的不同可用性區域中，也可以位在不同地區中。專用網路對等作業 CLI 外掛程式可以與 Bluemix CLI 外掛程式搭配使用。

專用網路對等作業 CLI 外掛程式適用於 Windows、MAC 及 Linux 作業系統。請確定您是使用適用的外掛程式。

開始之前，請建立 Bluemix 空間。請確定空間中的每一個容器都有不同網路的 IP 位址。如需詳細資料，請參閱[使用您自己的專用 IP 位址](https://www.{DomainName}/docs/containers/container_security_network.html#container_cli_ips_byoip)

**附註：**在您對 Bluemix 空間使用專用網路對等作業之後，如果需要刪除該空間，請先刪除該空間中的專用網路對等作業連線。

若要開始使用，請安裝 IBM Bluemix CLI。如需詳細資料，請參閱 [Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html)。

## 安裝專用網路對等作業 CLI 外掛程式

**附註**：如果您有舊版的已安裝外掛程式，則需要將它解除安裝。使用下列指令，以解除安裝外掛程式：

```
bluemix plugin uninstall private-network-peering
```
### 在本端安裝
從 [IBM Bluemix CLI 外掛程式儲存庫](http://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins)，下載您平台的專用網路對等作業外掛程式。

使用下列指令，以安裝專用網路對等作業外掛程式：

**附註**：請切換至外掛程式的位置，或指定外掛程式位置的路徑。

* 若為 Microsoft Windows OS：

```
bluemix plugin install private-network-peering-windows-amd64.exe
```

* 若為 Apple MAC OS：

```
bluemix plugin install private-network-peering-darwin-amd64
```

* 若為 Linux OS：

```
bluemix plugin install private-network-peering-linux-amd64
```

**附註**：當您安裝 Linux OS 的外掛程式時，如果看到顯示拒絕許可權的錯誤訊息，請執行下列指令，並變更許可權：

```
chmod a+x ./private-network-peering-linux-amd64
```

### 從 Bluemix 儲存庫安裝

遵循下列步驟，以從 Bluemix 儲存庫安裝外掛程式：

1. 新增 Bluemix 外掛程式登錄端點：
	```
	bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
	```

2. 請執行下列指令：

	```
	bluemix plugin install private-network-peering -r bluemix-bx
	```

## 專用網路對等作業指令清單
支援下列指令。使用 `bluemix network` 指令，以查看可用的指令清單：

| 指令     | 說明                                    |
|-------------|------------------------------------------------|
| pnp-routers | 列出對等作業的所有可用路由器        |
| pnp-create  | 建立專用網路對等作業連線   |
| pnp-delete  | 刪除專用網路對等作業連線   |
| pnp-show    | 列出所有專用網路對等作業連線  |
{: caption="表 1. 專用網路對等作業指令" caption-side="top"}


### 指令用法
若要檢視指令的說明資訊，請執行：`bluemix network [command] -h`。

#### 列出對等作業的所有可用路由器
```
bluemix network pnp-routers [--verbose (or -v)]
```

#####選用參數
{: #op1}

* **--verbose（或 -v）**（旗標）：檢視每一個路由器的詳細網路資訊。

######指令範例
{: #ex1}

若要檢視所有路由器的網路資訊，請執行下列指令：

	$ bluemix network pnp-routers
	Listing available routers ...
	OK

	IP              NAME            COMPUTE    REGION          ORGANIZATION    SPACE
	129.41.234.246  default-router  Container  US-South        ywu@us.ibm.com  demo1
	129.41.237.172  default-router  Container  US-South        ywu@us.ibm.com  demo2
	129.41.238.212  default-router  Container  United-Kingdom  ywu@us.ibm.com  demo3


若要檢視所有路由器的詳細網路資訊，請執行下列指令：


	$ bluemix network pnp-routers -v
	Listing available routers ...
	OK

	Router 'bce1aa25-bad0-4cf1-a831-d53c16463d06':
	FIELD          VALUE
	IP             129.41.234.246
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo1
	Networks       172.31.0.0/16

	Router '9ea160f2-1a30-44cd-bd25-794d441b274b':
	FIELD          VALUE
	IP             129.41.237.172
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo2
	Networks       172.25.0.0/16

	...


#### 使用 IP 位址建立專用網路對等作業連線
```
bluemix network pnp-create <router_ip> <router_ip> <name>
```

#####參數
{: #p1}

* **router_ip**：您要連接的兩個路由器的 IP 位址。您可以使用下列指令來找出 IP 位址：`bluemix network pnp-routers`
* **name**：專用網路對等作業連線的名稱。

######指令範例
{: #ex2}

	$ bluemix network pnp-create 129.41.234.246 129.41.237.172 demo
	Creating private network peering connection 'demo' ...
	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


####使用連線名稱建立專用網路對等作業連線

```
bluemix network pnp-create -i <name>
```

#####參數
{: #p2}

* **--interactive (-i)**（旗標）：互動模式以選取路由器。
* **name**：專用網路對等作業連線的名稱。

######指令範例
{: #ex3}

	$ bluemix network pnp-create -i demo
	Creating private network peering connection 'demo' ...
	List of available routers (select TWO for peering):

	#  ROUTER                          COMPUTE    REGION          ORGANIZATION    SPACE
	1  default-router(129.41.234.246)  Container  US-South        ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  Container  US-South        ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  Container  United-Kingdom  ywu@us.ibm.com  demo3

	Select first router for peering> 1
	Select second router for peering> 2

	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


#### 列出所有專用網路對等作業連線
```
bluemix network pnp-show [--verbose (or -v)]
```

#####選用參數
{: #op2}

* **--verbose（或 -v）**（旗標）：檢視每一個路由器的詳細網路資訊。

######指令範例
{: #ex4}

檢視基本資訊：

	$ bluemix network pnp-show
	Listing private network peering connections ...
	OK

	ID                                    NAME  STATUS  ROUTER1                         ROUTER2
	17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  Active  default-router(129.41.234.246)  default-router(129.41.237.172)

檢視詳細資訊：

	$ bluemix network pnp-show -v
	Listing private network peering connections ...
	OK

	Connection 'bedbc077-8040-41cc-a4aa-d9ce09a2e8ec':
	FIELD              VALUE
	Name               demo
	Status             Active
	Router1 Name       default-router
	Router1 IP         129.41.234.246
	Router1 Networks   172.31.0.0/16
	Router2 Name       default-router
	Router2 IP         129.41.237.172
	Router2 Networks   172.25.0.0/16


#### 刪除專用網路對等作業連線
```
bluemix network pnp-delete [--force (or -f)] <connection_id>
```
#####參數
{: #p3}
* **connection_id**：一個以上的連線 ID（以逗點隔開）。

#####選用參數
{: #op3}

* **--force（或 -f）**（旗標）：刪除連線，而不提示進行確認。

######指令範例：
{: #ex5}

刪除連線：

	$ bluemix network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	Warning: deleted connections cannot be restored.
	Are you sure you want to delete the connection? (yes/no)> yes

	Deleting private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' ...
	OK

	Private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' deleted.


刪除多個連線：

```
bluemix network pnp-delete [-f] <connection_id>,<connection_id>,<connection_id>
```
