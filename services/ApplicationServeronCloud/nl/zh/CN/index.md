---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 入门
{: #getting_started}

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} 是一种服务，有助于您在 {{site.data.keyword.Bluemix_notm}} 的托管云环境中快速设置预配置的 WebSphere Application Server Liberty、传统 Network Deployment 或传统 WebSphere Java EE 实例。
{: shortdesc}

## WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 概述
{: #overview}

WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 为使用者提供预配置的传统 WebSphere 和 Liberty 概要文件服务器。
该服务在虚拟机上托管，具有根访问权的虚拟机访客可以访问访客操作系统。创建服务时，请在 *Liberty*、*传统 ND* 或*传统 WebSphere* 之间进行选择。

**注**：现在，使用者在创建新的*传统 ND* 或*传统 WebSphere* 实例时，可以选择 V8.5 或 V9.0。

为您提供了熟悉的 WebSphere 管理体验，并且您对底层的操作系统具有完全访问权。您可以复用现有脚本，并视需要进行一些系统微调，以便与您自己的或第三方的框架搭配使用。系统提供了管理中心和管理控制台来管理 WebSphere Application Server Liberty、ND 或传统服务，就像内部部署 WebSphere 配置那样。

WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment 套餐包含带有两个或更多虚拟机的 WebSphere Application Server Network Deployment 单元环境。第一个虚拟机包含 Deployment Manager 和 IBM HTTP Server，而其余的虚拟机包含联合到 Deployment Manager 的定制节点（节点代理程序）。使用现有的 wsadmin 脚本来创建 WebSphere 配置，或者使用 WebSphere 管理控制台来手动配置环境。这些新功能允许用户设置集群环境，这是任何中间件企业应用程序的一个关键方面。现在，客户可以选择建立拓扑集群，以实现两个或更多实例之间的请求负载平衡。


WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core 套餐包含使用 Liberty 集合。Liberty 集合是 Liberty 概要文件（服务器）组的管理域，该集合由两个或更多虚拟机组成。第一个虚拟机包含 Collective Controller Liberty 服务器作为 Liberty 集合的控制点。除了 Liberty 集合之外，此虚拟机还包含 IBM HTTP Server，允许从 Web 浏览器访问应用程序。其余的虚拟机是集合成员（Liberty 概要文件服务器）所在的集合主机。同时还在 Liberty 控制器服务器上启用了 Liberty 管理中心功能。

下图显示了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment 单元和 Liberty 集合环境的体系结构。

图 1. Network Deployment 单元和 Liberty 集合的体系结构

![图 1. Network Deployment 单元和 Liberty 集合的体系结构](images/CellCollectiveDiagram.gif)

**注**：在以上*图 1* 中，描述 Deployment Manager 或 Collective 控制器与 IBM HTTP Server 并置的模式用于开发和测试目的。WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 还允许您重新配置预安装的软件，以满足生产应用程序和操作需求，就像内部部署一样。有关最严格生产需求，请联系 IBM 销售代表，他们可以介绍单租户 IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 产品，该产品提供单独的网络和计算资源。


## 运营环境
{: #operational_environment}

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 是一种在共享环境中返回访客（虚拟机）供使用者部署应用程序的服务。VPN 可以使公共服务不用进行通用端口扫描，还可以使其免于遭受其他基于主动网络的攻击。但是，值得注意的是您用来访问服务实例的服务 VPN 可
能在多个 {{site.data.keyword.Bluemix_notm}} 组织和用户之间进行共享。虚拟机可提供计算资源、内存资源和 I/O 资源，这些资源都来自于 IaaS 资源共享池。

由于虚拟机在共享环境中运行特定的计算资源、内存资源和 I/O 资源，因此服务配置可能会所有不同。通过 IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 服务仪表板和门户网站，可查看每个特定服务实例的配置。

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 提供虚拟机实例。通过这些实例，客户可使用简单门户网站，以一致且可重复的方式创建并管理企业 WebSphere Application Server 部署，并极其自由地调整其应用程序。用户可对托管云环境中的预配置 WebSphere Application Server Liberty、ND 或传统虚拟机快速入门和熟悉运用。用户可将现有 WebSphere Application Server 应用程序迁移到 {{site.data.keyword.Bluemix_notm}}，并完全控制底层操作系统和中间件。

## 定价策略
{: #pricing_strategy}

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 为应用程序占用大量内存的客户提供了 T 恤型号的实例，以便使用更大型的虚拟机来合理调整其环境的大小。客户可选择具有特定资源大小且最多包含 32 GB RAM 虚拟机的已配置 WebSphere Application Server 组件或单个系统。

下表列出了 IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 套餐截至 2016 年 4 月 1 日的价格，以美元 (USD) 表示。

*表 1. Liberty Core 套餐*

| **T 恤** | **vCPU** | **RAM (GB)** | **HD (GB)** | **价格/小时** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.21 |
| M | 2 | 4 | 25 | $0.42 |
| L | 4 | 8 | 50 | $0.84 |
| XL | 8 | 16 | 100 | $1.68 |
| XXL | 16 | 32 | 200 | $3.36 |

*表 2. WebSphere Application Server 基本版套餐*

| **T 恤** | **vCPU** | **RAM (GB)** | **HD (GB)** | **价格/小时** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.30 |
| M | 2 | 4 | 25 | $0.60 |
| L | 4 | 8 | 50 | $1.20 |
| XL | 8 | 16 | 100 | $2.40 |
| XXL | 16 | 32 | 200 | $4.80 |

*表 3. WebSphere Application Server ND 套餐*

| **T 恤** | **vCPU** | **RAM (GB)** | **HD (GB)** | **价格/小时** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.70 |
| M | 2 | 4 | 25 | $1.40 |
| L | 4 | 8 | 50 | $2.80 |
| XL | 8 | 16 | 100 | $5.60 |
| XXL | 16 | 32 | 200 | $11.20 |

<p></p>

我们提供的 IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 适用以下收费标准：

*  *实例-小时*：对实例的定义是访问 IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 服务的特定配置。在结算周期内，针对所部署服务的每个实例执行的每个完整小时或部分小时对客户收费。每个“实例小时”按月计费，而如果当月仅部分时候使用了实例，那么将按比例计算使用率。

例如，如果使用 ND 计划，那么一个实例等于包含 2 GB RAM 和 12 GB HD 的 1vCPU。因此，如果选择为您的单元配置 1 个“控制”节点和 8 个“定制”节点，那么您需要为 9 个节点（实例）付费。

**注**：最低收费设置为每个“定制”节点或 Liberty 主机的 0.25 个实例小时。在上面的示例中，配置 1 个“控制”节点和 1 个“定制”节点长达 15 分钟即等于最低收费（0.25 * 实例数）。

**注**：根据特定的计算、内存和 I/O 资源量，对于处于“已停止”状态的累计实例，我们会向客户减免百分之五。客户的固定“已停止”实例数将会控制为 10 个 IP 地址或 64 GB 内存以内。

# 相关链接
{: #rellinks}
## 常规
{: #general}
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [WebSphere Application Server V9 文档](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
