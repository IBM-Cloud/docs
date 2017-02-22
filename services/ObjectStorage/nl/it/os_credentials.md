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


# Generating service credentials {: #credentials}

Service credentials are used to provide authentication and security for the service. You can generate new credentials by using the CLI or the {{site.data.keyword.Bluemix_notm}} UI.
{: shortdesc}


## To add credentials in the UI:

1. In the **Service Credentials** tab on your service instance dashboard, click **New Credential** and give it a name.
2. Optional: In the **Add Inline Configuration Parameters** text field, input the credential information for the role with the [type of access](/docs/services/ObjectStorage/os_access_types.html) you want to give. The information must be formatted as a JSON payload.
    - To create an administrative user: `{"role":"admin"}`
    - To create a non-administrative user: `{"role":"member"}`
3. Click **Add**.


## To add credentials by using Cloud Foundry commands in the CLI:

1. If you are not logged in to {{site.data.keyword.Bluemix_notm}}, log in as a user with a developer role. You must be located within the space of the service instance you want to manage.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Generate service credentials. Give your credential a name by replacing the variable
`service-key-name`. Optionally, you can also assign a [user role](/docs/services/ObjectStorage/os_access_types.html).

  ```
  cf create-service-key "<service_instance_name>" <service-key-name> -c '{"role":"<user_role>"}'
  ```
  {: pre}

  Example:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. Validate the credentials for the key you created.

  ```
  cf service-keys <service_instance_name>
  ```
  {: pre}

  Example key for an instance that is named Object-Storage-Acl-Test for a user with a member role:

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



#### To add credentials by using cURL commands in the CLI:

1. If you are not logged in to {{site.data.keyword.Bluemix_notm}}, log in as a user with a developer role. You must be located within the space of the service instance you want to manage.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Run the following command to generate service credentials.

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name: <service_instance_name>", "role: <user_role>"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: <content_type" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> Table 1. cURL service credential variables explained </caption>
    <tr>
      <th> Variable  </th>
      <th> Explanation </th>
    </tr>
    <tr>
      <td> <code>https://api.ng.bluemix.net/v2/service_keys</code> </td>
      <td> The service key endpoint.  </td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> Can be found in your URL.  </td>
    </tr>
    <tr>
      <td><i> name </i></td>
      <td> The name of your service instance. </td>
    </tr>
    <tr>
      <td><i> role </i></td>
      <td> Specify the <a href= /docs/services/ObjectStorage/os_constructing.html>user's role</a> as either an admin or a member. </td>
    </tr>
    <tr>
      <td><i> bearer_token </i></td>
      <td> The token that you received when you authenticated your instance with Keystone. </td>
    </tr>
  </table>



3. Validate your credentials by running the following command.

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: screen}
