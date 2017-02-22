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


# 授與讀取權 

具有[管理者角色](/docs/services/ObjectStorage/os_access_types.html)的 {{site.data.keyword.objectstorageshort}} 使用者可以授與另一位使用者對容器的讀取權，以及操作讀取 ACL 組合。
{: shortdesc}

<table>
<caption> 表 1. 依選項列出的讀取權</caption>
  <tr>
    <th> 許可權</th>
    <th> 讀取 ACL 選項</th>
  </tr>
  <tr>
    <td> 無論帳戶連結為何，所有參照者皆可讀取</td>
    <td> <code> .r,&#42;  </code> </td>
  </tr>
  <tr>
    <td> 所有參照者及清單皆可讀取及列出</td>
    <td> <code> .r:&#42;,.rlistings </code> </td>
  </tr>
  <tr>
    <td> 特定專案中指定的使用者可以讀取及列出</td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 每個專案中指定的使用者可以讀取及列出</td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> 指定專案中的每個使用者皆可讀取及列出</td>
    <td> <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> 每個專案中的每個使用者皆可讀取及列出</td>
    <td> <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. 鑑別您的認證。您可以使用在使用者介面的服務認證標籤中找到的認證，也可以產生新的認證。如需產生新認證的相關資訊，請參閱[產生服務認證](/docs/services/ObjectStorage/os_credentials.html)。您會收到 {{site.data.keyword.objectstorageshort}} URL 及鑑別記號作為輸出。

    Swift 指令：

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

    cURL 指令：

    ```
    curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
    ```
    {: pre}

2. 執行下列指令來授與讀取權。Swift 指令：

    ```
    swift post <container_name> --read-acl "<user_id>:<project_id>"
    ```
    {: pre}

    cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}
    **附註**：使用逗點 (,) 來區隔存取控制清單。


3. 驗證「讀取 ACL」值。

    Swift 指令：

    ```
    swift stat <container_name>
    ```
    {: pre}

    cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    範例：`X-Container-Read` 值顯示已將讀取權授與哪個容器及哪個人。

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
