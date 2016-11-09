---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# オブジェクトのバージョン管理の処理 {: #work-with-object-versioning}

*最終更新日: 2016 年 10 月 19 日*
{: .last-updated}

オブジェクト・バージョン管理を使用して、ファイル名を変更せずに、オブジェクトの異なるバージョンを保持することができます。これにより、各オブジェクトの履歴を表示して、いつ変更が行われたかを追跡することができます。
{: shortdesc}


### オブジェクト・バージョン管理のセットアップ{: #setting-up-versioning}

`X-Versions-Location` パラメーターを使用して、コンテナーに各オブジェクトの複数バージョンをセットアップすることができます。これを行うには、以下のように、オブジェクトの古いバージョンを保存するための追加コンテナーを作成します。

オブジェクト・バージョン管理をセットアップするには、Swift クライアントまたは cURL コマンドを使用できます。
* Swift クライアントを使用する場合は、以下のコマンドを実行します。

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}
    
* cURL を使用する場合は、次のようにセットアップします。

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}
    
**注**: バックアップ・コンテナー内のオブジェクトには、`<Length><Object_name>/<Timestamp>` というフォーマットで自動的に名前が付けられます。
<table>
  <tr>
    <th> 属性 </th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td> `Length` </td>
    <td> オブジェクトの名前の長さ。これは、3 文字のゼロ埋め込み 16 進数です。</td>
  </tr>
  <tr>
    <td> `Object_name` </td>
    <td> オブジェクトの名前。</td>
  </tr>
  <tr>
    <td> `Timestamp` </td>
    <td> オブジェクトの該当バージョンが最初にアップロードされたときのタイム・スタンプ。</td>
  </tr>
</table>

### オブジェクト・バージョン管理の無効化 {: #disabling-versioning}

オブジェクト・バージョン管理を無効にするには、Swift クライアントまたは cURL コマンドを使用できます。

* Swift クライアントを使用する場合は、以下のコマンドを実行します。

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* 以下の cURL コマンドを実行して、バージョン管理を無効にします。

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}


### オブジェクト・バージョン管理のチュートリアル {: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

以下のチュートリアルを利用して、オブジェクト・バージョン管理の全ライフサイクルを把握することができます。

1. `container_one` という名前のコンテナーを作成します。

    ```
    swift post container_one
    ```
    {: pre}
    
3. `container_two` という名前で 2 つ目のコンテナーを作成します。

    ```
    swift post container_two
    ```
    {: pre}
    
2. バージョン管理をセットアップします。

    ```
swift post container_one -H "X-Versions-Location:container_two"
```
    {: pre}
    
4. 初めてメイン・コンテナーにオブジェクトをアップロードします。

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. オブジェクトの新しいバージョンを container_one にアップロードします。ファイルの新しいバージョンをアップロードすると、バージョン管理のセットアップで指定したバックアップ・コンテナーに、前のバージョンが自動的に移動されます。

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. コンテナー内のファイルの新しいバージョンを確認するために、container_one 内のオブジェクトをリストします。

    ```
    swift list container_one
    ```
    {: pre}
    
9. container_two 内のオブジェクトをリストします。ファイルの以前のバージョンがこのコンテナーに保管されることが分かります。

    ```
    swift list container_two
    ```
    {: pre}
    
10. container_one 内のオブジェクトを削除します。オブジェクトを削除すると、バックアップ・コンテナー内の前のバージョンが、メイン・コンテナーに自動的に移動されます。

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. 両方のコンテナーをリストします。元のファイルが `container_one` にあり、`container_two` は空になります。

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
