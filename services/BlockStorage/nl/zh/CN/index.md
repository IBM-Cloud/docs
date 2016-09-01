{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}} (Beta) 入门

上次更新时间：2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.blockstoragefull}} 针对需要持久存储的事务密集型工作负载和运行时提供了对块级别存储的访问。您可以使用 {{site.data.keyword.blockstorageshort}} 服务来管理卷生命周期、将卷连接到 IBM Virtual Servers 以及为块存储卷创建快照。

开始之前，请查看以下信息。

* {{site.data.keyword.blockstorageshort}} 仅在未绑定的上下文中受支持。 
* 您必须已创建 IBM {{site.data.keyword.virtualmachinesshort}}，才能连接块存储卷。要了解有关将块存储卷与 IBM {{site.data.keyword.virtualmachinesshort}} 配合使用的更多信息，请参阅[块存储卷和 IBM Virtual Servers](../../virtualmachines/vm_create.html#storage_BS)。 

要开始使用 {{site.data.keyword.blockstorageshort}}，请完成以下步骤：

1. 创建卷。
   
   a. 打开 {{site.data.keyword.blockstorageshort}} 服务。

   b. 单击**创建**，以启动**创建卷**对话框。

   c.	提供所需的卷大小。不接受小数。大小受分配给组织的配额限制。
   
   d.	提供名称。名称仅用于显示。
   
   e.（可选）提供更详细的卷描述。
   
   f.	单击**创建**，以提交信息并关闭对话框。

  创建卷可能需要几分钟时间。

2. 将卷连接到虚拟服务器。

   a. 打开 {{site.data.keyword.blockstorageshort}} 服务。
   
   b. 从可用卷列表中选择卷。
   
   c.	单击**连接**。
   
   d.	在“连接”对话框中，从下拉列表中选择虚拟服务器实例。 
   
   e.（可选）指定要用于连接此卷的设备。如果未指定设备，系统会自动选择虚拟服务器上第一个可用的设备。
   
   f.	单击**连接**，以提交信息并关闭对话框。
   
   卷会列在已连接卷的表中，其中还会列出有关虚拟服务器实例的信息。现在，虚拟服务器可以使用该设备来持久存储数据。 
 
后续步骤

准备卷，以便开始使用。有关更多信息，请参阅[准备卷](../BlockStorage/blockstorage_preparingvolume.html)。

# 相关链接
{: #rellinks}

## 教程和样本
{:id="samples"}

* [How to Use IBM Block Storage for Bluemix with IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [Getting Started with IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [IBM Block Storage for Bluemix Demo](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## API 参考
{: #api}
* [OpenStack Block Storage (Cinder) API V2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

