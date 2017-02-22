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

# 下载对象

您可以通过 UI 或 CLI 下载存储的对象以进行查看或编辑。
{: shortdesc}


## 通过 UI 下载对象 {: #downloading-ui}

1. 为了防止意外覆盖导致数据毁坏，请[设置对象版本控制](/docs/services/ObjectStorage/os_versioning.html)。如果您不希望进行对象版本控制，请根据需要重命名目录或文件，然后再下载。
2. 在服务实例仪表板中，选择包含要下载的文件的容器。
3. 选择该文件。
4. 从**操作**下拉菜单中，选择**下载文件**。


## 使用 Swift CLI 下载对象 {: #downloading-cli}

1.  如果您未登录到 {{site.data.keyword.Bluemix_notm}}，请登录到包含您的 {{site.data.keyword.objectstorageshort}} 实例的组织和空间。

```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
{: pre}

2. 为了防止意外覆盖导致数据毁坏，请[设置对象版本控制](/docs/services/ObjectStorage/os_versioning.html)。如果您不希望设置对象版本控制，请列出存储中的现有文件，在必要时重命名目录或文件，然后再下载。

3. 通过运行以下命令下载文件：

```
swift download <container_name> <file_name>
```
{: pre}
