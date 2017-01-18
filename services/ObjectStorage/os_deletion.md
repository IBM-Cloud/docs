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


# Deleting objects

After you no longer have a need for them, you can delete objects and containers from your storage instance. You can manually do the delete, or you can [schedule a time](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion) for the objects to expire.
{: shortdesc}

**Note**: If you delete your container, any objects that are stored within that container are deleted.


## Deleting objects and containers through the UI {: #deleting-ui}

1. In your service instance dashboard, select the container with the file that you no longer need.
2. Select **Delete File** from the **Actions** drop-down menu.
3. If you no longer have use for your container, select **Delete Container** from the **Actions** drop-down menu.



## Deleting objects and containers through the CLI {: #deleting-cli}

1.  If you are not logged in to {{site.data.keyword.Bluemix_notm}}, log in to the org and space that contains your instance of {{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Optional: Confirm that you have a backup of your objects before you delete your files and containers.

3. Run the following command to delete a file:
  ```
  swift delete <container_name> <file_name>
  ```
  {: pre}

4. To delete your container, run the following command:
  ```
  swift delete <container_name>
  ```
  {: pre}



## Scheduling object deletion {: #schedule-object-deletion}


You can schedule the deletion of your objects by using either of the `X-Delete-At` or `X-Delete-After` headers.
{: shortdesc}

The `X-Delete-At` header takes an integer that represents the epoch time at which to delete the object. The `X-Delete_After` header takes an integer that represents the number of seconds after which the object is deleted.

**Note:** The actual deletion of an object might not happen at the exact time indicated. However, the object will in fact expire at the specified time. At that time, the object is longer reachable. The actual deletion will take place the next time the swift-object-expirer daemon that is configured in your Swift cluster runs.

#### To use Swift commands:

* To set the object to be deleted at a specific date and time, run the following command:

    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}

    Example:
    To set the object to be deleted on "2016/04/01 08:00:00", you would run the following command:

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* To set the object to be deleted after a specific amount of time, use the following command:

    ```
    swift post -H "X-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}

    Example:
    To set the object to be deleted an hour from now, you would run the following command:

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* To remove the expiration time from your object, use the following command:

    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}



#### To use cURL commands:

* To set the object to be deleted on "2016/04/01 08:00:00", use the following command:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
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
