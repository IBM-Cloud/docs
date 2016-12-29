---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 管理对象

您可以使用 Swift CLI 、API 或 Bluemix UI 来管理对象和容器。
{: shortdesc}

在可以管理之前，请确保您已认证服务实例、生成服务凭证并已配置 Swift CLI。

使用服务时，可以存储、下载和删除对象。管理对象时，须牢记以下若干事项。
  * 对于可以存储的数据量没有限制，但每次上传不能超过 5 GB。如果需要上传大于 5 GB 的文件，请执行[存储大对象](/docs/services/ObjectStorage/os_large_files.html)中的步骤。
  * Swift 没有真正的目录结构，但可以向命令添加[现有目录](/docs/services/ObjectStorage/os_directories.html)。
  * 为了避免意外覆盖文件，请[设置对象版本控制](/docs/services/ObjectStorage/os_versioning.html)。
  * 可以为要删除的对象[安排时间](/docs/services/ObjectStorage/os_deletion.html)。

