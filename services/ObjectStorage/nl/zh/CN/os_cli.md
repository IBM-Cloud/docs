---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
# 开始使用 {{site.data.keyword.objectstorageshort}}  {: #using-object-storage}
*上次更新时间：2016 年 10 月 19 日*
{: .last-updated}

# 使用 Swift CLI 访问 {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}


{{site.data.keyword.objectstorageshort}} 服务基于 OpenStack Swift，可以使用任何兼容的客户机应用程序进行访问。本部分描述如何利用 Python Swift 客户机来使用容器和文件；Python Swift 客户机是 {{site.data.keyword.objectstorageshort}} API 及其扩展的命令行界面。
{: shortdesc}

## 安装 Swift 客户机 {: #install-swift-client}

如果尚未准备就绪，请安装以下[必备软件](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}。
* Python 2.7 或更高版本
* setuptools 软件包
* pip 软件包

要安装 Python Swift 客户机，请运行以下命令：
  ```
sudo pip install python-swiftclient
```
  {: pre}

要安装 Python Keystone 客户机，请运行以下命令：
  ```
sudo pip install python-keystoneclient
```
  {: pre}




## 设置客户机 {: #setup-swift-client}

要设置 Swift 客户机，必须执行 `export` 命令以导出认证信息。可以使用在 UI 中找到的凭证，也可以[生成新凭证](../ObjectStorage/os_cli.html#generating-cli)。

示例：
  ```
  export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  {: codeblock}




## 生成 {{site.data.keyword.objectstorageshort}} 服务凭证 {: #generating-cli}

要使用 Swift CLI 来生成服务凭证，可以执行以下步骤。

1. 以开发者角色的用户身份登录到 {{site.data.keyword.Bluemix_notm}}。您必须位于要管理的服务实例的空间内。
      ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
      {: pre}
2. 生成服务凭证。`service-key-name` 是为凭证提供的名称。您可以使用 Cloud Foundry 命令或 cURL 命令。Cloud Foundry 命令：
      ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```
      {: pre}
      示例 Cloud Foundry 命令：
      ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
      {: screen}
  cURL 命令：
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```
      {: pre}
3. 为您所创建的服务密钥验证凭证。Cloud Foundry 命令：
      ```
  cf service-key <service_key_name> <member_name>
  ```
      {: pre}
      名为 Object-Storage-Acl-Test 的实例的示例成员服务密钥：
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
  cURL 命令：
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
      {: pre}




## 通过 CLI 将对象存储在容器中 {: #storing-cli}

1. 登录到 {{site.data.keyword.Bluemix_notm}}。确保位于正确的组织和空间中，以便使用 {{site.data.keyword.objectstorageshort}} 的实例。
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 通过运行以下命令，创建新容器。此时，您将设置 *container_name* 变量。
    ```
swift post <container_name>
```
    {: pre}
3. （*可选*）要验证容器是否已创建，请运行以下命令来列出容器。
    ```
swift list
```
    {: pre}
4. 通过运行以下命令，将文件上传到容器。
    ```
swift upload <container_name> <file_name>
```
    {: pre}
    **注**：要上传大于 5 GB 的文件，需要额外的步骤。有关更多信息，请参阅[使用大型文件](../ObjectStorage/os_large_files.html#large-files)。
5. （*可选*）要验证上传是否成功，请通过运行以下命令查看容器的内容：
    ```
swift list <container_name>
```
    {: pre}

**注**：上传同名文件时，{{site.data.keyword.objectstorageshort}} 会用新文件替换存储的文件。如果下载文件并进行了编辑，请确保在上传该文件之前对其另外命名，或者[设置对象版本控制](../ObjectStorage/os_versioning.html#work-with-object-versioning)以保留该文件的两个版本。



## 使用 Swift CLI 下载对象 {: #downloading-cli}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。确保位于正确的组织和空间中，以便使用 {{site.data.keyword.objectstorageshort}} 的实例。
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 通过运行以下命令下载文件：
    ```
swift download <container_name> <file_name>
```
    {: pre}




## 通过 CLI 删除对象和容器 {: #deleting-cli}

1.  登录到 {{site.data.keyword.Bluemix_notm}}。确保位于正确的组织和空间中，以便使用 {{site.data.keyword.objectstorageshort}} 的实例。
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 运行以下命令删除文件：
    ```
swift delete <container_name> <file_name>
```
    {: pre}
    **注**：您可以安排[删除对象的特定时间](../ObjectStorage/os_deletion.html#schedule-object-deletion)。
3. 要删除容器，请运行以下命令：
    ```
    swift delete <container_name>
    ```
    {: pre}
    **注意**：如果删除容器，还将删除该容器内存储的所有对象。




## 使用目录 {: #directory-cli}

#### 使用 Swift CLI 向容器添加目录

Swift 没有真正的目录结构，而是使用命名来表示目录布局。如果指定目录名称，那么会将该目录名称附加到所有文件名以作为相对路径的一部分。

1. 运行以下命令向容器添加目录：
    ```
swift upload <container_name> <directory_name>
```
    {: pre}

#### 下载目录
要下载目录结构，请使用 `-prefix` 参数来指示要下载的目录或目录结构。

1. 运行以下命令下载目录：
    ```
swift download <container_name> --prefix <directory>
```
    {: pre}
