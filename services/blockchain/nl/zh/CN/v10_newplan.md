---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 高安全性业务网络 (HSBN) vNext Beta
{: #etn_overview}

**HSBN vNext Beta** 提供可生成区块链业务网络的整体解决方案。该服务可快速为您供应网络并提供监视，以便轻松管理和维护资源。这种直截了当的形成和管控网络的流程可将更多的时间和精力直接用于开发和部署业务解决方案。
{:shortdesc}

**HSBN vNext Beta** 网络在 LinuxONE 上的高安全性环境中运行，其中网络资源（同级、订单、CA、源代码、分类帐）全部包含在 **IBM Secure Service Container** (SSC) 中。功能如下：
* 对等通信的性能优化
* 高可用性和可扩展性框架 
* 硬件加密、篡改防护密钥和安全加密的虚拟机
* 具有防篡改软件的安全启动
* 无根访问权
* FIPS 合规性、高 EAL 保护、可审计性和加密优化

**HSNB vNext Beta** 套餐的预订包括支持以下网络资源：

- 崩溃容错订购服务
- 每个成员 2 个同级
- 多达 5 个额外网络成员
- 每个成员 5 个实例化链代码
- 成员特定认证中心
- 多达 100 个通道
- 缺省管控策略（所有成员都是管理员且可以发出加入网络的邀请）

请参阅 [IBM Secure Service Container](etn_ssc.html) 一节，以获取有关环境安全功能的更多详细信息。

## 使用 HSBN vNext Beta 套餐
{: #use_hsbn}

### 套餐访问

IBM Blockchain on Bluemix **HSBN vNext Beta** 套餐按请求授权。当您从 Bluemix 目录中选择 HSBN vNext Beta 时，您加入最新 Beta 发行版的请求即会发送到 IBM Blockchain 团队。一旦获得核准，您将收到电子邮件邀请，以参与该套餐；请遵循指示信息来启动 HSBN vNext Beta 套餐仪表板。

在 HSBN vNext Beta 仪表板上，从三个选项中进行选择：
1. **网络快速入门**：创建 HSBN vNext Beta 网络，并邀请其他 Bluemix 组织加入。
2. **加入网络**：查看对您的邀请以加入其他 HSBN vNext Beta 网络。
3. **监视网络**：管理网络资源 - 同级、通道和链代码。

<!-- to do - the rest of this page final edit -->

### 样本场景

假设您是大理石制造商，想要利用 IBM Blockchain 网络与不同的供应商进行事务处理。这将如何运作？您可以创建一个联盟通道，其中包含所有网络成员和公共可用大理石存储库的当前状态。该网络上的所有成员都可查看和查询在此通道上发生的任何事务处理。但是，您还可以创建“子通道”或独立式通道，以满足隐私和机密性要求。例如，在某个供应商满足特定一组条件时，您可以为该供应商提供更好的价格。此事务处理可在子通道上执行，同时确保对整个大理石供应的影响在联盟通道中得到更新。或者，您也许想要交易在联盟通道中不可用的特定类别的大理石。您只要在独立式通道上与必要方进行事务处理即可，这不会影响到联盟通道的分类帐。通道为隐私提供了强大的机制，这是因为它们全部都有独特的分类帐，且只有向该通道预订和认证的成员才可与分类帐进行交互。  

### 创建网络
{: create_a_network}
网络包含以下组件：
* 订购服务，负责认证事务处理并将它们订购到区块，以写入通道分类帐。
* 成员特定认证中心 (CA)，负责为每个成员的网络组件发出身份材料。
* 成员特定同级，执行并提交事务处理，同时维护通道分类帐。

在区块链服务的仪表板上，单击**网络快速入门**按钮并遵循以下向导：
1. 在**命名网络**页面上，输入代表成员身份的区块链网络名称和公司名称，然后单击**下一步**；
2. 在下一个**邀请成员**页面上，为您要邀请的参与者指定相关组织信息。在加入网络时，系统会为每个参与者供应同级和 CA，所有网络成员都将为他们加入的任何通道维护一个分类帐。<br>
   **注：**您最多可以邀请 5 个成员加入网络。
3. 在**定义管控规则**页面上，您将看到网络策略设置。缺省情况下，网络中的任何人都可以创建新通道并邀请成员。  
4. 在**生成证书**页面上，使用**自动生成**选项，为组织的网络组件创建证书。这些 x509 证书不会向用户公开。  
5. 最后，在**查看摘要**页面上，查看网络的配置，然后单击**完成**以引导网络。

此过程即完成网络的初始设置。

### 加入网络
{: invite_members}

初始化网络后，被邀请者将收到电子邮件，指示邀请加入的网络和加入指示信息。被邀请者将看到在 HSBN vNext 套餐仪表板上启用**待邀请**按钮。单击该按钮以加入网络：

1. 在列表上选择网络并单击**加入网络**。
2. 在下一个屏幕上，查看管控规则并单击**下一步**。
3. 在**生成证书**页面上，输入“组织名称”，然后选择**自动生成**选项。
4. 在**查看网络摘要**页面上，查看网络的设置，然后单击**完成**。设置还会显示已收到加入网络邀请的**受邀参与者**。

请参阅[监视器](v10_dashboard.html)以获取创建通道以及安装/实例化链代码的指示信息。

<!-- I think all of this is adequately covered in the Monitor Section; and we already tell the story in the Sample Scenario topic above -->


<!-- From Jeff: Agreed. Commenting out all the rest sections on the page.


### Creating new channels
{: prepare_private_channels}

With the latest HSBN vNext plan, you can create a private channel, install a customized chaincode, complete the trade, and update the inventory number upon the other parties in the network make a query or propose a new transaction.

1. On the HSBN vNext plan dashboard, select **Enter Monitor**.
2. Select **Channels**, and click **New Channel**.
3. On the **Create a Channel** page, enter the channel name and choose the company that you want to make trade with by adding members. Then, click **Create** to create another private consortium channel.
4. Select **Chaincode** after you click the **Enter Monitor** button on the dashboard. You can view the chaincode that are already installed on your peer, or install a new chaincode to the peer.<br>
  **Note:** You can install at most 5 chaincode apps per peer.
5. Click **Install Chaincode** to install the smart contract to the peer. A smart contract, also known as chaincode, is the programmatic code installed and instantiated onto a channel’s peers by an appropriately authorized member. End users then invoke chaincode through a client-side application that interfaces with a network peer. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state. Chaincode can be developed for business contracts, asset definitions, and collectively-managed decentralized applications. You can download [this sample code](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} to your local environment for testing.

**Note:** After you install the chaincode onto the peer, you must instantiate the chaincode by providing the initial arguments. In the case of the Marbles sample chaincode, you can input `marble1, blue, 35` in a comma separated list to indicate that you have 35 blue marble1 for trade.


### Commencing transactions
{: commence_txs}

To make transactions within your network, the trading parties must:
* Join the same channel within the network.
* Install the same version of the chaincode onto the peer that represents each organization.


Each successful transaction results in a new block appended to the blockchain, and the ledger in the levelDB updated with the new state. Other members in the network can query the ledger or the transaction history to decide the next transaction.



### Monitoring your network
{: monitor_network}

You can perform the following tasks after you click the **Enter Monitor** button on the dashboard:
* Create new channels and invite other members to join your channels to trade privately.
* Install new chaincodes to your peer to initiate or participate into new trade.
* View the changes of blocks, transactions, chaincode invocations.
* View the log on your peer.
* View the information of resources that your organization owns.
* Export a JSON file containing the low-level networking information for each of your components (such as enrollID/enrollSecret for your CA).  

See the [HSBN vNext Beta dashboard](v10_dashboard.md) for more information about the usage of each panel on the dashboard. 


-->
