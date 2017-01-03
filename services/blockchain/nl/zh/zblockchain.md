---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# z 上的区块链
{: #zblockchain}
上次更新时间：2016 年 7 月 8 日
{: .last-updated}



您可以在 z/OS 中使用 Bluemix 专用产品中的区块链服务，以创建私有的安全数字资产，随后可以通过经许可的网络快速、安全地交易这些资产。*（作为简短描述组成部分的其他信息）*
{:shortdesc}


* 内容量值得自成一个部分吗？还是希望将其保留为“关于”下的嵌入主题？
* 需要有关 PBFT、安全性、性能和支持的信息。


## PBFT
{: #PBFT}

实用拜占庭容错 (PBFT) 是一种重要的共识协议，可针对每个部署单独进行插入和配置。`obcpbft` 包是重要 [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT") 共识协议的一种实现，可在验证者之间提供共识，尽管有某个阈值数量的验证者充当*拜占庭*，即恶意或以不可预测方式发生故障。在缺省配置中，PBFT 和 Sieve 都设计为至少在 *3t+1* 个验证者（副本）上运行，最多容忍 *t* 个潜在有故障（包括恶意或*拜占庭*）的副本。要了解有关核心 PBFT 功能的更多信息，请参阅 Linux Foundation 的 Hyperledger 项目中的[协议规范](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric)部分。 

观看 [![预览](http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)](http://www.youtube.com/watch?v=EKa5Gh9whgU)

*（需要指示用户需要了解 PBFT 的实际原因。PBFT 在 z 支持上的区块链中扮演的角色及其与此支持的关系。）*


### 支持的故障案例
{: #failure}

*在此支持和不支持的故障案例。*

*（Barry Mosakowski/Raleigh/IBM 或 Tuan Dang/Raleigh/IBM 可提供更多详细信息。）*

### z/OS 上专用产品的可用性
{: #Availability}

*基于 PBFT 测试的可用性和可用性预期。*

*（需要更多详细信息。）*

### 验证 PBFT 的基本功能
{: #Test PBFT}

*（来自 Gari 的输入。需要 Jason 提供有关如何执行测试步骤的更多详细信息，包括屏幕快照。）*

要验证基本 PBFT 功能，请执行以下步骤：

1. 对网络中的一个或多个同级提交交易。
2. 验证是否至少 *2f+1*（本例中为 3）个同级具有相同状态。*（如何验证？需要测试用例的详细信息。）*

  *使用 REST API 的示例*
3. 在仪表板上，单击相应按钮以停止同级 4。*（使用仪表板中的“停止同级”功能以停止同级 4。需要测试用例以描述详细操作。）*
4. 验证网络是否继续处理。*（如何验证？）*
5. 在仪表板上，单击相应按钮以停止同级 3。
6. 验证网络是否停止处理。
7. 在仪表板上，单击相应按钮以重新启动同级 3。

如果同级 3 赶上并且网络继续处理，那么您可以使用基本 PBFT 功能。

**注：**
* 重新启动同级 3 后，需要等待超时，然后才可向同级 3 提交新交易。

* 在网络停止处理时发送到活动同级的交易会缓存，并在网络继续处理后提交到网络。

## z 上区块链的环境
{: #z environment}

要在 z/OS 中使用 Bluemix 专用产品中的区块链服务，请确保您的环境满足以下需求：

* 四个同级网络，正在通过成员资格服务运行 PBFT。要了解有关成员资格服务的更多信息，请参阅 Linux Foundation 的 Hyperledger 项目中的[协议规范](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric)部分。 
* 一个隔离网络，不包含共享计算机或内存。
* 网络内隔离的同级。
* 云系统管理员不可访问的一个系统。

区块链监视器提供了区块链环境的概览图，并可检索有关网络的详细信息。要了解有关区块链环境以及如何对其进行监视的更多信息，请参阅 [Managing chaincode with the blockchain monitor](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) 和 [Sample apps and tutorials for blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html)。

## 安全性

*文档中没有提供安全信息吗？*

## 性能

*文档中没有提供性能信息吗？*

## 获取客户支持

如果在 z/OS 上使用 Bluemix 专用产品中的区块链服务时遇到问题，请遵循 IBM Bluemix 故障诊断过程。请参阅[故障诊断](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html)，以了解有关如何获取帮助的更多信息。
