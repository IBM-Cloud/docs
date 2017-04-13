---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 高安全性业务网络
{: #etn_overview}


IBM Blockchain“高安全性业务网络”在隔离的高度安全环境中运行，从而有别于其他云托管的产品。操作系统、Fabric 和节点全部位于 IBM Secure Service Container 中，从而提供了企业客户采用 z Systems 技术所能获得的安全性和坚固性。IBM Secure Service Container 还能为对等通信、可用性、可伸缩性、硬件加密、防篡改加密密钥和安全加密的 VM 提供性能优化。  
{:shortdesc}

环境 (LinuxONE on z) 由实现 PBFT 且启用了“成员资格服务”的包含四个同级的网络构成，该网络在一个应用程序容器中运行。应用程序容器会保护系统中运行的区块链软件、链代码和数据。可以对安全引导内的区块链软件进行签名、验证和加密；区块链软件一旦安装在应用程序容器中，即具有防篡改功能。平台的 root 用户和系统管理员无法访问或查看安全容器内容。LinuxONE on z 还提供了 FIPS 合规性、高评估保证级别保护、高度可审计操作系统以及加密优化。

请参阅 [IBM Secure Service Container](etn_ssc.html) 部分，以获取有关安全功能的更多详细信息。
