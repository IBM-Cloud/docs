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


# ラージ・オブジェクトの保管 {: #large-files}

アップロードは、1 回のアップロードにつき最大サイズ 5 GB に制限されています。ただし、ラージ・オブジェクトは小さい断片にセグメント化し、マニフェスト・ファイルを使用してそれらのセグメントを連結することができます。連結後のオブジェクトには最大サイズはありません。
{: shortdesc}

ラージ・オブジェクトは動的または静的のいずれかです。静的ラージ・オブジェクト (SLO) では、セグメントが同じコンテナー内に存在する必要はありません。各セグメントを任意のコンテナーに保管し、任意の名前を付けることができます。動的ラージ・オブジェクトでは、Swift クライアントがコンテナーを作成し、番号付けられたセグメントが並行してコンテナーにアップロードされます。


## 動的ラージ・オブジェクト: {: #dynamic}

動的ラージ・オブジェクトは次の 2 とおりの方法でアップロードできます。
  * Swift クライアントですべてを自動的に処理する
  * Swift API を使用して自分で行う

#### Swift クライアントを使用して動的ラージ・オブジェクトを処理する

Swift クライアントは、`-segment-size` パラメーターを使用して、オブジェクトを小さな断片に分割します。クライアントは、ファイルのアップロード先コンテナーの名前で新しいコンテナーを作成し、セグメント番号を含む接尾部を追加します (`<container_name>_segments`)。セグメントは並行してアップロードされます。
すべてのセグメントがアップロードされた後、それらは、
マニフェスト・ファイルに従って連結された 1 つのオブジェクトとして元のファイル名でダウンロードされます。

1. {{site.data.keyword.Bluemix_notm}} にログインしてアップロードの準備ができたら、以下のコマンドを実行してファイルをセグメント化します。
    ```
    swift upload <container_name> <file_name> --segment-size <size_in_bytes>
    ```
    {: pre}

#### Swift API を使用して動的ラージ・オブジェクトを処理する

5 GB 以下になるようにオブジェクトを自分でセグメント化し、次に Swift API を使用してそれらをアップロードすることができます。

**注**: アップロード時には、すべてのセグメントがマニフェスト・ファイルよりも前にアップロードされる必要があります。すべてのセグメントがアップロードされる前にオブジェクトがダウンロードされると、ダウンロードされたオブジェクトの連結は不整合になります。

ラージ・ファイルをアップロードするには、以下の手順を行います。

1. セグメントを名前でソートします (元のオブジェクトを形成するには、この順序で連結する必要があります)。
2. マニフェスト・ファイルが入ったコンテナーとは別のコンテナーに、セグメントをアップロードします。10 個目のセグメントがアップロードされた後、アップロードの減速が始まり、アップロード時間が著しく増大します。  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000002
    ```
    {: pre}

3. ヘッダー `X-Object-Manifest` に対応する `<container>/prefix>` 値を設定して、空のマニフェスト・ファイルをアップロードします。

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Object-Manifest: <container_name>/<object_name>/" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}

    **注**: マニフェスト・ファイルは空である必要があります。そうでないと、ファイルの内容がセグメントの 1 つと見なされ、ソートされた名前で指示される連結順序に入ります。
4. オブジェクトをダウンロードします。結果として、オブジェクト全体を受け取ります。セグメントを追加または削除する場合、マニフェスト・ファイルを更新する必要はありません。正しい接頭部を持つセグメントは、オブジェクトの一部としてそのまま残ります。マニフェストを削除しても、セグメントは削除されません。

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


## 静的ラージ・オブジェクト{: #static}

静的ラージ・オブジェクトはセグメントとマニフェスト・ファイルを使用しますが、詳細な制御が可能です。SLO では、セグメントが同じコンテナー内に存在する必要はありません。各セグメントを任意のコンテナーに保管し、任意の名前を付けることができます。ただし、セグメントは少なくとも 1 MB でなければなりません。マニフェスト・ファイルのヘッダーを設定する必要はありませんが、正しいマニフェストがアップロードされた後、ヘッダー“X-Static-Large-Object”が自動的に追加されて true に設定されます。
{: shortdesc}

マニフェスト・ファイルは、セグメントの詳細を示す JSON 文書で、すべてのセグメントをアップロードした後に、アップロードされなければなりません。マニフェスト内で各セグメントについて提供されるデータが、実際のセグメントのメタデータと比較されます。一致しないものがあると、マニフェストはアップロードされません。

<table>
<caption> 表 1. マニフェスト・ファイル内の JSON 属性</caption>
  <tr>
    <th> 属性 </th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td> <i> path </i> </td>
    <td> セグメントの場所および名前。container_name/object_name として指定されます。</td>
  </tr>
  <tr>
    <td> <i> etag </i> </td>
    <td> オブジェクトのアップロード時に PUT 要求によって提供されます。これは、オブジェクトに HEAD を実行することでも、入手できます。</td>
  </tr>
  <tr>
    <td> <i> size_bytes </i> </td>
    <td> オブジェクトのサイズ (バイト数)。</td>
  </tr>
</table>



#### ラージ・ファイルのアップロード方法

1. 以下のコマンドを実行して、セグメントをアップロードします。10 個目のセグメントがアップロードされた後、アップロードの減速が始まり、アップロード時間が著しく増大します。  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    ```
    {: pre}

2. マニフェストを作成します。

    ```
    [
        {
            "path": "<container_one>/<segment>",
            "etag": "e0ed3b751eb8d4b2c648d2dd78576e36",
            "size_bytes": 801882690
        },
        {
            "path": "container_two/<segment>",
            "etag": "65a301e71c82cbd325a5efe5877e1a24",
            "size_bytes": 1048576
        },
        {
            "path": "<container_one>/<segment>",
            "etag": "aea8b7462d527ad5ed0cfc22ea161062",
            "size_bytes": 138257
        }
    ]
    ```
    {: pre}

3. マニフェストの名前に照会 `multipart-manifest=put` を追加することによって、マニフェスト・ファイルをアップロードします。

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}

4. オブジェクトをダウンロードします。

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}


#### 静的ラージ・オブジェクトの処理

以下のコマンドを使用してファイルを管理できます。

**注**: オブジェクトに対してセグメントを追加または削除するには、新しいセグメント・リストを含む新しいマニフェスト・ファイルをアップロードします。マニフェスト名は同じままにすることができます。

* マニフェスト・ファイルの内容をダウンロードするには、コマンドに照会 `multipart-manifest=get` を追加する必要があります。受け取る内容は、アップロードした内容と同じではありません。

    ```
    curl -O -X GET -H "X-Auth-Token:<token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=get
    ```
    {: pre}

* マニフェストを削除するには、以下のコマンドを実行します。

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}

* マニフェストとすべてのセグメントを削除するには、マニフェストの名前の後に照会 `multipart-manifest=delete` を追加します。

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=delete
    ```
    {: pre}
