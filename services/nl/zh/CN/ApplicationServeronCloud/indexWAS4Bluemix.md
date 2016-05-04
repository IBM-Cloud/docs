---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM WebSphere Application Server for Bluemix 入门
{: #getting_started}

*上次更新时间：2016 年 4 月 8 日*

{{site.data.keyword.IBM}}WebSphere Application Server for {{site.data.keyword.Bluemix}} 是一种服务，有助于您在 Bluemix 的托管云环境中快速设置预配置的 WebSphere Application Server Liberty、Network Deployment 或传统实例。
{: shortdesc}

## WebSphere Application Server for Bluemix 概述
{: #overview}

WebSphere Application Server for Bluemix 为使用者提供预配置的传统 WebSphere 和 Liberty 概要文件服务器。
该服务在虚拟机上托管，具有根访问权的虚拟机访客可以访问访客操作系统。创建服务时，请在 *Liberty*、*ND* 或*传统 WebSphere* 之间进行选择。

为您提供了熟悉的 WebSphere 管理体验，并且您对底层的操作系统具有完全访问权。您可以复用现有脚本，并视需要进行一些系统微调，以便与您自己的或第三方的框架搭配使用。系统提供了管理中心和管理控制台来管理 WebSphere Application Server Liberty、ND 或传统服务，就像内部部署 WebSphere 配置那样。

**注**：WebSphere Application Server for Bluemix Network Deployment 计划现在具有更多功能。该计划包含带有两个或更多虚拟机的 WebSphere Application Server Network Deployment 单元环境。第一个虚拟机包含部署管理程序和 IBM HTTP Server，而其余的虚拟机包含联合到部署管理程序的定制节点（节点代理程序）。使用现有的 wsadmin 脚本来创建 WebSphere 配置，或者使用 WebSphere 管理控制台来手动配置环境。这些新功能允许用户设置集群环境，以用于高可用性、故障转移和可扩展性。集群是任何中间件企业应用程序的一个关键方面，并且客户现在可以选择建立拓扑集群，以实现两个或更多实例之间的请求负载平衡。


WebSphere Application Server for Bluemix Liberty Core 计划还提供了更多功能。该计划包含使用 Liberty 集合，作为 Liberty 概要文件（服务器）组的管理域，该集合由两个或更多虚拟机组成。第一个虚拟机包含 Collective Controller Liberty 服务器作为 Liberty 集合的控制点。除了 Liberty 集合之外，此虚拟机还包含 IBM HTTP Server，允许从 Web 浏览器访问应用程序。其余的虚拟机是集合成员（Liberty 概要文件服务器）所在的集合主机。同时还在 Liberty 控制器服务器上启用了 Liberty 管理中心功能。

下图显示了 WebSphere Application Server for Bluemix Network Deployment 单元和 Liberty 集合环境的体系结构。

![图 1. Network Deployment 单元和 Liberty 集合的体系结构](images/CellCollectiveDiagram.gif)

## 运营环境
{: #operational_environment}

IBM WebSphere Application Server for Bluemix 是一种在共享环境中返回访客（虚拟机）供使用者部署应用程序的服务。VPN 可以使公共服务不用进行通用端口扫描，还可以使其免于遭受其他基于主动网络的攻击。但是，值得注意的是您用来访问服务实例的服务 VPN 可能在多个 Bluemix 组织和用户之间进行共享。虚拟机可提供计算资源、内存资源和 I/O 资源，这些资源都来自于 IaaS 资源共享池。如果要在专用环境中运行应用程序，请联系 IBM 销售代表，他们可为您介绍我们的专用 IBM WebSphere Application Server for Bluemix 产品。

由于虚拟机在共享环境中运行特定的计算资源、内存资源和 I/O 资源，因此服务配置可能会所有不同。通过 IBM WebSphere Application Server for Bluemix 服务仪表板和门户网站，可查看每个特定服务实例的配置。

**注**：IBM WebSphere Application Server for Bluemix 现在为应用程序占用大量内存的客户提供了一个选项，以便使用更大型的虚拟机来合理调整其环境的大小。客户可选择具有特定资源大小且最多包含 32 GB RAM 虚拟机的已配置 WebSphere Application Server 组件或单个系统。

## 定价策略
{: #pricing_strategy}

IBM WebSphere Application Server for Bluemix 提供虚拟机实例。通过这些实例，客户可使用简单门户网站，以一致且可重复的方式创建并管理企业 WebSphere Application Server 部署，并极其自由地调整其应用程序。用户可对托管云环境的预配置 WebSphere Application Server Liberty、ND 或传统虚拟机快速入门和熟悉运用。用户可将现有 WebSphere Application Server 应用程序迁移到 Bluemix，并完全控制底层操作系统和中间件。

我们提供的 IBM WebSphere Application Server for Bluemix 适用以下收费标准：

*  *实例-小时*：对实例的定义是访问 IBM WebSphere Application Server for Bluemix 服务的特定配置。在结算周期内，针对所部署服务的每个实例执行的每个完整小时或部分小时对客户收费。每个“实例小时”按月计费，而如果当月仅部分时候使用了实例，那么将按比例计算使用率。

例如，如果使用 ND 计划，那么一个实例等于包含 2 GB RAM 和 12 GB HD 的 1vCPU。因此，如果选择为您的单元配置 1 个“控制”节点和 8 个“定制”节点，那么您需要为 9 个节点（实例）付费。

**注**：最低收费设置为每个“定制”节点或 Liberty 主机的 0.25 个实例小时。在上面的示例中，配置 1 个“控制”节点和 1 个“定制”节点长达 15 分钟即等于最低收费（0.25 * 实例数）。

# 相关链接
## 常规
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [WebSphere Application Server 文档](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/as_ditamaps/was855_welcome_ndmp.html){: new_window}
* [WebSphere Application Server 传统 V9 Beta 文档](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
