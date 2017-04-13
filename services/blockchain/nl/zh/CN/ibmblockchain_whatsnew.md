---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 新增功能
{: #whatsnew}

**HSBN vNext Beta** 套餐以稳定提交的 [Hyperledger Fabric V1.0](https://www.hyperledger.org/){:new_window} 开放式源代码库为基础构建。Hyperledger Fabric V1.0 实施模块化体系结构，可提供灵活、安全和可定制的平台，用于构建企业区块链网络。  
{: shortdesc}

**HSBN vNext Beta** 服务远不止是单个沙箱环境，其可利用资源组，跨各种 Bluemix 组织提供分布式区块链网络。有关网络体系结构的更多信息，请参阅[概述](v10_netoverview.html)主题。

## V1.0 中的新体系结构
{:why}

Hyperledger Fabric 体系结构在 V1.0 中取得了长足发展，其可为致力于安全性、可扩展性、机密性和性能的企业级网络提供强大支持。
同级分成两个不同的运行时 - **保证**和**提交** - 而事务处理订购的责任已提取到另一个组件中。
至于隐私和机密性问题则交由通道解决，其可提供数据隔离。
分类帐按通道存在，因此可以对网络进行定制以支持双边、多边甚至公共事务处理的不同组合。


请查看 [Hyperledger 体系结构深入探究](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window}一节，以获取网络拓扑和交互的更多信息。

## 其他更改

HSBN vNext Beta 套餐还包括以下更改：
* [新仪表板](v10_dashboard.html)允许订户创建区块链网络、邀请成员、加入其他网络，以及管理资源和资产。

* [V1.0 的新 Marbles 示例链代码应用程序](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window}可试验最新的代码库。
* Hyperledger Fabric V1.0 中的新[事务处理流程](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html)通过在整个事务处理过程中实施多个检查点，可确保数据一致性和完整性。

