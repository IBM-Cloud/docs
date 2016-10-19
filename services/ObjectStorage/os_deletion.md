---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Scheduling object deletion {: #schedule-object-deletion}
*Last updated: 19 October 2016*
{: .last-updated}

You can schedule the deletion of your objects. You can do this by making use of either of the `X-Delete-At` or `X-Delete-After` headers.
{: shortdesc}

The `X-Delete-At` header takes an integer number representing the epoch time at which to delete the object. The `X-Delete_After` header takes an integer number representing the number of seconds after which the object will be deleted. To use the swift client to schedule object deletion run the following command that best fits your need.

* To set the object to be deleted at a specific date and time, run the following command:
    
    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}
    
    Example:
    To set the object to be deleted on "2016/04/01 08:00:00", you would run the following command:
    
    ```
    swift post -H "X-Delete-At:1459515600" <container_name> <object_name>
    ```
    {: screen}
* To set the object to be deleted an hour from now, use the following command:
    
    ```
    swift post -H "X-Delete-After:<number_of_seconds" <container_name> <object_name>
    ```
    {: pre}
    
    Example:
    To set the object to be deleted an hour from now, you would run the following command:
    
    ```
    swift post -H "X-Delete-After:3600" container object
    ```
    {: screen}
* To remove the expiration time from your object, use the following command:
    
    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" container object
    ```
    {: pre}

To use cURL commands for scheduled object deletion you can run the following command that best fits your need. The standards for time are the same as the Swift client.

* To set the object to be deleted on "2016/04/01 08:00:00", use the following command:
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name/<object_name>
    ```
    {: pre}
    
* To set the object to be deleted an hour from now, use the following command:
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* To check if the object has the header, use the following command:
    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
    
* To remove the expiration time, use the following command:
    
    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

**Note:** The actual deletion of an object might not happen at the exact time indicated. However, the object will in fact expire at the specified time. This means that it will no longer be reachable. The actual deletion will take place the next time the swift-object-expirer daemon configured in your Swift cluster runs.
