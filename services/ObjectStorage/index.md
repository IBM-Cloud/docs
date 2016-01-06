{:new_window: target="_blank"}

# Getting started with {{site.data.keyword.objectstorageshort}}  (BETA) {: #getting-started-with-object-storage} 

{{site.data.keyword.objectstoragefull}} provides you with access to a fully provisioned Swift {{site.data.keyword.objectstorageshort}} account to manage your data. Swift provides a fully distributed, API-accessible storage platform. You can use it directly in your applications or for backups, making it ideal for cost effective, scale-out storage.

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} uses OpenStack Identity (Keystone) for authentication and can be accessed directly by using OpenStack Object Storage (Swift) API v1 calls. IBM {{site.data.keyword.objectstorageshort}} can be bound to a {{site.data.keyword.Bluemix_notm}} application or accessed from outside a {{site.data.keyword.Bluemix_notm}} application. 

More information and documentation about using OpenStack Swift and Keystone is available at the [OpenStack documenation site](http://docs.openstack.org){: new_window}.

**Note:** Provider side encryption is not provided. It is the responsibility of the client application to encrypt data before uploading.

## Creating an {{site.data.keyword.objectstorageshort}} instance in {{site.data.keyword.Bluemix_notm}} {: #creating-object-storage-instance} 

### How to create an {{site.data.keyword.objectstorageshort}} service instance
1.	Go to the **{{site.data.keyword.Bluemix_notm}}** catalog and select the **Solutions** tab. Select the **Storage** category, and then select **{{site.data.keyword.objectstorageshort}}**.
2.	Select your space, app, service name, and plan and click **Create**. 
**Note:** If you initially choose the **Leave Unbound** option for the **App** field, you can still bind the service instance to your {{site.data.keyword.Bluemix_notm}} application after you complete the configuration (see the following instructions).

## Using {{site.data.keyword.objectstorageshort}} from a {{site.data.keyword.Bluemix_notm}} app {: #using-object-storage-from-bluemix-app} 

### How to bind your {{site.data.keyword.objectstorageshort}} service to an application after creation {: #bind-object-storage-to-application} 
1.	In the **{{site.data.keyword.Bluemix_notm}}** dashboard, select the app that you want to bind.
2.	In the app overview, click **Bind a Service or API**.
3.	Select your {{site.data.keyword.objectstorageshort}} instance from the list of services and click **Add**.
4.	Click **Restage** when prompted. Your app must be restaged to use the new service.

### Bound context

If you want to use {{site.data.keyword.objectstorageshort}} in a bound context, the cloud credentials are provided indirectly through the application binding process. After you successfully bind a service instance to your application, a configuration similar to the following example is added to your `VCAP_SERVICES` environment variable.

    {
    "Object-Storage": [
    {
      "name": "Object-Storage - YP",
      "label": "Object-Storage",
      "plan": "Free",
      "credentials": {
         "auth_url": "https://identity.open.softlayer.com",
         "project": "object_storage_d049255b",
         "projectId": "0f47b41b06d047f9aae3b33f1db061ed",
         "region": "dallas",
         "userId": "ad78b2a3f843466988afd077731c61fc",
         "username": "user_202db1f8a7aa3f3ac51ec68f10dbe7dc29070bc7",
         "password": "K/jyIi2jR=1?D.TP",
         "domainId": "2df6373c549e49f8973fb6d22ab18c1a",
         "domainName": "639347"
        }
       }
      ]
    }

## Using the {{site.data.keyword.objectstorageshort}} user interface {: #using-object-storage-ui}

### UI elements and navigation
When your {{site.data.keyword.objectstorageshort}} is provisioned, you can see your instance information in the {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} service instance dashboard. From the dashboard, select your {{site.data.keyword.objectstorageshort}} instance to view the panel with more detailed information.  
#### Usage data
At the top of the panel, you’ll see the storage usage information for your instance. It also shows the current number of **Storage Containers** and the total number of **Objects** in all of your containers. It lists your memory usage in megabytes. **Storage Consumed** refers to the current amount of space that is used. 
#### Actions
To retrieve the latest usage data, click the **Refresh** button.   
####Object browser 
The bottom section of the panel contains the object browser. Use the object browser to manage object storage containers and objects. You can create containers, upload files, delete containers, and delete files among other actions.

## Using the Swift CLI to access {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

You can access {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} over the Internet and from applications and virtual machines within IBM {{site.data.keyword.Bluemix_notm}}. Common use cases for {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} include:

* Backing up volume data from your instances
* Using as an intermediary location when transferring large amounts of data
* Transferring data between environments that are not directly connected
* Acting as a central repository

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} is based on OpenStack Swift and can be accessed by using any compatible client application. This section describes how to use the Python Swift client, which is the command-line interface (CLI) for the {{site.data.keyword.objectstorageshort}} API and its extensions, to work with containers and files.

### Installing the Swift client

Install the following prerequisite software if not already installed. For more information, see the [Openstack Documentation](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}. 
* Python 2.7 or later
* setuptools package
* pip package

Install the Python Swift client using Python pip:

	sudo pip install python-swiftclient

### Setting up the client

The Swift client takes the authentication information from the environment variables ```OS_AUTH_URL```, ```OS_USER_ID```, and ```OS_PASSWORD``` for the endpoint URL, username, and password respectively.

Set the authentication information as follows. 

	export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
	export OS_PASSWORD=aaa55AAAaaaaa]?,
	export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
	export OS_AUTH_URL=https://identity.open.softlayer.com/v3
	export OS_REGION_NAME=dallas
	export OS_IDENTITY_API_VERSION=3
	export OS_AUTH_VERSION=3

You can find the credential values for your {{site.data.keyword.objectstorageshort}} service from the **Service Credentials** page in the {{site.data.keyword.objectstorageshort}} user interface. 

**Note:** Make sure that you add a ```/v3``` to the ```auth_url``` from the credentials in the {{site.data.keyword.objectstorageshort}} user interface when configuring the environment variables ```OS_AUTH_URL``` for the Swift client.


![{{site.data.keyword.objectstorageshort}} Service Credentials](images/service_credentials.jpg)

*Figure 1. {{site.data.keyword.objectstorageshort}} Service Credentials*

### Working with containers

Listing containers:

	swift list
	
Creating a new container:

	swift post <container_name>
	
Listing the content of a container:

	swift list <container_name>

### Working with objects

#### Adding a file to a container

	swift upload <container_name> <file_name>

#### Adding files larger than 5 GB to a container

If you are uploading a file that is larger than 5GB, you must split it into smaller chunks. You can instruct the Swift client to handle this by supplying the ```-segment-size``` parameter:

	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
	
Each segment is uploaded in parallel into a separate container named ```<container_name>_segments```. Once all the segments are uploaded, Swift creates a manifest file so that the segments can be downloaded in a single file from the orginal container ```<container_name>``` with the orginal filename ```<file_name>```.

For example, the following command uploads a file named ```large_file``` from a container named ```test_container``` with the segment size ```1073741824```.

	swift upload test_container -S 1073741824 large_file

You can run the following command to download the file:

	swift download test_container large_file

#### Downloading a file

	swift download <container_name> <file_name>
	
#### Adding a directory to a container

Swift does not have a true directory structure, but uses the naming to represent a directory layout. To add a directory to a container, run the following command:

	swift upload <container_name> <directory_name>
	
This will upload the full directory structure as a relative path. For example, if you specify ```/mnt/volume1```, the directory structure mnt/volume1 will be attached to all the file names to indicate the directory structure.

	
#### Downloading a directory

To download a directory structure, use the ```-prefix``` parameter to indicate the directory or directory structure you want to download.

	swift download <container_name> --prefix <directory>
	
#### Deleting a file

	swift delete <container_name> <file_name>

### Creating a temporary URL

A temporary URL is a long, difficult-to-guess URL that can be used for a specified period of time to download objects without requiring further authentication. There are three steps to generate a temporary URL:

1. Identify your authentication account.
2. Set a secret key.
3. Create the temporary URL.

#### Identifying your authentication account

The Swift stat command prints information about your account:

	swift stat

Locate the Account field and note the full string behind *Account*: including ```AUTH_```.

#### Setting a secret key

This key can be anything you select, but best practice is that it should be a long, random, and hard to guess string.

	swift post -m "Temp-URL-Key:<key>"

#### Creating the temporary URL

The swift tempurl command takes these positional arguments:

* [method] GET to allow download, PUT to allow upload
* [seconds] Time in seconds that the temporary URL will be available
* [path] The full path of the object expressed as /v1/<auth_account>/<container_name>/<object_name>
* [key] The key that you set in step 2

```
swift tempurl GET <seconds> <path> <key>
```

This will return a URL that you can append to your cluster name to get a full URL. Use the full URL to download the object with any compatible HTTP client such as curl, wget, or firefox.

## Using the Swift REST API to access {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

You can use the Swift REST API with a command–line client interface, such as cURL, or call the API from your application.  

### {{site.data.keyword.objectstorageshort}} URL

To interact with the {{site.data.keyword.objectstorageshort}} API, construct the {{site.data.keyword.objectstorageshort}} URL as follows:

	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>

For example:

![{{site.data.keyword.objectstorageshort}} URL](images/Swift_URL.png)

*Figure 2. {{site.data.keyword.objectstorageshort}} URL*

The URL consists of five parts. You can find the ```<API version>```, ```<project ID>```, ```<container namespace>```, and ```<object namespace>``` of your {{site.data.keyword.objectstorageshort}} from the {{site.data.keyword.objectstorageshort}} user interface. For the ```<access point>```, see the following table:


| **Region**  |     **Internal access point**                             |     **Public access point**                  |
|-------------|-----------------------------------------------------------|----------------------------------------------|
| Dallas      | https://dal.objectstorage.service.open.networklayer.com   | https://dal.objectstorage.open.softlayer.com | 


*Table 1. {{site.data.keyword.objectstorageshort}} access point*

Use the internal access point when accessing the {{site.data.keyword.objectstorageshort}} service from inside {{site.data.keyword.Bluemix_notm}} or the public access point when accessing the {{site.data.keyword.objectstorageshort}} service from outside of {{site.data.keyword.Bluemix_notm}}.

### {{site.data.keyword.objectstorageshort}} API

See the [Openstack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window} for a comprehensive list of the {{site.data.keyword.objectstorageshort}} REST API options and examples.

## Understanding authentication and credentials {: #understanding-authentication-credentials}

### Generating {{site.data.keyword.objectstorageshort}} credentials without binding an application

To generate {{site.data.keyword.objectstorageshort}} cloud credentials for use outside a {{site.data.keyword.Bluemix_notm}} application, you must generate a service key for your {{site.data.keyword.objectstorageshort}} instance. You can generate a new key by using the **Service Credentials** button in the sidebar of the user interface or by using the Cloud Foundry CLI (version 6.11.3 or later). After you generate and retrieve a service key for your {{site.data.keyword.objectstorageshort}} instance, you can use the cloud integration information to request a Keystone token using an OpenStack SDK or the OpenStack Identity API and start using the Swift account to manage objects.
   
To create the key by using the Cloud Foundry CLI, log in and run the following command:
 
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>

To retrieve the service credentials from the Cloud Foundry CLI, run the following command:

	cf service-key <object_storage_instance_name> <unique_name_for_this_key>


### Cloud projects and users
Provisioning a new {{site.data.keyword.objectstorageshort}} instance creates an isolated Keystone project in the IBM Public Cloud. When you bind a new application to the {{site.data.keyword.objectstorageshort}} instance, a new Keystone user with access to the project is created. When you deprovision the instance, the project and user are deleted.

### OpenStack Identity (Keystone) v3
The credentials structure contains a complete set of attributes to allow to you to choose the OpenStack token request method or OpenStack SDK that best fits your application. 
 
The recommended v3 token request is a POST request to https://identity.open.softlayer.com/v3/auth/tokens as shown in the following curl command:

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
						"password": "K/jyIi2jR=1?D.TP"
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

Use the value of the X-Subject-Token field from the response header as the X-Auth-Token field when making requests to the {{site.data.keyword.objectstorageshort}} service.

An example response is as follows:

	HTTP/1.1 201 Created
	X-Subject-Token: MIIFfQ...
	Vary: X-Auth-Token
	Content-Type: application/json
	Content-Length: 960
	Date: Tue, 10 Jun 2014 20:40:14 GMT
	
	{"token": 
	{"audit_ids": ["ECwrVNWbSCqmEgPnu0YCRw"], "methods": ["password"],
	 "roles": [{"id": "c703057be878458588961ce9a0ce686b", "name": "admin"}],
	 "expires_at": "2014-06-10T21:40:14.360795Z", 
	 "project": {"domain": {"id": "default", "name": "Default"}, "id": "3d4c2c82bd5948f0bcab0cf3a7c9b48c", "name": "demo"}, 
	 "catalog": [{"endpoints": 
		[{"region_id": "london", "url": "https://lon-api.open.softlayer.com:8777", "region": "london", "interface": "public", "id": "44e7992960994729ab15437dd422e4cf"}, 
		 {"region_id": "sydney", "url": "https://syd-api.open.softlayer.com:8777", "region": "sydney", "interface": "public", "id": "67b14f2beb0643f3b8ee559e473d0cc5"},
		 {"region_id": "sydney", "url": "https://syd-api.open.softlayer.com:8777", "region": "sydney", "interface": "admin", "id": "8bf4c2d57e1f4e46b27c5d123a626c19"}, 
		 {"region_id": "london", "url": "https://lon-api.open.softlayer.com:8777", "region": "london", "interface": "internal", "id": "9157d426a9074e85afc4568b405e3f13"}, 
		 {"region_id": "sydney", "url": "https://syd-api.open.softlayer.com:8777", "region": "sydney", "interface": "internal", "id": "a1998b1733764f9b9d5a576a3096e40c"}, 
		 {"region_id": "london", "url": "https://lon-api.open.softlayer.com:8777", "region": "london", "interface": "admin", "id": "cb17d65b75b64abe9ef1973002498465"}], 
		"type": "metering", "id": "3d71660734514bd8a012a04409a0dd13", "name": "ceilometer"}], 
	 "extras": {},
	 "user": {"domain": {"id": "default", "name": "Default"}, "id": "3ec3164f750146be97f21559ee4d9c51", "name": "admin"},  "issued_at": "2014-06-10T20:40:14.360822Z"}}


The {{site.data.keyword.objectstorageshort}} URL is found in the Service Catalog. The Service Catalog is contained in the response body of the token request. Select the endpoint from the Service Catalog with type of object-storage, region that matches the region field in the credentials, and internal interface (`internalURL`) when accessing the {{site.data.keyword.objectstorageshort}} service from inside {{site.data.keyword.Bluemix_notm}} or public interface (`publicURL`) when accessing the {{site.data.keyword.objectstorageshort}} service from outside of {{site.data.keyword.Bluemix_notm}}.

### OpenStack Identity (Keystone) v2
The v2 token request is a POST request to https://identity.open.softlayer.com/v2.0/tokens as shown in the following curl command:

	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"tenantId": "0f47b41b06d047f9aae3b33f1db061ed",
			"passwordCredentials": {
				"userId": "ad78b2a3f843466988afd077731c61fc",
				"password": "K/jyIi2jR=1?D.TP "
			}
		}
	}' \
	  https://identity.open.softlayer.com/v2.0/tokens ; echo

**Note:** This request method is not documented on the OpenStack Identity v2 website. You cannot use `tenantName` and `username`.

Use the value of the access token id field from the response body as the X-Auth-Token field when making requests to the {{site.data.keyword.objectstorageshort}} service.

The {{site.data.keyword.objectstorageshort}} URL is found in the Service Catalog. The Service Catalog is contained in the response body of the token request. Select the endpoint from the Service Catalog with type of object-storage, region which matches the region field in the credentials, and internal interface (`internalURL`) when accessing the {{site.data.keyword.objectstorageshort}} service from inside {{site.data.keyword.Bluemix_notm}} or public interface (`publicURL`) when accessing the {{site.data.keyword.objectstorageshort}} service from outside of {{site.data.keyword.Bluemix_notm}}.


## Unbinding and deprovisioning {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### How to deprovision your {{site.data.keyword.objectstorageshort}} service
1.	Select your service from the **{{site.data.keyword.Bluemix_notm}}** dashboard.  
2.	Click the gear icon in the upper right corner and select **Delete Service**.
	
**Warning:** If you deprovision an IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} service instance, the cloud project and Swift account are deleted. All containers and objects in the deprovisioned instance are deleted from Swift and cannot be restored.

### Unbinding an application or deleting a service key

If you unbind an application from the {{site.data.keyword.objectstorageshort}} instance or delete the service key, the credentials are deleted. The {{site.data.keyword.objectstorageshort}} account is not deleted until the {{site.data.keyword.objectstorageshort}} instance is deprovisioned. You can generate new cloud credentials by [rebinding or creating a new service key](#bind-object-storage-to-application).

## FAQ {: #FAQ} 

### Cost information
Pricing varies depending on the chosen plan. For more pricing information, refer to the [IBM Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/){: new_window} or use the [Calculator](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window} for more detailed estimates.

># Related Links {:class="linklist"}
>## API Reference {:id="api"}
>* [OpenStack Object Storage (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
>* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}
>
># Related Links {:class="linklist"}
>## SDK {:id="sdk"}
>* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}
>
># Related Links {:class="linklist"}
>## Tutorials and Samples {:id="samples"}
>* [Connecting to IBM Object Storage for Bluemix with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
>* [Use Python to access your Bluemix Object Storage](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
>* [Bluemix Object Storage Community](https://www.ibm.com/developerworks/community/groups/service/html/communityoverview?communityUuid=1b48459f-4091-43cb-bca4-37863606d989){: new_window}
>
># Related Links {:class="linklist"}
>## Compatible Runtimes {:id="buildpacks"}
>* [Liberty for Java](https://www.ng.bluemix.net/docs/starters/liberty/index.html){: new_window}
>* [SDK for Node.js](https://www.ng.bluemix.net/docs/starters/nodejs/index.html){: new_window}
>* [Go](https://www.ng.bluemix.net/docs/starters/go/index.html){: new_window}
>* [PHP](https://www.ng.bluemix.net/docs/starters/php/index.html){: new_window}
>* [Python](https://www.ng.bluemix.net/docs/starters/python/index.html){: new_window}
>* [Ruby](https://www.ng.bluemix.net/docs/starters/rails/index.html){: new_window}
>* [Community buildpacks](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}
>
># Related Links {:class="linklist"}
>## Related Links {:id="general"}
>* [IBM Bluemix Pricing Sheet](https://www.ng.bluemix.net/#/pricing){: new_window}
>* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
>
>{:elementKind="article" id="rellinks"}
