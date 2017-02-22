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


# オブジェクトの削除

オブジェクトおよびコンテナーがもう必要なくなったら、それらをストレージ・インスタンスから削除することができます。削除は手動で行うことも、オブジェクトの有効期限が切れる[時間をスケジュール](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion)に入れることもできます。
{: shortdesc}

**注**: コンテナーを削除すると、そのコンテナー内に保管されているすべてのオブジェクトが削除されます。


## UI を使用したオブジェクトおよびコンテナーの削除 {: #deleting-ui}

1. サービス・インスタンス・ダッシュボードで、もう必要ないファイルを含むコンテナーを選択します。
2. **「アクション」**ドロップダウン・メニューから**「ファイルの削除」**を選択します。
3. もうコンテナーを使用しない場合は、**「アクション」**ドロップダウン・メニューから**「コンテナーの削除」**を選択します。



## CLI によるオブジェクトおよびコンテナーの削除 {: #deleting-cli}

1.  {{site.data.keyword.Bluemix_notm}} にログインしていない場合は、{{site.data.keyword.objectstorageshort}} のインスタンスを含む組織およびスペースにログインします。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. オプション: ファイルおよびコンテナーを削除する前に、オブジェクトのバックアップを取ってあることを確認します。

3. 以下のコマンドを実行して、ファイルを削除します。
  ```
  swift delete <container_name> <file_name>
  ```
  {: pre}

4. コンテナーを削除するために、以下のコマンドを実行します。
  ```
  swift delete <container_name>
  ```
  {: pre}



## オブジェクトの削除のスケジューリング {: #schedule-object-deletion}


`X-Delete-At` ヘッダーまたは `X-Delete-After` ヘッダーを使用して、オブジェクトの削除をスケジュールすることができます。
{: shortdesc}

`X-Delete-At` ヘッダーでは、オブジェクトの削除が行われるエポック時刻を表す整数が指定されます。`X-Delete_After` ヘッダーでは、オブジェクトが削除されるまでの秒数を表す整数が指定されます。

**注:** オブジェクトの実際の削除は、指示された正確な時刻に行われるとは限りません。ただし、オブジェクトは実際に指定の時刻に期限切れになります。その時点で、オブジェクトは到達可能ではなくなります。実際の削除は、Swift クラスターに構成されている swift-object-expirer デーモンの次回の実行時に行われます。

#### Swift コマンドの使用方法

* 特定日時にオブジェクトを削除するように設定するには、次のコマンドを実行します。

    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}

    例: 「2016/04/01 08:00:00」にオブジェクトを削除するように設定するには、以下のコマンドを実行します。

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* 特定の時間後にオブジェクトを削除するように設定するには、以下のコマンドを使用します。

    ```
    swift post -H "X-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}

    例: 今から 1 時間後にオブジェクトを削除するように設定するには、以下のコマンドを実行します。

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* オブジェクトから有効期限を削除するには、次のコマンドを使用します。

    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}



#### cURL コマンドの使用方法

* 「2016/04/01 08:00:00」にオブジェクトを削除するように設定するには、次のコマンドを使用します。

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 今から 1 時間後にオブジェクトを削除するように設定するには、次のコマンドを使用します。

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* オブジェクトにヘッダーが付いているかどうかを確認するには、次のコマンドを使用します。

    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 有効期限を削除するには、次のコマンドを使用します。

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
