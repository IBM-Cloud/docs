---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 一時 URL の作成 {: #create-temporary-url}

*最終更新日: 2016 年 10 月 19 日*
{: .last-updated}

一時 URL は、指定された期間、追加の認証を必要とせずにオブジェクトをダウンロードするために使用できる、推測が困難な長い URL です。
{: shortdesc}


1. 以下のコマンドでアカウント情報を出力して、認証情報を確認します。

    ```
swift stat
```
    {: pre}
    
    **注**: Account フィールドを見つけて、*Account* : の後ろの `AUTH_` を含むすべての文字列をメモします。
2. 秘密鍵を設定します。この鍵は自由に選択できますが、ベスト・プラクティスは、ランダムで推測が困難な長いストリングを選択することです。鍵を設定するには、以下のコマンドを実行します。

    ```
swift post -m "Temp-URL-Key:<key>"
```
    {: pre}
    
3. 以下のコマンドを実行して、`Temp-URL-Key` が正常に設定されたことを確認します。

    ```
swift stat
```
    {: pre}
    
4. 以下のコマンドを実行して、一時 URL を作成します。

    ```
swift tempurl GET <seconds> <path> <key>
```
    {: pre}
    
    以下の表に、Swift `tempurl` コマンドで使用する定位置引数を説明します。
    <table>
      <tr>
        <th> 引数 </th>
        <th> 説明 </th>
      </tr>
      <tr>
        <td> [method] </td>
        <td> ダウンロードを許可する場合は GET。アップロードを許可する場合は PUT。</td>
      </tr>
      <tr>
        <td> [seconds] </td>
        <td> 一時 URL が使用可能な時間 (秒数)。</td>
      </tr>
      <tr>
        <td> [path] </td>
        <td> オブジェクトの絶対パス (`/v1/<auth_account>/<container_name>/<object_name>` として表現)。詳しくは、[{{site.data.keyword.objectstorageshort}} URL の資料](/os_api.html#access-points)を参照してください。</td>
      </tr>
      <tr>
        <td> [key] </td>
        <td> ステップ 2 で設定した秘密鍵。</td>
      </tr>
    </table>
    *表 2: tempurl の定位置引数*
5. (*オプション* ): 返された URL をクラスター名に付加すると、完全な URL が得られます。その後、この完全な URL を使用して、互換性のある HTTP クライアント (cURL、wget、Firefox など) でオブジェクトをダウンロードできます。
