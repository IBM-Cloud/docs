---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Swift および Cloud Foundry のコマンドを使用するように CLI を構成

Swift または Cloud Foundry のコマンドを使用して {{site.data.keyword.objectstorageshort}} サービスと対話するには、前提ソフトウェアをインストールする必要があります。
{: shortdesc}


## Swift クライアントのインストール {: #install-swift-client}

以下の前提ソフトウェアをまだインストールしていない場合は、インストールしてください。
* Python 2.7 以降
* setuptools パッケージ
* pip パッケージ
* Cloud Foundry CLI


Python Swift クライアントをインストールするには、以下のコマンドを実行します。
```
pip install python-swiftclient
```
{: pre}

Python Keystone クライアントをインストールするには、以下のコマンドを実行します。
```
pip install python-keystoneclient
```
{: pre}

前提条件について詳しくは、[Openstack の資料](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}を参照してください。


## クライアントのセットアップ {: #setup-swift-client}

Swift クライアントを構成するには、認証情報を `export` する必要があります。[資格情報の生成](/docs/services/ObjectStorage/os_credentials.html)は、Cloud Foundry または cURL のコマンドを使用して CLI を介して行うか、{{site.data.keyword.Bluemix_notm}} UI を介して行うことができます。クライアントは、以下の表の環境変数から情報を取得します。

<table>
<caption> 表 1. 環境変数と説明</caption>
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
    <td> エンドポイント URL。必ず、URL の最後に <code>/v3</code> を追加してください。</td>
  </tr>
</table>



認証情報をエクスポートするには、資格情報を入力して、以下のコマンドを実行します。
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
    ```
{: codeblock}


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
{: screen}
