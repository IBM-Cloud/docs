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


# Securing files {: #understanding-authentication}


## Understanding service credentials {: #understanding-credentials}

Service credentials are used to provide authentication and security for the service. A set of credentials is automatically generated when an instance is provisioned. The Swift client takes the authentication information from the environment variables in the following table.

<table>
  <tr>
    <th> Environment variable </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <code> OS_USER_ID </code> </td>
    <td> Your {{site.data.keyword.objectstorageshort}} user ID. </td>
  </tr>
  <tr>
    <td> <code> OS_PASSWORD </code> </td>
    <td> The password for your {{site.data.keyword.objectstorageshort}} instance. </td>
  </tr>
  <tr>
    <td> <code> OS_PROJECT_ID </code> </td>
    <td> Your project ID. </td>
  </tr>
  <tr>
    <td> <code> OS_REGION_NAME </code> </td>
    <td> The region in which your objects are stored. {{site.data.keyword.objectstorageshort}} is available in the Dallas and London regions. </td>
  </tr>
  <tr>
    <td> <code> OS_AUTH_URL </code> </td>
    <td> The endpoint URL. Be sure that `/v3` is added to the end of the URL. </td>
  </tr>
</table>

Table 1: Authentication variables and descriptions

####  Adding service credentials in the UI
1. In the **Service Credentials** tab on your service instance dashboard, click **New Credential** and give it a name.
2. (*Optional*) In the **Add Inline Configuration Parameters** text field, input the credential information for the role you want to create. The information must be formatted as a JSON payload. For more information about {{site.data.keyword.objectstorageshort}} user roles, see [Types of access](/docs/services/ObjectStorage/os_security.html#access-types).
    - To create an administrative user: `{"role":"admin"}`
    - To create a non-administrative user: `{"role":"member"}`
3. Click **Add**.


## Types of access {: #access-types}

Access to the service is controlled by user roles and container access control lists. {{site.data.keyword.objectstorageshort}} users can be either administrative or non-administrative. Access control lists are enabled by administrative users at the container level and are not available for the service instance, storage account, or at the project level.

<table>
  <tr>
    <th> Administrative users (admin) </th>
    <th> Non-administrative users (member) </th>
  </tr>
  <tr>
    <td> Manage access control </td>
    <td> By default, have no access to the service or its containers </td>
  </tr>
  <tr>
    <td> Can create and delete containers </td>
    <td> Can perform actions based on the containers read/write ACLs </td>
  </tr>
  <tr>
    <td> Can read and write to containers </td>
    <td> Can perform actions as determined by the admin </td>
  </tr>
</table>

Table 2: User roles defined

You can manage {{site.data.keyword.objectstorageshort}} users through the {{site.data.keyword.Bluemix_notm}} user interface, the Cloud Foundry API, or the Cloud Foundry CLI.




## Granting read access {: #read-access}

An {{site.data.keyword.objectstorageshort}} user with an admin role can grant read access to a container for another user and manipulate read ACL combinations.

<table>
  <tr>
    <th> Permission </th>
    <th> Read ACL options </th>
  </tr>
  <tr>
    <td> Read for all referers regardless of account affiliation </td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> Read and list for all referers and listing </td>
    <td> <code> .r:*,.rlistings </code> </td>
  </tr>
  <tr>
    <td> Read and list for a specified user in a specific project </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Read and list for a specified user in every project </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Read and list for a every user in a specified project </td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Read and list for every user in every project  </td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

Table 3: Read access permissions by option



1. Authenticate your credentials. You can use either the credentials that are found in the service credentials tab of the UI or you can generate new credentials. For more information about generating new credentials, see [Generating service credentials](/docs/services/ObjectStorage/os_cli.html#generating-cli). You receive your {{site.data.keyword.objectstorageshort}} URL and authentication token as an output.
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
    swift post <container_name> --read-acl "<project_id>:<user_id>"
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

    You can see in the following example output that read access has been granted:

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



## Granting write access {: #write-access}

An {{site.data.keyword.objectstorageshort}} user with an admin role can grant write access to a container for another user and manipulate write ACL combinations.

<table>
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
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Write for every user in a specified project </td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Write for every user in every project </td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

Table 4: Write access permissions by option



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

2. Grant write access by running the following command:
    Swift command:

    ```
    swift post <container_name> --write-acl "<project_id>:<user_id>"
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



## Removing access {: #removing-access}

To remove read ACLs from a container:
* Swift command:

    ```
    swift post <container_name> --read-acl “”
    ```
    {: pre}

*  cURL command:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

To remove write ACLs from a container:

* Swift command:

    ```
    swift post <container_name> --write-acl “”
    ```
    {: pre}

*  cURL command:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

To verify that you have removed an ACL:

* Swift command:

    ```
    swift stat <container_name>
    ```
    {: pre}

  The following example output shows both the Read ACL and Write ACL as blank which means that access has been removed.

  ```
           Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
         Container: Test
           Objects: 1
             Bytes: 31512
          Read ACL:
         Write ACL:
           Sync To:
          Sync Key:
     Accept-Ranges: bytes
  X-Storage-Policy: standard
       X-Timestamp: 1462818314.11220
        X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
      Content-Type: text/plain; charset=utf-8
  ```
  {: screen}

* cURL command:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
