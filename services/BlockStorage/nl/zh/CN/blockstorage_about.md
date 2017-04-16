{:new_window: target="_blank"}


# 关于 {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

上次更新时间：2016 年 9 月 7 日
{: .last-updated}

IBM {{site.data.keyword.blockstorageshort}} 服务允许您将持久性存储器连接到虚拟服务器。要使用该存储器，需要将块卷连接到虚拟服务器。块存储卷中的数据持续存储的时间长于虚拟服务器的生命周期。这表示可以将卷从一个服务器实例上拆离后连接到另一个服务器实例上，但不会对数据造成任何更改。{{site.data.keyword.blockstorageshort}} 使用 OpenStack Cinder 来管理卷生命周期。 

在您可以分区、格式化和安装的块设备（例如 /dev/vdb）上访问该存储器。除非您删除数据，否则数据会一直存在。 

## 卷 
{: #using-volumes-concept}

{{site.data.keyword.blockstorageshort}} 卷是通过 {{site.data.keyword.blockstorageshort}} 服务实例进行创建的。您可以使用以下方式将卷连接到虚拟服务器：
  

* 指定您提供的特定设备。 
* 指定系统自动选择可用的设备名。 

虚拟服务器会独立于 {{site.data.keyword.blockstorageshort}} 服务而直接与指定的设备执行其 I/O 操作。

## 快照 
{: #using-snapshots-concept}

您还可以创建卷的块级别快照。快照会捕获块存储卷上特定时间点的数据。您可以使用快照执行数据增量备份。不过，这些快照与原始卷存在于同一存储器上。因此，快照不足以构成灾难恢复策略。

**注**：卷连接到服务器实例时不能创建快照。 

从快照创建卷时，所创建新卷的状态与拍摄快照时原始卷的状态相同。 

从快照创建卷有以下影响：

* 不会除去现有卷。
* 新卷中不会包含拍摄相关快照后创建、修改或删除的数据。

后续步骤

创建卷。有关更多信息，请参阅[创建卷](../BlockStorage/blockstorage_creatingvolume.html)。
