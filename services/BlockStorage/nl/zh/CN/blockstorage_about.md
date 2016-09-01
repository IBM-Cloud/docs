{:new_window: target="_blank"}


# 关于 {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

上次更新时间：2016 年 8 月 1 日
{: .last-updated}

## 卷 
{: #using-volumes-concept}

您可以使用 IBM {{site.data.keyword.blockstorageshort}} 来创建卷以及将卷连接到虚拟服务器。缺省情况下，IBM {{site.data.keyword.virtualmachinesshort}} 并没有持久存储，而且会在重新启动时还原为缺省映像。{{site.data.keyword.blockstorageshort}} 为您的虚拟服务器提供了持久存储。块存储卷中的数据持续存储的时间长于虚拟服务器的生命周期。{{site.data.keyword.blockstorageshort}} 使用 OpenStack Cinder 来管理卷生命周期。

{{site.data.keyword.blockstorageshort}} 卷是通过 {{site.data.keyword.blockstorageshort}} 服务实例进行创建的。您可以使用以下方式将卷连接到虚拟服务器：
  

* 指定您提供的特定设备。 
* 指定系统自动选择可用的设备名。 

虚拟服务器会独立于 {{site.data.keyword.blockstorageshort}} 服务而直接与指定的设备执行其 I/O 操作。

## 快照 
{: #using-snapshots-concept}

您还可以创建卷的块级别快照。不过，不能在卷处于连接状态时创建快照，这样生成的快照将处于崩溃一致状态。 

后续步骤

创建卷。有关更多信息，请参阅[创建卷](../BlockStorage/blockstorage_creatingvolume.html)。
