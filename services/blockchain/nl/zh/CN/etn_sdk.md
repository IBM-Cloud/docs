---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HFC SDK for Node.js
{: #etn_sdk}


Hyperledger Fabric Client (HFC) SDK 支持应用程序开发者构建与区块链网络进行交互的 Node.js 应用程序。利用 HFC SDK 的 Node.js 应用程序可以用于执行以下网络任务：
{:shortdesc}

* 安全地注册并登记用户。具有 `registrar` 权限的 Web 应用程序管理员可通过动态方式注册并登记已向该 Web 应用程序认证的用户。
* 向区块链网络提交交易（部署、调用和查询）。所有交易都是匿名且机密的，只能通过“auditor”权限进行链接。
* 在任意位置（例如，区块链外的数据库）存储敏感专用密钥和证书。这需要实现简单的键/值存储器接口。

HFC SDK 提供了多个 API，应用程序可通过这些 API 与 Hyperledger Fabric 区块链网络进行交互。这些 API 设计为支持两种可插拔组件：

1. 可插拔键/值存储器，用于检索和存储与成员关联的键。`chain.setKeyValStore()` 方法覆盖基于文件的缺省键/值存储器实现。链键/值存储器用于存放敏感专用密钥，因此对此存储器的访问必须得到相应保护。
2. 可插拔成员服务，用于注册并登记成员。`chain.setMemberServices()` 方法覆盖 `MemberServices` 中的缺省实现。成员服务将 Hyperledger Fabric 实现为经许可的区块链网络，这将提供匿名性、交易不可链接性和机密性。

可以使用脱机方法或 npm 方法，在 Node.js 应用程序中包含 HFC SDK：
*  脱机方法：首先将 Hyperledger Fabric 源树 (https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/lib) 中的文件复制到 Node.js 应用程序 `/lib` 目录。然后，通过添加以下代码片段，在应用程序中包含 HFC SDK：

```js
var hfc = require("./lib/hfc");
```

* npm 方法：在命令行中，首先使用以下片段通过 npm 来安装 HFC SDK：

```
npm install hfc@0.6.5
```

然后，通过以下代码片段，在应用程序中包含 HFC SDK：

```js
var hfc = require('hfc');
```  
<br>
## HFC 对象
{: #objects}

以下 HFC 对象（类和接口）在高级别进行了描述，以帮助指导您逐步了解对象层次结构：

* 顶级类为 `Chain`，这是区块链网络的客户机表示。HFC 允许您根据需要与多个网络进行交互，以及与多个 `Chain` 对象共享单个 `KeyValStore` 和 `MemberServices` 对象。对于每个区块链网络，您将添加一个或多个 `Peer` 对象，这些对象表示 HFC 为了提交交易而连接到的端点。
* `KeyValStore` 接口由 HFC 用于存储和检索所有持久数据。这些数据包含专用密钥，因此必须始终保证安全。缺省实现是基于文件的版本，位于 `FileKeyValStore` 类中。
* `MemberServices` 接口由 `MemberServicesImpl` 类实现，用于提供安全性以及与身份相关的功能，例如隐私性、不可链接性和机密性。此实现会发出 *eCert*（成员登记证书）和 *tCert*（每个成员的交易证书）。
* `Member` 类表示在网络上执行交易的最终用户以及其他类型的成员，例如同级（节点）。使用 `Member` 类（该类与 `MemberServices` 对象进行交互）来*注册*并*登记*成员和用户。您还可以通过与 `Peer` 对象进行交易，直接从“Member”类部署、查询和调用链代码；此实现只是将工作委派给临时的 `TransactionContext` 对象。
* `TransactionContext` 类实现了部署、调用和查询逻辑的大部分内容。每个 `TransactionContext` 实例都会收到来自 `MemberServices` 的唯一 tCert，该实例始终使用此 tCert 来提交交易。要使用同一 tCert 发出多个交易，请直接在 Member 对象中检索 `TransactionContext` 对象，然后发出多个 deploy、invoke 和 query 操作（即“部署”、“调用”和“查询”操作）。但是，将单个 tCert 用于多个交易会将这些交易链接在一起，从而使这些交易由于涉及同一匿名用户而易于识别。为了避免交易链接，请在 `User` 或 `Member` 对象上调用 deploy、invoke 和 query 操作。  

<br>

## 样本 Node.js 应用程序
{: #nodesample}

以下样本 Node.js 应用程序利用 HFC SDK API 以与 Bluemix 区块链网络进行交互。该程序针对两种区块链网络套餐（入门模板和 HSBN）以及任何客户机端操作系统均可正常运行。

目标是使用 JavaScript 应用程序 [helloblockchain.js](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/helloblockchain.js) 将一段链代码 [chaincode_example02](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/src/chaincode/chaincode_example02.go) 成功部署到 Bluemix 网络，随后执行调用和查询。  

1. 此程序需要 Node.js 和 npm JavaScript 包管理器。安装最新版本的 [Node.js](https://nodejs.org/en/) 时将自动包含 npm。  

1. 打开终端，然后创建将放置此演示的源代码的目录（工作空间）。例如：

    ```
    mkdir -p $HOME/workspace
    ```

1. 转至新创建的目录，并克隆 [SDK-Demo](https://github.com/IBM-Blockchain/SDK-Demo) 存储库。执行 `git clone` 命令之前，确保您为操作系统安装的 [Git](https://git-scm.com/downloads) 的版本正确：

     ```
     cd $HOME/workspace
     git clone https://github.com/IBM-Blockchain/SDK-Demo.git
     ```
 如果网络运行的是 Hyperledger Fabric V0.5，请在克隆后检出 V0.5 分支：

     ```
     cd $HOME/workspace/SDK-Demo
     git checkout v0.5
     ```

1. 现在，需要利用区块链实例中的服务凭证。

1. 如果尚未这样做，请访问 Bluemix 中的[区块链](https://console.ng.bluemix.net/catalog/services/blockchain/)磁贴，然后创建该服务的实例。选择**入门模板开发者**套餐或**高安全性业务网络**套餐。一旦组织网络后，即可单击**创建**按钮。这将打开“服务仪表板”。单击页面靠上部分的**服务凭证**选项卡，以访问网络的同级和用户登记数据。**注**：对于 HSBN 网络，可能不会自动生成“服务凭证”。请单击**新建凭证**按钮，这将打开新窗口。然后，单击窗口底部的**添加**。这将填充包含“服务凭证”的 JSON 有效内容。

1. 使用新凭证更新克隆 SDK-Demo 存储库时收到的 ServiceCredentials.json 文件。

1. 程序运行时，HFC SDK 会在 $HOME/workspace/SDK-Demo 内创建 `keyValStore-<network-id>` 目录。此 `keyValStore-<network-id>` 目录包含每个已登记用户的密钥。连接到新的 Bluemix 网络时，无需删除 `keyValStore` 目录，系统将会为每个 Bluemix 实例创建唯一的 `keyValStore-<network-id>` 目录。在删除或重置网络之前，**请勿**删除此加密资料。没有此数据，客户机将无法与 Bluemix CA 服务器进行通信，并且登记将失败。

1. 从 SDK-Demo 文件夹中，运行 node 程序：

	```
	node helloblockchain.js
	```
	启用调试日志：
```
	DEBUG=hfc node helloblockchain.js
	```

	启用 gRPC 跟踪：
	```
	GRPC_TRACE=all DEBUG=hfc node helloblockchain.js
	```

如果 `deploy`、`invoke` 和 `query` 交易成功，您将在终端中看到以下消息：

```
Successfully deployed chaincode: request={"fcn":"init","args":["a","100","b","200"],"certificatePath":"/certs/blockchain-cert.pem","chaincodePath":"github.com/chaincode_example02/"}, response={"uuid":"2d6ad8d6-1390-4c60-a01b-f4c301175eb7","chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","result":"TODO: get actual results; waited 120 seconds and assumed deploy was successful"}

Successfully submitted chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"uuid":"f9a902d2-44d8-4b68-b43d-419470ba73ae"}

Successfully completed chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"result":"waited 20 seconds and assumed invoke was successful"}

Successfully queried  chaincode function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, value=99
```

**注**：链代码源代码保存在 SDK-Demo 存储库中的 **src/chaincode** 文件夹下。此文件夹**还**包含 **/vendor** 文件夹，其中含有 Hyperledger Fabric 代码库中的库和依赖项。如果将当前链代码文件 chaincode_example02.go 替换为自己的链代码，请确保保留 **/vendor** 文件夹。这些依赖项对于同级成功编译链代码并创建容器是必需的。此外，如果您具有任何从属库，请确保将其添加到 **/vendor** 文件夹下。

请注意，在“入门模板开发者”网络上运行时，有时可能需要更长的时间才能成功部署并启动链代码容器。但是，一旦启动后，后续部署和调用将立即执行，因为必备文件已存储在区块链实例的主机上。  

浏览到**网络控制台**中的**区块链**选项卡。此视图显示 helloblockchain.js 程序发出 deploy 和 invoke 交易时，要附加到区块链分类帐的区块。以下屏幕快照显示的是运行 helloblockchain.js 两次（使用“a”和“b”的缺省自变量）的结果：

   ![节点工作空间 3](images/nodeworkspace3.PNG "节点工作空间 3")  

<br>

## 故障诊断
通过从 **/workspace** 目录发出以下任一命令，确保运行的是 **hfc@0.5.4** 或 **hfc@0.6.5**：
  * npm list | grep hfc
  * npm list -g | grep hfc（如果是使用全局 `-g` 标志安装的）

使用 V0.5 分支的网络将需要更早的 hfc 版本 - 0.5.4

如果收到查询消息，请使用以下过程：

  ```
Failed to query chaincode, function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, error={"error":{"status":"FAILURE","msg":{"type":"Buffer","data":[69,114,114,111,114,58,70,97,105,108,101,100,32,116,111,32,108,97,117,110,99,104,32,99,104,97,105,110,99,111,100,101,32,115,112,101,99,40,112,114,101,109,97,116,117,114,101,32,101,120,101,99,117,116,105,111,110,32,45,32,99,104,97,105,110,99,111,100,101,32,40,57,98,101,48,97,48,101,100,51,102,49,55,56,56,101,56,55,50,56,99,56,57,49,49,99,55,52,55,100,50,102,54,100,48,101,50,48,53,102,97,54,51,52,50,50,100,99,53,57,56,100,52,57,56,102,101,55,48,57,98,57,98,56,100,41,32,105,115,32,98,101,105,110,103,32,108,97,117,110,99,104,101,100,41]}},"msg":"Error:Failed to launch chaincode spec(premature execution - chaincode (9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d) is being launched)"}
  ```

在 Node.js 应用程序中增大部署等待时间。缺省值设置为 60 秒，但代码在 Docker 容器中正确部署、编译和开始运行可能需要更长时间。请尝试将部署等待时间增大到 120 秒。仅在“入门模板开发者”套餐上会观察到此特点，因为托管区块链实例的机器上使用的是共享计算资源：

  ```js
chain.setDeployWaitTime(120);
  ```

一旦链代码成功部署在网络上，即可将部署等待时间减小到正常时间长度，例如若干秒。

如果收到握手错误，请尝试其他 `grpc` 版本。可以通过以下任一命令访问您的 grpc 版本：
    - `npm list | grep grpc`
    - `npm list -g | grep grpc`  



<br>
## 公用密钥和专用密钥
{: #keys}

Hyperledger Fabric 使用认证中心及其底层公用密钥和专用密钥来满足共享区块链上运行的业务的安全需求。成员身份管理、角色管理和交易性隐私全部可以通过 HFC SDK 进行控制。

共享区块链上的用户和交易性隐私是通过实现 PKI（公用密钥基础架构）框架进行管理的。PKI 通过认证中心来管理密钥和数字证书的生成、分发和撤销。PKI 和成员资格服务的完整技术规范在 Hyperledger Fabric V0.6 [协议规范](http://hyperledger-fabric.readthedocs.io/en/v0.6/protocol-spec/)的“安全性”部分中进行了描述。下面说明了 Hyperledger Fabric PKI 的基本原则：

1. 注册中心 (RA) 对请求访问区块链网络的用户的身份进行验证。这可以由具有 `registrar` 权限的用户以动态方式执行，也可以通过编辑 membersrvc.yaml 文件来手动执行。注册过程在频带外通过 `RegisterUser` 函数执行。RA 会将登记凭证 `<enrollID>` 和 `<enrollPWD>` 分配给用户。

2. 接着，该用户使用 `CreateCertificatePair` 函数向登记认证中心 (ECA) 发送登记请求。此有效内容包含用户的一次性 `<enrollPWD>`、公用签名验证密钥和公用加密密钥，并且是使用用户的专用签名验证密钥进行签名的。<br><br>收到登记请求时，ECA 会向用户发出加密的质询，此质询只能使用该用户的专用加密密钥进行解密。对质询解密后，用户会重新发送证书请求。ECA 在响应得到准确解密的情况下，返回使用其数字签名进行签名的已认证证书对。<br><br>数字签名是通过使用 SHA-2 算法生成“摘要”，以加密方式对证书请求（消息）进行散列而生成的。随后，将使用 ECA 的专用签名密钥对此“消息摘要”加密。网络成员接着可以通过使用 ECA 的公用签名密钥对数字签名解密来认证该数字签名。返回的登记证书 (eCert) 对包含一个用于数据签名的证书（专用）和一个用于数据加密的证书（公用）。此 eCert 对是静态的长期证书，可以对交易可视或不可视。

3. 要在任何区块链网络上进行交易，每个用户还必须具有交易证书 (tCert)。成功登记后，用户将向交易认证中心 (TCA) 提交请求以获取批量 tCert。tCert 是特定于一个交易的短期证书，可以由客户机使用 API 进行修改。验证用户的 eCert 后，TCA 会分配批量 tCert 和 KeyDF_Key（密钥派生函数密钥），以允许用户对其专用密钥解密。单个 KeyDF_Key 用于批次中的每个 tCert 时，生成的后续专用密钥对于每个 tCert 是唯一的。要进行交易，客户机必须能够使用解密的专用密钥对交易有效内容进行签名。只有这时，交易才会转发到网络验证同级以便达成共识。
