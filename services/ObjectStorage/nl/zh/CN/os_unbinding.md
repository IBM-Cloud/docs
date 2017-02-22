---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 取消绑定和撤销供应 {{site.data.keyword.objectstorageshort}} 实例 {: #deprovisioning-object-storage}

如果已将 {{site.data.keyword.objectstorageshort}} 服务绑定到 Cloud Foundry 应用程序，但不再需要存储器，那么可以取消绑定并撤销供应实例。
{: shortdesc}


## 取消绑定实例

您可以保留已保存的数据，并从 Cloud Foundry 应用程序取消绑定服务。{{site.data.keyword.objectstorageshort}} 帐户要到撤销供应服务后才会删除。

**注意**：如果取消 {{site.data.keyword.objectstorageshort}} 实例与 {{site.data.keyword.Bluemix_notm}} 应用程序的绑定或删除服务密钥，那么该实例的所有凭证都会被删除，并且无法复原。通过重新绑定实例或创建新的服务密钥，可以生成新的云凭证。

1. 要查看绑定到应用程序的服务，请单击 Cloud Foundry 应用程序上的“连接”选项卡。
2. 找到想要取消绑定的服务，并单击服务磁贴上的菜单按钮。
3. 选择**取消绑定服务**。
4. 清除**删除服务实例**框并单击**确定**。
5. 单击**重新编译打包**以使更改生效。



## 撤销供应实例

如果不再需要某个 {{site.data.keyword.objectstorageshort}} 实例，那么可以删除该实例。

**注意**：撤销供应 {{site.data.keyword.objectstorageshort}} 实例时，将删除云项目和 Swift 帐户。撤销供应的实例中的所有容器和对象也将被删除，并且无法复原。

1. 要查看绑定到应用程序的服务，请单击 Cloud Foundry 应用程序上的“连接”选项卡。
2. 找到想要撤销供应的服务，并单击服务磁贴上的菜单按钮。
3. 选择**删除服务**。
4. 单击**删除**以确认。
5. 单击**重新编译打包**以使更改生效。
