---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 保障文件安全 {: #understanding-authentication}


## 了解服务凭证 {: #understanding-credentials}

服务凭证用于为服务提供认证和安全性。供应实例时，会自动生成一组凭证。Swift 客户机通过下表中的环境变量获取认证信息：

<table>
  <tr>
    <th> 环境变量</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> 您的 {{site.data.keyword.objectstorageshort}} 用户标识。</td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> {{site.data.keyword.objectstorageshort}} 实例的密码。</td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> 项目标识。</td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> 存储对象的区域。{{site.data.keyword.objectstorageshort}} 可在达拉斯和伦敦区域中使用。</td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> 端点 URL。确保将 `/v3` 添加到 URL 末尾。</td>
  </tr>
</table>

表 1：认证变量和描述

####  在 UI 中添加服务凭证
1. 在服务实例仪表板上的**服务凭证**选项卡中，单击**新建凭证**并对其命名。
2. （*可选*）在**添加内联配置参数**文本字段中，输入要创建的角色的凭证信息。信息格式必须为 JSON 有效内容。有关 {{site.data.keyword.objectstorageshort}} 用户角色的更多信息，请参阅[访问权类型](../os_security.html#access-types)。
    - 创建管理用户：`{"role":"admin"}`
    - 创建非管理用户：`{"role":"member"}`
3. 单击**添加**。


## 访问权类型 {: #access-types}

对服务的访问权是通过用户角色和容器访问控制表进行控制的。{{site.data.keyword.objectstorageshort}} 用户可以是管理用户，也可以是非管理用户。访问控制表由管理用户在容器级别启用，其在服务实例、存储帐户或项目级别不可用。

<table>
  <tr>
    <th> 管理用户 (admin)</th>
    <th> 非管理用户 (member)</th>
  </tr>
  <tr>
    <td> 管理访问控制</td>
    <td> 缺省情况下，无权访问服务或其容器</td>
  </tr>
  <tr>
    <td> 可以创建和删除容器</td>
    <td> 可以基于容器读/写 ACL 执行操作</td>
  </tr>
  <tr>
    <td> 可以读取和写入容器</td>
    <td> 可以执行由 admin 确定的操作</td>
  </tr>
</table>

表 2：定义的用户角色

您可以通过 {{site.data.keyword.Bluemix_notm}} 用户界面、Cloud Foundry API 或 Cloud Foundry CLI 来管理 {{site.data.keyword.objectstorageshort}} 用户。




## 授予读访问权 {: #read-access}

具有 admin 角色的 {{site.data.keyword.objectstorageshort}} 用户可以授予其他用户对容器的读访问权，还可以控制读 ACL 组合。

<table>
  <tr>
    <th> 许可权</th>
    <th> 读 ACL 选项</th>
  </tr>
  <tr>
    <td> 读取（针对所有引用方，而不论帐户亲缘关系为何）</td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> 读取和列示（针对所有引用方和列表）</td>
    <td> <code>.r:*,.rlistings</code></td>
  </tr>
  <tr>
    <td> 读取和列示（针对特定项目中的指定用户）</td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 读取和列示（针对每个项目中的指定用户）</td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> 读取和列示（针对指定项目中的每个用户）</td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> 读取和列示（针对每个项目中的每个用户）</td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

表 3：按选项列出的读访问许可权



1. 对凭证进行认证。您可以使用在 UI 的“服务凭证”选项卡中找到的凭证，也可以生成新凭证。有关生成新凭证的更多信息，请参阅[生成服务凭证](insert link here)。您会在输出中收到 {{site.data.keyword.objectstorageshort}} URL 和认证令牌。Swift 命令：

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


3. 验证读 ACL 值。Swift 命令：

    ```
  swift stat <container_name>
  ```
    {: pre}
  cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
    {: pre}

    在以下示例输出中，可以看到已经授予了读访问权：

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



## 授予写访问权 {: #write-access}

具有 admin 角色的 {{site.data.keyword.objectstorageshort}} 用户可以授予其他用户对容器的写访问权，还可以控制写 ACL 组合。

<table>
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
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> 写入（针对指定项目中的每个用户）</td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> 写入（针对每个项目中的每个用户）</td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

表 4：按选项列出的写访问许可权



1. 通过您所创建的服务凭证中的信息，认证您的凭证。您会在输出中收到 {{site.data.keyword.objectstorageshort}} URL 和认证令牌。Swift 命令：

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

2. 通过运行以下命令，授予写访问权：
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



## 除去访问权 {: #removing-access}

要从容器除去读 ACL，请使用：
* Swift 命令：

    ```
    swift post <container_name> --read-acl “”
    ```
    {: pre}

*  cURL 命令：

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

要从容器除去写 ACL，请使用：

* Swift 命令：

    ```
  swift post <container_name> --write-acl “”
  ```
    {: pre}

*  cURL 命令：

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}

要验证是否已除去 ACL，请使用：

* Swift 命令：

    ```
  swift stat <container_name>
  ```
    {: pre}

  以下示例输出中显示的“读 ACL”和“写 ACL”均为空白，这表示访问权已除去。

  ```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8

  ```
  {: screen}

* cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
