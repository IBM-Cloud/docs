---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilefoundation_short}} 入门
{: #gettingstartedtemplate}

*上次更新时间：2016 年 6 月 15 日*
{: .last-updated}

{{site.data.keyword.mobilefoundation_long}} 加快设置 {{site.data.keyword.mfp_full}} 环境，您可在此环境中开发、测试和操作企业移动应用程序。{{site.data.keyword.mobilefoundation_short}} 提供了两种不同服务套餐：Developer 和 Professional 1 Application。
{:shortdesc}

Professional 1 Application 套餐允许在可扩展容器组上部署 {{site.data.keyword.mobilefoundation_short}} 服务器。使用 Professional 1 Application 套餐，可管理所有受支持操作系统（例如，Android、iOS、Windows 或移动 Web）中构建的单个应用程序。Developer 套餐不支持在具有多个节点的容器组上部署 {{site.data.keyword.mobilefoundation_short}}。此套餐最适合进行开发和测试。

## {{site.data.keyword.mobilefoundation_short}}: Developer 套餐入门

创建 {{site.data.keyword.mobilefoundation_short}}: Developer 的实例后，只需通过几次单击，就能开始构建移动通道。

*	要使用缺省配置创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**启动基本服务器**。

  `基本服务器实例包括单一节点、1 GB 内存和 64 GB 存储容量。`

* 要使用拓扑、安全性和其他服务器配置的高级配置来创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**使用高级配置启动服务器**。请参阅[设置高级配置](c_using_mfs_p1.html#using_mfs_advanced_p1)，以获取更多信息。

## {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 套餐入门

创建 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服务的实例后，可以通过完成以下步骤开始构建移动通道。

1.  连接到 {{site.data.keyword.Bluemix_notm}} 上的现有 {{site.data.keyword.dashdbshort}}: Enterprise Transactional 服务。

    1.  从当前`组织`中可用的空间列表选择具有 {{site.data.keyword.dashdbshort_notm}} 服务实例的 {{site.data.keyword.Bluemix_notm}} `空间`。

    2.  选择 {{site.data.keyword.dashdbshort_notm}} `服务名称`和`凭证`以连接到现有 {{site.data.keyword.dashdbshort_notm}} 服务实例。

    3.  通过单击**测试连接**测试与所选 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 服务实例的连接。

    4.  单击**添加**，然后会出现弹出窗口，询问您是否确认所选的 {{site.data.keyword.dashdbshort_notm}} 服务，请单击**继续**。此操作可在配置的 {{site.data.keyword.dashdbshort_notm}} 数据库服务实例中创建需要的表。

2.  创建并启动服务器。

    * 要使用缺省配置创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**启动基本服务器**。

      `基本服务器实例包括单一节点、1 GB 内存和 64 GB 存储容量。`

    * 要使用拓扑、安全性和其他服务器配置的高级配置来创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**使用高级配置启动服务器**。请参阅[设置高级配置](c_using_mfs_p2.html#using_mfs_advanced_p2)，以获取更多信息。

转至 [Using the Mobile Foundation service to set up MobileFirst Server on IBM Containers](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/)，以了解有关如何开始使用 {{site.data.keyword.mobilefoundation_short}} 的更多信息。

# 相关链接
{: #rellinks}

## 相关链接
{: #general}

*	[IBM MobileFirst Platform Foundation V8.0.0 产品文档](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform 开发者中心](https://mobilefirstplatform.ibmcloud.com){: new_window}
