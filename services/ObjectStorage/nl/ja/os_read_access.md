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


# 読み取り権限の付与 

[管理者の役割](/docs/services/ObjectStorage/os_access_types.html)を持つ {{site.data.keyword.objectstorageshort}} ユーザーは、別のユーザーのコンテナーに対する読み取り権限を付与し、読み取り ACL の組み合わせを操作することができます。
{: shortdesc}

<table>
<caption> 表 1. オプション別の読み取りアクセス許可</caption>
  <tr>
    <th> 許可 </th>
    <th> 読み取り ACL オプション </th>
  </tr>
  <tr>
    <td> アカウントの加入に関係なくすべての参照者に対する読み取り</td>
    <td> <code> .r,&#42;  </code> </td>
  </tr>
  <tr>
    <td> すべての参照者に対する読み取りとリストおよびリスト作成 </td>
    <td> <code> .r:&#42;,.rlistings </code> </td>
  </tr>
  <tr>
    <td> 特定のプロジェクトの指定されたユーザーに対する読み取りとリスト </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトの指定されたユーザーに対する読み取りとリスト </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> 指定されたプロジェクトのすべてのユーザーに対する読み取りとリスト</td>
    <td> <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトのすべてのユーザーに対する読み取りとリスト</td>
    <td> <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. 資格情報を認証します。UI のサービス資格情報タブにある資格情報を使用することも、資格情報を新規に生成することも可能です。新規資格情報の生成について詳しくは、[サービス資格情報の生成 (Generating service credentials)](/docs/services/ObjectStorage/os_credentials.html) を参照してください。出力として、{{site.data.keyword.objectstorageshort}} URL と認証トークンを受け取ります。

    Swift コマンド:

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

    cURL コマンド:

    ```
    curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
    ```
    {: pre}

2. 以下のコマンドを実行して、読み取り権限を付与します。
    Swift コマンド:

    ```
    swift post <container_name> --read-acl "<user_id>:<project_id>"
    ```
    {: pre}

    cURL コマンド:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}
    **注**: アクセス制御リストを区切るには、コンマ (,) を使用します。


3. 読み取り ACL 値を検証します。

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

    例: `X-Container-Read` 値は、読み取り権限が付与されるコンテナーおよびユーザーを示します。

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
