---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IBM {{site.data.keyword.blockchain}} 入门
{: #gettingstartedtemplate}
上次更新时间：2016 年 11 月 10 日
{: .last-updated}

**注意：**在使用“入门模板开发者”套餐 (Beta) 或“高安全性业务网络”套餐 (GA) 之前，您必须阅读[您需要了解的内容](needtoknow.html)中的技术和支持信息。
<br><br>

## 产品套餐状态

“入门模板开发者”套餐是 Beta 发行版，提供多租户开发环境。“高安全性业务网络”套餐是 GA 发行版。“高安全性业务网络”套餐提供了高度安全的单租户 LinuxONE on z 环境，通过 [IBM Secure Service Container](etn_ssc.html) 进行代码隔离。
<br><br>

## IBM Blockchain on Bluemix

{{site.data.keyword.blockchainfull}} on Bluemix&reg; 服务提供了四节点开发和测试区块链网络供您选择，只需点击一个按钮即可使用。开发者不用从头创建区块链网络，而是可以立即开始编写应用程序并部署链代码。IBM Blockchain on Bluemix 服务是一种经许可的点对点网络，基于 Linux Foundation 的 Hyperledger 项目中的 [Hyperledger Fabric V0.6.1](https://github.com/hyperledger/fabric/tree/v0.6) 代码进行构建。
{:shortdesc}

区块链网络用于以安全、高效的方式交换和跟踪数字资产，并可将所有交易永久记录在共享分类帐上。有关区块链的详细信息，请参阅[关于区块链](ibmblockchain_overview.html)主题。
<br><br>

## 选择网络套餐

您有两个 IBM Blockchain on Bluemix 套餐可选择：**入门模板开发者网络**或**高安全性业务网络**。使用下面的比较图表可选择适合您的环境。

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Bluemix 套餐：      | 入门模板开发者网络       | 高安全性业务网络
| ------------------------- |:--------------------------:|:-----:|
| 状态：    | Beta     | GA |
| 用途：  |  开发，以及测试安全、性能和可用性级别 |  模拟企业网络，以及测试安全、性能和可用性级别 |
| 节点：    | 4 个节点 + 认证中心     | 4 个节点 + 认证中心 |
| [仪表板监视器：](ibmblockchainmonitor.html) | 是 | 是 |
| 保密交易： | 是 | 是 |
| [共识：](etn_pbft.html) | PBFT | PBFT |
| 环境：     | 共享多租户 | 隔离单租户 |
| [IBM Secure Service Container：](etn_ssc.html) | 否 | 是 |

<br>
## 启动网络套餐

使用以下步骤可创建并部署区块链网络的未绑定服务实例。网络包含具有验证节点和安全服务的开发环境，并支持您部署链代码、查看日志和构建应用程序：

1. 在 [{{site.data.keyword.blockchain}} 服务](https://console.ng.bluemix.net/catalog/services/blockchain/)页面上，填写右窗格中的**添加服务**表单：
  - **空间：**选择**开发**。
  - **应用程序：**选择**保留未绑定状态**，或将服务绑定到某个 Bluemix.org 应用程序（**选择应用程序**）。
  - **服务名称：**输入唯一名称或值，例如 **Blockchain Test Net123**。
  - **凭证名称：**保留缺省值。
  - **所选套餐：**选择**入门模板开发者**或**高安全性**。
  - 单击**创建**按钮。
2.  现在，您位于新服务的**服务仪表板**屏幕上。在其中，可以**管理**网络实例；单击**启动**以使用区块链监视器。
3.  区块链监视器显示网络详细信息、实时日志、当前分类帐状态、API 和链代码模板。使用仪表板可执行以下任一功能：
  - 访问网络同级的发现和 API 路径。
  - 查看任何正在运行的链代码容器。
  - 查看实时日志，并对链代码进行故障诊断。
  - 查看分类帐的全局状态。
  - 访问 Swagger UI，并通过 REST API 与网络进行交互。
  - 部署三个链代码示例之一。


# 相关链接
{: #rellinks}
## 教程和样本
{: #samples}
* [IBM Marbles Demo (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM Commercial Paper Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [IBM Car Lease Demo (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Art Auction Demo (Github)](https://github.com/ITPeople-Blockchain/auction)

## API 参考
{: #api}
* [Swagger UI](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [Hyperledger Fabric API (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## 相关链接
{: #general}
* [Fabric Code](https://github.com/hyperledger/fabric)
* [Whitepaper](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [Protocol Spec & Related Docs](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
