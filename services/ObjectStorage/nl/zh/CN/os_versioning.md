---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用对象版本控制 {: #work-with-object-versioning}

*上次更新时间：2016 年 10 月 19 日*
{: .last-updated}

通过对象版本控制，您可以保留不同版本的对象，而无需对文件重命名。这样您就可以查看每个对象的历史记录，并跟踪所做的更改。
{: shortdesc}


### 设置对象版本控制 {: #setting-up-versioning}

通过使用 `X-Versions-Location` 参数，您可以设置容器中每一个对象的版本。要执行此操作，请创建附加容器，以保留较旧版本的对象，如下所示。

可以通过 Swift 客户机或使用 cURL 命令来设置对象版本控制。
* 如果您使用 Swift 客户机，请运行以下命令：

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}
    
* 如果您使用 cURL，那么您可以对其进行如下设置：

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}
    
**注**：备份容器中的对象将会自动以下列格式命名：`<Length><Object_name>/<Timestamp>`。
<table>
  <tr>
    <th> 属性</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td> `Length`</td>
    <td> 对象名称的长度。这是 3 字符零填充十六进制数字。</td>
  </tr>
  <tr>
    <td> `Object_name`</td>
    <td> 对象的名称。</td>
  </tr>
  <tr>
    <td> `Timestamp`</td>
    <td> 最初上传此版本对象的时间戳记。</td>
  </tr>
</table>

### 禁用对象版本控制 {: #disabling-versioning}

可以通过 Swift 客户机或使用 cURL 命令来禁用版本控制。

* 要使用 Swift 客户机，请运行以下命令：

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* 运行以下 cURL 命令禁用版本控制：

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}


### 对象版本控制教程 {: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

您可以使用以下教程来了解对象版本控制的完整生命周期。

1. 创建名为 `container_one` 的容器。

    ```
    swift post container_one
    ```
    {: pre}
    
3. 创建名为 `container_two` 的第二个容器。

    ```
    swift post container_two
    ```
    {: pre}
    
2. 设置版本控制。

    ```
swift post container_one -H "X-Versions-Location:container_two"
```
    {: pre}
    
4. 首次将对象上传到主容器。

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. 将新版本的对象上传到 container_one。上传新版本的文件时，先前的版本会自动移入设置版本控制时指定的备份容器。

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. 要查看容器中新版本的文件，请列出 container_one 中的对象。

    ```
    swift list container_one
    ```
    {: pre}
    
9. 列出 container_two 中的对象。您将看到上一个版本的文件将存储在此容器中。

    ```
    swift list container_two
    ```
    {: pre}
    
10. 删除 container_one 中的对象。删除对象时，备份容器中的上一个版本将自动移入主容器中。

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. 列出这两个容器。您将看到 `container_one` 和 `container_two` 中的原始文件将为空。

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
