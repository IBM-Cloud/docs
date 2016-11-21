---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 安排对象删除 {: #schedule-object-deletion}
*上次更新时间：2016 年 10 月 19 日*
{: .last-updated}

您可以安排删除对象。通过使用 `X-Delete-At` 或 `X-Delete-After` 标头，可以完成此操作。
{: shortdesc}

`X-Delete-At` 标头采用整数代表删除对象的戳记时间。`X-Delete_After` 标头采用整数代表在该秒数之后删除对象。要使用 Swift 客户机来安排对象删除，请运行以下命令中最适合您需求的命令。

* 要将对象设置为在特定日期和时间被删除，请运行以下命令：
    
    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}
    
    示例：
    
    要将对象设置为在“2016/04/01 08:00:00”被删除，请运行以下命令：
    
    ```
    swift post -H "X-Delete-At:1459515600" <container_name> <object_name>
    ```
    {: screen}
* 要将对象设置为在此后一小时删除，请使用以下命令：
    
    ```
    swift post -H "X-Delete-After:<number_of_seconds" <container_name> <object_name>
    ```
    {: pre}
    
    示例：
    
    要将对象设置为在此后一小时被删除，请运行以下命令：
    
    ```
swift post -H "X-Delete-After:3600" container object
```
    {: screen}
* 要从对象除去到期时间，请使用以下命令：
    
    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" container object
    ```
    {: pre}

要使用 cURL 命令来安排对象删除，可以运行以下命令中最适合您需求的命令。时间标准与 Swift 客户机相同。

* 要将对象设置为在“2016/04/01 08:00:00”删除，请使用以下命令：
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name/<object_name>
    ```
    {: pre}
    
* 要将对象设置为在此后一小时删除，请使用以下命令：
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* 要检查对象是否有标头，请使用以下命令：
    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* 要除去到期时间，请使用以下命令：
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

**注：**对象的实际删除可能不会在所指示的确切时间发生。但事实上，对象会在指定的时间到期。这表示将无法再使用该对象。实际删除操作将会在下一次 Swift 集群中配置的 swift-object-expirer 守护程序运行时发生。
