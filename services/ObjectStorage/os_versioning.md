---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Working with object versioning {: #work-with-object-versioning}

*Last updated: 19 October 2016*
{: .last-updated}

With object versioning you are able to keep separate versions of your objects without renaming your files. This allows you to see a history of each object and keep track of when changes were made.
{: shortdesc}


### Setting up object versioning {: #setting-up-versioning}

You can set up versions of each object in your container by using the `X-Versions-Location` parameter. To do this, create an additional container to keep older versions of your objects as follows.

You can set up object versioning through the Swift client or by using cURL commands.
* If you are using the Swift client, run the following command:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}
    
* If you are using cURL, you can set it up like this:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}
    
**Note**: The objects in your backup container will be automatically named with the following format: `<Length><Object_name>/<Timestamp>`.
<table>
  <tr>
    <th> Attribute </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> `Length` </td>
    <td> The length of the name of your object. This is a 3-character, zero-padded hexadecimal number. </td>
  </tr>
  <tr>
    <td> `Object_name` </td>
    <td> The name of your object. </td>
  </tr>
  <tr>
    <td> `Timestamp` </td>
    <td> The timestamp of when that version of the object was originally uploaded. </td>
  </tr>
</table>

### Disabling object versioning {: #disabling-versioning}

You can disable versioning through the Swift client or by using cURL commands.

* To use the Swift client run the following command:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* Run the following cURL command to disable versioning:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}


### Object versioning tutorial {: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

You can use the following tutorial to get an understanding of the full lifecycle of object versioning.

1. Create a container named `container_one`.

    ```
    swift post container_one
    ```
    {: pre}
    
3. Create a second container with the name `container_two`.

    ```
    swift post container_two
    ```
    {: pre}
    
2. Set up versioning.

    ```
    swift post container_one -H "X-Versions-Location:container_two"
    ```
    {: pre}
    
4. Upload an object to your main container for the first time.

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. Upload a new version of the object to container_one. When you upload a new version of your file, the previous version is automatically moved into the backup container you specified when you setup versioning.

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. To see the new version of your file in the container, list the objects in container_one.

    ```
    swift list container_one
    ```
    {: pre}
    
9. List objects in container_two. You will see the previous version of your file will be stored in this container.

    ```
    swift list container_two
    ```
    {: pre}
    
10. Delete the object in container_one. When you delete the object, the previous version in your backup container will automatically be moved into your main container.

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. List both containers. You will see your original file in `container_one` and `container_two` will be empty.

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
