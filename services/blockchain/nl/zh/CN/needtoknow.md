---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 免责声明
{: #etn_overview}

**注意：**使用任何 IBM Blockchain on Bluemix 套餐之前，必须查看以下信息。

## IBM 支持声明

IBM 一直以来都在创新方面颇具领导能力，在 IBM Blockchain on Bluemix 产品套餐中亦是如此。Blockchain 是一种快速处理技术，预计将影响从金融到供应链乃至物流的多个行业。IBM 客户和业务合作伙伴通过各种早期采用程序，一直积极推动区块链作为业界的解决方案。IBM Blockchain on Bluemix 就是这样一种程序。**就像任何新技术一样，IBM Blockchain on Bluemix 用户应该意识到可能发生的快速而基本的更改**。  
{:shortdesc}

IBM Blockchain 背后的体系结构是 Linux Foundation 的 Hyperledger 项目。Fabric 目前处于*活动*状态，且处于持续开发中。每一个开放式源代码社区贡献都会改进 Hyperledger Fabric，但是会带来采用挑战。在*活动*项目周期中，客户可使用 Hyperledger Fabric V1.0 进行网络测试和模拟。**IBM 提醒不要直接在任何 Hyperledger Fabric 区块链网络上定义或交换金融资产或任何有价值的资产**。  

## 开放式源代码声明

**高安全性业务网络 (HSBN) vNext Beta** 套餐以 Linux Foundation 的 Hyperledger Fabric V1.0 开放式源代码为基础构建。“入门模板开发者”和“高安全性业务网络”(HSBN) 套餐以 Hyperledger Fabric V0.6 代码为基础构建。Hyperledger 项目成员（包括 IBM）将持续向源代码提供代码，然后代码将由社区进行审查、核实和测试。
Hyperledger Fabric V1.0 目前处于*活动*状态；有关*活动*状态的详细信息，以及有关 Hyperledger 项目的整个生命周期的详细信息，请访问以下站点：https://wiki.hyperledger.org/community/project-lifecycle。  

## 链代码支持声明

IBM Blockchain 网络不支持以下编码实践：

1. 使用具有迭代的相关联数组（顺序在 Go 中为随机的）。
2. 从 KVS 表中读取项目列表（不保证顺序）。
3. 编写线程不安全链代码（可能会并行调用查询和呼叫调用）。
4. 在链代码中将全局内存或高速缓存存储器替换为分类帐状态变量。
5. 从链代码中直接访问外部服务，如数据库。
6. 使用可能引入非确定性的库或全局变量（如使用“random”或“time”）。
7. 使用 GetRows 进行迭代。  

此外，HSBN 和入门模板套餐 (Hyperledger Fabric V0.6) 不支持非确定性链代码，这会对数据一致性和完整性产生风险；有关详细信息，请参阅[非确定性链代码](nondeterministic.html)。
