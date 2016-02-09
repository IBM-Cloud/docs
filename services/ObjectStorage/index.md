{:new_window: target="_blank"}

# Getting started with {{site.data.keyword.objectstorageshort}}  (BETA) {: #getting-started-with-object-storage} 

{{site.data.keyword.objectstoragefull}} provides you with access to a fully provisioned Swift {{site.data.keyword.objectstorageshort}} account to manage your data. Swift provides a fully distributed, API-accessible storage platform. You can use it directly in your applications or for backups, making it ideal for cost effective, scale-out storage.

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} uses OpenStack Identity (Keystone) for authentication and can be accessed directly by using OpenStack Object Storage (Swift) API v1 calls. IBM {{site.data.keyword.objectstorageshort}} can be bound to a {{site.data.keyword.Bluemix_notm}} application or accessed from outside a {{site.data.keyword.Bluemix_notm}} application. 

More information and documentation about using OpenStack Swift and Keystone is available at the [OpenStack documentation site](http://docs.openstack.org){: new_window}.

The {{site.data.keyword.objectstorageshort}} architecture diagram is as follows:

[![{{site.data.keyword.objectstorageshort}} Architecture Diagram](images/object_storage_solution_archectiture_small.png)](http://www.ng.bluemix.net/docs/api/content/services/ObjectStorage/images/object_storage_solution_archectiture.png){: new_window}

*Figure 1. {{site.data.keyword.objectstorageshort}} Architecture Diagram*

**Note:** Provider side encryption is not provided. It is the responsibility of the client application to encrypt data before uploading.

**Note:** The {{site.data.keyword.objectstorageshort}} Service Beta plan will be removed from the catalog after the General Availability of the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} Service. After a grace period, service instances that use the Beta plan will be removed. [Update your pricing plan](#changeplan) to continue using the {{site.data.keyword.objectstorageshort}} service. 




## Creating an {{site.data.keyword.objectstorageshort}} instance in {{site.data.keyword.Bluemix_notm}} {: #creating-object-storage-instance} 

### How to create an {{site.data.keyword.objectstorageshort}} service instance
1.	Go to the {{site.data.keyword.Bluemix_notm}} **Catalog** tab and enter **{{site.data.keyword.objectstorageshort}}** into the search box, or go to **Services** and select **Storage**. Click the **{{site.data.keyword.objectstorageshort}}** service. 
2.	Select your space, app, service name, and plan and click **Create**. 
**Note:** If you initially choose the **Leave Unbound** option for the **App** field, you can still bind the service instance to your {{site.data.keyword.Bluemix_notm}} application after you complete the configuration. See the following instructions.

## Using {{site.data.keyword.objectstorageshort}} from a {{site.data.keyword.Bluemix_notm}} app {: #using-object-storage-from-bluemix-app} 

### How to bind your {{site.data.keyword.objectstorageshort}} service to an application after creation {: #bind-object-storage-to-application} 
1.	In the {{site.data.keyword.Bluemix_notm}} dashboard, select the app that you want to bind.
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

You can access the {{site.data.keyword.objectstorageshort}} service over the Internet and from applications and virtual machines within IBM {{site.data.keyword.Bluemix_notm}}. Common use cases for the {{site.data.keyword.objectstorageshort}} service are as follows:

* Backing up volume data from your instances
* Using as an intermediary location when you transfer large amounts of data
* Transferring data between environments that are not directly connected
* Acting as a central repository

The {{site.data.keyword.objectstorageshort}} service is based on OpenStack Swift and can be accessed by using any compatible client application. This section describes how to use the Python Swift client, which is the command-line interface (CLI) for the {{site.data.keyword.objectstorageshort}} API and its extensions, to work with containers and files.

### Installing the Swift client

Install the following prerequisite software if not already installed. For more information, see the [OpenStack Documentation](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}. 
* Python 2.7 or later
* setuptools package
* pip package

Install the Python Swift client by using Python pip:

	sudo pip install python-swiftclient

### Setting up the client

The Swift client takes the authentication information from the following environment variables:
* ```OS_AUTH_URL``` is the endpoint URL
* ```OS_USER_ID``` is the user name
* ```OS_PASSWORD``` is the password

Set the authentication information as follows. 

	export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
	export OS_PASSWORD=aaa55AAAaaaaa]?,
	export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
	export OS_AUTH_URL=https://identity.open.softlayer.com/v3
	export OS_REGION_NAME=dallas
	export OS_IDENTITY_API_VERSION=3
	export OS_AUTH_VERSION=3

You can find the credential values for your {{site.data.keyword.objectstorageshort}} service from the **Service Credentials** page in the {{site.data.keyword.objectstorageshort}} user interface. 

**Note:** Make sure that you add a ```/v3``` to the ```auth_url``` from the credentials in the {{site.data.keyword.objectstorageshort}} user interface when you configure the environment variables ```OS_AUTH_URL``` for the Swift client.


![{{site.data.keyword.objectstorageshort}} Service Credentials](images/service_credentials.jpg)

*Figure 2. {{site.data.keyword.objectstorageshort}} Service Credentials*

### Working with containers

Listing containers:

	swift list
	
Creating a container:

	swift post <container_name>
	
Listing the content of a container:

	swift list <container_name>

### Working with objects

#### Adding a file to a container

	swift upload <container_name> <file_name>

#### Adding files larger than 5 GB to a container

If you are uploading a file that is larger than 5 GB, you must split it into smaller chunks. You can instruct the Swift client to handle such upload by supplying the ```-segment-size``` parameter:

	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
	
Each segment is uploaded in parallel into a separate container named ```<container_name>_segments```. After all the segments are uploaded, Swift creates a manifest file so that the segments can be downloaded in a single file from the original container ```<container_name>``` with the original file name ```<file_name>```.

For example, the following command uploads a file named ```large_file``` from a container named ```test_container``` with the segment size ```1073741824```.

	swift upload test_container -S 1073741824 large_file

You can run the following command to download the file:

	swift download test_container large_file

#### Downloading a file

	swift download <container_name> <file_name>
	
#### Adding a directory to a container

Swift does not have a true directory structure, but uses the naming to represent a directory layout. To add a directory to a container, run the following command:

	swift upload <container_name> <directory_name>
	
This command will upload the full directory structure as a relative path. For example, if you specify ```/mnt/volume1```, the directory structure mnt/volume1 will be attached to all the file names to indicate the directory structure.

	
#### Downloading a directory

To download a directory structure, use the ```-prefix``` parameter to indicate the directory or directory structure that you want to download.

	swift download <container_name> --prefix <directory>
	
#### Deleting a file

	swift delete <container_name> <file_name>

### Creating a temporary URL

A temporary URL is a long, difficult-to-guess URL that can be used for a specified period to download objects without requiring further authentication. Generate a temporary URL with the following steps:

1. Identify your authentication account.
2. Set a secret key.
3. Create the temporary URL.

#### Identifying your authentication account

The Swift ```stat``` command prints information about your account:

	swift stat

Locate the Account field and note the full string behind *Account*: including ```AUTH_```.

#### Setting a secret key

This key can be anything that you select, but best practice is that you select a long, random, and hard to guess string.

	swift post -m "Temp-URL-Key:<key>"

#### Creating the temporary URL

The Swift ```tempurl``` command takes these positional arguments:

* [method] GET to allow download, PUT to allow upload
* [seconds] Time in seconds that the temporary URL will be available
* [path] The full path of the object expressed as /v1/<auth_account>/<container_name>/<object_name>
* [key] The key that you set in step 2

```
swift tempurl GET <seconds> <path> <key>
```

This command will return a URL that you can append to your cluster name to get a full URL. Use the full URL to download the object with any compatible HTTP client such as curl, wget, or Firefox.

## Using the Swift REST API to access {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

You can use the Swift REST API with a command–line client interface, such as cURL, or call the API from your application.  

### {{site.data.keyword.objectstorageshort}} URL {: #access-points}

To interact with the {{site.data.keyword.objectstorageshort}} API, construct the {{site.data.keyword.objectstorageshort}} URL as follows:

	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>

For example:

![{{site.data.keyword.objectstorageshort}} URL](images/Swift_URL.png)

*Figure 3. {{site.data.keyword.objectstorageshort}} URL*

The URL consists of five parts. The ```<API version>``` is v1. You can find the  ```<project ID>```, ```<container namespace>```, and ```<object namespace>``` of your {{site.data.keyword.objectstorageshort}} from the {{site.data.keyword.objectstorageshort}} user interface.  For the ```<access point>```, see the following table: 


| **Region**  |     **Internal access point**                             |     **Public access point**                   |
|-------------|-----------------------------------------------------------|-----------------------------------------------|
| Dallas      | https://dal.objectstorage.service.open.networklayer.com/  | https://dal.objectstorage.open.softlayer.com/ | 
| London      | https://lon.objectstorage.service.open.networklayer.com/  | https://lon.objectstorage.open.softlayer.com/ |


*Table 1. {{site.data.keyword.objectstorageshort}} access point*

Use the internal access point when you access the {{site.data.keyword.objectstorageshort}} service from inside {{site.data.keyword.Bluemix_notm}} or the public access point when you access the {{site.data.keyword.objectstorageshort}} service from outside of {{site.data.keyword.Bluemix_notm}}.

### {{site.data.keyword.objectstorageshort}} API

See the [OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window} for a comprehensive list of the {{site.data.keyword.objectstorageshort}} REST API options and examples.

## Using {{site.data.keyword.objectstorageshort}} across multi-regions {: #multi-regions}  

The IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} service supports the Dallas and London storage regions. These storage regions are independent of the {{site.data.keyword.Bluemix_notm}} region, such as US-South and United Kingdom, in which the {{site.data.keyword.objectstorageshort}} service instance is created.  For example, if you create an {{site.data.keyword.objectstorageshort}} instance in the US-South {{site.data.keyword.Bluemix_notm}} region, you can read and write data to either the Dallas or London storage region.  

For the US-South {{site.data.keyword.Bluemix_notm}} region, the Dallas storage region is the default. For the United Kingdom {{site.data.keyword.Bluemix_notm}} region, the London storage region is the default.  The {{site.data.keyword.objectstorageshort}} user interface always launches to the default storage region of the {{site.data.keyword.Bluemix_notm}} region. To switch regions, click the {{site.data.keyword.objectstorageshort}} Region drop-down list and choose another region.

![{{site.data.keyword.objectstorageshort}} Change Region](images/change_region.png)

*Figure 4. {{site.data.keyword.objectstorageshort}} Change Region*

**Note:** The {{site.data.keyword.objectstorageshort}} service does NOT support cross storage region replication.

### Multi-region access

To use the {{site.data.keyword.objectstorageshort}} service, you must [authenticate to OpenStack Keystone](#keystone-authentication). After you successfully authenticated, an ```X-Subject-Token``` and the {{site.data.keyword.objectstorageshort}} endpoints will be available in the response.

For example, to create a container named ```my_container``` in the Dallas storage region, specify a Dallas access point in the curl command as follows:

	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT


To create a container named ```my_container``` in the London storage region, specify a London access point in the curl command as follows:

	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT

**Note:** The ```X-Subject-Token``` that you acquired from Keystone works across storage regions. 

For more information about the access points for different regions, see the [Object Storage access point](#access-points) table.


## Understanding authentication and credentials {: #understanding-authentication-credentials}

### Generating {{site.data.keyword.objectstorageshort}} credentials without binding an application

To generate {{site.data.keyword.objectstorageshort}} cloud credentials for use outside a {{site.data.keyword.Bluemix_notm}} application, you must generate a service key for your {{site.data.keyword.objectstorageshort}} instance. You can generate a new key by selecting  **Service Credentials** from the sidebar of the user interface or by using the Cloud Foundry CLI (version 6.11.3 or later). After you generate and retrieve a service key for your {{site.data.keyword.objectstorageshort}} instance, you can use the cloud integration information to request a Keystone token by using an OpenStack SDK or the OpenStack Identity API and start using the Swift account to manage objects.
   
To create the key by using the Cloud Foundry CLI, log in and run the following command:
 
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>

To retrieve the service credentials from the Cloud Foundry CLI, run the following command:

	cf service-key <object_storage_instance_name> <unique_name_for_this_key>


### Cloud projects and users
Provisioning a new {{site.data.keyword.objectstorageshort}} instance creates an isolated Keystone project in the IBM Public Cloud. When you bind a new application to the {{site.data.keyword.objectstorageshort}} instance, a new Keystone user with access to the project is created. When you deprovision the instance, the project and user are deleted.

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
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

Use the value of the ```X-Subject-Token``` field from the response header as the ```X-Auth-Token``` field when you make requests to the {{site.data.keyword.objectstorageshort}} service.

An example response is as follows:

	HTTP/1.1 201 Created
	X-Subject-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9
	Vary: X-Auth-Token
	Content-Type: application/json
	Content-Length: 960
	Date: Tue, 10 Jun 2014 20:40:14 GMT
	
	{"token": 
	{"audit_ids": ["ECwrVNWbSCqmEgPnu0YCRw"], "methods": ["password"],
	 "roles": [{"id": "c703057be878458588961ce9a0ce686b", "name": "admin"}],
	 "expires_at": "2014-06-10T21:40:14.360795Z", 
	 "project": {"domain": {"id": "default", "name": "Default"}, "id": "3d4c2c82bd5948f0bcab0cf3a7c9b48c", "name": "demo"}, 
	 "catalog": [
	 {
		"endpoints": [
			{
			"adminURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "20cbfa6ff22b4a67a1484d30235bfc80",
			"internalURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://lon.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "london"
			},
			{
			"adminURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "4207049680fa4effbecd044c7448a8cb",
			"internalURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://dal.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "dallas"
			}
			],
		"endpoints_links": [],
		"name": "swift",
		"type": "object-store"
		},
	 ], 
	 "extras": {},
	 "user": {"domain": {"id": "default", "name": "Default"}, "id": "3ec3164f750146be97f21559ee4d9c51", "name": "admin"},  "issued_at": "2014-06-10T20:40:14.360822Z"}}


The {{site.data.keyword.objectstorageshort}} URL is found in the Service Catalog. The Service Catalog is contained in the response body of the token request. The response is a full catalog of OpenStack services that are available. Select the endpoint from the Service Catalog with type of ```object-store```, region that matches the region field in the credentials, and internal interface (`internalURL`) when you access the {{site.data.keyword.objectstorageshort}} service from inside {{site.data.keyword.Bluemix_notm}} or public interface (`publicURL`) when you access the {{site.data.keyword.objectstorageshort}} service from outside of {{site.data.keyword.Bluemix_notm}}.



## Unbinding and deprovisioning {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### How to deprovision your {{site.data.keyword.objectstorageshort}} service
1.	Select your service from the {{site.data.keyword.Bluemix_notm}} dashboard.  
2.	Click the gear icon in the upper right corner and select **Delete Service**.
	
**Warning:** If you deprovision an IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} service instance, the cloud project and Swift account are deleted. All containers and objects in the deprovisioned instance are deleted from Swift and cannot be restored.

### Unbinding an application or deleting a service key

If you unbind an application from the {{site.data.keyword.objectstorageshort}} instance or delete the service key, the credentials are deleted. The {{site.data.keyword.objectstorageshort}} account is not deleted until the {{site.data.keyword.objectstorageshort}} instance is deprovisioned. You can generate new cloud credentials by [rebinding or creating a new service key](#bind-object-storage-to-application).

## FAQ {: #FAQ} 

### How do prices vary depending on which plan I choose?
Pricing varies depending on the chosen plan. For more pricing information, see the [IBM Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/){: new_window} or use the [Calculator](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window} for more detailed estimates.

### How do I change my plan from Beta to Standard? {: #changeplan}  
The {{site.data.keyword.objectstorageshort}} Service Beta plan will be removed from the catalog after the General Availability of the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} Service. Customer service instances are NOT migrated from Beta to Standard plan automatically. You will need to update your plan by following these steps:

1.	Click **Plan** from the left navigation bar in the {{site.data.keyword.objectstorageshort}} user interface.
2.	Select **Standard** as the new plan and then click **Save**.

![{{site.data.keyword.objectstorageshort}} Change Pricing Plan](images/Change_plan.png)

*Figure 5. {{site.data.keyword.objectstorageshort}} Change Pricing Plan*

Your services instances and customer data are moved to the new plan.

You can also change your payment plan by using the command line interface. For more information, see [How to change your plan](../../pricing/index.html#changing)  

**Note:** Beta plan service instances cannot be moved to the Free plan. Any service instances not migrated will be disabled, and after 60 days, deleted. 

### What accounts and payment plans can I use for {{site.data.keyword.objectstorageshort}}?
The {{site.data.keyword.objectstorageshort}} service comes with multiple plan options. As of our general availability release, two plans are currently offered, Standard and Free. The Standard plan is available only to {{site.data.keyword.Bluemix_notm}} Paid Accounts, either Pay-As-You-Go or Subscription, and to IBM internal users.

Trial accounts that are still active are able to use the Free plan which allows only one instance to exist in a {{site.data.keyword.Bluemix_notm}} Organization. After the time on the {{site.data.keyword.Bluemix_notm}} trial expires, the associated {{site.data.keyword.objectstorageshort}} service instance will be disabled, meaning that the storage account cannot be accessed either by the {{site.data.keyword.Bluemix_notm}} user interface or command line. After a grace period of 30 days, your {{site.data.keyword.Bluemix_notm}} account will be purged, and all data deleted. To avoid data loss, it is recommended that you upgrade to a {{site.data.keyword.Bluemix_notm}} Paid Account as soon as possible. To upgrade your account, click on the user management menu in the upper-right corner, and select **Account**, which provides instructions about the upgrade process.

Instances that are created on the Free plan can be upgraded to the Standard plan with the steps described in [How do I change my plan from Beta to Standard?](#changeplan). To upgrade to the Standard plan, the associated organization must be a {{site.data.keyword.Bluemix_notm}} Paid Account. Trial accounts with {{site.data.keyword.objectstorageshort}} instances cannot be upgraded to the Standard plan, and instances on the Standard plan cannot be downgraded to other plans.

### How will I be charged and billed for my use of {{site.data.keyword.objectstorageshort}}?

The {{site.data.keyword.objectstorageshort}} service charges only for what you use.  There are no minimum fee, set-up fees, or commitments to begin using the service. There is no charge for API request or inbound data network traffic.

Your {{site.data.keyword.objectstorageshort}} usage is billed based on average daily storage usage throughout the billing cycle. This includes all object data in containers that you created under your {{site.data.keyword.Bluemix_notm}} organization account. 

Outbound Data Transfer charge applies whenever data is read from any of your object containers over the public network. It is billed based on average daily public outbound data transfer throughout the billing cycle.

The metrics components to {{site.data.keyword.objectstorageshort}} pricing are as follows:
* Storage Usage  - $0.04 per GB per month
* Public Outbound Data Transfer  - $0.09 per GB per month 

At the end of the billing cycle, {{site.data.keyword.Bluemix_notm}} will automatically bill you for the usage for the current billing period. You can view your charges for the current billing period via {{site.data.keyword.Bluemix_notm}} reporting.

The standard service plan that is released for London and Dallas has the same pricing.

### How is data replication performed in {{site.data.keyword.objectstorageshort}}?
The {{site.data.keyword.objectstorageshort}} service maintains three copies of your data, which are replicated across multiple storage nodes. For more information, see the [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window} document.

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
