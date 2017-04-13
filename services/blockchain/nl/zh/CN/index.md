---

copyright:
  years: 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 入门
{: #gettingstartedtemplate}

**注意：**在使用任何 IBM Blockchain on Bluemix 套餐之前，您必须阅读[免责声明](needtoknow.html)中的技术和支持信息。
{:shortdesc}

## IBM Blockchain on Bluemix

{{site.data.keyword.blockchainfull}} on Bluemix&reg; 服务包含三种区块链网络套餐。最新的套餐**高安全性业务网络 (HSBN) vNext Beta** 以 Hyperledger Fabric V1.0 代码库为基础构建，其利用模块化体系结构来提供新功能。通过 IBM Blockchain on Bluemix 套餐，开发者可以立即编写链代码应用程序并进行测试，而无需设计和配置专用区块链网络。链代码是在 Fabric 区块链网络上得以实现安全高效资产交换，以及在分类帐上得以永久记录这些事务处理背后的引擎

## 产品套餐

新 IBM Blockchain on Bluemix 订户现在可以加入 **HSBN vNext Beta** 套餐。这款最新的产品以 Hyperledger Fabric V1.0 为基础进行构建，其提供下一代的安全性、完整性、可扩展性和性能。表 1 描述 Bluemix 套餐：

表 1：IBM Blockchain on Bluemix 套餐  

| Bluemix 套餐      | 状态       | 新订户可以使用  | Hyperledger Fabric 版本
| ------------------------- |:--------------------------:|:-----:|:-----:|
| **HSBN vNext Beta** (1)   | Beta     | 是 |  V1.0 |
| HSBN (2) |  GA |  是 |  V0.6 |
| 入门模板开发者 (3)    | Beta     | 是 | V0.6 |

(1) **高安全性业务网络 (HSBN) vNext Beta** 套餐提供加入 Bluemix 组织并构建分布式区块链网络的简单机制。  
(2) **高安全性业务网络 (HSBN) GA** 套餐提供了高度安全的单租户 LinuxONE on z Systems 环境，通过 [IBM Secure Service Container](etn_ssc.html) 进行代码隔离。  
(3)“入门模板开发者”Beta 套餐提供仅多租户开发环境。  

## 产品套餐详细信息

表 2 提供 IBM Blockchain on Bluemix 产品套餐的详细比较。新 IBM Blockchain on Bluemix 订户必须选择 **HSBN vNext Beta** 套餐。新订户无法选择 HSBN 和“入门模板开发者”套餐，但 IBM 仍支持这两个套餐：

表 2：IBM Blockchain on Bluemix 套餐详细信息  

| Bluemix 套餐：      | 入门模板开发者网络       | 高安全性业务网络       | 高安全性业务网络 (HSBN) vNext Beta
| ------------------------- |:--------------------------:|:-----:|:-----:|
| 状态：    | Beta     | GA | Beta |
| 用途：  |  开发，以及测试安全、性能和可用性级别 |  模拟企业网络，以及测试安全、性能和可用性级别 |  设置具有生产级别安全性、性能和可用性的企业业务网络 |
| 节点：    | 4 个同级 + 认证中心     | 4 个同级 + 认证中心 | 网络组件的动态管理 |
| 仪表板监视器： | [是](ibmblockchainmonitor.html) | [是](ibmblockchainmonitor.html) | [是](v10_dashboard.html) |
| 环境：     | 共享多租户 | 隔离单租户 | 多个隔离级别 |

# 相关链接
{: #rellinks}
## 教程和样本
{: #samples}
* [IBM Marbles Demo (GitHub)](https://github.com/IBM-Blockchain/marbles) - V0.6 和 V1.0
* [IBM Commercial Paper Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme) - V0.6
* [IBM Car Lease Demo (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) - V0.6
* [Art Auction Demo (Github)](https://github.com/ITPeople-Blockchain/auction) V0.6 - V1.0（本地运行）

## API 参考
{: #api}
* [Hyperledger Fabric API (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## 相关链接
{: #general}
* [Fabric Code](https://github.com/hyperledger/fabric)
* [Fabric Composer](https://fabric-composer.github.io/)
* [Fabric V1.0 文档](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [Fabric V0.6 文档](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
