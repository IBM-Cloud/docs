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


# 授予读访问权 

具有 [admin 角色](/docs/services/ObjectStorage/os_access_types.html)的 {{site.data.keyword.objectstorageshort}} 用户可以授予其他用户对容器的读访问权，还可以控制读 ACL 组合。
{: shortdesc}

<table>
<caption> 表 1. 按选项列出的读访问许可权</caption>
  <tr>
    <th> 许可权</th>
    <th> 读 ACL 选项</th>
  </tr>
  <tr>
    <td> 读取（针对所有引用方，而不论帐户亲缘关系为何）</td>
    <td> <code> .r,&#42;  </code></td>
  </tr>
  <tr>
    <td> 读取和列示（针对所有引用方和列表）</td>
    <td> <code> .r:&#42;,.rlistings </code></td>
  </tr>
  <tr>
    <td> 读取和列示（针对特定项目中的指定用户）</td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 读取和列示（针对每个项目中的指定用户）</td>
    <td> <code> &#42;:user_id </code></td>
  </tr>
  <tr>
    <td> 读取和列示（针对指定项目中的每个用户）</td>
    <td> <code> project_id:&#42; </code></td>
  </tr>
  <tr>
    <td> 读取和列示（针对每个项目中的每个用户）</td>
    <td> <code> &#42;:&#42; </code></td>
  </tr>
</table>



1. 对凭证进行认证。您可以使用在 UI 的“服务凭证”选项卡中找到的凭证，也可以生成新凭证。有关生成新凭证的更多信息，请参阅[生成服务凭证](/docs/services/ObjectStorage/os_credentials.html)。您会在输出中收到 {{site.data.keyword.objectstorageshort}} URL 和认证令牌。

    Swift 命令：

    ```
  export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
  export OS_TENANT_ID=<project_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
    {: codeblock}

      cURL 命令：

    ```
  curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
  ```
    {: pre}

2. 通过运行以下命令，授予读访问权：
    Swift 命令：


    ```
  swift post <container_name> --read-acl "<user_id>:<project_id>"
  ```
    {: pre}

      cURL 命令：

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}
    **注**：请使用逗号 (,) 来分隔访问控制表。


3. 验证读 ACL 值。

    Swift 命令：

    ```
  swift stat <container_name>
  ```
    {: pre}

      cURL 命令：

    ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
    {: pre}

    示例：`X-Container-Read` 值显示已对哪个用户授予哪个容器的读访问权。

    ```
    HTTP/1.1 204 No Content
    Content-Length: 0
    X-Container-Object-Count: 1
    Accept-Ranges: bytes
    X-Storage-Policy: standard
    X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
    X-Container-Bytes-Used: 31512
    X-Timestamp: 1462818314.11220
    Content-Type: text/plain; charset=utf-8
    X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
    Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}
