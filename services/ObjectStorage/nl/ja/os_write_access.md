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


# 書き込み権限の付与 

[管理者の役割](/docs/services/ObjectStorage/os_access_types.html)を持つ {{site.data.keyword.objectstorageshort}} ユーザーは、別のユーザーに書き込み権限を付与し、書き込み ACL の組み合わせを操作することができます。
{: shortdesc}

<table>
<caption> 表 1. オプション別の書き込みアクセス許可</caption>
  <tr>
    <th> 許可 </th>
    <th> 書き込み ACL オプション </th>
  </tr>
  <tr>
    <td> 特定のプロジェクトの指定されたユーザーに対する書き込み</td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトの指定されたユーザーに対する書き込み</td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> 指定されたプロジェクトのすべてのユーザーに対する書き込み</td>
    <td>  <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトのすべてのユーザーに対する書き込み</td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. 作成したサービス資格情報内の情報を使用して、資格情報を認証します。出力として、{{site.data.keyword.objectstorageshort}} URL と認証トークンを受け取ります。

    Swift コマンド:

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

    cURL コマンド:

    ```
    curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. 以下のコマンドを実行して書き込み権限を付与します。

    Swift コマンド:

    ```
    swift post <container_name> --write-acl "<user_id>:<project_id>"
    ```
    {: pre}

    cURL コマンド:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    **注**: アクセス制御リストを区切るには、コンマ (,) を使用します。

3. 書き込み ACL 値を検証します。

    Swift コマンド:

    ```
    swift stat <container_name>
    ```
    {: pre}

    cURL コマンド:

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}
