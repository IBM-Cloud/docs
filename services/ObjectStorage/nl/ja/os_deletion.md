---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# オブジェクトの削除のスケジューリング {: #schedule-object-deletion}
*最終更新日: 2016 年 10 月 19 日*
{: .last-updated}

オブジェクトの削除をスケジュールすることができます。これを行うには、`X-Delete-At` ヘッダーまたは `X-Delete-After` ヘッダーのどちらかを使用します。
{: shortdesc}

`X-Delete-At` ヘッダーは、オブジェクトを削除するエポック時刻を表す整数値です。`X-Delete_After` ヘッダーは、オブジェクトが削除されるまでに経過する秒数を表す整数値です。
swift クライアントを使用してオブジェクト削除をスケジュールするには、以下のうちニーズに最適なコマンドを実行します。

* 特定日時にオブジェクトを削除するように設定するには、次のコマンドを実行します。
    
    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}
    
    例:
    
    「2016/04/01 08:00:00」にオブジェクトを削除するように設定するには、次のコマンドを実行します。
    
    ```
    swift post -H "X-Delete-At:1459515600" <container_name> <object_name>
    ```
    {: screen}
* 今から 1 時間後にオブジェクトを削除するように設定するには、次のコマンドを使用します。
    
    ```
    swift post -H "X-Delete-After:<number_of_seconds" <container_name> <object_name>
    ```
    {: pre}
    
    例:
    
    今から 1 時間後にオブジェクトを削除するように設定するには、次のコマンドを実行します。
    
    ```
swift post -H "X-Delete-After:3600" container object
```
    {: screen}
* オブジェクトから有効期限を削除するには、次のコマンドを使用します。
    
    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" container object
    ```
    {: pre}

cURL コマンドを使用してオブジェクト削除をスケジュールするには、以下のうちニーズに最適なコマンドを実行します。時間の規格は、Swift クライアントと同じです。

* 「2016/04/01 08:00:00」にオブジェクトを削除するように設定するには、次のコマンドを使用します。
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name/<object_name>
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

**注:** オブジェクトの実際の削除は、指示された正確な時刻に行われるとは限りません。ただし、オブジェクトは実際に指定の時刻に期限切れになります。つまり、それ以降は到達不能になります。実際の削除は、Swift クラスターに構成されている swift-object-expirer デーモンの次回の実行時に行われます。

