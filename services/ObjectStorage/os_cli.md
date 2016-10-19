---

copyright:
  years: 2014, 2016
lastupdated: "2016-10-19"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Accessing {{site.data.keyword.objectstorageshort}} using the Swift CLI {: #using-swift-cli}


The {{site.data.keyword.objectstorageshort}} service is based on OpenStack Swift and can be accessed by using any compatible client application. This section describes how to use the Python Swift client, which is the command-line interface (CLI) for the {{site.data.keyword.objectstorageshort}} API and its extensions, to work with containers and files.
{: shortdesc}

## Installing the Swift client {: #install-swift-client}

If you haven't already, install the following [prerequisite software](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}.
* Python 2.7 or later
* setuptools package
* pip package

To install the Python Swift client, run the following command:
  ```
  sudo pip install python-swiftclient
  ```
  {: pre}

To install the Python Keystone client, run the following command:
  ```
  sudo pip install python-keystoneclient
  ```
  {: pre}




## Setting up the client {: #setup-swift-client}

To set up the Swift client, you must `export` your authentication information. You can use your credentials found in the UI, or you can [generate new credentials](../ObjectStorage/os_cli.html#generating-cli).

Example:
  ```
  export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  {: codeblock}




## Generating {{site.data.keyword.objectstorageshort}} service credentials {: #generating-cli}

To generate service credentials using the Swift CLI, you can use the following steps.

1. Log in to {{site.data.keyword.Bluemix_notm}} as a user with a developer role. You must be located within the space of the service instance you want to manage.
      ```
      cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
      ```
      {: pre}
2. Generate service credentials. `service-key-name` is the name you give your credential. You can use either the Cloud Foundry command or the cURL command.
    Cloud Foundry command:
      ```
      cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
      ```
      {: pre}
      Example Cloud Foundry command:
      ```
      cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
      ```
      {: screen}
      cURL command:
      ```
      curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
      ```
      {: pre}
3. Validate the credentials for the Service Key you created.
      Cloud Foundry command:
      ```
      cf service-key <service_key_name> <member_name>
      ```
      {: pre}
      Example member service key for an instance named Object-Storage-Acl-Test:
      ```
      {
        "auth_url": "https://identity.open.softlayer.com",
        "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
        "domainName": "757955",
        "password": "xxxxxxxx",
        "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
        "projectId": "c727d7e248b448f6b268f31a1bd8691e",
        "region": "dallas",
        "role": "member",
        "userId": "3c5b516655e4479881d3d216895faedb",
        "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
      }
      ```
      {: screen}
      cURL command:
      ```
      curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
      ```
      {: pre}




## Storing objects in containers through the CLI {: #storing-cli}

1. Log in to {{site.data.keyword.Bluemix_notm}}. Be sure to be in the correct org and space to work with your instance of {{site.data.keyword.objectstorageshort}}.
    ```
    cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
    ```
    {: pre}
2. Create a new container by running the following command. The *container_name* variable is set, by you, at this time.
    ```
    swift post <container_name>
    ```
    {: pre}
3. (*Optional*) To verify that your container was created, run the following command to list your containers.
    ```
    swift list
    ```
    {: pre}
4. Upload a file to your container by running the following command.
    ```
    swift upload <container_name> <file_name>
    ```
    {: pre}
    **Note**: To upload files larger than 5GB extra steps are needed. For more information see [Working with large files](../ObjectStorage/os_large_files.html#large-files).
5. (*Optional*) To verify that upload was successful, view the content of your container by running the following command:
    ```
    swift list <container_name>
    ```
    {: pre}

**Note**: When you upload a file with the same name, {{site.data.keyword.objectstorageshort}} replaces the stored file with the new file. If you download a file and make edits, be sure to give the file another name, or [set up object versioning](../ObjectStorage/os_versioning.html#work-with-object-versioning) before you upload to keep both versions of the file.



## Downloading objects with the Swift CLI {: #downloading-cli}

1.  Log in to {{site.data.keyword.Bluemix_notm}}. Be sure to be in the correct org and space to work with your instance of {{site.data.keyword.objectstorageshort}}.
    ```
    cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
    ```
    {: pre}
2. Download a file by running the following command:
    ```
    swift download <container_name> <file_name>
    ```
    {: pre}




## Deleting objects and containers through the CLI {: #deleting-cli}

1.  Log in to {{site.data.keyword.Bluemix_notm}}. Be sure to be in the correct org and space to work with your instance of {{site.data.keyword.objectstorageshort}}.
    ```
    cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
    ```
    {: pre}
2. Run the following command to delete a file:
    ```
    swift delete <container_name> <file_name>
    ```
    {: pre}
    **Note**: You can schedule a [specific time for your object to be deleted](../ObjectStorage/os_deletion.html#schedule-object-deletion).
3. To delete your container, run the following command:
    ```
    swift delete <container_name>
    ```
    {: pre}
    **Attention**: If you delete your container, you will delete any objects that are stored within the container.





## Working with directories {: #directory-cli}

#### Adding a directory to a container with the Swift CLI

Swift does not have a true directory structure, but uses naming to represent a directory layout. If you specify a directory name, it will be attached to all file names as part of the relative path.

1. Run the following command to add a directory to a container:
    ```
    swift upload <container_name> <directory_name>
    ```
    {: pre}

#### Downloading a directory
To download a directory structure, use the `-prefix` parameter to indicate the directory or directory structure that you want to download.

1. Run the following command to download a directory:
    ```
    swift download <container_name> --prefix <directory>
    ```
    {: pre}
