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


# 授予写访问权 

具有 [admin 角色](/docs/services/ObjectStorage/os_access_types.html)的 {{site.data.keyword.objectstorageshort}} 用户可以授予其他用户写访问权，还可以控制写 ACL 组合。
{: shortdesc}

<table>
<caption> 表 1. 按选项列出的写访问许可权</caption>
  <tr>
    <th> 许可权</th>
    <th> 写 ACL 选项</th>
  </tr>
  <tr>
    <td> 写入（针对特定项目中的指定用户）</td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 写入（针对每个项目中的指定用户）</td>
    <td> <code> &#42;:user_id </code></td>
  </tr>
  <tr>
    <td> 写入（针对指定项目中的每个用户）</td>
    <td>  <code> project_id:&#42; </code></td>
  </tr>
  <tr>
    <td> 写入（针对每个项目中的每个用户）</td>
    <td>  <code> &#42;:&#42; </code></td>
  </tr>
</table>



1. 通过您所创建的服务凭证中的信息，认证您的凭证。您会在输出中收到 {{site.data.keyword.objectstorageshort}} URL 和认证令牌。

    Swift 命令：

    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
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
  curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
  ```
    {: pre}

2. 通过运行以下命令，授予写访问权。

    Swift 命令：

    ```
  swift post <container_name> --write-acl "<user_id>:<project_id>"
  ```
    {: pre}

      cURL 命令：

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
    {: pre}

    **注**：请使用逗号 (,) 来分隔访问控制表。

3. 验证写 ACL 值。


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
