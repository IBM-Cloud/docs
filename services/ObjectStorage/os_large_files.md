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


# Storing large objects {: #large-files}

Uploads are limited to a maximum size of 5 GB for a single upload. However, you can segment larger objects into smaller pieces and use a manifest file to concatenate the segments. Once an object is concatenated, there is no maximum size.
{: shortdesc}

Large objects can either be dynamic or static. With static large objects (SLO), segments don't have to be in the same container; each segment can be stored in any container and given any name. With dynamic large objects, the Swift client, creates container and numbered segments are uploaded in parallel to the container.


## Dynamic large objects: {: #dynamic}

You can upload dynamic large objects in two ways:
  * Have the Swift client handle everything automatically
  * Use the Swift API to do it yourself

#### Using the Swift client to handle dynamic large objects

The Swift client uses the `-segment-size` parameter to break down your object into smaller pieces. The client creates a new container with the name of the container you want to upload the files to and adds a suffix with the segment number (`<container_name>_segments`). Segments are uploaded in parallel. After all of the segments are uploaded, they are downloaded as one concatenated object to a manifest file with the original file name.

1. After you've logged in to {{site.data.keyword.Bluemix_notm}} and you're ready to upload, run the following command to segment your file.
    ```
    swift upload <container_name> <file_name> --segment-size <size_in_bytes>
    ```
    {: pre}

#### Using the Swift API to handle Dynamic Large Objects

You can segment the objects so that they are 5 GB or less yourself, and then upload them through the Swift API.

**Note**: When uploading, all of the segments must be uploaded before the manifest file. If the object is downloaded before all of the segments are uploaded, the downloaded object concatenates inconsistently.

You can upload large files by completing the following steps.

1. Sort the segments by name in the order in which they need to concatenate to form the original object.
2. Upload your segments into one container that is separate from the container that holds the manifest file. Throttling for uploads starts after the 10th segment is uploaded, and increases the upload time considerably.  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000002
    ```
    {: pre}

3. Upload an empty manifest file with the header `X-Object-Manifest` set to the corresponding `<container>/prefix>` value.

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Object-Manifest: <container_name>/<object_name>/" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}

    **Note**: The manifest file must be empty. If not, the content of the file is considered as one of the segments and falls in the order of concatenation that is dictated by the sorted names.
4. Download the object. As a result, you receive the whole object. You can add or remove segments without having to update the manifest file. Segments with the correct prefix remain part of the object. Deleting the manifest does not delete the segments.

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


## Static large objects {: #static}

Static large objects use segments and a manifest file, but you have more control. With SLO, segments don't have to be in the same container; each segment can be stored in any container and given any name. However, segments must be at least 1 MB. You are not required to set a header for the manifest file, although the header “X-Static-Large-Object” is automatically added and set to true after a correct manifest is uploaded.
{: shortdesc}

The manifest file is a JSON document that provides details of the segments and must be uploaded after all the segments have been uploaded. The data that is provided for each segment in the manifest is compared to the metadata of the actual segments. If something doesn’t match, the manifest isn't uploaded.

<table>
<caption> Table.1 JSON attributes in the manifest file </caption>
  <tr>
    <th> Attribute </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> path </i> </td>
    <td> The location and name of the segment. Specified as container_name/object_name. </td>
  </tr>
  <tr>
    <td> <i> etag </i> </td>
    <td> Provided by the PUT request when the object is uploaded. You can also find it by doing a HEAD to the object. </td>
  </tr>
  <tr>
    <td> <i> size_bytes </i> </td>
    <td> The size of the object in bytes. </td>
  </tr>
</table>



#### To upload large files

1. Run the following command to upload the segments. Throttling for uploads starts after the 10th segment is uploaded, and increases the upload time considerably.  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    ```
    {: pre}

2. Build the manifest:

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

3. Upload the manifest file by adding the query `multipart-manifest=put` to the name of the manifest.

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}

4. Download the object.

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}


#### Working with static large objects

You can manage your files by using the following commands.

**Note**: To add or remove segments to the object, upload a new manifest file with a new list of segments. The manifest name can stay the same.

* To download the content of the manifest file, you must add the query `multipart-manifest=get` to your command. The content that you receive is not identical to the content that you uploaded.

    ```
    curl -O -X GET -H "X-Auth-Token:<token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=get
    ```
    {: pre}

* To delete the manifest run the following command:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}

* To delete the manifest and all the segments, add the query `multipart-manifest=delete` after the name of the manifest:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=delete
    ```
    {: pre}
