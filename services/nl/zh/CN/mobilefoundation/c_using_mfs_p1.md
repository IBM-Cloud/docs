---

copyright:
  years: 2016

---

#	使用 {{site.data.keyword.mobilefoundation_short}}: Developer
{: #using_mobilefoundation_p1}

创建 {{site.data.keyword.mobilefoundation_short}}: Developer 服务实例后，执行以下步骤开始使用该服务：

* 同意 {{site.data.keyword.mfp_full_notm}} V8.0.0.0 的许可条款。

* 输入您的 {{site.data.keyword.Bluemix_notm}} 凭证。这样可授权该服务在 {{site.data.keyword.Bluemix_notm}} 空间中执行更改操作，并创建托管 {{site.data.keyword.mobilefirst_notm}} 服务器的 {{site.data.keyword.containerlong}}。

几秒钟后，可以访问 {{site.data.keyword.Bluemix_notm}} 上的“*概述*”页面，其中为您提供教程和视频，可帮助您开始使用 {{site.data.keyword.mobilefoundation_short}} 服务。

## 启动 {{site.data.keyword.mobilefirst}} 服务器
{: #start_mobilefoundation_p1}
* 要使用缺省设置启动 {{site.data.keyword.mfserver_short_notm}}，请单击**启动基本服务器**。

![启动基本服务器](images/start_basic_server.png "图 1. 启动基本服务器")
{: screen}

此选择将为 {{site.data.keyword.mfserver_long_notm}} 供应以下设置：
*	1 GB 内存，64 GB 存储空间。此大小足够开发和轻量测试活动使用。

*	自动为您生成 *username* 和 *password*。服务器启动并运行时，您可以对其进行访问。

供应过程启动。此过程会花费大约 10 分钟，并且消息窗口会指示此操作的进度。完成后，会显示仪表板，在其中您可以看到：
*	正在运行的服务器的状态（状态、大小、存储空间）。

*	为您创建的服务器路径。使用此路径可从公共因特网访问移动服务器。移动应用程序使用该路径访问服务器。

*	用于访问 {{site.data.keyword.mfp_oc_short_notm}} 的个人 *username* 和 *password*。*password* 会隐藏。单击小眼睛图标可显示密码。

*	单击**启动控制台**以启动 {{site.data.keyword.mfp_oc_short_notm}}。

![启动控制台](images/launch_console.png "图 2. 启动控制台")
{: screen}

此控制台在容器内部运行。通过控制台，您可以管理移动应用程序和移动设备、使用服务器作为移动后端以及发送推送通知等。

## 重新创建 {{site.data.keyword.mobilefirst}} 服务器
{: #recreate_mobilefoundation_p1}

*	单击**重新创建**以重新创建服务器。

![重新创建](images/recreate.png "图 3. 重新创建")
{: screen}

* 此操作将停止现有服务器并将其删除。移动服务器中的所有数据都将丢失。将创建新的服务器实例。此操作会花费几分钟才能完成。

##	设置高级配置
{: #using_mfs_advanced_p1}

使用“*概述*”页面中的**使用高级配置启动服务器**，可使用高级或定制设置创建服务器。还可以通过单击**配置**选项卡更新服务器设置，以定制服务器配置。{{site.data.keyword.mobilefoundation_short}} 为您提供对某些高级设置的访问权。

*	在**拓扑**选项卡中，可以选择容器的拓扑大小。缺省 1 GB 服务器足够开发和中等测试使用，但是您可能需要更多容量，例如用于执行装入测试。
  - 根据您的需要，选择正确的服务器大小。  


* **节点**显示已创建的节点数。此字段在 {{site.data.keyword.mobilefoundation_short}}: Developer 中不可编辑。您可以查看 {{site.data.keyword.IBM_notm}} 容器组中获取的节点数。容器组提供高可用性和可扩展性。

请参阅 [{{site.data.keyword.mobilefoundation_long}} 文档](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}以获取更多详细信息。
