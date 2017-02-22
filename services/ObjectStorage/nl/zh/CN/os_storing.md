---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 存储对象

您可以使用 UI 或 CLI 将对象上传到存储器。在单个上传中，上传对象的最大大小限制为 5 GB。但是，可以通过将大于此限制的对象分段为较小的对象来进行上传。
{: shortdesc}


## 通过 UI 将对象存储在容器中 {: #storing-ui}

**注**：上传同名文件时，{{site.data.keyword.objectstorageshort}} 会用新文件替换存储的文件。如果下载文件并进行了编辑，请确保在上传该文件之前对其另外命名，或者[设置对象版本控制](/docs/services/ObjectStorage/os_versioning.html)以保留该文件的两个版本。


1. 在服务实例仪表板中，从**操作**下拉菜单中添加容器。
2. 对容器命名，然后单击**创建**。
3. 从**操作**下拉菜单中，选择**添加文件**。这将打开一个对话框。
4. 选择要上传的一个或多个文件，然后单击**打开**。



## 通过 CLI 将对象存储在容器中 {: #storing-cli}

1. 如果您未登录到 {{site.data.keyword.Bluemix_notm}}，请登录到包含您的 {{site.data.keyword.objectstorageshort}} 实例的组织和空间。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 通过运行以下命令，创建 {{site.data.keyword.objectstorageshort}} 容器。现在，您将设置 *container_name* 变量。

  ```
swift post <container_name>
```
  {: pre}

**注**：如果收到错误消息，请确认是否已安装[必备软件](/docs/services/ObjectStorage/os_configuring.html#install-swift-client)。

3. 可选：要验证容器是否已创建，请运行以下命令来列出容器。

  ```
swift list
```
  {: pre}

4. 为了防止意外覆盖导致数据毁坏，请[设置对象版本控制](/docs/services/ObjectStorage/os_versioning.html)。如果您不希望设置对象版本控制，请列出存储中的现有文件，在必要时重命名目录或文件，然后再上传。

5. 通过运行以下命令，将文件上传到容器。

  ```
swift upload <container_name> <file_name>
```
  {: pre}

  **注**：要上传大于 5GB 的文件，[需要执行额外的步骤](/docs/services/ObjectStorage/os_large_files.html)。

6. 可选：要验证上传是否成功，请通过运行以下命令查看容器的内容：

  ```
swift list <container_name>
```
  {: pre}
