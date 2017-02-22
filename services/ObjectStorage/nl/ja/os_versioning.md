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


# オブジェクト・バージョン管理のセットアップ {: #setting-up-versioning}

オブジェクト・バージョン管理をセットアップすることによって、古いバージョンのオブジェクトを自動的に保持できます。バージョン管理を使用すると、各オブジェクトのヒストリーを確認できます。
{: shortdesc}

ファイルの新しいバージョンをメイン・コンテナーにアップロードすると、前のバージョンは自動的にバックアップ・コンテナーに移動されます。メイン・コンテナーからファイルを削除すると、最新バージョンが自動的にバックアップ・コンテナーからメイン・コンテナーに移動されて、削除されたファイルを置換します。

1. コンテナーを作成し、名前を付けます。変数 *container_name* を、コンテナーに付けたい名前に置換します。

    ```
  swift post <container_name>
  ```
    {: pre}

2. バックアップ・ストレージとして機能する 2 番目のコンテナーを作成し、名前を付けます。

    ```
    swift post <backup_container_name>
    ```
    {: pre}

3. バージョン管理をセットアップします。

    Swift コマンド:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}

    cURL コマンド:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. 初めてメイン・コンテナーにオブジェクトをアップロードします。

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

5. オブジェクトを変更します。

6. オブジェクトの新しいバージョンをメイン・コンテナーにアップロードします。

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

7.  バックアップ・コンテナー内のオブジェクトは、`<Length><Object_name>/<Timestamp>` のフォーマットで自動的に命名されます。
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
      <td> <i>Timestamp</i> </td>
      <td> オブジェクトの該当バージョンが最初にアップロードされたときのタイム・スタンプ。</td>
    </tr>
  </table>


6. メイン・コンテナー内のオブジェクトをリストして、ファイルの新しいバージョンを表示します。

    ```
    swift list --lh <container_name>
    ```
    {: pre}

7. バックアップ・コンテナー内のオブジェクトをリストします。このコンテナーに保管されている、ファイルの以前のバージョンが表示されます。タイム・スタンプがファイルに追加されることに注意してください。

    ```
    swift list --lh <backup_container_name>
    ```
    {: pre}

8. メイン・コンテナー内のオブジェクトを削除します。オブジェクトを削除すると、バックアップ・コンテナー内の最新バージョンがメイン・コンテナーに自動的に移動されます。

    ```
  swift delete <container_name>
  <object>
    ```
    {: pre}

9. オプション: オブジェクトのバージョン管理を使用不可にします。

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
