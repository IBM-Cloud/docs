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


# 一時 URL の作成 {: #create-temporary-url}

一時 URL は、指定された期間、追加の認証を必要とすることも、ストレージ・アカウントに全アクセス権限を付与することもなく、オブジェクトをダウンロードするために使用できる、推測の難しい長い URL です。
{: shortdesc}


1. 以下のコマンドでアカウント情報を出力して、認証情報を確認します。

  ```
swift stat
```
  {: pre}
  **注**: `AUTH_` を含め、*Account* の後のフル・ストリングをメモします。

2. 秘密鍵を設定します。推測の難しいランダムな長いストリングを選択してください。鍵を設定するには、以下のコマンドを実行します。

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

  以下の表で、Swift `tempurl` コマンドで使用する位置引数について説明します。
  <table>
  <caption> 表 1. 一時 URL の位置引数</caption>
    <tr>
      <th> 引数 </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> method </i> </td>
      <td> ダウンロードを許可する場合は GET。アップロードを許可する場合は PUT。</td>
    </tr>
    <tr>
      <td> <i> seconds </i> </td>
      <td> 一時 URL が使用可能な時間 (秒数で示す)。</td>
    </tr>
    <tr>
      <td> <i> path </i> </td>
      <td> オブジェクトの絶対パス (<code>/v1/<i>auth_account</i>/<i>container_name</i>/<i>object_name</i></code> で示す)。</td>
    </tr>
    <tr>
      <td> <i> key </i> </td>
      <td> ステップ 2 で設定した秘密鍵。</td>
    </tr>
  </table>

5. オプション: 返された URL をクラスター名に付加して、完全な URL を取得します。その後、この完全な URL を使用して、互換性のある HTTP クライアント (cURL、wget、Firefox など) でオブジェクトをダウンロードできます。
