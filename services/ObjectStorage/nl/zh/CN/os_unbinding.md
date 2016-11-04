---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 取消绑定和撤销供应 {{site.data.keyword.objectstorageshort}} 实例 {: #deprovisioning-object-storage}

*上次更新时间：2016 年 10 月 19 日*
{: .last-updated}


### 取消绑定实例
如果在 Cloud Foundry 应用程序中不再需要 {{site.data.keyword.objectstorageshort}}，但又希望保留已保存的数据，那么可以取消服务实例与应用程序的绑定。

**注意**：如果取消 {{site.data.keyword.objectstorageshort}} 实例与 {{site.data.keyword.Bluemix_notm}} 应用程序的绑定或删除服务密钥，那么该实例的所有凭证都会被删除，并且无法复原。

1. 在 {{site.data.keyword.Bluemix_notm}} 控制台中打开应用程序详细信息。
2. 选择 {{site.data.keyword.objectstorageshort}} 实例，然后单击**取消绑定服务**。
3. 单击**除去**。
4. 单击**重新编译打包**。



### 撤销供应实例

如果不再需要某个已取消绑定的 {{site.data.keyword.objectstorageshort}} 实例，那么可以删除该实例。

**注意**：撤销供应 {{site.data.keyword.objectstorageshort}} 实例时，将删除云项目。撤销供应的实例中的所有容器和对象也将被删除，并且无法复原。

1. 在 {{site.data.keyword.Bluemix_notm}} 控制台中打开应用程序详细信息。
2. 选择 {{site.data.keyword.objectstorageshort}} 实例，然后单击**删除**。
3. 单击**重新编译打包**。
