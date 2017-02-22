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


# 授與寫入權 

具有[管理者角色](/docs/services/ObjectStorage/os_access_types.html)的 {{site.data.keyword.objectstorageshort}} 使用者可以授與另一位使用者寫入權，以及操作寫入 ACL 組合。
{: shortdesc}

<table>
<caption> 表 1. 依選項列出的寫入權</caption>
  <tr>
    <th> 許可權</th>
    <th> 寫入 ACL 選項</th>
  </tr>
  <tr>
    <td> 特定專案中指定的使用者可以寫入</td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 每個專案中指定的使用者可以寫入</td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> 指定專案中的每個使用者皆可寫入</td>
    <td>  <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> 每個專案中的每個使用者皆可寫入</td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. 使用您所建立之服務認證中的資訊來鑑別您的認證。您會收到 {{site.data.keyword.objectstorageshort}} URL 及鑑別記號作為輸出。

    Swift 指令：

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

    cURL 指令：

    ```
    curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. 執行下列指令來授與寫入權。

    Swift 指令：

    ```
    swift post <container_name> --write-acl "<user_id>:<project_id>"
    ```
    {: pre}

    cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    **附註**：使用逗點 (,) 來區隔存取控制清單。

3. 驗證寫入 ACL 值。

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
