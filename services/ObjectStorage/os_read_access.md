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


# Granting read access

An {{site.data.keyword.objectstorageshort}} user with an [admin role](/docs/services/ObjectStorage/os_access_types.html) can grant read access to a container for another user and manipulate read ACL combinations.
{: shortdesc}

<table>
<caption> Table 1. Read access permissions by option </caption>
  <tr>
    <th> Permission </th>
    <th> Read ACL options </th>
  </tr>
  <tr>
    <td> Read for all referers regardless of account affiliation </td>
    <td> <code> .r,&#42;  </code> </td>
  </tr>
  <tr>
    <td> Read and list for all referers and listing </td>
    <td> <code> .r:&#42;,.rlistings </code> </td>
  </tr>
  <tr>
    <td> Read and list for a specified user in a specific project </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Read and list for a specified user in every project </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Read and list for every user in a specified project </td>
    <td> <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Read and list for every user in every project  </td>
    <td> <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. Authenticate your credentials. You can use either the credentials that are found in the service credentials tab of the UI or you can generate new credentials. For more information about generating new credentials, see [Generating service credentials](/docs/services/ObjectStorage/os_credentials.html). You receive your {{site.data.keyword.objectstorageshort}} URL and authentication token as an output.

    Swift command:

    ```
    export OS_USER_ID=<user_id>
    export OS_PASSWORD=<password>
    export OS_TENANT_ID=<project_id>
    export OS_AUTH_URL=https://identity.open.softlayer.com/v3
    export OS_REGION_NAME=<region>
    export OS_IDENTITY_API_VERSION=3
    export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}

    cURL command:

    ```
    curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
    ```
    {: pre}

2. Grant read access by running the following command:
    Swift command:

    ```
    swift post <container_name> --read-acl "<user_id>:<project_id>"
    ```
    {: pre}

    cURL command:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}
    **Note**: Use a comma (,) to separate access control lists.


3. Verify the Read ACL value.

    Swift command:

    ```
    swift stat <container_name>
    ```
    {: pre}

    cURL command:

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    Example: The `X-Container-Read` value shows to which container and to whom read access is granted.

    ```
    HTTP/1.1 204 No Content
    Content-Length: 0
    X-Container-Object-Count: 1
    Accept-Ranges: bytes
    X-Storage-Policy: standard
    X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
    X-Container-Bytes-Used: 31512
    X-Timestamp: 1462818314.11220
    Content-Type: text/plain; charset=utf-8
    X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
    Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}
