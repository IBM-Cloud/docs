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


# オブジェクト・バージョン管理のセットアップ {: #setting-up-versioning}

オブジェクト・バージョン管理をセットアップすることによって、 古いバージョンのオブジェクトを自動的に保持できます。バージョ
ン管理を使用すると、偶発的な上書きを防ぎ、前のバージョンのファイルを取り出すことができます。
{: shortdesc}


#### オブジェクト・バージョン管理の仕組み

オブジェクト・バージョン管理は、変更される可能性のあるオブジェクトをユーザーが保管するための手段です。バージョン管理を使用すると、作業コンテナーでは常に現行バージョンのオブジェクトが使用可能であり、前のバージョンはすべてアーカイブ・コンテナーにバックアップされます。

<dl>
  <dt>保管</dt>
    <dd>新規オブジェクトとは、初めて保管するオブジェクトです。このオブジェクトは、真新しいオブジェクトか、または 2 度目にアップロードする編集済みオブジェクトです。
</dd>
  <dt>アーカイブ</dt>
    <dd>バージョン管理を使用すると、既存のオブジェクトと同じ名前のオブジェクトが作業コンテナーに保存される場合、古い方のオブジェクトはアーカイブ・コンテナーに移動されます。オブジェクトの名前にタイム・スタンプが追加されます。</dd>
  <dt>リストア</dt>
    <dd>作業コンテナーからオブジェクトが削除され、そのオブジェクトのアーカイブ済みバージョンが存在する場合、アーカイブ済みバージョンがリストアされます。アーカイブ済みオブジェクトは、いつでもリストアできます。
</dd>
</dl>

![オブジェクト・バージョン管理の概要](images/os_versioning.png)

図 1. オブジェクト・バージョン管理の概要


#### チュートリアル

オブジェクト・バージョン管理を理解するには、以下のチュートリアルを完了してください。

1. コンテナーを作成し、名前を付けます。変数 *container_name* を、コンテナーに付けたい名前に置換します。

    ```
  swift post <container_name>
  ```
    {: pre}

2. バックアップ・ストレージとして機能する 2 番目のコンテナーを作成し、名前を付けます。

    ```
    swift post <archive_container_name>
    ```
    {: pre}

3. バージョン管理をセットアップします。

    Swift コマンド:

    ```
    swift post <container_name> -H "X-Versions-Location: <archive_container_name>"
    ```
    {: pre}

    cURL コマンド:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<archive_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. 初めて作業コンテナーにオブジェクトをアップロードします。

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

5. オブジェクトを編集し、その新しいバージョンを作業コンテナーにアップロードします。

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

6.  アーカイブ・コンテナー内のオブジェクトには、形式で自動的に名前が付けられます。`<Length><Object_name>/<time stamp>`
    <table>
    <caption> 表 1. 命名属性の説明</caption>
      <tr>
        <th> 属性 </th>
        <th> 説明 </th>
      </tr>
      <tr>
        <td> <i>Length</i> </td>
        <td> オブジェクトの名前の長さ。これは、3 文字のゼロ埋め込み 16 進数です。</td>
      </tr>
      <tr>
        <td> <i>Object_name</i> </td>
        <td> オブジェクトの名前。</td>
      </tr>
      <tr>
        <td> <i> time stamp </i> </td>
        <td> そのバージョンのオブジェクトが最初にアップロードされたときのタイム・スタンプ。</td>
      </tr>
    </table>

7. 作業コンテナー内のオブジェクトをリストして、新規バージョンのファイルを確認します。

    ```
    swift list --lh <container_name>
    ```
    {: pre}

8. アーカイブ・コンテナー内のオブジェクトをリストして、タイム・スタンプが追加された前のバージョンのファイルを確認します。

    ```
    swift list --lh <backup_container_name>
    ```
    {: pre}

9. 作業コンテナー内のオブジェクトを削除します。アーカイブ・コンテナー内の最新バージョンが自動的に作業コンテナーにリストアされます。

    **注**: オブジェクトを削除するには、すべてのバージョンのファイルを削除する必要があります。

    ```
  swift delete <container_name>
  <object>
    ```
    {: pre}

10. オプション: オブジェクトのバージョン管理を使用不可にします。

    Swift コマンド:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

    cURL コマンド:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}
