---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 关于
{: #about}

{{site.data.keyword.bplong}} 可用于创建基础架构构建块。可以将 {{site.data.keyword.IBM_notm}} Cloud 服务组合使用以创建可部署且可复用的基础架构。
{:shortdesc}

{{site.data.keyword.bpshort}} 使用 Terraform 来简化基础架构管理。例如，对于使用应用程序服务器集群、负载均衡器和数据库服务器的服务，如果要启动该服务的多个副本，可以编写 bash 脚本来运行多个命令以启动这些组件。但是，使用运行器来获取配置并将其变成实资源会更轻松、更快速且更有条理。通过 Terraform，可以将大量资源作为一个集合组同时启动，在该组中映射了依赖关系。 

## 使用 {{site.data.keyword.bpshort}} 的理由
{: #reasons}

在以下场景中，您可能希望使用已编码的基础架构：
{:shortdesc}

| 场景     | 理由    |
| :------------- | :------------- |
| 您希望重新创建和复用基础架构。 | 可以使用 {{site.data.keyword.bpshort}} 来管理基础架构。使用 {{site.data.keyword.bpshort}}，可以通过编程方式来供应、修改和销毁资源。对资源进行编码和配置时，可以构建可反复复用的资源库以得到同样的结果。|
| 您需要透明地了解环境是如何设置的。 | {{site.data.keyword.bpshort}} 会使用源代码控制中的配置，这将支持协作、复查和审计跟踪，以便您了解更改是何时以及如何进行的。此外，如果需要回滚到先前的配置，还可以查看更改。 |
| 您希望简化环境更改的执行。 | {{site.data.keyword.bpshort}} 采用声明式模型，这种模型提供了单一的真实源。计划对环境进行更改时，可声明需要的结果。 |
| 您已经使用配置管理 (CM) 工具，但希望采用更自动化的方式来设置环境。 | {{site.data.keyword.bpshort}} 可以与 CM 工具一起使用。使用 {{site.data.keyword.bpshort}} 部署的环境是高度抽象的环境，可以创建基础架构资源。然后，可以使用 CM 工具在 {{site.data.keyword.bpshort}} 供应的资源上安装并配置软件。  
  
## 工作方式
{: #how}

可以使用 {{site.data.keyword.bpshort}} 将资源部署到环境。
{:shortdesc}

{{site.data.keyword.bpshort}} 将 Terraform 用作底层工具以支持基础架构作为代码，以便您可以将 {{site.data.keyword.IBM}} Cloud 资源定义为代码。Cloud 资源可以是基础架构中的不同组件，例如裸机服务器、虚拟服务器、负载均衡器和软件定义的联网组件。 

### 用于定义资源的配置
{: #how-define}

配置（即 Terraform 配置）是一个文件，用于定义构成基础架构的资源。配置是可部署的体系结构，可以应用于一个或多个环境。下图显示了配置的构成部分以及各部分如何一起工作以在 {{site.data.keyword.bpshort}} 中创建可部署的环境。


![{{site.data.keyword.bpshort}} 体系结构图](/images/anatomy_of_a_schematic.png)

图 1. {{site.data.keyword.bpshort}} 体系结构图

### 用于支持协作的源代码控制
{: #how-collaborate}

配置存储在 GitHub 中，以便团队可以复查代码并进行协作。使用 GitHub，您将具有内置审计跟踪，并可以查看对配置所做更改的完整落实历史记录。您可以在自述文件中保存用法信息，使配置可由多个团队共享并使用。

### 用于供应资源的 {{site.data.keyword.bpshort}} 环境
{: #how-provision}

可以使用 {{site.data.keyword.bpshort}} 来扫描 GitHub 中的代码，并将资源部署到环境。环境可以共享公共配置。例如，可以启动类似于生产的临时 QA 环境，然后在执行完测试后将其破坏掉。您可以构建可由您 {{site.data.keyword.Bluemix_notm}} 帐户中的所有用户进行标记并搜索的公共环境配置库。
