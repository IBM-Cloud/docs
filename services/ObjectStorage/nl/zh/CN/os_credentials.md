---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 生成服务凭证 {: #credentials}

服务凭证用于为服务提供认证和安全性。可以使用 CLI 或 {{site.data.keyword.Bluemix_notm}} UI 来生成新凭证。
{: shortdesc}


## 要在 UI 中添加凭证，请执行以下操作：

1. 在服务实例仪表板上的**服务凭证**选项卡中，单击**新建凭证**并对其命名。
2. 可选：在**添加内联配置参数**文本字段中，输入您想要授予其[访问类型](/docs/services/ObjectStorage/os_access_types.html)的角色的凭证信息。信息格式必须为 JSON 有效内容。
    - 创建管理用户：`{"role":"admin"}`
    - 创建非管理用户：`{"role":"member"}`
3. 单击**添加**。


## 要在 CLI 中使用 Cloud Foundry 命令添加凭证，请执行以下操作：

1. 如果您未登录到 {{site.data.keyword.Bluemix_notm}}，请以具有开发者角色的用户身份进行登录。您必须位于要管理的服务实例的空间内。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 生成服务凭证。通过替换 `service-key-name` 变量，对凭证命名。（可选）您还可以分配[用户角色](/docs/services/ObjectStorage/os_access_types.html)。

  ```
  cf create-service-key "<service_instance_name>" <service-key-name> -c '{"role":"<user_role>"}'
  ```
  {: pre}

  示例：
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
  {: screen}

3. 为您所创建的密钥验证凭证。

  ```
  cf service-keys <service_instance_name>
  ```
  {: pre}

  对于具有 member 角色的用户，名为 Object-Storage-Acl-Test 的实例的示例密钥：

  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  {: screen}



#### 要在 CLI 中使用 cURL 命令添加凭证，请执行以下操作：

1. 如果您未登录到 {{site.data.keyword.Bluemix_notm}}，请以具有开发者角色的用户身份进行登录。您必须位于要管理的服务实例的空间内。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 运行以下命令以生成服务凭证。

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name: <service_instance_name>", "role: <user_role>"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: <content_type" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> 表 1. cURL 服务凭证变量说明</caption>
    <tr>
      <th> 变量</th>
      <th> 说明</th>
    </tr>
    <tr>
      <td> ```https://api.ng.bluemix.net/v2/service_keys``` </td>
      <td> 服务密钥端点。</td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> 可以在 URL 中找到。</td>
    </tr>
    <tr>
      <td><i> name </i></td>
      <td> 服务实例的名称。</td>
    </tr>
    <tr>
      <td><i> role </i></td>
      <td> 将<a href= /docs/services/ObjectStorage/os_constructing.html>用户角色</a>指定为 admin 或 member。</td>
    </tr>
    <tr>
      <td><i> bearer_token </i></td>
      <td> 使用 Keystone 认证实例时收到的令牌。</td>
    </tr>
  </table>

3. 通过运行以下命令验证凭证。

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: screen}
