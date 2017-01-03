---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# オブジェクト・バージョン管理のセットアップ {: #setting-up-versioning}

オブジェクト・バージョン管理を使用すると、オブジェクトの古いバージョンをバックアップ・コンテナー内に自動的に保管することにより、それらを保持することができます。バージョン管理により、各オブジェクトの履歴を表示し、いつ変更が行われたかを追跡することができます。
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

  表 1: 命名属性の説明

6. メイン・コンテナー内のオブジェクトをリストして、ファイルの新しいバージョンを表示します。

    ```
    swift list --lh <container_name>
    ```
    {: pre}

7. バックアップ・コンテナー内のオブジェクトをリストします。このコンテナーに保管されている、ファイルの以前のバージョンが表示されます。タイム・スタンプがファイルに追加されていることに留意してください。

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
