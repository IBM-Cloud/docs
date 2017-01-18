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


# Setting up object versioning {: #setting-up-versioning}

You can keep older versions of your objects automatically by setting up object versioning. With versioning, you can see a history of each object.
{: shortdesc}

When you upload a new version of your file to your main container, the previous version is automatically moved into your backup container. If you delete the file from your main container, the most recent version is automatically moved from your backup container into the main container to replace the deleted file.

1. Create a container and give it a name. Replace the variable *container_name* with the name you want to give your container.

    ```
    swift post <container_name>
    ```
    {: pre}

2. Create a second container to act as your backup storage and give it a name.

    ```
    swift post <backup_container_name>
    ```
    {: pre}

3. Set up versioning.

    Swift command:

    ```
    swift post <container_name> -H "X-Versions-Location: <backup_container_name>"
    ```
    {: pre}

    cURL command:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. Upload an object to your main container for the first time.

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

5. Make a change to your object.

6. Upload the new version of the object to your main container.

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

7.  The objects in your backup container are automatically named with the following format: `<Length><Object_name>/<Timestamp>`.
  <table>
  <caption> Table 1. Naming attributes described </caption>
    <tr>
      <th> Attribute </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> Length </i> </td>
      <td> The length of the name of your object. This is a 3-character, zero-padded hexadecimal number. </td>
    </tr>
    <tr>
      <td> <i> Object_name </i> </td>
      <td> The name of your object. </td>
    </tr>
    <tr>
      <td> <i> Timestamp </i> </td>
      <td> The timestamp of when that version of the object was originally uploaded. </td>
    </tr>
  </table>


6. List the objects in your main container to see the new version of your file.

    ```
    swift list --lh <container_name>
    ```
    {: pre}

7. List objects in your backup container. You see the previous version of your file that is stored in this container. Note that a timestamp is added to your file.

    ```
    swift list --lh <backup_container_name>
    ```
    {: pre}

8. Delete the object in your main container. When you delete the object, the most recent version in your backup container is automatically moved back into your main container.

    ```
    swift delete <container_name> <object>
    ```
    {: pre}

9. Optional: Disable object versioning.

    Swift command:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

    cURL command:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}
