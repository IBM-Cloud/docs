---

copyright:
  years: 2017
lastupdated: "2017-03-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HSBN 已知问题
{: #etn_overview}



已报告了以下 HSBN 套餐问题：

1. 使用利用 Hyperledger Fabric V0.6.1 的“高安全性业务网络”时，如果有大约 50 个以上的链代码部署，建议在开发阶段定期重置该网络。重置网络可除去已部署的链代码以及已收集的数据。对于已经被迭代开发阶段内进行的改进所取代的较旧链代码，可借机除去这些代码。如果您处于开发后阶段，那么应该监视链代码部署数，以便留出容量用于最重要的链代码。
2. 执行网络和同级的状态查询时，收到不定时发生的“503 服务不可用”和“502 网关错误”错误。
3. 在 vp1 的日志中，可能有“Server.Serve 未能完成安全握手”消息。这是非致命错误，与网络运行无关。
4. **服务凭证**可能无法自动填充；在这种情况下，请如下所示生成凭证：

 a) 在“服务仪表板”中，单击**服务凭证**选项卡：

  ![服务凭证 HSBN](images/hsbn.png "服务凭证 HSBN")

 b) 在**服务凭证**选项卡中，单击**新建凭证**的按钮。

  ![新建凭证 HSBN](images/hsbn1.png "新建凭证 HSBN")

c) 这将显示标题为**添加新凭证**的新窗口；单击此窗口底部的**添加**按钮：

  ![添加新凭证 HSBN](images/hsbn2.png "添加新凭证 HSBN")

 d) 现在，屏幕应该看起来类似以下示例。单击**查看凭证**将显示包含 HSBN 实例的服务凭证的 JSON 有效内容。  

  ![凭证已生成 HSBN](images/hsbn3.png "凭证已生成")


## 获取帮助

有关 IBM Blockchain on Bluemix 网络的支持和帮助，请参阅[获取帮助](ibmblockchain_support.html)。
