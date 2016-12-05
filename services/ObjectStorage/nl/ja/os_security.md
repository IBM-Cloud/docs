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


# ファイルの保護 {: #understanding-authentication}


## サービス資格情報の概要 {: #understanding-credentials}

サービス資格情報は、サービスの認証およびセキュリティーを提供するために使用されます。インスタンスをプロビジョンすると、一連の資格情報が自動的に生成されます。Swift クライアントは、以下の表の環境変数から認証情報を取得します。

<table>
  <tr>
    <th> 環境変数 </th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> {{site.data.keyword.objectstorageshort}} のユーザー ID。</td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> {{site.data.keyword.objectstorageshort}} インスタンスのパスワード。</td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> プロジェクト ID。</td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> オブジェクトが保管された地域。{{site.data.keyword.objectstorageshort}} は、ダラスとロンドンの地域で利用可能です。</td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> エンドポイント URL。必ず、URL の最後に `/v3` を追加してください。</td>
  </tr>
</table>

表 1: 認証の変数と説明

####  UI でのサービス資格情報の追加
1. サービス・インスタンス・ダッシュボードの**「サービス資格情報」**タブで、**「新規資格情報 (New Credential)」**をクリックして、名前を指定します。
2. (*オプション* ) **「インライン構成パラメーターの追加」**テキスト・フィールドに、作成する役割の資格情報を入力します。この情報は、JSON ペイロードとしてフォーマット設定する必要があります。{{site.data.keyword.objectstorageshort}} ユーザー役割について詳しくは、[アクセスのタイプ](../os_security.html#access-types)を参照してください。
    - 管理ユーザーを作成する場合: `{"role":"admin"}`
    - 非管理ユーザーを作成する場合: `{"role":"member"}`
3. **「追加」**をクリックします。


## アクセスのタイプ {: #access-types}

サービスへのアクセスは、ユーザーの役割とコンテナーのアクセス制御リストによって制御されます。{{site.data.keyword.objectstorageshort}} のユーザーは、管理ユーザーまたは非管理ユーザーのいずれかです。アクセス制御リストは、管理ユーザーによってコンテナー・レベルで有効にされ、サービス・インスタンス、ストレージ・アカウント、およびプロジェクト・レベルでは使用できません。

<table>
  <tr>
    <th> 管理ユーザー (管理者) </th>
    <th> 非管理ユーザー (メンバー) </th>
  </tr>
  <tr>
    <td> アクセス制御を管理 </td>
    <td> デフォルトでは、サービスおよびコンテナーに対するアクセス権限がない </td>
  </tr>
  <tr>
    <td> コンテナーの作成および削除が可能 </td>
    <td> コンテナーの読み取り/書き込み ACL に基づいてアクションを実行可能 </td>
  </tr>
  <tr>
    <td> コンテナーの読み取りおよび書き込みが可能 </td>
    <td> 管理者の決定に従ってアクションを実行可能 </td>
  </tr>
</table>

表 2: 定義済みのユーザー役割

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェース、Cloud Foundry API、または Cloud Foundry CLI を使用して、{{site.data.keyword.objectstorageshort}} ユーザーを管理できます。




## 読み取り権限の付与 {: #read-access}

管理者の役割を持つ {{site.data.keyword.objectstorageshort}} ユーザーが、別のユーザーに対してコンテナーの読み取り権限を付与し、読み取り ACL の組み合わせを処理することができます。

<table>
  <tr>
    <th> 許可 </th>
    <th> 読み取り ACL オプション </th>
  </tr>
  <tr>
    <td> アカウントの加入に関係なくすべての参照者に対する読み取り</td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> すべての参照者に対する読み取りとリストおよびリスト作成 </td>
    <td> <code>.r:*,.rlistings</code> </td>
  </tr>
  <tr>
    <td> 特定のプロジェクトの指定されたユーザーに対する読み取りとリスト </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトの指定されたユーザーに対する読み取りとリスト </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> 指定されたプロジェクトのすべてのユーザーに対する読み取りとリスト</td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトのすべてのユーザーに対する読み取りとリスト</td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

表 3: オプション別の読み取りアクセス許可



1. 資格情報を認証します。UI のサービス資格情報タブにある資格情報を使用することも、資格情報を新規に生成することも可能です。新規資格情報の生成について詳しくは、[サービス資格情報の生成 (Generating service credentials)](insert link here) を参照してください。出力として、{{site.data.keyword.objectstorageshort}} URL と認証トークンを受け取ります。
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

    以下の出力例では、読み取り権限が付与されています。

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



## 書き込み権限の付与 {: #write-access}

管理者の役割を持つ {{site.data.keyword.objectstorageshort}} ユーザーが、別のユーザーに対してコンテナーの書き込み権限を付与し、書き込み ACL の組み合わせを処理することができます。

<table>
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
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> 指定されたプロジェクトのすべてのユーザーに対する書き込み</td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトのすべてのユーザーに対する書き込み</td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

表 4: オプション別の書き込みアクセス許可



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

2. 以下のコマンドを実行して、書き込み権限を付与します。
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

3. 書き込み ACL 値を検証します。Swift コマンド:

    ```
    swift stat <container_name>
    ```
    {: pre}

    cURL コマンド:

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}



## アクセス権限の削除 {: #removing-access}

コンテナーから読み取り ACL を削除するには、以下のようにします。
* Swift コマンド:

    ```
    swift post <container_name> --read-acl “”
    ```
    {: pre}

*  cURL コマンド:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

コンテナーから書き込み ACL を削除するには、以下のようにします。

* Swift コマンド:

    ```
    swift post <container_name> --write-acl “”
    ```
    {: pre}

*  cURL コマンド:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

ACL が削除されたことを確認するには、以下のようにします。

* Swift コマンド:

    ```
    swift stat <container_name>
    ```
    {: pre}

  以下の出力例では、読み取り ACL と書き込み ACL がブランクとして示されています。これは、アクセス権限が削除されたことを意味します。

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

* cURL コマンド:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
