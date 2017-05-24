---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 将 IBM UrbanCode Deploy 服务器连接到 Delivery Insights
{: #connect_ucd}

要在 Delivery Insights 中查看 IBM UrbanCode Deploy 服务器中的数据，必须在该服务器上安装补丁，然后将该服务器连接到 DevOps Connect。
{:shortdesc}

## 开始之前

- 请参阅[先决条件](uc_insights_prereqs.html)，包括设置 DevOps Connect 的实例。
- IBM UrbanCode Deploy 服务器必须为 V6.2 或更高版本。

## 过程

1. 将补丁安装到 IBM UrbanCode Deploy 服务器中。所有版本的 IBM UrbanCode Deploy 都需要补丁才能与 DevOps Connect 进行通信。 
  1. 转至以下页面并下载与您的 IBMUrbanCode Deploy 版本相应的正确补丁：
   [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. 解压缩该文件。它包含必须添加到服务器的一个或多个补丁文件。

  1. 停止服务器。请参阅[启动和停止服务器](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html)。

  1. 将补丁文件放入 <code><em>application_data</em>/patches</code> 文件夹中，其中 <code><em>application_data</em></code> 是服务器应用程序数据文件夹。缺省应用程序数据文件夹在 Linux 上为 `/opt/ibm-ucd/server/appdata`，在 Windows 上为 `C:\Program Files\ibm-ucd\server\appdata`。在高可用性系统上，应用程序数据文件夹始终位于每个服务器都可访问的共享网络驱动器上。

  1. 可选：服务器停止期间，要提高从此服务器导入数据的性能，请在数据库上运行以下 SQL 命令：  
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time); 
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
  将您的数据库的名称用于 `MyUCDDatabase`。
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. 启动服务器。 

    **注：**您需要等待的时间可能要比通常等待 IBM UrbanCode Deploy 服务器启动的时间更长。如果服务器最终未启动或未正常运行，请删除补丁文件，然后重新启动服务器。补丁文件不会永久影响服务器。

1. 某些版本的 IBM UrbanCode Deploy 需要额外的补丁才能使服务器连接到 DevOps Connect。如果使用的是 IBM UrbanCode Deploy V6.2 到 V6.2.1.2，那么必须在服务器上安装以下额外补丁：
  1. 下载补丁：[http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar)。
  1. 停止服务器。
  1. 将补丁文件放入 <code><em>application_data</em>/patches</code> 文件夹中。
  1. 启动服务器。

1. 创建 DevOps Connect 与 IBM UrbanCode Deploy 服务器的集成：  
  **重要信息：**集成首次运行时，DevOps Connect 会检索前 90 天的数据。如果有大量部署数据，那么此过程可能需要很长时间。要检索少于 90 天的数据，请参阅[故障诊断](uc_insights_connect_ucd.html#troubleshooting)。
  1. 在 IBM UrbanCode Deploy 中，创建认证令牌。请参阅[令牌](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html)。
  1. 在 DevOps Connect 中，单击**集成**，然后单击**添加新项**。
  1. 指定集成的名称和描述。DevOps Connect 的缺省位置为 `https://hostname:8443/`，其中 `hostname` 是托管 DevOps Connect 的系统的主机名。
  1. 从**集成类型**列表中，选择 **IBM UrbanCode Deploy for Cloud Reporting**。
  1. 在**服务器 URI** 字段中，输入 IBM UrbanCode Deploy 服务器的公共 URL，例如 `https://my_UCD.example.com:8447`。
  1. 在**认证令牌**字段中，输入或粘贴 IBM UrbanCode Deploy 生成的认证令牌。
  1. 在**管理用户**字段中，输入要向其授予 DevOps Connect 界面访问权的 IBM 标识的逗号分隔列表。
  1. 可选：单击**运行集成**以立即运行集成。缺省情况下，集成会每分钟运行一次。
  1. 单击**保存**。

  ![在 DevOps Connect 中设置集成](images/uc_insights_dc_integration.gif)

现在，您的数据已经与 Delivery Insights 同步。可以立即创建并查看基于这些数据的报告。

## 故障诊断
{: #troubleshooting}

如果在 IBM UrbanCode Deploy 服务器数据库中存储了许多应用程序和组件流程请求，那么在检索过程中可能会发生错误。在服务器输出日志中会记录类似以下文本的消息：

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

要解决此行为，请编辑插件的 `plugin.properties` 文件，以减少要检索的数据天数。`plugin.properties` 文件位于安装了 DevOps Connect 的计算机上的 `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` 目录中。编辑以下行以除去井号 (#) 并减少天数：

`#numDaysToRetrieve=90`

例如，将该行更改为以下文本，以只检索前 30 天的数据：

`numDaysToRetrieve=30`

保存文件，然后重新运行集成。检查服务器日志以确保该错误不再发生。
