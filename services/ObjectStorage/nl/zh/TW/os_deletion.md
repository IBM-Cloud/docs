---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 排定物件刪除 {: #schedule-object-deletion}
*前次更新：2016 年 10 月 19 日*
{: .last-updated}

您可以排定物件刪除。若要這樣做，您可以利用 `X-Delete-At` 或 `X-Delete-After` 標頭。
{: shortdesc}

`X-Delete-At` 標頭會接受一個代表新紀元時間的整數，將會在該時間刪除物件。`X-Delete_After` 標頭會接受一個代表秒數的整數，在該秒數之後將會刪除物件。若要使用 Swift 用戶端排定物件刪除，請執行下列最符合您需求的指令。

* 若要設定在特定日期和時間刪除物件，請執行下列指令：
    
    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}
    
    範例：
    
    若要設定在 "2016/04/01 08:00:00" 刪除物件，請執行下列指令：
    
    ```
    swift post -H "X-Delete-At:1459515600" <container_name> <object_name>
    ```
    {: screen}
* 若要設定將在現在起的一小時後刪除物件，請使用下列指令：
    
    ```
    swift post -H "X-Delete-After:<number_of_seconds" <container_name> <object_name>
    ```
    {: pre}
    
    範例：
    
    若要設定將在現在起的一小時後刪除物件，請執行下列指令：
    
    ```
    swift post -H "X-Delete-After:3600" container object
    ```
    {: screen}
* 若要移除物件的有效期限，請使用下列指令：
    
    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" container object
    ```
    {: pre}

若要使用 cURL 指令進行已排定物件刪除，您可以執行下列最符合您需求的指令。時間的標準與 Swift 用戶端相同。

* 若要設定將在 "2016/04/01 08:00:00" 刪除物件，請使用下列指令：
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name/<object_name>
    ```
    {: pre}
    
* 若要設定將在現在起的一小時後刪除物件，請使用下列指令：
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* 若要檢查物件是否有標頭，請使用下列指令：
    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* 若要移除有效期限，請使用下列指令：
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

**附註：**物件實際刪除可能不會按照指出的確切時間發生。不過，物件實際上會在指定的時間到期。這表示無法再呼叫到它。實際的刪除將在 Swift 叢集中配置的 swift-object-expirer 常駐程式下次執行時發生。
