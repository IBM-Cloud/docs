---

copyright:
  years: 2017
lastupdated: "2017-03-15"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# IBM Secure Service Container
{: #etn_ssc}

**HSBN vNext Beta** 套餐和 HSBN 套餐作为设备部署到 IBM Secure Service Container 中，后者将为托管区块链服务提供基本的基础架构。该设备将自主工作的操作系统、Docker 容器、中间件和软件组件组合在一起，并提供安全性经过优化的核心服务和基础架构。
{:shortdesc}

以下体系结构图说明了 IBM Secure Service Container 和区块链设备是如何进行组织的：

![体系结构图](images/Architecture_HSBN_SSC_vNext.png "IBM Secure Service Container 和区块链设备")
*图 1. IBM Secure Service Container 和区块链设备概览图*

IBM Secure Service Container 为区块链服务带来了 z Systems LinuxONE 平台的高级加密、安全性和可靠性，用于处理敏感和受监管数据。区块链通过 IBM Secure Service Container 中的一系列功能进行保护：封装的操作系统、加密的设备磁盘、防篡改功能、受保护的内存以及可以配置为与 EAL5+ 认证相匹配的强大 LPAR 隔离。

## 关键安全功能
IBM Secure Service Container 为区块链服务提供了以下优化的安全功能：  

### 限制系统管理员访问
>即便是平台或系统管理员，也无法访问设备代码。数据访问由设备进行控制，因此禁用了未经授权的访问。这是通过组合使用对所有动态和静态数据进行签名和加密的功能来予以支持的。所有对内存的访问权也已除去。固件通过安全引导体系结构支持此功能。

>区块链由 IBM Secure Service Container 进行保护时，系统管理员存在以下限制：
>* 无法访问节点
>* 无法查看区块链网络

### 防篡改  
>IBM Secure Service Container 禁用了所有提供 LPAR 内存访问的外部接口。对映像引导装入程序进行了签名，以确保无法通过其他装入程序对其进行篡改或交换。
### 已加密设备磁盘
>存储在磁盘上的所有代码和数据始终使用 Linux 加密层进行加密：  
- 封装的操作系统
- 受保护 IP
- 嵌入式监视和自我复原功能  
