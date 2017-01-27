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


# 删除对象

不再需要对象和容器时，可以将其从存储器实例中删除。您可以手动执行删除操作，也可以[安排时间](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion)使对象到期。
{: shortdesc}

**注**：如果删除容器，还将删除该容器内存储的所有对象。


## 通过 UI 删除对象和容器 {: #deleting-ui}

1. 在服务实例仪表板中，选择包含不再需要的文件的容器。
2. 从**操作**下拉菜单中，选择**删除文件**。
3. 如果不再使用容器，请从**操作**下拉菜单中，选择**删除容器**。



## 通过 CLI 删除对象和容器 {: #deleting-cli}

1.  如果您未登录到 {{site.data.keyword.Bluemix_notm}}，请登录到包含您的 {{site.data.keyword.objectstorageshort}} 实例的组织和空间。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 可选：在删除文件和容器之前，确认您已经拥有对象的备份。

3. 运行以下命令删除文件：
  ```
swift delete <container_name> <file_name>
```
  {: pre}

4. 要删除容器，请运行以下命令：
  ```
    swift delete <container_name>
    ```
  {: pre}



## 安排对象删除 {: #schedule-object-deletion}


通过使用 `X-Delete-At` 或 `X-Delete-After` 头，可以安排删除对象。
{: shortdesc}

`X-Delete-At` 头采用整数，代表删除对象的戳记时间。`X-Delete_After` 头采用整数，代表在该秒数之后删除对象。

**注：**对象的实际删除可能不会在所指示的确切时间发生。但事实上，对象会在指定的时间到期。此时无法再使用该对象。实际删除操作将会在下一次 Swift 集群中配置的 swift-object-expirer 守护程序运行时发生。

#### 使用 Swift 命令：

* 要将对象设置为在特定日期和时间被删除，请运行以下命令：

    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}

    示例：
    要将对象设置为在“2016/04/01 08:00:00”时删除，请运行以下命令：

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* 要将对象设置为在特定时间后删除，请运行以下命令：

    ```
    swift post -H "X-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}

    示例：
    要将对象设置为在一小时后删除，请运行以下命令：

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* 要从对象除去到期时间，请使用以下命令：

    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}



#### 使用 cURL 命令：

* 要将对象设置为在“2016/04/01 08:00:00”删除，请使用以下命令：

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 要将对象设置为在此后一小时删除，请使用以下命令：

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 要检查对象是否有标头，请使用以下命令：

    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 要除去到期时间，请使用以下命令：

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
