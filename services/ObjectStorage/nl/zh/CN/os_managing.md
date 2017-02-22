---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 管理对象

您可以使用 Swift CLI 、API 或 Bluemix UI 来管理对象和容器。
{: shortdesc}

在可以管理对象之前，请确保您已[认证](/docs/services/ObjectStorage/os_authenticate.html)服务实例、[生成](/docs/services/ObjectStorage/os_credentials.html)服务凭证并已[配置](/docs/services/ObjectStorage/os_configuring.html) Swift CLI。

管理对象时请记住以下几点：
  * 对于可以存储的数据量没有限制，但每次上传不能超过 5 GB。如果需要上传大于 5 GB 的文件，请执行[存储大对象](/docs/services/ObjectStorage/os_large_files.html)中的步骤。
  * Swift 没有真正的目录结构，但可以向命令添加[现有目录](/docs/services/ObjectStorage/os_directories.html)。
  * 为了避免意外覆盖文件，请[设置对象版本控制](/docs/services/ObjectStorage/os_versioning.html)。
  * 可以为要删除的对象[安排时间](/docs/services/ObjectStorage/os_deletion.html)。

