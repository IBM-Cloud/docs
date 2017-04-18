---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

#	使用 Developer 套餐
{: #using_mobilefoundation_p1}

创建 {{site.data.keyword.mobilefoundation_short}}: Developer 服务实例的几秒钟后，您就可以访问 {{site.data.keyword.Bluemix_notm}} 上的“`概述`”页面，其中为您提供了教程和视频，可帮助您开始使用 {{site.data.keyword.mobilefoundation_short}} 服务。

## 启动 MobileFirst 服务器
{: #start_mobilefoundation_p1}
* 要使用缺省设置启动 {{site.data.keyword.mfserver_short_notm}}，请单击**启动基本服务器**。

此选择将为 {{site.data.keyword.mfserver_long_notm}} 供应以下设置：
*	1 GB 内存。此大小足够用于开发、轻量测试活动和小规模生产工作负载。

*	自动为您生成 `username` 和 `password`。服务器启动并运行时，您可以对其进行访问。

供应过程启动。此过程会花费大约 10 分钟，并且消息窗口会指示此操作的进度。完成后，会显示仪表板，在其中您可以看到：
*	正在运行的服务器的状态（状态和大小）。

*	为您创建的服务器路径。在您的移动应用程序中使用此路径可连接到 {{site.data.keyword.mfserver_short_notm}}。

*	用于访问 {{site.data.keyword.mfp_oc_short_notm}} 的个人 `username` 和 `password`。`password` 会隐藏。单击**显示密码**图标以使其可见。

*	单击**启动控制台**以启动 {{site.data.keyword.mfp_oc_short_notm}}。


<!--This console runs inside the container.--> 通过控制台，您可以管理移动应用程序和移动设备、使用服务器作为移动后端以及发送推送通知等。



##  添加移动分析服务器
{: #adding_analytics_server_dev}

 现在，您可以将移动分析服务器添加到 {{site.data.keyword.mobilefoundation_short}} 服务实例来监视 {{site.data.keyword.mobilefirst}} 服务器上的移动应用程序。Developer 套餐会在包含具有 1 GB 内存的单一节点的容器组中创建移动分析服务器。

* 单击**添加分析**，将移动分析服务器添加到 {{site.data.keyword.mobilefoundation_short}} 服务实例。

供应过程启动。此过程会花费大约 10 分钟，并且消息窗口会指示此操作的进度。  

* 从 {{site.data.keyword.mfp_oc_short_notm}} 启动 MobileFirst Analytics Console。

* 在 {{site.data.keyword.mfserver_short_notm}} 与移动分析服务器之间启用单点登录。为移动分析服务器配置与 {{site.data.keyword.mfserver_short_notm}} 相同的 LTPA 密钥和用户凭证。您可以像登录 {{site.data.keyword.mfp_oc_short_notm}} 一样，使用相同的 `username` 和 `password` 登录到“移动分析”控制台。

有关 MobileFirst Analytics 的更多信息，请参阅 [MobileFirst Foundation Operational Analytics ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: new_window}。

**注：**删除 {{site.data.keyword.mobilefoundation_short}} 服务实例或尝试重新创建 {{site.data.keyword.mfserver_short_notm}} 时，会除去移动分析服务器。

##  删除移动分析服务器
{: #deleting_analytics_server_dev}

您现在可以从 {{site.data.keyword.mobilefoundation_short}} 服务仪表板删除已添加到 {{site.data.keyword.mobilefoundation_short}} 服务实例的移动分析服务器。

* 单击**删除分析**，可删除已添加到 {{site.data.keyword.mobilefoundation_short}} 服务实例的移动分析服务器。

 这会删除分析容器组。删除分析容器的过程需要 10 分钟左右。可以刷新屏幕以查看更新的状态。删除分析容器后，会重新启用**添加分析**按钮，您可以选择使用此按钮再次添加移动分析服务器。


## 重新创建 MobileFirst 服务器
{: #recreate_mobilefoundation_p1}

*	单击**重新创建**以重新创建服务器。

* 此操作将停止现有服务器并删除数据。移动服务器中的所有数据都将丢失。将会使用更新的版本（如果可用）来创建新的服务器实例。此操作会花费几分钟才能完成。

##	设置高级配置
{: #using_mfs_advanced_p1}

使用“`概述`”页面中的**使用高级配置启动服务器**，可使用高级或定制设置创建服务器。还可以通过单击**配置**选项卡更新服务器设置，以定制服务器配置。{{site.data.keyword.mobilefoundation_short}} 为您提供对某些高级设置的访问权。

*	在**拓扑**选项卡中，可以选择服务器大小以及所需的实例数。缺省 1 GB 服务器足够开发和中等测试使用。

  - 根据您的需要，选择正确的服务器大小。

* **节点**显示已创建的节点数。此字段在 {{site.data.keyword.mobilefoundation_short}}: Developer 中不可编辑。在 Developer 套餐中，节点数<!--in your {{site.data.keyword.IBM_notm}} container group-->缺省为 **1**。

请参阅 [{{site.data.keyword.mobilefoundation_long}} 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}，以了解更多详细信息。
