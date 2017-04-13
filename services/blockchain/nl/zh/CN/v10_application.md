---

copyright:
  years: 2017
lastupdated: "2017-03-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 应用程序开发
{: #v10_dashboard}


使用 marbles02 示例链代码和相应的 JavaScript 应用程序作为模板来创建自己的业务解决方案。
{:shortdesc}


该应用程序利用 Node.js SDK API 与供应的网络组件进行交互，并最终通过事务处理请求将同级设定为目标。在“监视器”的**资源**屏幕的**服务凭证**选项卡中，为您的同级、认证中心和网络订购服务找到 API 端点，并将这些字符串插入到应用程序随附的配置文件中。但是请注意，如果您想要以网络中的其他同级作为目标（当您需要不属于组织的同级的保证时会发生这种情况），那么您需要为那些同级获取正确的 API 端点。您还需要为其他组织存储 CA 证书，以便验证返回到应用程序的响应。此信息不会在**资源**视图中公开，因此您必须联系 Bluemix 组织的适当管理员，并在带外操作中获取此数据。订购服务 URL 在整个网络中很常用；对于此组件，您不需要任何成员特定信息。  

请访问 [Marbles](https://github.com/IBM-Blockchain/marbles/tree/v3.0) GitHub 存储库，以获取源代码和必备软件；请遵循自述文件并激活您的应用程序。  

浏览 [SDK 存储库](https://github.com/hyperledger/fabric-sdk-node)，以试验端到端测试并更深入地了解 API。
