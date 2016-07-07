---

copyright:
  years: 2016

---

#	使用 Professional 1 Application 套餐
{: #using_mobilefoundation_p2}

*上次更新时间：2016 年 6 月 15 日*
{: .last-updated}

创建 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服务实例后，请阅读以下步骤以开始使用该服务。

## 先决条件
{: #prerequisites_p2}

配置 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服务实例之前，请考虑以下内容。
* 仅 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional（支持 OLTP）{{site.data.keyword.Bluemix_notm}} 套餐支持 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application。

* 必须提供 {{site.data.keyword.dashdbshort_notm}} 服务实例及其凭证，才能配置 {{site.data.keyword.mobilefoundation_short}} 服务实例的设置。

**注**：{{site.data.keyword.dashdbshort_notm}} 服务实例可以存在于 {{site.data.keyword.Bluemix_notm}} `组织`的任何`空间`中。如果选择将 {{site.data.keyword.mobilefoundation_short}} 服务部署到不具有 {{site.data.keyword.dashdbshort_notm}} 服务的 {{site.data.keyword.Bluemix_notm}} `空间`，那么必须确保具有访问 {{site.data.keyword.dashdbshort_notm}} 服务的许可权。


## 添加数据库连接
{: #configure_dashdb_p2}

###  首要步骤
{: #firststeps_p2}

创建 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服务实例后，请同意 {{site.data.keyword.mfp_full_notm}} V8.0 的许可条款以开始使用此服务实例。

### 设置与 {{site.data.keyword.dashdbshort_notm}} 服务实例的连接
{: #connect_dashdb_p2}

创建 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服务实例后，将看到“*概述*”页面，在其中需要指定 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 服务实例的连接信息。

1.  从当前`组织`中可用的空间列表选择具有 {{site.data.keyword.dashdbshort_notm}} 服务实例的 {{site.data.keyword.Bluemix_notm}} `空间`。

+ 选择 {{site.data.keyword.dashdbshort_notm}} `服务名称`和`凭证`以连接到现有 {{site.data.keyword.dashdbshort_notm}} 服务实例。

+  测试与指定 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 服务实例的连接。

+  单击**继续**。此操作可在配置的 {{site.data.keyword.dashdbshort_notm}} 数据库服务实例中创建需要的表。

**注**：您无法更改配置为由 {{site.data.keyword.mobilefoundation_short}} 服务实例使用的 {{site.data.keyword.dashdbshort_notm}} 服务实例。但是，您可以在多个 {{site.data.keyword.mobilefoundation_short}} 服务实例上使用同一 {{site.data.keyword.dashdbshort_notm}} 服务实例，因为每个 {{site.data.keyword.mobilefoundation_short}} 服务实例都将在所选 {{site.data.keyword.dashdbshort_notm}} 服务实例中创建自己的模式。

* 几秒钟后，可以访问“`概述`”页面，其中为您提供教程和视频，可帮助您开始使用 {{site.data.keyword.mobilefoundation_short}} 服务。

## 启动 {{site.data.keyword.mobilefirst}} 服务器
{: #start_mobilefoundation_p2}

* 要使用缺省设置启动 {{site.data.keyword.mfserver_short_notm}}，请单击**启动基本服务器**。

* 此选择将为 {{site.data.keyword.mfserver_long_notm}} 供应以下设置：
    -  1 GB 内存，64 GB 存储空间。此大小足够开发和中等测试活动使用。

    -	自动为您生成 `username` 和 `password`。服务器启动并运行时，您可以对其进行访问。

供应服务器的过程启动。此过程会花费大约 10 分钟，并且消息窗口会指示此操作的进度。完成后，会显示仪表板，在其中您可以看到：

  -	正在运行的服务器的状态（状态、大小、存储空间）。

  -	为您创建的服务器路径。使用此路径可从公共因特网访问移动服务器。移动应用程序使用该路径访问服务器。

  -	用于访问 {{site.data.keyword.mfp_oc_short_notm}} 的个人 `username` 和 `password`。`password` 会隐藏。单击**显示密码**以使其可见。

*	单击**启动控制台**以打开 {{site.data.keyword.mfp_oc_short_notm}}。


此控制台在容器内部运行。通过控制台，您可以管理移动应用程序和移动设备、使用服务器作为移动后端以及发送推送通知等。

## 重新创建 {{site.data.keyword.mobilefirst}} 服务器
{: #recreate_mobilefoundation_p2}

*	单击**重新创建**以重新创建服务器。

* 此操作将停止现有服务器并将其删除。将创建新的服务器实例。此操作会花费几分钟才能完成。

**注**：先前服务器实例中的所有数据（包括有关应用程序和适配器的信息）会持久存储在配置的 {{site.data.keyword.dashdbshort_notm}} 服务实例中，在重新创建服务器后可使用这些数据。

##	设置高级配置
{: #using_mfs_advanced_p2}

使用“`概述`”页面中的**使用高级配置启动服务器**，可使用高级或定制设置创建服务器。还可以通过单击**配置**选项卡更新服务器设置，以定制服务器配置。{{site.data.keyword.mobilefoundation_short}} 为您提供对某些高级设置的访问权。

*	在**拓扑**选项卡中，可以选择容器的大小。缺省 1 GB 服务器足够开发和轻量测试使用。
  - 根据您的需要，选择正确的服务器大小。

  - **节点**显示已创建的节点数。
      - 您可以配置 {{site.data.keyword.IBM_notm}} 容器组中需要的最小节点数和最大节点数。容器组提供高可用性和可扩展性。

      - 配置此处列出的节点数可创建 {{site.data.keyword.mobilefirst}} 服务器机群。

请参阅 [{{site.data.keyword.mobilefoundation_long}} 文档](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}，以获取更多详细信息。
