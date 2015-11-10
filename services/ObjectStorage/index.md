# Getting started with IBM Object Storage for Bluemix (BETA)

IBM® Object Storage for Bluemix™ provides you with access to a fully provisioned Swift Object Storage account to manage your data. Swift provides a fully distributed, API-accessible storage platform. You can use it directly in your applications or for backups, making it ideal for cost effective, scale-out storage.

IBM Object Storage for Bluemix uses OpenStack Identity (Keystone) for authentication and can be accessed directly by using OpenStack Object Storage (Swift) API v1 calls. IBM Object Storage can be bound to a Bluemix application or accessed from outside a Bluemix application. IBM Object Storage for Bluemix creates a public cloud project (tenant) and Swift account for your Bluemix account. All public cloud projects for your Bluemix account are contained within a single OpenStack domain that is unique to your account. OpenStack domains provide an added layer of privacy for securing your data.

**Note:** Provider side encryption is not provided. It is the responsibility of the client application to encrypt data before uploading.

### How to create an Object Storage service instance
1.	Go to the **Bluemix** catalog and select the **Solutions** tab. Select the **Storage** category, and then select **Object Storage**.
2.	Select your space, app, service name, and plan and click **Create**. 
**Note:** If you initially choose the **Leave Unbound** option for the **App** field, you can still bind the service instance to your Bluemix application after you complete the configuration (see the following instructions).

### How to bind your Object Storage service to an application after creation
1.	In the **Bluemix** dashboard, select the app that you want to bind.
2.	In the app overview, click **Bind a Service or API**.
3.	Select your Object Storage instance from the list of services and click **Add**.
4.	Click **Restage** when prompted. Your app must be restaged to use the new service.

### How to deprovision your Object Storage service
1.	Select your service from the **Bluemix** dashboard.  
2.	Click the gear icon in the upper right corner and select **Delete Service**.
	
**Warning:** If you deprovision an IBM Object Storage for Bluemix service instance, the cloud project and Swift account are deleted. All containers and objects in the deprovisioned instance are deleted from Swift and cannot be restored.
 
### UI elements and navigation
When your Object Storage is provisioned, you can see your instance information in the Object Storage for Bluemix service instance dashboard. From the dashboard, select your Object Storage instance to view the panel with more detailed information.  
#### Usage data
At the top of the panel, you’ll see the storage usage information for your instance. It also shows the current number of **Storage Containers** and the total number of **Objects** in all of your containers. It lists your memory usage in megabytes. **Storage Consumed** refers to the current amount of space that is used. 
#### Actions
To retrieve the latest usage data, click the **Refresh** button.   
####Object browser 
The bottom section of the panel contains the object browser. Use the object browser to manage object storage containers and objects. You can create containers, upload files, delete containers, and delete files among other actions.

### Generating Object Storage credentials without binding an application

To generate Object Storage cloud credentials for use outside a Bluemix application, you must generate a service key for your Object Storage instance. You can generate a new key by using the **Service Credentials** button in the sidebar of the user interface or by using the Cloud Foundry CLI (version 6.11.3 or later). After you generate and retrieve a service key for your object storage instance, you can use the cloud integration information to request a Keystone token using an OpenStack SDK or the OpenStack Identity API and start using the Swift account to manage objects.
   
To create the key by using the Cloud Foundry CLI, log in and run the following command:
 
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>

To retrieve the service credentials from the Cloud Foundry CLI, run the following command:

	cf service-key <object_storage_instance_name> <unique_name_for_this_key>

### Bound context

If you want to use Object Storage in a bound context, the cloud credentials are provided indirectly through the application binding process. After you successfully bind a service instance to your application, a configuration similar to the following example is added to your `VCAP_SERVICES` environment variable.

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

### Unbinding an application or deleting a service key

If you unbind an application from the Object Storage instance or delete the service key, the cloud user is deleted. The Object Storage account is not deleted until the Object Storage instance is deprovisioned. Generate new cloud credentials by rebinding or creating a new service key.
  
### Cloud projects and users
Provisioning a new Object Storage instance creates an isolated Keystone project in the IBM Public Cloud and creates a new user for the dashboard to use. When you bind a new application to the Object Storage instance, a new Keystone user with access to the project is created. The Object Storage instance shares the project. When you deprovision the instance, the project and user are deleted.

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

Use the value of the X-Subject-Token field from the response header as the X-Auth-Token field when making requests to the Object Storage service.

The Object Storage URL is found in the Service Catalog. The Service Catalog is contained in the response body of the token request. Select the endpoint from the Service Catalog with type of object-storage, region that matches the region field in the credentials, and internal interface when accessing the Object Storage service from inside Bluemix or public interface when accessing the Object Storage service from outside of Bluemix.

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

Use the value of the access token id field from the response body as the X-Auth-Token field when making requests to the Object Storage service.

The Object Storage URL is found in the Service Catalog. The Service Catalog is contained in the response body of the token request. Select the endpoint from the Service Catalog with type of object-storage, region which matches the region field in the credentials, and internal interface (`internalURL`) when accessing the Object Storage service from inside Bluemix or public interface (`publicURL`) when accessing the Object Storage service from outside of Bluemix.

### Cost information
Pricing varies depending on the chosen plan. For more pricing information, refer to the [IBM Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/) or use the [Calculator](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet) for more detailed estimates.

># Related Links {:class="linklist"}
>## API Reference {:id="api"}
>* [OpenStack Object Storage (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html)
>* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html)
>
># Related Links {:class="linklist"}
>## SDK {:id="sdk"}
>* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs)
>
># Related Links {:class="linklist"}
>## Tutorials and Samples {:id="samples"}
>* [Connecting to IBM Object Storage for Bluemix with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/)
>* [Use Python to access your Bluemix Object Storage](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/)
>* [Bluemix Object Storage Community](https://www.ibm.com/developerworks/community/groups/service/html/communityoverview?communityUuid=1b48459f-4091-43cb-bca4-37863606d989)
>
># Related Links {:class="linklist"}
>## Compatible Runtimes {:id="buildpacks"}
>* [Liberty for Java](https://www.ng.bluemix.net/docs/starters/liberty/index.html)
>* [SDK for Node.js](https://www.ng.bluemix.net/docs/starters/nodejs/index.html)
>* [Go](https://www.ng.bluemix.net/docs/starters/go/index.html)
>* [PHP](https://www.ng.bluemix.net/docs/starters/php/index.html)
>* [Python](https://www.ng.bluemix.net/docs/starters/python/index.html)
>* [Ruby](https://www.ng.bluemix.net/docs/starters/rails/index.html)
>* [Community buildpacks](https://www.ng.bluemix.net/docs/starters/byob.html)
>
># Related Links {:class="linklist"}
>## Related Links {:id="general"}
>* [IBM Bluemix Pricing Sheet](https://www.ng.bluemix.net/#/pricing)
>* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs)
>
>{:elementKind="article" id="rellinks"}
