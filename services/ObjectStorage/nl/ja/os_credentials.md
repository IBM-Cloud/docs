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


# サービス資格情報の生成 {: #credentials}

サービス資格情報は、サービスの認証およびセキュリティーを提供するために使用されます。CLI または {{site.data.keyword.Bluemix_notm}} UI を使用して、新しい資格情報を生成することができます。
{: shortdesc}


## UI で資格情報を追加する方法

1. サービス・インスタンス・ダッシュボードの**「サービス資格情報」**タブで、**「新規資格情報 (New Credential)」**をクリックして、名前を指定します。
2. オプション: **「インライン構成パラメーターの追加」**テキスト・フィールドに、付与したい[アクセスのタイプ](/docs/services/ObjectStorage/os_access_types.html)を持つ役割の資格情報情報を入力します。この情報は、JSON ペイロードとしてフォーマット設定する必要があります。
    - 管理ユーザーを作成する場合: `{"role":"admin"}`
    - 非管理ユーザーを作成する場合: `{"role":"member"}`
3. **「追加」**をクリックします。


## CLI で Cloud Foundry コマンドを使用して資格情報を追加する方法

1. {{site.data.keyword.Bluemix_notm}} にログインしていない場合は、開発者の役割を持つユーザーとしてログインします。ユーザーは管理対象のサービス・インスタンスのスペース内にいる必要があります。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. サービス資格情報を生成します。変数 `service-key-name` を置換して、資格情報に名前を付けます。オプションで、[ユーザー役割](/docs/services/ObjectStorage/os_access_types.html)も割り当てることができます。

  ```
  cf create-service-key "<service_instance_name>" <service-key-name> -c '{"role":"<user_role>"}'
  ```
  {: pre}

  例:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. 作成したキーの資格情報を検証します。

  ```
  cf service-keys <service_instance_name>
  ```
  {: pre}

  メンバーの役割を持つユーザーに対する、Object-Storage-Acl-Test という名前のインスタンスのサンプル・キー

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



#### CLI で cURL コマンドを使用して資格情報を追加する方法

1. {{site.data.keyword.Bluemix_notm}} にログインしていない場合は、開発者の役割を持つユーザーとしてログインします。ユーザーは管理対象のサービス・インスタンスのスペース内にいる必要があります。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 以下のコマンドを実行して、サービス資格情報を生成します。

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name: <service_instance_name>", "role: <user_role>"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: <content_type" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> 表 1. cURL サービス資格情報変数の説明</caption>
    <tr>
      <th> 変数  </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <code>https://api.ng.bluemix.net/v2/service_keys</code> </td>
      <td> サービス・キーのエンドポイント。</td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> ご使用の URL に含まれています。</td>
    </tr>
    <tr>
      <td><i> name </i></td>
      <td> サービス・インスタンスの名前。</td>
    </tr>
    <tr>
      <td><i> role </i></td>
      <td> <a href= /docs/services/ObjectStorage/os_constructing.html>ユーザーの役割</a>を、管理者またはメンバーとして指定します。</td>
    </tr>
    <tr>
      <td><i> bearer_token </i></td>
      <td> Keystone を使用してインスタンスを認証した時に受け取ったトークン。</td>
    </tr>
  </table>



3. 以下のコマンドを実行して資格情報を検証します。

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: screen}
