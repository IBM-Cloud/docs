---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Working with large files {: #large-files}


Uploading objects is limited to a maximum size of 5 GB in a single upload. However, you can still upload objects larger than 5GB if segment them into smaller objects. Once the segmented objects have been uploaded, a manifest file is also needed to concatenate the segments into the original object. There are two ways to do this: Dynamic Large Objects (DLO) and Static Large Objects (SLO).
{: shortdesc}

### Dynamic Large Objects: {: #dynamic}

There are two ways to handle DLO:
  * Have the Swift client handle everything automatically
  * Use the Swift API to do it yourself

#### Using the Swift client to handle Dynamic Large Objects

The Swift client uses the `-segment-size` parameter to break down your object into smaller pieces. The client creates a new container with the name of the container you want to upload the files to and adds a suffix with the segment number (`<container_name>_segments`). Segments are uploaded in parallel. After all of the segments are uploaded, they are downloaded as one concatenated object to a manifest file with the original file name.

1. After you've logged in to {{site.data.keyword.Bluemix_notm}} and you're ready to upload, run the following command to segment your file.

    ```
    swift upload <container_name> <file_name> --segment-size <size_in_bytes>
    ```
    {: pre}

#### Using the Swift API to handle Dynamic Large Objects

You can segment the objects so that they are 5GB or less yourself, and then upload them through the Swift API. It is important when uploading, that you first upload all of the segments before uploading the manifest. If the object is downloaded before all of the segments have finished uploaded the downloaded object will be inconsistent. You can upload large files by completing the following steps.

1. Sort the segments by name in the order in which they should be concatenated to form the original object.
2. Upload your segments into one container that is separate from the container that holds the manifest file. Throttling for uploads starts after the 10th segment has been uploaded, and increases the upload time considerably.  For this reason, it is recommended that your segment size is no smaller than the size of the file divided by 10.

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

    **Note**: The manifest file must be empty. If not, the content of the file will be considered as one of the segments and will fall in the order of concatenation that is dictated by the sorted names.
4. Download the object. You will receive the whole object as a result. You can add or remove segments without having to update the manifest file. Segments with the correct prefix will remain part of the object. Deleting the manifest will not delete the segments.

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


### Static Large Objects {: #static}

Static Large Objects make use of segments and a manifest file, but allow you more control. With SLO, segments don't have to be in the same container; each each segment can be stored in any container and given any name. However, segments must be at least 1 MB. You are not required to set a header for the manifest file, although the header “X-Static-Large-Object” is automatically added and set to true after a correct manifest has been uploaded.
{: shortdesc}

The manifest file is a JSON document that provides details of the segments and must be uploaded after all the segments have been uploaded. The data provided for each segment in the manifest is compared to the metadata of the actual segments. If something doesn’t match, the manifest will not be uploaded.

<table>
  <tr>
    <th> Attribute </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> path </td>
    <td> The location and name of the segment. Specified as container_name/object_name. </td>
  </tr>
  <tr>
    <td> etag </td>
    <td> Provided by the PUT request when the object is uploaded. You can also find it by doing a HEAD to the object. </td>
  </tr>
  <tr>
    <td> size_bytes </td>
    <td> The size of the object in bytes. </td>
  </tr>
</table>

*Table 1: JSON attributes in the manifest file in the order of concatenation*

You can upload large files by completing the following steps:

1. Run the following command to upload the segments. Throttling for uploads starts after the 10th segment has been uploaded, and increases the upload time considerably.  For this reason, it is recommended that your segment size is no smaller than the size of the file divided by 10.

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

3. Upload the manifest. To do this, you must add the query `multipart-manifest=put` to the name of the manifest by running the following command:

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}

4. Download the object.

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}

Here are some commands that you might need when working with Static Large Objects.

* To download the content of the manifest file, you must add the query `multipart-manifest=get` to your command. The content you receive will not be identical to the content you uploaded.

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

**Note**: To add segments to the object or to remove segments from it, you need to upload a new manifest file with a new list of segments. The manifest name can stay the same.
