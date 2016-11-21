---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
# {{site.data.keyword.objectstorageshort}} の使用開始 {: #using-object-storage}
*最終更新日: 2016 年 10 月 19 日*
{: .last-updated}

# Swift CLI を使用した {{site.data.keyword.objectstorageshort}} へのアクセス {: #using-swift-cli}


{{site.data.keyword.objectstorageshort}} サービスは OpenStack Swift に基づいており、互換性のある任意のクライアント・アプリケーションを使用してアクセスできます。このセクションでは、Python Swift クライアント ({{site.data.keyword.objectstorageshort}} API のコマンド・ライン・インターフェース (CLI) とその拡張機能) を使用してコンテナーおよびファイルを処理する方法について説明します。
{: shortdesc}

## Swift クライアントのインストール {: #install-swift-client}

以下の [前提ソフトウェア](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}をまだインストールしていなければ、インストールします。
* Python 2.7 以降
* setuptools パッケージ
* pip パッケージ

Python Swift クライアントをインストールするには、以下のコマンドを実行します。
  ```
sudo pip install python-swiftclient
```
  {: pre}

Python Keystone クライアントをインストールするには、以下のコマンドを実行します。
  ```
sudo pip install python-keystoneclient
```
  {: pre}




## クライアントのセットアップ {: #setup-swift-client}

Swift クライアントをセットアップするには、認証情報の `export` が必要です。UI に示された資格情報を使用するか、[資格情報を新規に生成する](../ObjectStorage/os_cli.html#generating-cli)ことができます。

例:
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




## {{site.data.keyword.objectstorageshort}} サービス資格情報の生成 {: #generating-cli}

Swift CLI を使用してサービス資格情報を生成するには、以下の手順を使用します。

1. 開発者の役割を持つユーザーとして、{{site.data.keyword.Bluemix_notm}} にログインします。ユーザーは管理対象のサービス・インスタンスのスペース内にいる必要があります。
      ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
      {: pre}
2. サービス資格情報を生成します。`service-key-name` は、資格情報に付ける名前です。Cloud Foundry コマンドまたは cURL コマンドのいずれかを使用できます。Cloud Foundry コマンド:
      ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```
      {: pre}
      Cloud Foundry コマンドの例:
      ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
      {: screen}
  cURL コマンド:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```
      {: pre}
3. 作成したサービス・キーの資格情報を検証します。
      Cloud Foundry コマンド:
      ```
  cf service-key <service_key_name> <member_name>
  ```
      {: pre}
      インスタンス Object-Storage-Acl-Test のメンバー・サービス・キーの例:
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
  cURL コマンド:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
      {: pre}




## CLI によるコンテナーへのオブジェクトの保管 {: #storing-cli}

1. {{site.data.keyword.Bluemix_notm}} にログインします。{{site.data.keyword.objectstorageshort}} のインスタンスで作業するために適切な組織およびスペースを必ず使用してください。
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 以下のコマンドを実行して、新しいコンテナーを作成します。*container_name* 変数をこの時点で設定します。
    ```
swift post <container_name>
```
    {: pre}
3. (*オプション* ) コンテナーが作成されたことを確認するために、以下のコマンドを実行してコンテナーをリストします。
    ```
swift list
```
    {: pre}
4. 以下のコマンドを実行して、ファイルをコンテナーにアップロードします。
    ```
swift upload <container_name> <file_name>
```
    {: pre}
    **注**: 5 GB を超えるファイルをアップロードする場合には、追加の手順が必要です。詳しくは、[ラージ・ファイルの操作](../ObjectStorage/os_large_files.html#large-files)を参照してください。
5. (*オプション* ) アップロードが成功したことを確認するために、以下のコマンドを実行してコンテナーの内容を表示します。
    ```
swift list <container_name>
```
    {: pre}

**注**: 同じ名前でファイルをアップロードすると、保管されているファイルが {{site.data.keyword.objectstorageshort}} によって新しいファイルに置き換えられます。ファイルをダウンロードして編集する場合は、必ず、ファイルに別の名前を付けるか、またはアップロードの前に[オブジェクト・バージョン管理をセットアップ](../ObjectStorage/os_versioning.html#work-with-object-versioning)して、両方のバージョンのファイルを保持してください。



## Swift CLI によるオブジェクトのダウンロード {: #downloading-cli}

1.  {{site.data.keyword.Bluemix_notm}} にログインします。{{site.data.keyword.objectstorageshort}} のインスタンスで作業するために適切な組織およびスペースを必ず使用してください。
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 以下のコマンドを実行して、ファイルをダウンロードします。
    ```
swift download <container_name> <file_name>
```
    {: pre}




## CLI によるオブジェクトおよびコンテナーの削除 {: #deleting-cli}

1.  {{site.data.keyword.Bluemix_notm}} にログインします。{{site.data.keyword.objectstorageshort}} のインスタンスで作業するために適切な組織およびスペースを必ず使用してください。
    ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
    {: pre}
2. 以下のコマンドを実行して、ファイルを削除します。
    ```
swift delete <container_name> <file_name>
```
    {: pre}
    **注**: [オブジェクトを削除する特定時刻](../ObjectStorage/os_deletion.html#schedule-object-deletion)をスケジュールすることができます。
3. コンテナーを削除するために、以下のコマンドを実行します。
    ```
    swift delete <container_name>
    ```
    {: pre}
    **注意**: コンテナーを削除すると、そのコンテナーに保管されたすべてのオブジェクトが削除されます。





## ディレクトリーの処理 {: #directory-cli}

#### Swift CLI によるコンテナーへのディレクトリーの追加

Swift には本当のディレクトリー構造はありませんが、ディレクトリー・レイアウトを表す命名法が使用されています。ディレクトリー名を指定すると、相対パスの一部としてすべてのファイル名にそれが加えられます。

1. 以下のコマンドを実行して、ディレクトリーをコンテナーに追加します。
    ```
swift upload <container_name> <directory_name>
```
    {: pre}

#### ディレクトリーのダウンロード
ディレクトリー構造をダウンロードするには、`-prefix` パラメーターを使用して、ダウンロードするディレクトリーまたはディレクトリー構造を示します。

1. 以下のコマンドを実行して、ディレクトリーをダウンロードします。
    ```
swift download <container_name> --prefix <directory>
```
    {: pre}
