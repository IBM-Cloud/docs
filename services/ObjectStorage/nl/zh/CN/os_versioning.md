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


# 设置对象版本控制 {: #setting-up-versioning}

通过设置对象版本控制，可自动保留较旧版本的对象。使用版本控制，可查看每个对象的历史记录。
{: shortdesc}

将新版本的文件上传到主容器时，上一个版本会自动移入备份容器。如果从主容器中删除文件，那么最新版本会自动从备份容器移入主容器，以代替删除的文件。

1. 创建容器并对其命名。将 *container_name* 变量替换为希望为容器提供的名称。

    ```
swift post <container_name>
```
    {: pre}

2. 再创建一个容器以充当备份存储器，并对其命名。

    ```
    swift post <backup_container_name>
    ```
    {: pre}

3. 设置版本控制。

    Swift 命令：

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}

      cURL 命令：

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. 首次将对象上传到主容器。

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

5. 对对象进行更改。

6. 将新版本的对象上传到主容器。

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

7.  备份容器中的对象将会自动以下列格式命名：`<Length><Object_name>/<Timestamp>`。
  <table>
  <caption> 表 1. 描述的命名属性</caption>
    <tr>
      <th> 属性</th>
      <th> 描述</th>
    </tr>
    <tr>
      <td> <i>Length</i></td>
      <td> 对象名称的长度。这是 3 字符零填充十六进制数字。</td>
    </tr>
    <tr>
      <td> <i>Object_name</i></td>
      <td> 对象的名称。</td>
    </tr>
    <tr>
      <td> <i>Timestamp</i></td>
      <td> 最初上传此版本对象的时间戳记。</td>
    </tr>
  </table>


6. 列出主容器中的对象，以查看新版本的文件。

    ```
    swift list --lh <container_name>
    ```
    {: pre}

7. 列出备份容器中的对象。您将看到上一个版本的文件已存储在此容器中。请注意，已向该文件添加时间戳记。

    ```
    swift list --lh <backup_container_name>
    ```
    {: pre}

8. 删除主容器中的对象。删除对象时，备份容器中的最新版本将自动移回主容器中。

    ```
    swift delete <container_name>
    <object>
    ```
    {: pre}

9. 可选：禁用对象版本控制。

    Swift 命令：

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

      cURL 命令：

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}
