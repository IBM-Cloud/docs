{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}} (BETA) 入门

{{site.data.keyword.blockstoragefull}} 针对需要持久存储器的事务密集型工作负载和运行时，提供了对块级别存储器的访问。

您可以使用 IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} 来创建可以连接到虚拟机的 {{site.data.keyword.blockstorageshort}} 卷。块存储卷中的数据持续存储的时间长于虚拟机的生命周期。IBM {{site.data.keyword.blockstorageshort}} 使用 OpenStack Cinder 来管理卷生命周期。

{{site.data.keyword.blockstorageshort}} 卷通过 IBM {{site.data.keyword.blockstorageshort}} 服务实例进行创建。可以将卷连接到虚拟机中所提供特定设备下，否则系统可以自动选择可用设备名。虚拟机会直接通过独立于 {{site.data.keyword.blockstorageshort}} 服务的指定设备执行其 I/O 操作。

您还可以创建卷的块级别快照。{{site.data.keyword.blockstorageshort}} 服务不允许卷处于连接状态时创建快照，这样生成的快照将处于崩溃一致状态。 

## 如何创建 {{site.data.keyword.blockstorageshort}} 服务实例
要在空间中创建 {{site.data.keyword.blockstorageshort}} 服务实例，请执行以下步骤：
 
1.	转至 {{site.data.keyword.Bluemix_notm}} **目录**选项卡，然后在搜索框中输入 **{{site.data.keyword.blockstorageshort}}**，或者转至**服务**，然后选择**存储器**。单击 **{{site.data.keyword.blockstorageshort}}** 服务。 
2.	输入空间和服务名称。选择套餐，然后单击**创建**。
 	
仅未绑定的上下文中支持 {{site.data.keyword.blockstorageshort}} 服务。 

{{site.data.keyword.blockstorageshort}} 服务的实例将在空间中创建。可以通过单击服务实例图标来随时打开 {{site.data.keyword.blockstorageshort}} UI 以管理卷。

## {{site.data.keyword.blockstorageshort}} 用户界面 (UI)
{{site.data.keyword.blockstorageshort}} 图形用户界面在窗口顶部提供了存储卷、快照以及卷和快照的存储器消耗总量的高级别概述。 

标题包含上次 UI 刷新的日期和时间。如果需要，可以使用“刷新”图标（循环箭头图标）来手动刷新 UI。 

使用搜索栏根据输入的字符串来查找卷。输入时会对表进行过滤，以仅显示与输入的搜索字符串匹配的卷。

下面是卷和快照这两个选项卡的概述。缺省情况下已选择“卷”选项卡。此选项卡上的表列出有关可用卷和已连接卷的详细信息。表中每行显示的是卷的最重要属性。展开行可显示更多属性。已连接卷还会显示虚拟机实例以及卷连接到的设备。 

“快照”选项卡显示属性和行为类似的快照的表。 

使用表上方的“创建”图标可创建新卷或处理现有卷。如果要从快照创建卷，也可以使用“操作”下拉列表。


## 卷操作

### 创建卷

1.	单击**创建**以启动**创建卷**对话框。
2.	提供所需卷的大小。不接受小数。大小受分配给组织的配额限制。
3.	提供名称。名称仅用于显示。
4.	（可选）提供更详细的卷描述。 
5.	单击**创建**以提交信息并关闭对话框。 

创建卷可能需要几分钟时间。 

### 删除卷

1.	选择要删除的卷。
2.	单击**删除**。
3.	确认删除此卷。

无法删除连接到虚拟机的卷。必须先拆离该卷。

### 扩展卷
可以通过**扩展**操作来增大卷大小。不能减小卷大小。

1.	选择要扩展的卷。
2.	单击**扩展**。
3.	选择卷的新大小。提供卷的新总大小。
4.	单击**扩展**以提交信息并关闭对话框。 

要进行扩展，卷必须处于**可用**状态。 

### 将卷连接到虚拟机和从虚拟机拆离卷
卷作为具有特定设备名的设备连接到虚拟机，并可从虚拟机拆离。为了使虚拟机能够在卷上持久存储数据，必须将卷连接到虚拟机。

要连接卷，请执行以下步骤： 

1.	从可用卷列表中选择卷。
2.	单击**连接**。
3.	在“连接”对话框中，从下拉列表中选择虚拟机的实例。 
4.	（可选）指定要用于连接此卷的设备。如果未指定设备，系统会自动选择虚拟机上第一个可用的设备。
5.	单击**连接**以提交信息并关闭对话框。

卷会列在已连接卷的表中，并包含有关虚拟机实例的信息。现在，虚拟机可以使用该设备来持久存储数据。 

要拆离卷，请执行以下步骤： 

1.	从已连接卷的列表中选择卷。 
2.	单击**拆离**。
3.	在对话框中确认拆离。 

拆离后，该卷不再可用于虚拟机实例中的 I/O 操作。在 {{site.data.keyword.blockstorageshort}} 服务 UI 中，现在该卷可用于连接到其他虚拟机。

## 快照操作

### 创建快照

1.	选择**卷**选项卡以获得卷的列表。
2.	在未连接卷列中，选择要创建其快照的卷。确保所选的卷未连接。所选卷会突出显示。 
3.	单击**操作**，然后从下拉列表中选择**创建快照**。
4.	为快照提供名称，然后单击**创建**。

**注：**存在卷的快照时，不能删除卷。 

### 从快照创建卷

1.	选择**快照**选项卡以获得快照的列表。
2.	选择要从中创建卷的快照。所选快照会突出显示。
3.	单击**操作**，然后从下拉列表中选择**创建卷**。
4.	为新卷提供名称，并可选择新的大小，然后单击**创建**。 

**注：**新的卷大小必须等于或大于快照大小。 

### 删除快照

1.	选择**快照**选项卡以获得快照的列表。
2.	选择要删除的快照。所选快照会突出显示。
3.	单击**操作**，然后选择**删除**。 



># 相关链接{:class="linklist"}
>## API 参考{:id="api"}
>* [OpenStack Block Storage (Cinder) API V2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}
>
>{:elementKind="article" id="rellinks"}
