{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}} (Beta) 入门

*上次更新时间：2016 年 7 月 15 日*
{: .last-updated}

{{site.data.keyword.blockstoragefull}} 针对需要持久存储器的事务密集型工作负载和运行时，提供了对块级别存储器的访问。

您可以使用 IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} 来创建可连接到虚拟服务器的 {{site.data.keyword.blockstorageshort}} 卷。块存储卷中的数据持续存储的时间长于虚拟服务器的生命周期。IBM {{site.data.keyword.blockstorageshort}} 使用 OpenStack Cinder 来管理卷生命周期。

{{site.data.keyword.blockstorageshort}} 卷通过 IBM {{site.data.keyword.blockstorageshort}} 服务实例进行创建。您可以将卷连接到虚拟服务器中您所提供的特定设备下，否则系统会自动选择一个可用的设备名。虚拟服务器会直接使用独立于 {{site.data.keyword.blockstorageshort}} 服务的指定设备执行其 I/O 操作。

您还可以创建卷的块级别快照。{{site.data.keyword.blockstorageshort}} 服务不允许卷处于连接状态时创建快照，这样生成的快照将处于崩溃一致状态。 


## 如何创建 {{site.data.keyword.blockstorageshort}} 服务实例
要在空间中创建 {{site.data.keyword.blockstorageshort}} 服务实例，请执行以下步骤：
 
1.	转至 {{site.data.keyword.Bluemix_notm}} **目录**选项卡，然后在搜索框中输入 **{{site.data.keyword.blockstorageshort}}**，或者转至**服务**，然后选择**存储器**。单击 **{{site.data.keyword.blockstorageshort}}** 服务。 
2.	输入空间和服务名称。选择套餐，然后单击**创建**。
 	
仅未绑定的上下文中支持 {{site.data.keyword.blockstorageshort}} 服务。 

{{site.data.keyword.blockstorageshort}} 服务的实例将在空间中创建。可以通过单击服务实例图标来随时打开 {{site.data.keyword.blockstorageshort}} UI 以管理卷。



## 使用 {{site.data.keyword.blockstorageshort}} 用户界面 (UI) {: #using-block-storage-ui}
{{site.data.keyword.blockstorageshort}} 图形用户界面在窗口顶部提供了存储卷、快照以及卷和快照的存储器消耗总量的高级别概述。 

标题包含上次 UI 刷新的日期和时间。如果需要，可以使用“刷新”图标（循环箭头图标）来手动刷新 UI。 

使用搜索栏根据输入的字符串来查找卷。输入时会对表进行过滤，以仅显示与输入的搜索字符串匹配的卷。

下面是卷和快照这两个选项卡的概述。缺省情况下已选择“卷”选项卡。此选项卡上的表列出有关可用卷和已连接卷的详细信息。表中每行显示的是卷的最重要属性。展开行可显示更多属性。已连接卷还会显示虚拟服务器实例以及卷连接到的设备。 

“快照”选项卡显示属性和行为类似的快照的表。 

使用表上方的“创建”图标可创建新卷或处理现有卷。如果要从快照创建卷，也可以使用“操作”下拉列表。




## 将卷连接到虚拟服务器 {: #attaching-detaching-volume}
您可以将卷作为具有特定设备名的设备连接到虚拟服务器或从其拆离卷。为了使虚拟服务器能够在卷上持久存储数据，必须将卷连接到虚拟服务器。

要连接卷，请执行以下步骤： 

1.	从可用卷列表中选择卷。
2.	单击**连接**。
3.	在“连接”对话框中，从下拉列表中选择虚拟服务器的实例。 
4.	（可选）指定要用于连接此卷的设备。如果未指定设备，系统会自动选择虚拟服务器上第一个可用的设备。
5.	单击**连接**以提交信息并关闭对话框。

卷会列在已连接卷的表中，其中还会列出有关虚拟服务器实例的信息。现在，虚拟服务器可以使用该设备来持久存储数据。 


# 相关链接
{: #rellinks}

## API 参考
{: #api}
* [OpenStack Block Storage (Cinder) API V2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

