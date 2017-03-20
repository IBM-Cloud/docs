---

copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Bluemix CLI 的专用网络对等连接插件
{: #private_network_cli}

使用专用网络对等连接命令行界面 (CLI) 可配置和管理两个 {{site.data.keyword.Bluemix}} 空间之间的专用网络对等连接。IBM Containers（Docker 容器）支持专用网络对等连接。Bluemix 空间可以位于同一区域中的不同可用性区域中，也可以位于不同区域中。专用网络对等连接 CLI 插件可与 Bluemix CLI 插件一起使用。

专用网络对等连接 CLI 插件可用于 Windows、MAC 和 Linux 操作系统。请确保使用适合于您的插件。

开始之前，请先创建 Bluemix 空间。确保空间中的每个容器都具有来自不同网络的 IP 地址。有关详细信息，请参阅[使用自己的专用 IP 地址](https://www.{DomainName}/docs/containers/container_security_network.html#container_cli_ips_byoip)。

**注：**将专用网络对等连接用于 Bluemix 空间后，如果需要删除空间，请首先删除该空间内的专用网络对等连接。

首先，请安装 IBM Bluemix CLI。有关详细信息，请参阅 [Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html)。

## 安装专用网络对等连接 CLI 插件

**注**：如果已安装先前版本的该插件，您需要将其卸载。使用以下命令来卸载插件：

```
bluemix plugin uninstall private-network-peering
```
### 本地安装
从 [IBM Bluemix CLI 插件存储库](http://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins)下载适用于您平台的专用网络对等连接插件。

使用以下命令来安装专用网络对等连接插件：

**注**：切换到插件所在位置，或指定插件位置的路径。

* 对于 Microsoft Windows 操作系统：

```
bluemix plugin install private-network-peering-windows-amd64.exe
```

* 对于 Apple MAC OS：

```
bluemix plugin install private-network-peering-darwin-amd64
```

* 对于 Linux 操作系统：

```
bluemix plugin install private-network-peering-linux-amd64
```

**注**：在为 Linux 操作系统安装插件时，如果看到错误消息指示许可权被拒绝，请运行以下命令并更改许可权：

```
chmod a+x ./private-network-peering-linux-amd64
```

### 从 Bluemix 存储库进行安装

执行以下步骤以从 Bluemix 存储库安装插件：

1. 添加 Bluemix 插件注册表端点：
	```
	bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
	```

2. 运行以下命令：

	```
	bluemix plugin install private-network-peering -r bluemix-bx
	```

## 列出专用网络对等连接命令
支持以下命令。使用 `bluemix network` 命令可查看可用命令的列表：

| 命令     | 描述                                    |
|-------------|------------------------------------------------|
| pnp-routers | 列出用于对等连接的所有可用路由器        |
| pnp-create  | 创建专用网络对等连接   |
| pnp-delete  | 删除专用网络对等连接   |
| pnp-show    | 列出所有专用网络对等连接  |
{: caption="表 1. 专用网络对等连接命令" caption-side="top"}


### 命令用法
要查看命令的帮助信息，请运行：`bluemix network [command] -h`。

#### 列出用于对等连接的所有可用路由器
```
bluemix network pnp-routers [--verbose（或 -v）]
```

#####可选参数
{: #op1}

* **--verbose（或 -v）**（标志）：查看有关每个路由器的详细网络信息。

######命令示例
{: #ex1}

查看有关所有路由器的网络信息：

	$ bluemix network pnp-routers
	正在列出可用路由器...
	正常

	IP              名称            计算    区域          组织            空间
	129.41.234.246  default-router  容器    美国（南部）  ywu@us.ibm.com  demo1
	129.41.237.172  default-router  容器    美国（南部）  ywu@us.ibm.com  demo2
	129.41.238.212  default-router  容器    英国          ywu@us.ibm.com  demo3


查看有关所有路由器的详细网络信息：


	$ bluemix network pnp-routers -v
	正在列出可用路由器...
	正常

	路由器“bce1aa25-bad0-4cf1-a831-d53c16463d06”：
	字段           值
	IP             129.41.234.246
	名称           default-router
	计算           容器
	区域           美国（南部）
	组织           ywu@us.ibm.com
	空间           demo1
	网络           172.31.0.0/16

	路由器“9ea160f2-1a30-44cd-bd25-794d441b274b”：
	字段           值
	IP             129.41.237.172
	名称           default-router
	计算           容器
	区域           美国（南部）
	组织           ywu@us.ibm.com
	空间           demo2
	网络           172.25.0.0/16

	...


#### 使用 IP 地址来创建专用网络对等连接
```
bluemix network pnp-create <router_ip> <router_ip> <name>
```

#####参数
{: #p1}

* **router_ip**：要连接的两个路由器的 IP 地址。可以使用命令 `bluemix network pnp-routers` 来查找 IP 地址。
* **name**：专用网络对等连接的名称。

######命令示例
{: #ex2}

	$ bluemix network pnp-create 129.41.234.246 129.41.237.172 demo
	正在创建专用网络对等连接“demo”...
	正在连接“default-router(129.41.234.246)”和“default-router(129.41.237.172)”...
	正常

	专用网络对等连接“demo”已创建。


####使用连接名称来创建专用网络对等连接

```
bluemix network pnp-create -i <name>
```

#####参数
{: #p2}

* **--interactive (-i)**（标志）：以交互方式选择路由器。
* **name**：专用网络对等连接的名称。

######命令示例
{: #ex3}

	$ bluemix network pnp-create -i demo
	正在创建专用网络对等连接“demo”...
	可用路由器列表（请选择两个路由器用于对等连接）：

	#  路由器                          计算    区域          组织            空间
	1  default-router(129.41.234.246)  容器   美国（南部）  ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  容器   美国（南部）  ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  容器   英国          ywu@us.ibm.com  demo3

	选择用于对等连接的第一个路由器 > 1
	选择用于对等连接的第二个路由器 > 2

	正在连接“default-router(129.41.234.246)”和“default-router(129.41.237.172)”...
	正常

	专用网络对等连接“demo”已创建。


#### 列出所有专用网络对等连接
```
bluemix network pnp-show [--verbose（或 -v）]
```

#####可选参数
{: #op2}

* **--verbose（或 -v）**（标志）：查看有关每个路由器的详细网络信息。

######命令示例
{: #ex4}

查看基本信息：

	$ bluemix network pnp-show
	正在列出专用网络对等连接...
	正常

	标识                                  名称  状态    路由器 1                        路由器 2
 17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  活动    default-router(129.41.234.246)  default-router(129.41.237.172)

查看详细信息：

	$ bluemix network pnp-show -v
	正在列出专用网络对等连接...
	正常

	连接“bedbc077-8040-41cc-a4aa-d9ce09a2e8ec”：
	字段               值
	名称               demo
	状态               活动
	路由器 1 名称      default-router
	路由器 1 IP        129.41.234.246
	路由器 1 网络      172.31.0.0/16
	路由器 2 名称      default-router
	路由器 2 IP        129.41.237.172
	路由器 2 网络      172.25.0.0/16


#### 删除专用网络对等连接
```
bluemix network pnp-delete [--force（或 -f）] <connection_id>
```
#####参数
{: #p3}
* **connection_id**：一个或多个连接标识，用逗号分隔。

#####可选参数
{: #op3}

* **--force（或 -f）**（标志）：删除连接，而不提示确认。

######命令示例：
{: #ex5}

删除连接：

	$ bluemix network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	警告：删除的连接无法复原。
	确定要删除连接吗？（是/否）> 是

	正在删除专用网络对等连接“17b1c3c7-d614-4fc5-9afe-961e38ee79f8”...
	正常

	专用网络对等连接“17b1c3c7-d614-4fc5-9afe-961e38ee79f8”已删除。


删除多个连接：

```
bluemix network pnp-delete [-f] <connection_id>,<connection_id>,<connection_id>
```
