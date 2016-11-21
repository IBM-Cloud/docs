---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 创建临时 URL {: #create-temporary-url}

*上次更新时间：2016 年 10 月 19 日*
{: .last-updated}

临时 URL 较长且难以猜中，可用于在指定时间段内下载对象，而不必请求进一步认证。
{: shortdesc}


1. 通过使用以下命令打印帐户信息来确定认证信息：

    ```
swift stat
```
    {: pre}
    
    **注**：找到“帐户”字段，并记录*帐户：*后面的完整字符串，包括 `AUTH_`。
2. 设置密钥。此密钥可以是所选的任何内容，但最佳做法是选择难以猜中的随机长字符串。要设置密钥，请运行以下命令：

    ```
swift post -m "Temp-URL-Key:<key>"
```
    {: pre}
    
3. 通过运行以下命令，验证 `Temp-URL-Key` 是否设置成功。

    ```
swift stat
```
    {: pre}
    
4. 通过运行以下命令，创建临时 URL：

    ```
swift tempurl GET <seconds> <path> <key>
```
    {: pre}
    
    下表说明了 Swift `tempurl` 命令采用的位置参数。
    <table>
      <tr>
        <th> 参数</th>
        <th> 描述</th>
      </tr>
      <tr>
        <td> [method]</td>
        <td> GET 用于允许下载。PUT 用于允许上传。</td>
      </tr>
      <tr>
        <td> [seconds]</td>
        <td> 临时 URL 将可用的时间（以秒为单位）。</td>
      </tr>
      <tr>
        <td> [path]</td>
        <td> 表示为 `/v1/<auth_account>/<container_name>/<object_name>` 的对象的完整路径。有关更多信息，请参阅 [{{site.data.keyword.objectstorageshort}} URL 文档](/os_api.html#access-points)。</td>
      </tr>
      <tr>
        <td> [key]</td>
        <td> 在步骤 2 中设置的密钥。</td>
      </tr>
    </table>
    *表 2：tempurl 位置参数*
5. （*可选*）将返回的 URL 附加到集群名称以获得完整 URL。然后可以使用该完整 URL 通过任何兼容的 HTTP 客户机（例如，cURL、wget 或 Firefox）来下载对象。
