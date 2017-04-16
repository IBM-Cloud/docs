---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Mobile Foundation 入门
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}} 加快设置 {{site.data.keyword.mfp_full}} 环境，您可在此环境中开发、测试和操作企业移动应用程序。{{site.data.keyword.mobilefoundation_short}} 提供了两种不同服务套餐：Developer 和 Professional 1 Application。
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> 使用 Professional 1 Application 套餐，可管理任何或所有受支持操作系统（例如 Android、iOS、Windows 或移动 Web）上构建的单个应用程序。
Developer 套餐<!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan -->最适合进行开发和测试。

## Mobile Foundation: Developer 套餐入门
{: #gettingstartedtemplate_dev}

创建 {{site.data.keyword.mobilefoundation_short}}: Developer 的实例后，只需通过几次单击，就能开始构建移动通道。

*	要使用缺省配置创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**启动基本服务器**。

  `基本服务器实例包含单一节点和 1 GB 内存。`

* 要使用拓扑、安全性和其他服务器配置的高级配置来创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**使用高级配置启动服务器**。请参阅[设置高级配置](c_using_mfs_p1.html#using_mfs_advanced_p1)，以获取更多信息。

## Mobile Foundation: Professional 1 Application 套餐入门
{: #gettingstartedtemplate_prof}

创建 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服务的实例后，可以通过完成以下步骤开始构建移动通道。

1.  连接到 {{site.data.keyword.Bluemix_notm}} 上的现有 {{site.data.keyword.dashdbshort}} for Transactions 服务。

    1.  选择 {{site.data.keyword.dashdbshort_notm}} 服务实例所在的 {{site.data.keyword.Bluemix_notm}} `组织`。

    + 从所选`组织`中可用的空间列表中选择具有 {{site.data.keyword.dashdbshort_notm}} 服务实例的 {{site.data.keyword.Bluemix_notm}} `空间`。

    + 选择 {{site.data.keyword.dashdbshort_notm}} `服务名称`和`凭证`以连接到现有 {{site.data.keyword.dashdbshort_notm}} 服务实例。

    + 通过单击**测试连接**测试与所选 {{site.data.keyword.dashdbshort_notm}} for Transactions 服务实例的连接。

    + 单击**添加**，然后会出现弹出窗口，询问您是否确认所选的 {{site.data.keyword.dashdbshort_notm}} for Transactions 服务，请单击**继续**。此操作可在配置的 {{site.data.keyword.dashdbshort_notm}} 数据库服务实例中创建需要的表。

    **注：**添加 {{site.data.keyword.mobilefoundation_short}} 实例的 {{site.data.keyword.dashdbshort_notm}} 连接后，您将无法对其进行更改。

2.  创建并启动服务器。

    * 要使用缺省配置创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**启动基本服务器**。

      `基本服务器实例包含单一节点和 1 GB 内存。`

    * 要使用拓扑、安全性和其他服务器配置的高级配置来创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**使用高级配置启动服务器**。请参阅[设置高级配置](c_using_mfs_p2.html#using_mfs_advanced_p2)，以获取更多信息。

## Mobile Foundation: Developer Pro 套餐入门
{: #gettingstartedtemplate_devpro}

创建 {{site.data.keyword.mobilefoundation_short}}: Developer Pro 服务的实例后，可以通过完成以下步骤开始构建移动通道。

  1.  连接到 {{site.data.keyword.Bluemix_notm}} 上的现有 {{site.data.keyword.dashdbshort}} for Transactions 服务。

      1.  选择 {{site.data.keyword.dashdbshort_notm}} 服务实例所在的 {{site.data.keyword.Bluemix_notm}} `组织`。

      + 从所选`组织`中可用的空间列表中选择具有 {{site.data.keyword.dashdbshort_notm}} 服务实例的 {{site.data.keyword.Bluemix_notm}} `空间`。

      + 选择 {{site.data.keyword.dashdbshort_notm}} `服务名称`和`凭证`以连接到现有 {{site.data.keyword.dashdbshort_notm}} 服务实例。

      + 通过单击**测试连接**测试与所选 {{site.data.keyword.dashdbshort_notm}} for Transactions 服务实例的连接。

      + 单击**添加**，然后会出现弹出窗口，询问您是否确认所选的 {{site.data.keyword.dashdbshort_notm}} for Transactions 服务，请单击**继续**。此操作可在配置的 {{site.data.keyword.dashdbshort_notm}} 数据库服务实例中创建需要的表。

      **注：**添加 {{site.data.keyword.mobilefoundation_short}} 实例的 {{site.data.keyword.dashdbshort_notm}} 连接后，您将无法对其进行更改。

  2.  创建并启动服务器。

      * 要使用缺省配置创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**启动基本服务器**。

      * 此选择将为 {{site.data.keyword.mfserver_long_notm}} 供应以下设置：

          - 单个节点具有 1GB 内存。此大小足够用于开发、中等测试活动和小规模生产工作负载。

          -	自动为您生成 `username` 和 `password`。服务器启动并运行时，您可以对其进行访问。

      * 要使用拓扑、安全性和其他服务器配置的高级配置来创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**使用高级配置启动服务器**。请参阅[设置高级配置](c_using_mfs_p3.html#using_mfs_advanced_p3)，以获取更多信息。

## Mobile Foundation: Professional Per Capacity 套餐入门
{: #gettingstartedtemplate_profper}

创建 {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 服务的实例后，可以通过完成以下步骤开始构建移动通道。

  1.  连接到 {{site.data.keyword.Bluemix_notm}} 上的现有 {{site.data.keyword.dashdbshort}} for Transactions 服务。

      1.  选择 {{site.data.keyword.dashdbshort_notm}} 服务实例所在的 {{site.data.keyword.Bluemix_notm}} `组织`。

      + 从所选`组织`中可用的空间列表中选择具有 {{site.data.keyword.dashdbshort_notm}} 服务实例的 {{site.data.keyword.Bluemix_notm}} `空间`。

      + 选择 {{site.data.keyword.dashdbshort_notm}} `服务名称`和`凭证`以连接到现有 {{site.data.keyword.dashdbshort_notm}} 服务实例。

      + 通过单击**测试连接**测试与所选 {{site.data.keyword.dashdbshort_notm}} for Transactions 服务实例的连接。

      + 单击**添加**，然后会出现弹出窗口，询问您是否确认所选的 {{site.data.keyword.dashdbshort_notm}} for Transactions 服务，请单击**继续**。此操作可在配置的 {{site.data.keyword.dashdbshort_notm}} 数据库服务实例中创建需要的表。

      **注：**添加 {{site.data.keyword.mobilefoundation_short}} 实例的 {{site.data.keyword.dashdbshort_notm}} 连接后，您将无法对其进行更改。

  2.  创建并启动服务器。

      * 要使用缺省配置创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**启动基本服务器**。

      * 此选择将为 {{site.data.keyword.mfserver_long_notm}} 供应以下设置：
          -  2 个节点，每个 1GB 内存。此大小适合用于开发、中等测试活动和小规模生产工作负载。

          -	自动为您生成 `username` 和 `password`。服务器启动并运行时，您可以对其进行访问。

      * 要使用拓扑、安全性和其他服务器配置的高级配置来创建 {{site.data.keyword.mobilefirst_notm}} 服务器实例，请单击**使用高级配置启动服务器**。请参阅[设置高级配置](c_using_mfs_p4.html#using_mfs_advanced_p4)，以获取更多信息。

转至[使用 Mobile Foundation 服务设置 MobileFirst 服务器<!-- on IBM Containers--> ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/){: new_window}，以了解有关如何开始使用 {{site.data.keyword.mobilefoundation_short}} 的更多信息。

##  已知限制
{: #knownlimitations_mfp}

* {{site.data.keyword.mobilefoundation_short}} 服务 UI 不会使用用户所选语言环境特定的模式来显示数字。


# 相关链接
{: #rellinks  notoc}

## 相关链接
{: #general notoc}

*	[IBM MobileFirst Platform Foundation V8.0.0 产品文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobilefirstplatform.ibmcloud.com){: new_window}
