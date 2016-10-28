---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Securing files {: #understanding-authentication}
*Last updated: 19 October 2016*
{: .last-updated}

## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

Provisioning a new {{site.data.keyword.objectstorageshort}} instance creates an isolated Keystone project in the IBM Public Cloud.
{: shortdesc}

The credentials structure contains a complete set of attributes to allow to you to choose the OpenStack token request method or OpenStack SDK that best fits your app. When you bind a new app to the instance, a new Keystone user with access to the project is created. When you deprovision the instance, the project and user are deleted.

For more information about using OpenStack Swift and Keystone, view the [OpenStack documentation site](http://docs.openstack.org).

The recommended v3 token request is a POST request to https://identity.open.softlayer.com/v3/auth/tokens as shown in the following curl command:

```
	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "XXXXXXXXXX"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo
```
{: codeblock}

Use the value of the `X-Subject-Token` field from the response header as the `X-Auth-Token` field when you make requests to the {{site.data.keyword.objectstorageshort}} service.

An example response is as follows. The response is trimmed to show only the {{site.data.keyword.objectstorageshort}} relevent information.

```
	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints" : [
	          {
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}
```
{: screen}

The {{site.data.keyword.objectstorageshort}} URL is found in the service catalog. The service catalog is contained in the response body of the token request. The response is a full catalog of OpenStack services that are available. Select the endpoint from the service catalog with type of `object-store` and the region that matches the region field in the credentials.

**Note:** Use the public interface (`publicURL`). The internal interface (`internalURL`) is not accessible from {{site.data.keyword.Bluemix_notm}}.


## Understanding service credentials {: #understanding-credentials}

Service credentials are used to provide authentication and security for the service. A set of credentials is automatically generated when an instance is provisioned. The Swift client takes the authentication information from the environment variables in the following table.

<table>
  <tr>
    <th> Environment variable </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> `OS_USER_ID` </td>
    <td> Your {{site.data.keyword.objectstorageshort}} user ID. </td>
  </tr>
  <tr>
    <td> `OS_PASSWORD` </td>
    <td> The password for your {{site.data.keyword.objectstorageshort}} instance. </td>
  </tr>
  <tr>
    <td> `OS_PROJECT_ID` </td>
    <td> Your project ID. </td>
  </tr>
  <tr>
    <td> `OS_REGION_NAME` </td>
    <td> The region in which your objects are stored. {{site.data.keyword.objectstorageshort}} is available in the Dallas and London regions. </td>
  </tr>
  <tr>
    <td> `OS_AUTH_URL` </td>
    <td> The endpoint URL. Be sure that `/v3` is added to the end of the URL. </td>
  </tr>
</table>

*Table 1: Authentication variables and descriptions*

####  Adding service credentials in the UI
1. In the **Service Credentials** tab on your service instance dashboard, click **New Credential** and give it a name.
2. (*Optional*) In the **Add Inline Configuration Parameters** text field, input the credential information for the role you want to create. The information must be formatted as a JSON payload. For more information about {{site.data.keyword.objectstorageshort}} user roles, see [Types of access](../os_security.html#access-types).
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

*Table 2: User roles defined*

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
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> Read and list for all referers and listing </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> Read and list for a specified user in a specific project </td>
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> Read and list for a specified user in every project </td>
    <td> `<*>:< user_id>` </td>
  </tr>
  <tr>
    <td> Read and list for a every user in a specified project </td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> Read and list for every user in every project  </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Table 3: Read access permissions by option*



1. Authenticate your credentials. You can use either the credentials that are found in the service credentials tab of the UI or you can generate new credentials. For more information about generating new credentials, see [Generating service credentials](insert link here). You receive your {{site.data.keyword.objectstorageshort}} URL and authentication token as an output.
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
    <td> `<project_id>:<user_id>` </td>
  </tr>
  <tr>
    <td> Write for a specified user in every project </td>
    <td> `*:<user_id>` </td>
  </tr>
  <tr>
    <td> Write for every user in a specified project </td>
    <td> `<project_id>:<*>` </td>
  </tr>
  <tr>
    <td> Write for every user in every project </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Table 4: Write access permissions by option*




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
