---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-23"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Granting write access

An {{site.data.keyword.objectstorageshort}} user with an [admin role](/docs/services/ObjectStorage/os_access_types.html) can grant write access for another user and manipulate write ACL combinations.
{: shortdesc}

<table>
<caption> Table 1. Write access permissions by option </caption>
  <tr>
    <th> Permission </th>
    <th> Write ACL options </th>
  </tr>
  <tr>
    <td> Write for a specified user in a specific project </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Write for a specified user in every project </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Write for every user in a specified project </td>
    <td>  <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Write for every user in every project </td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. Authenticate your credentials by using the information in the service credentials you created.  You receive your {{site.data.keyword.objectstorageshort}} URL and authentication token as an output.

    Swift command:

    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
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
    curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. Grant write access by running the following command.

    Swift command:

    ```
    swift post <container_name> --write-acl "<user_id>:<project_id>"
    ```
    {: pre}

    cURL command:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    **Note**: Use a comma (,) to separate access control lists.

3. Verify the write ACL value.

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
